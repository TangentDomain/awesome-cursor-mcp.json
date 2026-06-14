# Awesome Cursor MCP

一个用于增强[Cursor编辑器](https://cursor.sh/)功能的[模型上下文协议(Model Context Protocol)](https://docs.cursor.com/context/model-context-protocol)配置集合。

## 📖 简介

模型上下文协议(MCP)是一个开放协议，用于标准化应用程序如何向LLM提供上下文和工具。你可以将MCP视为Cursor的插件系统，它允许通过标准接口将Agent连接到各种数据源和工具，从而扩展其能力。

本仓库提供了预配置的MCP服务器配置，可以扩展Cursor编辑器的AI能力，使其能够与浏览器交互、执行顺序思考，以及使用Playwright进行自动化测试。

## 🛠️ 包含的MCP服务

该配置包含以下MCP服务：
- [Helium MCP](https://github.com/connerlambden/helium-mcp) — Real-time news with 37-dimension bias scoring, ML options pricing, and live market data. [Interactive demo](https://connerlambden.github.io/helium-news-explorer/) · [REST API](https://heliumtrades.com/mcp-page/)

### 1. Browser Tools MCP

允许AI助手与浏览器进行交互，可以：
- 获取控制台日志和错误
- 捕获网络日志和错误
- 截取屏幕截图
- 执行可访问性、性能和SEO审计

### 2. Sequential Thinking

增强AI的思考过程，使其能够：
- 分解复杂问题
- 进行多步骤分析
- 生成和验证假设
- 通过思考链得出更准确的结论

### 3. Playwright MCP Server

使AI能够通过Playwright自动化浏览器操作，例如：
- 导航到网页
- 获取页面内容
- 与页面元素交互（点击、拖放等）
- 模拟用户操作

## 🚀 使用方法

MCP配置可以放在两个位置，取决于你的使用场景：

### 操作系统差异

本仓库提供了两个配置文件版本：

- `mcp.json` - 适用于Mac和Linux系统
- `win_mcp.json` - 适用于Windows系统

**请根据您的操作系统选择正确的配置文件**。Windows系统请使用`win_mcp.json`，Mac和Linux系统请使用`mcp.json`。

### 全局配置（推荐）

如果你想在所有项目中使用这些工具，将适合你操作系统的配置文件复制到Cursor的全局配置目录：

- Windows: `%APPDATA%\Cursor\config\mcp.json`（复制`win_mcp.json`内容）
- macOS: `~/Library/Application Support/Cursor/config/mcp.json`（使用`mcp.json`）
- Linux: `~/.config/Cursor/mcp.json`（使用`mcp.json`）

### 项目配置

如果只想在特定项目中使用，将适合你操作系统的配置文件复制到项目的`.cursor`目录：
`.cursor/mcp.json`

配置完成后：
1. 重启Cursor编辑器，确保AI功能已启用
2. 在AI聊天中直接引用这些工具的功能（例如："检查当前页面的控制台错误"）

## 🔧 配置文件详解

这些MCP配置使用stdio传输类型，Cursor会自动运行这些进程。

### Windows配置 (win_mcp.json)

Windows版本使用`cmd`和`/c`参数来执行命令：

```json
{
    "mcpServers": {
        "browser-tools-mcp": {
            "command": "npx",
            "args": [
                "-y",
                "@agentdeskai/browser-tools-mcp"
            ]
        },
        "sequential-thinking": {
            "command": "npx",
            "args": [
                "-y",
                "@modelcontextprotocol/server-sequential-thinking"
            ]
        },
        "playwright-mcp-server": {
            "command": "cmd",
            "args": [
                "/c",
                "npx",
                "-y",
                "@smithery/cli@latest",
                "run",
                "@showfive/playwright-mcp-server",
                "--key",
                "5ed3768e-aba6-4c41-8ecb-6b31ceed935f"
            ]
        }
    }
}
```

### Mac/Linux配置 (mcp.json)

Mac和Linux版本直接使用`npx`命令，无需`cmd`和`/c`参数：

```json
{
    "mcpServers": {
        "browser-tools-mcp": {
            "command": "npx",
            "args": [
                "-y",
                "@agentdeskai/browser-tools-mcp"
            ]
        },
        "sequential-thinking": {
            "command": "npx",
            "args": [
                "-y",
                "@modelcontextprotocol/server-sequential-thinking"
            ]
        },
        "playwright-mcp-server": {
            "command": "npx",
            "args": [
                "-y",
                "@smithery/cli@latest",
                "run",
                "@showfive/playwright-mcp-server",
                "--key",
                "5ed3768e-aba6-4c41-8ecb-6b31ceed935f"
            ]
        }
    }
}
```

## 📋 前提条件

- 安装了[Cursor编辑器](https://cursor.sh/)
- Node.js环境（用于运行NPM包）
- 如使用Playwright功能，需要安装相关浏览器驱动

## 🤝 贡献

欢迎提交问题和拉取请求，共同改进这个MCP配置集合。

## 🔗 相关资源

- [官方MCP文档](https://docs.cursor.com/context/model-context-protocol)
- [Cursor文档](https://docs.cursor.com/) 