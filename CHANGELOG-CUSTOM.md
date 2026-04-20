# 自定义更新日志

## 2026-04-20 - MCP 全局配置化

### 🎯 核心改动

**将 MCP (Model Context Protocol) 服务器配置从项目级提升为全局级**，实现与 skills、agents、hooks 相同的全局可用性。

### ✨ 改进内容

#### 1. MCP 配置全局化
- **位置**：`~/.claude/settings.json` 新增 `mcpServers` 字段
- **范围**：所有项目目录启动 Claude Code 都能使用
- **服务器**：6 个 MCP 服务器全局可用
  - `github` - GitHub 仓库操作、PR、Issues
  - `context7` - 实时文档查询（库/框架）
  - `exa` - 网络搜索和内容抓取
  - `memory` - 跨会话知识图谱
  - `playwright` - 浏览器自动化测试
  - `sequential-thinking` - 深度推理链

#### 2. 配置结构
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github@2025.4.8"]
    },
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@2.1.4"]
    },
    "exa": {
      "type": "http",
      "url": "https://mcp.exa.ai/mcp"
    },
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory@2026.1.26"]
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@0.0.69", "--extension"]
    },
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking@2025.12.18"]
    }
  }
}
```

### 📊 对比

| 配置类型 | 之前 | 现在 |
|---------|------|------|
| **Skills** | ✅ 全局 | ✅ 全局 |
| **Agents** | ✅ 全局 | ✅ 全局 |
| **Commands** | ✅ 全局 | ✅ 全局 |
| **Hooks** | ✅ 全局 | ✅ 全局 |
| **MCP 服务器** | ❌ 项目级 | ✅ 全局 |

### 🎁 用户体验提升

**之前**：
```bash
cd /project-a  # 有 .mcp.json
claude         # ✅ MCP 可用

cd /project-b  # 无 .mcp.json
claude         # ❌ MCP 不可用
```

**现在**：
```bash
cd /any/project
claude         # ✅ MCP 始终可用
```

### 🔧 技术细节

- **加载优先级**：项目级 `.mcp.json` > 全局 `~/.claude/settings.json`
- **合并策略**：项目级配置完全覆盖全局配置（不合并）
- **版本固定**：所有 MCP 服务器使用固定版本，避免自动升级破坏
- **安全性**：配置文件已通过 `opensource-sanitizer` 扫描，无敏感信息泄露

### 📝 相关文件

- `~/.claude/settings.json` - 全局 MCP 配置（不在 git 中）
- `.mcp.json` - 原项目级配置（保留作为参考）
- `mcp-configs/mcp-servers.json` - MCP 服务器元数据

### 🚀 使用方法

在任意项目中直接使用自然语言调用 MCP：

```
搜索 GitHub 上的 TypeScript 项目
如何使用 React 的 useEffect 钩子？
打开 https://example.com 并截图
```

### ⚠️ 注意事项

1. **不要提交** `~/.claude/settings.json` 到 git（包含 API token）
2. **项目级覆盖**：如需特定项目使用不同 MCP，创建项目级 `.mcp.json`
3. **上下文窗口**：过多 MCP 会消耗 token，建议保持 ≤10 个

---

**贡献者**: Banananoloko  
**日期**: 2026-04-20  
**基于**: everything-claude-code v1.10.0
