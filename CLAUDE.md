# CLAUDE.md

此文件为 Claude Code (claude.ai/code) 在本仓库中工作时提供指导。

## 项目概述

本项目是 **ClaimAgent API** 文档站点，基于 [Mintlify](https://mintlify.com) 构建。ClaimAgent 是由 [TextIn/IntSig](https://github.com/intsig-textin) 开发的 AI 驱动型保险理赔材料智能处理平台。所有文档内容使用简体中文编写。

## 开发命令

```bash
# 安装 Mintlify CLI（仅需一次）
npm i -g mint

# 启动本地开发服务器（访问 http://localhost:3000）
mint dev

# 更新 Mintlify CLI
mint update
```

在仓库根目录（`docs.json` 所在位置）运行 `mint dev`。

## 项目结构

- **docs.json** - Mintlify 主配置文件：主题、导航标签页、颜色、Logo、导航栏、页脚等
- **api-reference/openapi-external.yaml** - OpenAPI 规范文件，定义所有 API 端点、Schema 及请求/响应结构。端点 `.mdx` 文件通过 `openapi` frontmatter 引用此文件
- **api-reference/endpoint/*.mdx** - 各 API 端点页面，大部分仅包含 frontmatter（引用 OpenAPI YAML）。修改 API 文档内容请编辑 OpenAPI YAML
- **index.mdx** - 产品简介，包含核心概念（stages、状态枚举、同步/异步模式）
- **quickstart.mdx** - 快速入门指南，含 curl 示例
- **authentication.mdx** - API Key 鉴权说明

### 导航结构（docs.json）

两个标签页，API参考下分两个分组：
1. **产品导览**：index、quickstart、authentication
2. **API参考**
   - **文件处理**：单文件维度的接口（图片质检、PS检测）
   - **案件处理**：案件维度的接口（创建案件、齐全性、分类、抽取、时间线等）

### API 核心概念

- Base URL：`/doc-agent/api/v1`
- 鉴权：`x-api-key` header
- 关键实体：`claim_id`（案件 ID）、`material_id`（材料 ID）
- 处理阶段（stages）：1=分类, 2=抽取, 3=时间线, 4=发票验真, 5=PS检测
- 仅支持特定的 stages 组合（必须从 1 开始，存在顺序依赖）

## 内容规范

- 所有面向用户的文档使用简体中文
- API 端点页面使用 OpenAPI frontmatter（`openapi: 'METHOD /path'`），而非内联内容
- 新增/修改 API 端点详情，请编辑 `api-reference/openapi-external.yaml`
- 新增端点页面：在 `api-reference/endpoint/` 下创建 `.mdx` 文件，并在 `docs.json` 导航中注册

## 部署

推送到默认分支后，通过 Mintlify 的 GitHub 集成自动部署。
