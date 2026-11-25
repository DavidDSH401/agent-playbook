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

## 推荐接入方式

把本仓库当作唯一规则源，宿主入口只保留一块受管引用，不复制任何规则正文。这是最省上下文、也最容易更新的用法。

在客户端的用户级入口文件中加入受管块，标记名可自定，示例用 `myworkflow`：

```markdown
<!-- myworkflow:start -->
## Shared global rules

Read `<检出根目录>/SYSTEM.md` in full before task actions unless it is already in context. Follow its conditional reading instructions and the active runtime's instruction hierarchy. Report any required file you cannot read.
<!-- myworkflow:end -->
```

- 支持导入语法的宿主用导入代替读取指令，例如 Antigravity 的 `@[label](path)`；其余宿主保留上面的文字块。
- 受管块让更新可控：同步时只替换 `start` 与 `end` 之间的内容，入口中的其他规则不受影响。
- 专项文件不写进入口。SYSTEM.md 只在触发条件成立时才读 PERFORMANCE、CODING、GIT 等，避免每个会话都付全量上下文成本。
- 入口中原有的工具类规则放在受管块之外，按宿主自身的加载顺序排列，无需重复。

更新与验证：

- 用 `git pull` 更新本仓库，再按受管块同步入口；不要把规则正文复制到入口或业务仓库。
- 首次接入或更新后启动新会话，确认客户端读到的是本次检出的 `SYSTEM.md`，并能按条件找到同一目录中的专项文件。
- 项目级 `AGENTS.md`、`CLAUDE.md` 只声明读取本检出；与本文档冲突时以项目规则为准。

只取少量文件（例如仅用 [GIT.md](GIT.md) 的提交与 PR 规范）也能工作，但会失去条件加载，引用关系需自行维护，因此不作为推荐方式。
