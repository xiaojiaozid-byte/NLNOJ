# NLNOJ 在线评测系统

一个功能完整的在线评测（Online Judge）系统，支持题目管理、代码提交、比赛、团队协作、论坛讨论等核心功能。

## 项目简介

本项目是一个全栈式在线评测平台，采用前后端分离架构设计。后端基于 Python FastAPI 构建，提供 RESTful API 服务；前端采用 Vue 3 + TypeScript 构建用户界面。系统支持多种编程语言的代码评测，包含比赛、团队、论坛、工单等完善的功能模块。

## 技术栈

### 后端

- **框架**: FastAPI (Python 3.13)
- **数据库**: SQLAlchemy ORM + Alembic 数据库迁移
- **数据库支持**: SQLite（开发环境）、PostgreSQL（生产环境）
- **认证**: JWT Token + Supabase
- **邮件服务**: SMTP

### 前端

- **框架**: Vue 3 + Composition API
- **语言**: TypeScript
- **构建工具**: Vite
- **样式**: Tailwind CSS
- **状态管理**: Pinia
- **路由**: Vue Router

### 其他组件

- **GCC 插件**: judge-plugin（防止选手自行控制编译优化等级）
- **容器化**: Docker + Docker Compose

## 功能特性

### 用户系统

- 用户注册与登录（支持邮箱、用户名、学号等多种标识符）
- JWT Token 认证与刷新机制
- 用户资料管理、头像/封面上传
- 主题自定义（背景图、明暗模式）
- 关注/粉丝系统

### 题目管理

- 题目创建、编辑、删除
- 题目难度分级与标签管理
- 题目来源追踪
- 测试点管理（支持单条添加和 ZIP 批量导入）
- 题目公开/私有权限控制

### 代码评测

- 实时提交代码评测
- 支持多种编程语言
- 比赛期间代码隐私保护
- 评测日志记录
- 评测结果查看

### 比赛系统

- 创建个人赛/团队赛
- ACM 赛制支持
- 比赛排名实时更新
- 比赛期间题目可见性控制
- 邀请码报名机制

### 团队系统

- 创建和管理团队
- 团队私有题库
- 成员管理与审核
- 团队转让与解散

### 论坛与社交

- 帖子发布与评论
- 置顶/锁定功能
- @提及通知
- 犇犇动态流
- 每日打卡

### 工单系统

- 提交技术问题工单
- 工单状态流转
- 指派负责人
- 附件上传

### 图床系统

- 图片上传与管理
- 水印处理（文字水印）
- 空间配额管理（普通/高级空间）

### 经验商店

- 打卡获取经验值
- 使用经验兑换 Tag 卡
- 贡献值系统

### 管理后台

- 用户管理（权限修改、封禁、密码重置）
- 批量用户操作
- 首页广告管理
- 评测管理员公示

## 项目结构

```
oj/
├── service/                 # 后端服务
│   ├── app/
│   │   ├── api/            # API 路由
│   │   ├── core/           # 核心配置
│   │   ├── models/         # 数据模型
│   │   ├── schemas/        # Pydantic 模型
│   │   ├── services/       # 业务逻辑
│   │   └── utils/          # 工具函数
│   ├── alembic/            # 数据库迁移
│   ├── scripts/            # 脚本工具
│   └── tests/              # 测试用例
│
├── web/                     # 前端应用
│   ├── src/
│   │   ├── api/            # API 客户端
│   │   ├── components/     # 公共组件
│   │   ├── stores/         # Pinia 状态
│   │   ├── views/          # 页面视图
│   │   └── utils/          # 工具函数
│   └── public/             # 静态资源
│
├── judge-plugin/           # GCC 评测插件
│   └── no_opt_pragma.cc    # 禁止优化pragma插件
│
├── docker-compose.yml      # Docker 编排
└── DEPLOY_CHECKLIST.md     # 部署清单
```

## 快速开始

### 前置要求

- Python 3.13+
- Node.js 20+
- Docker（生产部署）

### 本地开发

#### 后端启动

```bash
cd service

# 安装依赖
pip install uv
uv sync

# 复制环境配置
cp .env.example .env

# 初始化数据库（SQLite）
uv run alembic upgrade head

# 启动服务
uv run uvicorn app.main:app --reload
```

#### 前端启动

```bash
cd web

# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

#### 使用 Docker 运行

```bash
# 启动所有服务
docker-compose up -d
```

### 配置说明

后端配置文件 `service/.env`：

```env
# 数据库连接
DATABASE_URL=sqlite+aiosqlite:///./oj.db
# 或使用 PostgreSQL
DATABASE_URL=postgresql://user:pass@localhost:5432/oj

# JWT 密钥
JWT_SECRET=your-secret-key

# 环境模式
ENV=dev

# Supabase 配置（可选）
SUPABASE_URL=
SUPABASE_KEY=
```

## 部署指南

详细部署步骤请参阅 [DEPLOY_CHECKLIST.md](./DEPLOY_CHECKLIST.md)。

### 基本步骤

1. 服务器初始化，安装 Docker
2. 上传代码到服务器
3. 配置环境变量
4. 启动服务
5. 验证部署

### 访问服务

- 主页: `http://服务器IP/`
- 登录: `http://服务器IP/login`
- 管理后台: `http://服务器IP/admin`

## API 文档

服务启动后访问：

- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## 测试

```bash
cd service

# 运行所有测试
pytest

# 运行特定测试
pytest tests/test_auth_flow.py
```

## 开发规范

### 后端

- 使用 Pydantic 进行数据验证
- 使用 SQLAlchemy AsyncSession 进行数据库操作
- 所有 API 路由需包含权限依赖检查

### 前端

- 使用 TypeScript 进行类型安全开发
- 组件采用 Composition API 风格
- 样式使用 Tailwind CSS 工具类

## 许可证

本项目仅供学习交流使用。

## 相关文档

- [后端详细文档](./service/README.md)
- [前端详细文档](./web/README.md)
- [数据库配置指南](./service/SUPABASE_SETUP.md)
- [GCC 插件说明](./judge-plugin/README.md)
- [测试环境搭建](./service/scripts/README.md)
