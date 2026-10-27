# APN：可选的 macOS Apple Silicon 配置示例

此示例仅适用于 **Apple Silicon macOS + Node.js 24**，参考 APN v0.5.76。它不是 Windows/Linux/Intel 配置，也不加入现有的通用 `mcp.json` 或 `win_mcp.json`。

## 用途与前提

[Agent Payment Node (APN)](https://github.com/nuanu-ai/agent-payment-node) 是 MIT 开源的本地支付 CLI 和 stdio MCP，提供操作准备、状态与回执。软件许可免费，链上/服务商费用与资金另计。它不是托管 HTTP 支付端点。

所有者必须先按官方文档安装 APN，核对可执行文件来源、版本与 Node.js 24，并确认 Cursor 进程能找到该可执行文件。终端的 PATH 不一定与 GUI 应用相同。若环境不符合这些前提，请停止；不要让代理自动安装、更新或绕过权限。

```bash
apn --version
apn mcp config
```

参考版本的后者返回 `apn.mcp-launch.v1` 描述符：stdio、`command: apn`、`args: ["mcp", "serve"]`。这只是启动信息，不代表授予支付权限或证明 Cursor 连接成功。

## 手动合并配置

示例文件：[mcp.apn.macos-arm64.json](mcp.apn.macos-arm64.json)。按 [Cursor 官方 MCP 文档](https://cursor.com/docs/mcp) 的 stdio 字段，使用 `type`、`command` 和 `args`。

由所有者审查后，将所需条目合并到项目的 `.cursor/mcp.json`，保留已有条目，不要覆盖其他服务器设置。若文件已包含 `apn` 键，应先解决冲突。不要自动复制到全局配置或启用所有工具。

如果 GUI 找不到 `apn`，由所有者核对实际路径和 Node.js 版本后再决定是否填写绝对路径；不要在示例里写入猜测的机器路径。不要加入私钥、助记词、API token 或个人 `.env` 路径。

## 权限与验证范围

APN **不是只读工具**。直接转账/EVM 的批准包含所有者前台步骤；部分 Solana x402 支付可以在另行批准的所有者策略下执行。使用前必须另外核对操作效果、接收方、连接目标、权限与限额。MCP 返回前台命令不等于允许代理替所有者执行它。

此贡献只核对了 JSON 结构、Cursor 官方字段和 APN 的启动描述符。参考证据还包括隔离空状态目录中的 MCP factory 初始化/工具列表，**没有在 Cursor 中加载此文件或完成客户端互操作验证**。未创建/连接钱包、读取 Keychain、签名、发送资金或进行安全审计，也没有声明该配置强制执行 OS 沙箱。

此文由帮助 Nuanu AI 介绍 APN 的 AI 编写，不冒充独立使用体验。这个独立示例不改变仓库现有配置，也不表示本仓库作者已经测试或推荐 APN。
