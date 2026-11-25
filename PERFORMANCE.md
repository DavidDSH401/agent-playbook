# Resource budgets for agent workloads

Apply these rules on the user's workstation and any other machine they are using, including background and delegated work. Run brief reads, narrow searches, routine edits, and ordinary browser interaction directly. Treat builds, test suites, indexing, batch processing, and compute-heavy work as heavy jobs. Classify a command by the work it starts, including downstream workers.

## Before starting a heavy job

1. Run the smallest useful workload and one heavy job at a time per host. Defer if another heavy job is running or the host is under sustained CPU or memory pressure.
2. **CPU.** Use low priority. Cap total CPU time at the smaller of 200% and 25% of the workload's available logical CPUs, with 100% per CPU. Explicitly limit test workers, build parallelism, and configurable compute thread pools to one. Examples include `flutter test --concurrency=1`, `make -j1`, and `cargo test -j 1 -- --test-threads=1`. If a runner ignores its worker flag, use a smaller invocation that enforces the worker limit, or defer. Never assume one target means one worker.
3. **Memory.** Use Linux `MemAvailable` or its equivalent. Reserve the greater of 2 GiB and 20% of total RAM. Cap the job at the smallest of 6 GiB, half of available RAM, and available RAM minus the reserve. Round down and disable job swap where supported. Shrink or defer if the job will not fit or the host is actively swapping.
4. **GPU.** Select CPU-only compute by default. Require explicit authorization for GPU-heavy work. On a shared GPU, enforce memory and compute caps that leave at least half of each resource for other work. `ROCR_VISIBLE_DEVICES` selects ROCm devices. If either cap is unavailable, use a bounded CPU or authorized remote alternative, or get approval for that specific uncapped GPU run. Keep normal desktop and browser acceleration available.
5. **Thermal gate.** Use the host's documented sensor, throttling signals, temperature limits, and cooldown policy. On compatible Linux hosts, identify the CPU package sensor by hwmon name and label, not by index (`coretemp` on Intel CPUs, `k10temp` on AMD), and use the kernel thermal throttle counters under `/sys/devices/system/cpu/cpu*/thermal_throttle/` when exposed. Start below the host limit; where the host defines none, start below 85°C. Before releasing the scope after a thermal block or stop, record a host-wide cooldown and honor it on every later invocation; where the host defines none, require at least 10 seconds of readings taken every 2 seconds below 80°C with unchanged counters. Apply the same gate in every power profile. Defer when the required readings are unavailable.

## Apply and verify the limits

On Linux hosts with a user systemd manager and the required cgroup controllers, claim the fixed scope before starting heavy workers. If the scope name is occupied, defer. Keep the workers in the scope through exit. Use the command below with a locally available entry point in place of `SCOPE_GATE_AND_MONITOR_ENTRYPOINT`; that entry point must verify effective limits, check the thermal gate and persisted cooldown, and start monitoring before launching workers. Use the fallback below if the control path is unavailable or cannot preserve cooldown across invocations and detect interrupted updates. Set `quota` without the percent sign and `memory_max` to the calculated limit.

```sh
systemd-run --user --scope --unit=myworkflow-heavy.scope --collect \
  --expand-environment=no \
  -p CPUWeight=25 -p "CPUQuota=${quota}%" \
  -p "MemoryMax=${memory_max}" -p MemorySwapMax=0 -- nice -n 10 SCOPE_GATE_AND_MONITOR_ENTRYPOINT WORKLOAD [ARGS...]
```

Before starting workers, verify the effective cgroup limits (`cpu.max`, `memory.max`, and `memory.swap.max`) and recheck the thermal gate from inside the scope. For containers or daemon-backed jobs, enforce the limits where the workers run, hold the slot through their exit, and verify that cancellation reaches them. On other hosts, use equivalent job controls and thermal gates appropriate to the hardware. If the controls or monitoring are unavailable, use a light workload or an authorized executor with working controls.

## While the job runs

Start monitoring before launching workers. Sample the configured thermal signals at the host policy's interval through worker exit. On compatible Linux hosts, read the sensor files directly; do not shell out to `sensors` on a timer. Stop the entire job when the configured stop condition is met; where the host defines none, stop at 90°C, on any throttle-counter increase, or if monitoring fails. On a thermal stop, persist the cooldown before requesting termination if doing so will not delay the stop. Stop even if recording fails. Defer later launches if cooldown cannot be verified. A monitor inside its own scope can report the cause and queue `systemctl --user --no-block stop myworkflow-heavy.scope`.

Stop or shrink the job if the user reports lag, available RAM falls below the reserve, or the host starts sustained swapping. Verify that the job's workers and temporary services exit. If a limit stops the job, shrink the workload or report what could not complete. Leave user processes and system-wide settings alone.

Automatic enforcement of this policy is pending. A shared `run-lim` launcher, command interception hooks, and tighter parent-slice limits require separate implementation.
