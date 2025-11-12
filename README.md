# XFC 链式代理配置

> 🌐 多协议链式代理配置文件示例，支持 mihomo/Clash 核心

## 📋 项目简介

本项目提供了一系列精心设计的链式代理配置文件，展示了如何在 mihomo/Clash 中实现复杂的代理链路组合。配置支持多种主流代理协议，并提供了灵活的节点选择和负载均衡策略。

## ✨ 主要特性

- 🌍 **多地区节点**：香港、美国等多个地区的节点支持
- 🔗 **链式代理**：支持多层代理链路，实现更灵活的网络路由
- 🔐 **多协议支持**：Trojan、VLESS、SOCKS5 等主流协议
- ⚡ **智能选择**：手动/自动节点选择，支持负载均衡
- 🎯 **规则分流**：基于地理位置的智能路由规则

## 📁 项目结构

```
xfc-yaml-files/
├── README.md           # 项目说明文档
├── 链式.yaml          # 主要的链式代理配置文件
├── CLAUDE.md          # Claude Code 工作指南
└── .gitignore         # Git 忽略文件配置
```

## 🚀 快速开始

### 1. 下载配置文件

```bash
git clone https://github.com/masx200/xfc-yaml-files.git
cd xfc-yaml-files
```

### 2. 修改节点信息

编辑 `链式.yaml` 文件，将示例节点信息替换为您实际的节点配置：

```yaml
proxies:
  # 香港节点示例
  - { name: "🇭🇰 香港2-联通IEPL", type: trojan, server: your-server.com, port: 443, password: your-password }

  # 美国节点示例
  - { name: "🇺🇸 美国-Trojan", type: trojan, server: us-server.com, port: 443, password: your-password }
```

### 3. 导入到客户端

将修改后的配置文件导入到您的 mihomo/Clash 客户端中即可使用。

## ⚙️ 配置说明

### 代理组架构

当前配置实现了以下代理组结构：

```
🚀 节点选择
├── 🌉 中转链路 (香港 → 美国)
│   ├── 🇭🇰 香港入口
│   │   ├── 🇭🇰 香港2-联通IEPL
│   │   ├── 🇭🇰 香港3-移动IEPL
│   │   └── 🇭🇰 香港家宽1-联通IEPL
│   └── 🇺🇸 美国出口
│       ├── 🇺🇸 美国-Trojan
│       ├── 🇺🇸 美国-VLESS-Vision
│       └── 🇺🇸 美国-SOCKS5
├── 🇭🇰 香港入口 (直连)
├── 🇺🇸 美国出口 (直连)
└── DIRECT (直连)
```

### 支持的协议

- **Trojan**: 高性能伪装协议
- **VLESS**: 轻量级协议，支持 Vision 流控
- **SOCKS5**: 经典代理协议，支持住宅 IP

### 路由规则

- **国内流量**: 直连 (`GEOIP,CN,DIRECT`)
- **国际流量**: 通过代理链路 (`MATCH,🚀 节点选择`)

## 🔧 高级配置

### 链式代理优化

当前配置使用 `relay` 类型实现代理链，建议迁移到更现代的 `dialer-proxy` 方案以提高兼容性和性能。

### 节点健康检查

可以配置 URL 测试来实现自动节点健康检查和故障转移。

## 📖 文档

- **[CLAUDE.md](./CLAUDE.md)**: Claude Code 工作指南
- **[mihomo 官方文档](https://github.com/MetaCubeX/mihomo)**: 核心功能文档

## ⚠️ 注意事项

1. **安全提醒**: 请勿在配置文件中使用真实的节点信息
2. **协议兼容**: 确保您的 mihomo 版本支持所有使用的协议
3. **网络环境**: 根据实际网络环境调整节点选择策略
4. **合规使用**: 请遵守当地法律法规，合规使用代理服务

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进这个项目。

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

---

> 💡 **提示**: 如果您在使用过程中遇到问题，请查看 [CLAUDE.md](./CLAUDE.md) 获取更多技术细节。
