# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**xfc-yaml-files** 是一个 mihomo/Clash 代理配置文件项目，专注于链式代理配置示例。项目包含多种代理协议和复杂代理链的配置模板。

## Project Structure

```
xfc-yaml-files/
├── README.md           # 项目说明文档
├── 链式.yaml          # 主要的链式代理配置文件
└── CLAUDE.md          # 本文件
```

## 核心配置文件

### 链式.yaml
这是项目的主要配置文件，展示了以下功能：

#### 代理节点类型
- **香港节点**：3 个不同运营商的 Trojan 节点（联通IEPL、移动IEPL、家宽）
- **美国节点**：包含多种协议
  - Trojan 节点
  - VLESS with Vision
  - SOCKS5 住宅IP节点

#### 代理组结构
- **🇭🇰 香港入口**：香港节点的选择组
- **🇺🇸 美国出口**：美国节点的选择组
- **🌉 中转链路**：当前使用 relay 类型实现香港→美国的链式连接
- **🚀 节点选择**：最终的节点选择组，包含直连选项

#### 重要迁移说明
当前配置使用了即将被弃用的 `relay` 类型代理组。建议迁移到 `dialer-proxy` 方案：

1. **方案一**：为美国节点添加 `dialer-proxy` 字段指向香港节点组
2. **方案二**：使用 `proxy-providers` 配合 `override` 实现链式连接

## 配置管理指南

### 代理节点配置原则
- **安全性**：所有密码和敏感信息应使用占位符
- **协议支持**：支持 Trojan、VLESS、SOCKS5 等主流协议
- **运营商优化**：针对不同网络环境选择最优节点

### 代理组设计模式
- **地理分组**：按地理位置对节点进行分组
- **协议分层**：入口节点和出口节点可以使用不同协议
- **灵活切换**：支持直接连接和链式代理的切换

### 规则配置
当前使用简单的规则：
- 国内流量直连：`GEOIP,CN,DIRECT`
- 其他流量通过代理：`MATCH,🚀 节点选择`

## 常见维护任务

### 添加新节点
1. 在 `proxies` 部分添加节点配置
2. 根据地理位置添加到对应的代理组
3. 确保协议配置正确

### 迁移到 dialer-proxy
1. 移除 `relay` 类型的代理组
2. 为需要链式的节点添加 `dialer-proxy` 字段
3. 测试连接性和稳定性

### 配置验证
- YAML 语法检查
- 节点连通性测试
- 代理链路完整性验证