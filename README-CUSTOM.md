# My Everything Claude Code

这是基于 [everything-claude-code](https://github.com/affaan-m/everything-claude-code) 的个人定制版本。

## 🎯 定制内容

### MCP 全局配置化 (2026-04-20)

**核心改进**：将 MCP 服务器配置从项目级提升为全局级，实现真正的"一次配置，处处可用"。

#### 已配置的 MCP 服务器

| MCP 服务器 | 功能 | 版本 |
|-----------|------|------|
| **github** | GitHub 仓库操作、PR、Issues | 2025.4.8 |
| **context7** | 实时文档查询（库/框架） | 2.1.4 |
| **exa** | 网络搜索和内容抓取 | HTTP |
| **memory** | 跨会话知识图谱 | 2026.1.26 |
| **playwright** | 浏览器自动化测试 | 0.0.69 |
| **sequential-thinking** | 深度推理链 | 2025.12.18 |

#### 使用方法

在**任意项目目录**启动 Claude Code，直接使用自然语言：

```bash
cd /any/project
claude

# 然后直接说：
搜索 GitHub 上的 TypeScript 项目
如何使用 React 的 useEffect 钩子？
打开 https://example.com 并截图
```

#### 配置位置

- **全局配置**：`~/.claude/settings.json` 的 `mcpServers` 字段
- **项目配置**（可选）：项目根目录的 `.mcp.json`（覆盖全局）

详细说明见 [CHANGELOG-CUSTOM.md](CHANGELOG-CUSTOM.md)。

## 📦 安装

```bash
# 克隆仓库
git clone https://github.com/Banananoloko/My-everything-cc.git
cd My-everything-cc

# 安装依赖
npm install

# 运行安装脚本
./install.sh
```

## 🔗 上游项目

本项目基于 [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) v1.10.0。

## 📄 许可证

MIT License - 继承自上游项目

## 🙏 致谢

感谢 [Affaan Mustafa](https://github.com/affaan-m) 和所有 everything-claude-code 的贡献者。
