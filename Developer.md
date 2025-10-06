# Developer Guide

本文档介绍如何在本地开发和运行 Claude Code Router 项目。

## 环境准备

- Node.js (推荐使用 LTS 版本)
- npm 或其他包管理器

## 安装依赖

```bash
npm install
```

## 构建项目

项目使用 TypeScript 编写，使用 esbuild 进行构建：

```bash
npm run build
```

## 配置路由器

在运行之前，需要配置 `~/.claude-code-router/config.json`。可以参考项目中的 `config.example.json` 文件来创建配置文件：

```bash
# 创建配置目录
mkdir -p ~/.claude-code-router

# 复制示例配置文件
cp config.example.json ~/.claude-code-router/config.json

# 编辑配置文件，添加你的 API keys 和路由规则
```

配置文件包含：
- API providers 配置（API keys、base URLs 等）
- 路由规则（default、background、think、longContext、webSearch）
- 自定义 transformers

## 链接本地命令

为了在终端中使用 `myccr` 命令，需要全局链接这个包：

```bash
npm link
```

## 启动开发服务器

启动路由服务器：

```bash
myccr start
```

## 检查服务状态

```bash
myccr status
```

## 测试路由器

使用 `myccr code` 命令测试路由器是否正常工作：

```bash
myccr code "Hello, Claude!"
```

## 停止服务

```bash
myccr stop
```

## 项目架构

- **入口点**: `src/cli.ts` - 命令行界面逻辑
- **服务器**: `src/index.ts` - 服务器启动逻辑
- **路由**: `src/utils/router.ts` - 核心路由逻辑
- **配置**: `~/.claude-code-router/config.json` - 运行时配置
- **依赖**: `@musistudio/llms` - 本地依赖，基于 fastify 实现的 LLM API 交互库

## 发布新版本

```bash
npm run release
```

## 常见问题

### `myccr` 命令不可用

确保已经运行 `npm link` 将本地包链接到全局。

### 服务启动失败

检查配置文件是否正确，特别是 API keys 和 provider URLs。

### 路由不工作

检查 `~/.claude-code-router/config.json` 中的路由规则配置是否正确。
