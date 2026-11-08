# ai-memory-connect

**一个短入口，按当前任务只读需要的 Skill。** 把这个仓库链接交给 Agent 即可：

> 请读取这个仓库的 README，进入 ai-memory-connect 导航，只加载完成当前任务需要的 Skill，复用已有服务和配置。

## 从这里开始

读取 [总入口 skills/ai-memory-connect/SKILL.md](skills/ai-memory-connect/SKILL.md)。
入口只负责判断下一步，不包含整套安装操作。

| 当前要做什么 | 对应 Skill |
|---|---|
| 缺程序、服务停了、版本不兼容 | [安装与恢复](skills/ai-memory-install/SKILL.md) |
| GitHub 私有仓库没有访问权限 | [授权登录](skills/ai-memory-github-auth/SKILL.md) |
| 新 Agent 接入、配置采集或自动提取 | [Agent 接入](skills/ai-memory-agent-setup/SKILL.md) |
| 拉取／推送知识、配置后台同步 | [知识同步](skills/ai-memory-knowledge-sync/SKILL.md) |
| 检查刚才的改动是否实际有效 | [按需验收](skills/ai-memory-verify/SKILL.md) |

每个 Skill 是独立目录，包含自己的 `SKILL.md`。从 GitHub 读取对应文件即可；需要
本地安装时，只下载选中的 Skill 到当前 Agent 的技能目录。文件链接可从 GitHub
页面、raw 文件或 GitHub 工具读取，不要求 clone 整个仓库。存在引用时仅在该步骤
需要时读取；不要递归打开全部链接、拼成一个大提示词或写进全局指令。

例如：“同步知识库” → 只读知识同步；缺 GitHub 权限 → 再读授权，完成后返回同步。
只在确实缺少程序时读取安装。完整新设备接入也逐步加载，跳过已完成的阶段。
目录里有多个 Skill 不表示它们的正文需要同时进入上下文。

## 仓库和权限

| 仓库 | 放什么 | 同步方式 |
|---|---|---|
| 本公开仓库 | 入口与接入 Skills，不放记忆或密钥 | 按需下载说明 |
| 私有程序仓库 | Rust 程序、测试和开发文档 | 开发时手动提交 |
| 私有 Knowledge 仓库 | 个人知识、证据和可移植技能 | 后台自动同步，先拉再推 |

代码权限不代表记忆权限。已有 Knowledge 仓库就复用，没有才新建私有仓库；没有访问
权限先请用户登录。自动同步默认每小时或累计 100 个变更文件触发，两项可配置。
模型提取授权与 GitHub 授权分别配置。具体操作仅在对应 Skill 中展开。

Model configuration, Muse conversation capture and host-agent model work each
have a separate Skill selected by the router. The runtime keeps its existing
extraction pipeline; host-specific adapters supply events and inference.

## Agent entries

Start with the short router, or use the known host's entry directly:

- [Codex](skills/ai-memory-codex/SKILL.md): native hooks and Codex transcript adapter.
- [Muse desktop/cloud](skills/ai-memory-muse/SKILL.md): native chat export and local agent-model worker.

Both load shared installation, model or sync guidance only when needed. Adding
an agent means adding its entry and source adapter, not copying the memory engine.
