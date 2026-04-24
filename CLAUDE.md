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
- **api-reference/openapi-capability.yaml** - OpenAPI 规范文件（CapabilityService），定义所有 API 端点、Schema 及请求/响应结构。端点 `.mdx` 文件通过 `openapi` frontmatter 引用此文件
- **api-reference/endpoint/*.mdx** - 各 API 端点页面，仅包含 frontmatter（引用 OpenAPI YAML）。修改 API 文档内容请编辑 OpenAPI YAML
- **index.mdx** - 产品简介，包含核心概念（batch_id、material_id、处理状态、调用流程）
- **quickstart.mdx** - 快速入门指南，含 curl 示例
- **authentication.mdx** - 双 Header 鉴权说明（x-ti-app-id + x-ti-secret-code）

### 导航结构（docs.json）

两个标签页，API参考下分两个分组：
1. **产品导览**：index、quickstart、authentication
2. **API参考**
   - **文件与材料处理**：文件上传、图像质检、材料分类、材料抽取
   - **知识库查询**：ICD 疾病编码查询、医疗机构查询、医保目录查询、行政区划查询

### API 核心概念

- Base URL：`https://agents.textin.com/doc-agent/api/v1`
- 鉴权：`x-ti-app-id` + `x-ti-secret-code` 双 Header
- 关键实体：`batch_id`（批次 ID）、`material_id`（材料 ID）
- 处理状态（status）：0=待处理, 1=分类中, 2=抽取中, 3=已完成, 4=失败
- 各能力独立调用，不依赖案件流程，通过 batch_id 和 material_id 串联

## 内容规范

- 所有面向用户的文档使用简体中文
- API 端点页面使用 OpenAPI frontmatter（`openapi: 'METHOD /path'`），而非内联内容
- 新增/修改 API 端点详情，请编辑 `api-reference/openapi-capability.yaml`
- 新增端点页面：在 `api-reference/endpoint/` 下创建 `.mdx` 文件，并在 `docs.json` 导航中注册

## 部署

推送到默认分支后，通过 Mintlify 的 GitHub 集成自动部署。
