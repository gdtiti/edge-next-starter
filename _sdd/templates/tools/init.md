# SDD 初始化命令模板

## 命令描述
`sdd.init` - 现有项目技术栈分析和 SDD 范式初始化

## 功能说明
该命令专门用于分析现有项目的技术栈、架构模式和开发规范，自动生成适合该项目的技术方案和基本宪法，确保 SDD 范式能够与现有代码库无缝集成。

## 使用场景
- 现有项目需要引入 SDD 范式
- 需要为现有代码库制定开发规范
- 技术栈迁移和架构优化
- 团队开发流程标准化

## 分析流程

### 1. 项目结构分析
```bash
# 自动检测项目结构
- 框架识别：Next.js, React, Vue, Angular 等
- 构建工具：Webpack, Vite, Rollup 等
- 包管理器：npm, yarn, pnpm 等
- 目录结构：MVC, MVP, Clean Architecture 等
```

### 2. 技术栈分析
```bash
# 核心技术识别
- 前端框架：React 19, Next.js 15
- 类型系统：TypeScript 5
- 样式方案：Tailwind CSS 4, CSS-in-JS
- 状态管理：Zustand, React Query
- 数据库：Prisma + PostgreSQL
- 认证方案：NextAuth.js
- UI 组件：shadcn/ui + Radix UI
- 工具库：Framer Motion, date-fns, axios
```

### 3. 开发规范分析
```bash
# 代码质量和规范
- ESLint 配置
- Prettier 格式化
- TypeScript 严格模式
- 组件设计模式
- 命名约定
- 文件组织结构
```

## 输出内容

### 1. 项目宪法 (CONSTITUTION.md)
基于技术栈分析生成的项目核心原则：
- 技术选型原则
- 代码质量标准
- 性能要求
- 安全规范
- 开发流程约定

### 2. 技术方案 (tech-stack.md)
详细的技术实现指导：
- 架构设计原则
- 组件开发规范
- 数据流管理
- API 设计标准
- 测试策略
- 部署配置

### 3. 集成建议 (integration-guide.md)
SDD 范式与现有项目的集成方案：
- 渐进式迁移策略
- 团队培训计划
- 工具集成配置
- 质量门禁设置

## 命令参数

### 基础用法
```bash
/sdd.init
```

### 带参数用法
```bash
/sdd.init --framework nextjs --strict-mode
/sdd.init --team-size 5 --quality-level high
/sdd.init --include-tests --performance-focus
```

### 参数说明
- `--framework`: 指定主要框架 (nextjs, react, vue, angular)
- `--strict-mode`: 启用严格模式质量标准
- `--team-size`: 团队规模，影响规范复杂度
- `--quality-level`: 质量等级 (basic, standard, high, enterprise)
- `--include-tests`: 包含测试策略生成
- `--performance-focus`: 重点关注性能优化
- `--security-focus`: 重点关注安全规范

## 分析报告模板

### 技术栈概览
```markdown
## 🎯 技术栈分析结果

### 核心框架
- **前端**: Next.js 15 + React 19
- **类型系统**: TypeScript 5
- **样式方案**: Tailwind CSS 4
- **组件库**: shadcn/ui + Radix UI

### 状态管理
- **本地状态**: Zustand
- **服务端状态**: TanStack Query
- **表单状态**: React Hook Form + Zod

### 数据层
- **ORM**: Prisma
- **数据库**: PostgreSQL
- **认证**: NextAuth.js
- **API**: RESTful + WebSocket

### 开发工具
- **构建**: Next.js 内置
- **代码检查**: ESLint + TypeScript
- **格式化**: 预设配置
- **版本控制**: Git
```

### 项目宪法模板
```markdown
# 项目宪法

## 🎯 核心价值观
1. **代码质量优先** - 所有代码必须通过类型检查和 ESLint 验证
2. **用户体验至上** - 响应式设计，性能优化，无障碍访问
3. **开发效率** - 组件化开发，工具链自动化
4. **团队协作** - 清晰的文档，统一的代码风格

## 🔧 技术原则
- **类型安全**: 100% TypeScript 覆盖
- **组件化**: 可复用、可测试的组件设计
- **性能优先**: 代码分割、懒加载、优化渲染
- **渐进增强**: 功能增强不破坏基础体验

## 📏 质量标准
- **测试覆盖率**: 核心功能 80%+
- **性能预算**: 首屏加载 < 2s
- **代码审查**: 所有 PR 必须经过审查
- **文档更新**: 功能变更同步更新文档

## 🚀 开发流程
1. SDD 规范制定
2. 技术方案设计
3. 组件开发实现
4. 测试验证
5. 代码审查
6. 部署发布
```

## 常见技术栈配置

### Next.js + TypeScript 项目
```typescript
// 技术规范
{
  "framework": "Next.js 15",
  "language": "TypeScript 5",
  "styling": "Tailwind CSS 4",
  "components": "shadcn/ui",
  "stateManagement": "Zustand",
  "dataFetching": "TanStack Query",
  "database": "Prisma + PostgreSQL",
  "authentication": "NextAuth.js"
}
```

### React 企业级项目
```typescript
// 企业级规范
{
  "testing": "Jest + React Testing Library",
  "cicd": "GitHub Actions",
  "monitoring": "Sentry + Analytics",
  "performance": "Lighthouse CI",
  "security": "ESLint Security Rules",
  "documentation": "Storybook + MDX"
}
```

## 集成建议

### 渐进式迁移
1. **第一阶段**: 引入 SDD 规范，新功能使用 SDD 流程
2. **第二阶段**: 重构核心模块，统一技术标准
3. **第三阶段**: 全面迁移，建立质量门禁

### 团队培训
- SDD 方法论培训 (2小时)
- 技术规范讲解 (1小时)
- 工具使用培训 (1小时)
- 实践演练 (4小时)

## 质量保证

### 自动化检查
- 代码格式检查
- 类型安全验证
- 性能基准测试
- 安全漏洞扫描

### 人工审查
- 架构设计审查
- 代码质量审查
- 用户体验审查
- 文档完整性检查

---

**注意**: 该命令生成的所有内容都应作为初始配置，团队可根据具体项目需求进行调整和优化。