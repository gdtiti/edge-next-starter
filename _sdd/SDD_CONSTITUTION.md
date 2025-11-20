# SDD 项目宪法 (Project Constitution)

## 项目信息

**项目名称**: Cloudflare Edge Next.js Starter
**项目类型**: 云原生全栈应用 (Cloudflare Edge Runtime + Next.js)
**技术栈**: TypeScript, Next.js 15, React 19, Cloudflare D1/R2/KV
**开发框架**: SDD (规范驱动开发)

---

## 🔖 SDD 核心原则 (Core Principles)

### 1. 规范驱动，质量内建 (Specification-First, Quality-Built-In)

**指导思想**: 所有开发活动必须基于明确的规范，质量内建于开发流程而非事后检查。

**执行标准**:
- **需求规范**: 任何功能开发前必须包含完整的需求文档、API规范和验收标准
- **设计审查**: 技术方案必须经过架构师审查，确保符合Edge Runtime最佳实践
- **代码规范**: 严格遵循项目的TypeScript编码规范和架构模式
- **测试先行**: TDD/BDD模式，测试覆盖率不低于80%，关键路径100%覆盖

### 2. 云原生优先 (Cloud-Native First)

**指导思想**: 充分利用Cloudflare Edge生态优势，构建全球分布式的高性能应用。

**执行标准**:
- **Edge Runtime兼容**: 所有代码必须兼容Cloudflare Edge Runtime限制
- **无状态设计**: API路由和业务逻辑必须无状态，状态存储使用D1/KV
- **全球优化**: 数据访问和缓存策略考虑全球延迟优化
- **成本效率**: 合理使用R2存储和KV缓存，控制成本

### 3. Repository模式 + Service层架构

**指导思想**: 清晰的分层架构，数据访问与业务逻辑分离，确保可测试性和可维护性。

**执行标准**:
- **Repository层**: 所有数据访问操作通过Repository接口，支持测试和未来扩展
- **Service层**: 业务逻辑封装在lib/各模块中，保持单一职责
- **错误处理**: 统一的错误处理和日志记录机制
- **类型安全**: 完整的TypeScript类型定义，使用Zod进行运行时验证

---

## 🛠️ 开发规范 (Development Standards)

### 代码质量标准

```typescript
// 代码质量基线
export const CODE_QUALITY_BASELINE = {
  typescript: "strict",           // 严格TypeScript模式
  eslint: "recommended",         // ESLint推荐规则
  test_coverage: 80,             // 最低测试覆盖率
  performance: "lighthouse_95",  // Lighthouse性能评分
  bundle_size: "edge_optimized"  // Edge优化打包
}
```

### 架构约束

**允许的模块模式**:
- ✅ Repository Pattern (repositories/*.ts)
- ✅ Service Layer (lib/*/index.ts)
- ✅ Middleware Pattern (withMiddleware包装)
- ✅ Server Actions (app/actions/*.ts)
- ✅ API Routes (app/api/*/route.ts)

**禁止的反模式**:
- ❌ 直接在组件中调用数据库
- ❌ 硬编码的环境变量和配置
- ❌ 不兼容Edge Runtime的Node.js API
- ❌ 缺乏错误处理的异步操作

### 命名约定

```typescript
// 文件命名规范
export const FILE_NAMING = {
  components: "PascalCase.tsx",           // UserProfile.tsx
  repositories: "kebab-case.repository.ts", // user.repository.ts
  utilities: "kebab-case.util.ts",         // date.util.ts
  types: "kebab-case.types.ts",           // api.types.ts
  routes: "route.ts",                     // API路由文件名固定
  middleware: "kebab-case.middleware.ts"   // auth.middleware.ts
}

// 变量命名规范
export const VARIABLE_NAMING = {
  constants: "UPPER_SNAKE_CASE",          // MAX_FILE_SIZE
  variables: "camelCase",                 // userProfile
  functions: "camelCase",                 // getUserProfile
  classes: "PascalCase",                  // UserRepository
  interfaces: "PascalCase with I prefix", // IUserRepository
  types: "PascalCase"                     // UserProfile
}
```

---

## 🧪 测试策略 (Testing Strategy)

### 测试金字塔

```
           E2E Tests (5%)
         ┌─────────────────┐
        │  Integration     │ (15%)
       └─────────────────────┘
      │    Unit Tests         │ (80%)
     └─────────────────────────┘
```

**测试要求**:
- **单元测试**: Repository层、Service层、工具函数
- **集成测试**: API端点、数据库操作、云服务集成
- **组件测试**: React组件的交互和渲染
- **E2E测试**: 关键用户流程（可选）

### 测试工具链

```json
{
  "framework": "vitest",
  "environment": "jsdom",
  "assertions": "@testing-library/react",
  "mocking": "vi.mock",
  "coverage": "c8",
  "reporting": "verbose + html"
}
```

---

## 🚀 部署与运维 (Deployment & Operations)

### 环境管理

| 环境 | 分支 | 数据库 | 存储 | 监控 |
|------|------|--------|------|------|
| 本地开发 | local | SQLite本地 | 模拟 | 日志输出 |
| 测试环境 | develop | D1测试 | R2测试桶 | 可选分析 |
| 生产环境 | main | D1生产 | R2生产桶 | Analytics Engine |

### CI/CD流程

```yaml
# 提交流程检查
commit_flow:
  - pre_commit: lint + format + type_check
  - push: test_suite + coverage_report
  - pr: full_suite + security_scan + build_check

# 部署流程
deployment_flow:
  develop_branch: auto_deploy_to_test
  main_branch: auto_deploy_to_production
  pull_request: preview_deployment
```

---

## 📚 文档规范 (Documentation Standards)

### 文档结构

```
docs/
├── README.md              # 项目概览 (中英双语)
├── QUICKSTART.md          # 环境搭建指南
├── ARCHITECTURE.md        # 架构设计文档
├── DEVELOPMENT.md         # 开发规范和最佳实践
├── DEPLOYMENT.md          # 部署配置和故障排除
├── SDD_CONSTITUTION.md    # SDD项目宪法 (本文件)
└── guides/               # 专题指南
    ├── authentication.md
    ├── database-migrations.md
    └── repository-pattern.md
```

### 文档要求

- **双语支持**: 中文文档为主，关键文档提供英文版本
- **实时更新**: 代码变更必须同步更新相关文档
- **示例代码**: 所有关键概念必须包含可运行的示例代码
- **故障排除**: 常见问题和解决方案的详细说明

---

## 🔐 安全与合规 (Security & Compliance)

### 安全原则

```typescript
// 安全配置基线
export const SECURITY_BASELINE = {
  authentication: "nextauth_jwt",           // JWT令牌认证
  authorization: "role_based_access",       // 基于角色的访问控制
  rate_limiting: "kv_sliding_window",      // KV滑动窗口限流
  input_validation: "zod_schema_validation", // Zod模式验证
  secret_management: "cloudflare_secrets",  // Cloudflare密钥管理
  https_only: "enforced_by_platform"        // 强制HTTPS
}
```

### 数据保护

- **个人数据**: 遵循GDPR要求，最小化数据收集
- **数据加密**: 传输加密(HTTPS) + 存储加密(R2默认)
- **访问控制**: 最小权限原则，定期权限审查
- **审计日志**: 关键操作的完整审计追踪

---

## 🤖 AI辅助开发 (AI-Assisted Development)

### SDD工具集成

```typescript
// AI代码生成配置
export const AI_CODE_GENERATION = {
  api_routes: "enabled",        // 自动生成API路由模板
  repositories: "enabled",      // 自动生成Repository类
  test_suites: "enabled",       // 自动生成测试用例
  types: "enabled",            // 自动生成TypeScript类型
  documentation: "enabled"     // 自动生成文档注释
}

// AI质量检查
export const AI_QUALITY_CHECKS = {
  code_review: "enabled",      // AI代码审查
  best_practices: "enabled",   // 最佳实践建议
  security_scan: "enabled",    // 安全漏洞检查
  performance_analysis: "enabled", // 性能优化建议
  documentation_sync: "enabled" // 文档同步检查
}
```

### 人工监督

- **代码审查**: AI生成代码必须经过人工审查
- **架构决策**: 重要架构变更由人工决策
- **安全验证**: 安全相关的代码变更需要额外验证
- **测试验证**: AI生成的测试用例需要人工验证

---

## 📈 质量指标 (Quality Metrics)

### 技术指标

| 指标 | 目标值 | 测量频率 |
|------|--------|----------|
| 测试覆盖率 | ≥80% | 每次提交 |
| TypeScript严格模式 | 100% | 持续检查 |
| ESLint警告 | 0 | 每次提交 |
| Lighthouse性能 | ≥95 | 每次构建 |
| 构建时间 | <2分钟 | 每次CI |

### 业务指标

| 指标 | 目标值 | 测量频率 |
|------|--------|----------|
| API响应时间 | <200ms (P95) | 实时监控 |
| 错误率 | <0.1% | 实时监控 |
| 可用性 | ≥99.9% | 实时监控 |
| 用户体验评分 | ≥90 | 月度评估 |

---

## 🔄 持续改进 (Continuous Improvement)

### 回顾机制

- **每周代码回顾**: 代码质量和技术债务回顾
- **每月架构回顾**: 架构演进和技术选型评估
- **每季度流程回顾**: 开发流程和工具链优化
- **年度技术规划**: 技术栈升级和架构重构规划

### 知识管理

- **最佳实践库**: 收集和分享开发最佳实践
- **故障案例库**: 记录和分析生产故障
- **技术分享**: 定期技术分享和培训
- **外部学习**: 跟踪行业新技术和趋势

---

## 🎯 SDD 执行框架 (SDD Execution Framework)

### 代理角色定义

```typescript
export const SDD_AGENTS = {
  init_architect: {
    role: "项目初始化和架构设计",
    responsibilities: [
      "项目结构分析和规划",
      "技术栈选择和架构设计",
      "开发规范制定和维护",
      "SDD框架配置和优化"
    ]
  },

  planner: {
    role: "需求分析和技术方案制定",
    responsibilities: [
      "需求分析和规范制定",
      "技术方案设计和评估",
      "开发计划制定和跟踪",
      "风险评估和缓解策略"
    ]
  },

  implementer: {
    role: "代码实现和质量保证",
    responsibilities: [
      "代码实现和单元测试",
      "代码审查和质量检查",
      "文档更新和维护",
      "性能优化和调试"
    ]
  },

  analyzer: {
    role: "质量分析和架构评估",
    responsibilities: [
      "代码质量分析",
      "架构健康度评估",
      "性能分析和优化建议",
      "技术债务识别和管理"
    ]
  },

  debugger: {
    role: "问题诊断和解决方案",
    responsibilities: [
      "问题根因分析",
      "解决方案设计和实施",
      "故障排除和修复",
      "预防措施制定"
    ]
  },

  learner: {
    role: "经验总结和知识管理",
    responsibilities: [
      "项目经验总结",
      "最佳实践提炼",
      "知识库建设和维护",
      "团队能力提升建议"
    ]
  }
}
```

### 工作流程集成

```typescript
// SDD工作流配置
export const SDD_WORKFLOW_INTEGRATION = {
  on_feature_start: ["init_architect", "planner"],
  on_development: ["implementer", "analyzer"],
  on_issue: ["debugger", "analyzer"],
  on_completion: ["learner", "analyzer"],

  quality_gates: {
    planning: "规范完整性检查",
    development: "代码质量和测试覆盖",
    deployment: "性能和安全验证"
  },

  auto_triggers: {
    code_change: "质量分析和建议",
    test_failure: "问题诊断和修复建议",
    performance_regression: "性能优化建议"
  }
}
```

---

## 📋 宪法执行 (Constitution Enforcement)

### 合规检查

每次PR必须通过以下检查：
- [ ] SDD原则合规性检查
- [ ] 代码质量基线检查
- [ ] 测试覆盖率检查
- [ ] 文档同步检查
- [ ] 安全合规检查

### 违规处理

**轻微违规**:
- 提交修复建议
- 要求在指定时间内修复
- 记录违规事项

**严重违规**:
- 阻止PR合并
- 要求架构师审查
- 团队内部分享和改进

---

## 🎉 结语 (Conclusion)

本宪法确立了项目的核心价值观和开发准则，为团队提供统一的行动指南。通过严格执行SDD规范，我们致力于构建高质量、可维护、高性能的云原生应用。

**让规范驱动开发成为我们的标准实践！**

---

*宪法版本: v1.0.0*
*最后更新: 2025-11-21*
*维护者: SDD架构师团队*