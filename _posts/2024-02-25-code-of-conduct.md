---
layout: post
title:  "Code of Conduct"
date:   2024-02-25 23:10:07 +0800
categories: code
---

# 编码规范

## 前端

### 1. 项目结构

在GitHub上建立私有仓库，并使用Vscode，装上Copilot插件。

* README.md 以Markdown格式的项目说明书，简要介绍项目内容
* .env 环境变量文件，不要上传至仓库
* .gitignore 忽略的文件 
* package.json npm使用的项目文件
* next.config.js nextjs的配置文件
* pages/ - 存放Next.js页面的目录。
* components/ - 存放React组件的目录。
* public/ - 存放静态资源的目录，如图片、字体等。
* src/ - 存放可复用的JavaScript和TypeScript代码。
* app/ - 存放服务层代码，如API调用等。
* styles/ - 存放CSS样式文件。
* tests/ - 存放单元测试文件。

### 2. Git Commit

提交应该遵循一定的规范<https://www.conventionalcommits.org/en/v1.0.0/>，一定要简要精炼写做了什么样的事儿。

* 类型: feat (新功能), fix (修复), docs (文档), style (格式), refactor (重构), test (测试), chore (构建过程或辅助工具的变动)
* 范围: 可选，表示影响的范围，如component, utils, build。
* 描述: 简明扼要的描述本次提交解决的问题。
* 示例: feat(login): 实现了登录的页面
* 修复某个错误(issue)在脚标写：Closes #1

### 3. 使用框架

* 使用Typescript编写页面，使用ES6以上的语法，注释需要遵循tsdoc的规范来标注。
* 使用Nextjs同构渲染框架，注意区分代码运行在服务端还是客户端。
* 使用React，常用的内容要解耦成可复用组件或库，注意组件的状态管理，并写上文档。
* 组件库选用Shadcn/UI+TailwindCSS，或者Antd。
* 数据库关系型选用MySQL，缓存数据库选用Redis，消息数据库选用RabbitMQ，可以使用typeorm与数据库交互。
* 数据验证使用class-validator和class-transformer。
* 使用Docker一键部署或测试。
* 使用Electron构建桌面应用程序，使用React Native构建移动端应用程序。

### 4. 前后端交互

* 支持Restful和OpenAPI规范，并写上注释。
* 使用Swagger测试以及生成接口文档。

