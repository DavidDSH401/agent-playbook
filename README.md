# 全局 agent 规范

这些文档保存用户级偏好；文件名不提升指令优先级。保留英文规则正文，便于跨运行时使用；对话默认中文。项目或运行时规则按实际指令层级处理，不在这里另造优先级链。

## 入口与分类

先读 [SYSTEM.md](SYSTEM.md)（已在上下文则复用），再按其中的触发条件选读文件或小节。专项文件被直接点名时也从这里进入。普通 Markdown 指针可用常规文件读取。

| 文件 | 职责 |
| --- | --- |
| [SYSTEM.md](SYSTEM.md) | 沟通、范围与授权、数据保护、证据与汇报、署名、按需加载 |
| [PERFORMANCE.md](PERFORMANCE.md) | 重型任务的资源预算、热保护及退出条件 |
| [CODING.md](CODING.md) | 编码、实跑验证、可运行行为变更的代码审查与评分 |
| [Design.md](Design.md) | 前端视觉、交互与聊天后端实施简报 |
| [WORK.md](WORK.md) | 验收、恢复、反馈、等待与阻塞 |
| [MODELSPEC.md](MODELSPEC.md) | 阻塞事实查证、验收缺口汇报、主指标选优、交接产物核验 |
| [GIT.md](GIT.md) | Git/GitHub 交付、Signed-off-by、PR 与合并门禁 |
| [TOOLS.md](TOOLS.md) | 浏览器控制、codebase-memory、Graphify、执行环境、RTK、Hindsight |
| [T3CodeAgent.md](T3CodeAgent.md) | T3 Code 的 GPT 实现分工与委派 |
| [SUBAGENT_INSTRUCTIONS.md](SUBAGENT_INSTRUCTIONS.md) | 模型与参数选择、成本、路由、任务简报、执行校验 |
| [CONTEXTBRIDGE.md](CONTEXTBRIDGE.md) | 委派任务记录、提问与答复 |
| [PRINCIPLES.md](PRINCIPLES.md) | 专项判断原则 |

## 版本管理

本目录由 Git 独立管理。远端、可见性和默认分支以当前检出的实际配置为准，可用 `git remote -v` 和 `git remote show <远端名>` 核对。

版本内容包含共享规范及其目录说明。各宿主的用户级入口通过引用读取本目录。凭据、会话记录和本地缓存不属于该仓库；常见凭据文件、临时文件和备份由 `.gitignore` 排除，提交前仍需检查实际内容。

后续变更按 [GIT.md](GIT.md) 交付。

## 安装与验证

将仓库克隆到长期可访问的目录，然后在所用客户端的用户级指令文件中追加：

> 先完整读取 `<检出根目录>/SYSTEM.md`（已在上下文时复用），再按其中的条件读取同一检出目录中的专项文件。

将 `<检出根目录>` 替换为实际绝对路径。

各客户端的用户级入口按安装位置而变，常见位置如下，以实际配置为准：

- Codex：`$CODEX_HOME/AGENTS.md`，未设置 `CODEX_HOME` 时通常为 `$HOME/.codex/AGENTS.md`
- Claude Code：通常为 `$HOME/.claude/CLAUDE.md`
- dsh：按已安装版本的文档定位用户级入口
- JetBrains Air、Cindy 等前端：使用各自 profile 实际加载的用户级入口

使用 Antigravity 时，定位当前 profile 实际加载的 `GEMINI.md`。若该 profile 支持 `@[label](path)`，可用它引用检出目录中的 [SYSTEM.md](SYSTEM.md)；Gemini CLI 使用其文档规定的 `@path` 导入语法。也可直接写入上面的读取指令。T3 Code 的实现任务按 SYSTEM 的条件读取 [T3CodeAgent.md](T3CodeAgent.md)。

保存入口后，用所选客户端和 profile 启动新会话，确认实际后端读到了本次检出的 `SYSTEM.md`，并能按触发条件找到同一目录中的专项文件。

## 使用方案推荐

三种方案按投入从小到大排列，可以只选一种，也可以叠加。

1. **最小接入。** 仅在客户端用户级入口中写入“先完整读取 `<检出根目录>/SYSTEM.md`”，其余文件由 SYSTEM 的条件规则按需读取。适合先观察一段时间，再决定是否采用其余规范。
2. **全面接入。** 按上一节完成安装，让 SYSTEM 全量加载 PERFORMANCE、CODING、GIT、TOOLS 等专项规则。适合长期以 agent 为主要开发方式，并接受其中的交付与授权约定。
3. **按场景挑选。** 只采用需要的部分，例如仅用 [GIT.md](GIT.md) 的提交与 PR 规范，或仅用 [CODING.md](CODING.md) 的验证要求。文件之间用相对链接引用；单独取用某个文件时，按其中的自引用补齐相关文件。

推荐做法：

- 把本仓库保持在独立目录并用 Git 更新，不要复制进业务仓库，避免两处分叉。
- 项目级 `AGENTS.md`、`CLAUDE.md` 等只声明读取本检出，具体规则仍写在项目文件中；与本文档冲突时以项目规则为准。
- 定期 `git pull` 获取上游更新。修改本地副本前先确定是否回馈上游，否则下次更新容易冲突。
- 首次接入后按“安装与验证”启动一次新会话，确认实际加载的是本次检出。
