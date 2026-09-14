# PiBench Codex UModel Purple Agent

这是用于在 [AgentBeats](https://agentbeats.dev/) 注册 PiBench Purple Agent 的公开发布仓库。

仓库只包含公开部署元数据，不包含 Purple Agent 的实现源码。运行镜像发布在 GitHub Container Registry：

```text
ghcr.io/tanxiaobing-hl/leaderboard-pibench-agent:v0.1.1
```

## AgentBeats 注册信息

- Agent 类型：Purple Agent
- 推荐分类：Agent Safety
- A2A 端口：`9009`
- 平台：`linux/amd64`
- Amber manifest：[amber-manifest.json5](./amber-manifest.json5)

注册时使用以下公开 Raw URL：

```text
https://raw.githubusercontent.com/tanxiaobing-hl/leaderboard-pibench-agent/refs/heads/main/amber-manifest.json5
```

## 功能概览

该 Purple Agent 面向 PiBench 的 `retail`、`helpdesk` 和 `finra` 三个政策合规域：

- 通过 A2A 协议接收多轮任务与工具调用上下文；
- 使用只读 UModel 语义服务查询政策知识；
- 返回助手文本或结构化工具调用；
- 在单个容器中启动 A2A 服务和内置的只读 UModel MCP 服务。

## 拉取与启动

镜像是公开的，可直接拉取：

```powershell
docker pull ghcr.io/tanxiaobing-hl/leaderboard-pibench-agent:v0.1.1
```

启动时通过环境变量提供 DeepSeek API Key：

```powershell
docker run --rm -p 9009:9009 `
  -e OPENAI_API_KEY="$env:DEEPSEEK_API_KEY" `
  ghcr.io/tanxiaobing-hl/leaderboard-pibench-agent:v0.1.1
```

检查 A2A Agent Card：

```powershell
Invoke-RestMethod http://127.0.0.1:9009/.well-known/agent-card.json
```

## 配置与安全

`amber-manifest.json5` 只声明运行时需要的秘密参数，不包含任何真实 API Key。请在 AgentBeats 提交页面或排行榜仓库的 GitHub Actions Secrets 中配置密钥，禁止将密钥提交到 Git。

## 镜像版本

当前发布版本：`v0.1.1`

OCI 索引摘要：

```text
sha256:a697c565526ba7e3694fb72cec2266dc621132bc05c96a0d105faf39cec47a94
```

## PiBench

- AgentBeats 页面：<https://agentbeats.dev/agentbeater/pi-bench>
- 官方排行榜仓库：<https://github.com/RDI-Foundation/Pi-Bench-agentbeats-leaderboard>

注册成功并取得 Purple Agent ID 后，再在排行榜仓库的 fork 中配置该 ID 并提交评测。
