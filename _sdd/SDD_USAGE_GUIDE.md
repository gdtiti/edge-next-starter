# SDD 使用指南 (SDD Usage Guide)

## 概述 (Overview)

SDD (Specification-Driven Development) 是一个为Cloudflare Edge Next.js项目量身定制的开发框架，通过AI代理协作和规范驱动流程，提升开发效率、代码质量和团队协作。

## 🚀 快速开始 (Quick Start)

### 1. 激活SDD系统

```bash
# 启动SDD编排器
/sdd

# 加载项目技能包
/memory:skill-memory cloudflare-edge-next-starter

# 查看可用命令
/help
```

### 2. 基础工作流程

#### 新功能开发
```bash
# 1. 创建新功能任务
/task:create "实现用户认证功能"

# 2. 启动规划工作流
/workflow:plan "用户认证系统设计"

# 3. 执行开发工作流
/workflow:execute
```

#### 问题修复
```bash
# 1. 启动bug诊断工作流
/workflow:bug-diagnosis "用户登录失败问题"

# 2. 创建测试修复工作流
/workflow:test-fix-gen "登录功能测试失败"

# 3. 执行测试循环
/workflow:test-cycle-execute
```

#### 架构审查
```bash
# 1. 启动架构审查工作流
/workflow:review --type=architecture

# 2. 质量门验证
/workflow:action-plan-verify

# 3. TDD合规性验证
/workflow:tdd-verify
```

## 🤖 SDD代理系统 (SDD Agent System)

### 代理角色介绍

#### 1. 初始化架构师 (init-architect)
**职责**: 项目架构设计和技术标准制定
**触发场景**:
- 项目初始化
- 架构变更需求
- 技术标准更新
- 性能优化分析

**使用示例**:
```bash
# 分析项目架构
/memory:skill-memory cloudflare-edge-next-starter

# 架构健康评估
/cli:mode:plan 评估当前系统架构健康度
```

#### 2. 规划专家 (planner)
**职责**: 需求分析和技术方案制定
**触发场景**:
- 新功能需求
- 复杂任务分解
- 技术方案设计
- 风险评估

**使用示例**:
```bash
# 功能规划
/workflow:plan "实现文件上传功能"

# 任务分解
/task:breakdown task-id-123

# 需求分析
/ask:task-decomposition 分解用户管理功能
```

#### 3. 实现专家 (implementer)
**职责**: 代码实现和质量保证
**触发场景**:
- 功能开发
- 代码重构
- 测试编写
- 文档更新

**使用示例**:
```bash
# 执行开发任务
/task:execute task-id-456

# 代码生成
/cli:codex-execute "生成用户Repository类"

# TDD开发
/workflow:tdd-plan "实现文章评论功能"
```

#### 4. 分析专家 (analyzer)
**职责**: 代码质量分析和性能优化
**触发场景**:
- 代码质量检查
- 性能问题分析
- 技术债务评估
- 架构合规验证

**使用示例**:
```bash
# 代码质量分析
/cli:analyze 代码质量和架构健康度

# 性能分析
/cli:mode:bug-diagnosis "API响应时间过长"

# 架构审查
/workflow:review --type=architecture
```

#### 5. 调试专家 (debugger)
**职责**: 问题诊断和故障排除
**触发场景**:
- Bug报告处理
- 生产环境问题
- 测试失败诊断
- 性能问题排查

**使用示例**:
```bash
# Bug诊断
/workflow:bug-diagnosis "用户无法登录问题"

# 测试失败修复
/workflow:test-fix-gen source-session-789

# 错误分析
/cli:mode:bug-diagnosis "数据库连接错误"
```

#### 6. 学习专家 (learner)
**职责**: 经验总结和知识管理
**触发场景**:
- 任务完成总结
- 最佳实践提炼
- 团队能力提升
- 知识库更新

**使用示例**:
```bash
# 会话完成总结
/workflow:session:complete

# 工作流经验总结
/memory:workflow-skill-memory session-id-456

# 生成技能包
/memory:skill-memory cloudflare-edge-next-starter
```

## 🔄 SDD工作流程 (SDD Workflows)

### 1. 特性开发工作流 (Feature Development)

**流程**: `planner → implementer → analyzer → learner`
**时长**: 3-7天

```bash
# 启动特性开发
/workflow:plan "新功能需求分析"

# 创建实施任务
/task:create "具体功能实现"

# 执行开发
/workflow:execute

# 质量审查
/workflow:review
```

**质量门槛**:
- ✅ 需求规范完整性
- ✅ 代码质量和测试覆盖
- ✅ 性能和安全验证
- ✅ 文档同步和知识捕获

### 2. Bug解决工作流 (Bug Resolution)

**流程**: `debugger → implementer → analyzer`
**时长**: 0.5-2天

```bash
# 问题诊断
/workflow:bug-diagnosis "具体问题描述"

# 创建修复工作流
/workflow:test-fix-gen "问题源或描述"

# 执行修复循环
/workflow:test-cycle-execute --max-iterations=5
```

**严重级别**:
- 🔴 **关键**: 4小时内解决
- 🟠 **高**: 1天内解决
- 🟡 **中**: 3天内解决
- 🟢 **低**: 1周内解决

### 3. 架构审查工作流 (Architecture Review)

**流程**: `analyzer → init_architect → planner`
**时长**: 1-3天

```bash
# 启动架构审查
/workflow:review --type=architecture

# 设计一致性验证
/workflow:action-plan-verify

# TDD合规检查
/workflow:tdd-verify
```

**审查类型**:
- **全面审查**: 季度性系统架构评估
- **特性影响审查**: 特定功能的架构影响
- **性能审查**: 性能相关的架构分析
- **安全审查**: 安全架构组件评估

## 🛠️ CLI工具集成 (CLI Tool Integration)

### Gemini - 分析和规划
```bash
# 架构分析
cd /path/to/project && gemini -p "
PURPOSE: 分析项目架构和代码质量
TASK: • 评估架构设计 • 识别改进机会 • 提供优化建议
MODE: analysis
CONTEXT: @**/* @CLAUDE.md | Memory: 基于SDD架构标准
EXPECTED: 架构分析报告和改进建议
RULES: $(cat ~/.claude/workflows/cli-templates/prompts/analysis/02-review-architecture.txt)
"
```

### Qwen - 备用分析
```bash
# 代码模式分析
cd /path/to/project && qwen -p "
PURPOSE: 分析代码模式和设计规范
TASK: • 识别设计模式 • 评估代码质量 • 检查规范遵循
MODE: analysis
CONTEXT: @src/**/* @types/**/* | Memory: SDD编码标准
EXPECTED: 代码模式分析报告
RULES: $(cat ~/.claude/workflows/cli-templates/prompts/analysis/02-analyze-code-patterns.txt)
"
```

### Codex - 代码实现
```bash
# 功能实现
codex -C /path/to/project --full-auto exec "
PURPOSE: 实现用户认证功能
TASK: • 创建认证服务 • 实现JWT处理 • 添加中间件 • 编写测试
MODE: auto
CONTEXT: @src/auth/**/* @lib/auth/**/* | Memory: 遵循Repository模式和Edge Runtime规范
EXPECTED: 完整的认证功能实现和测试套件
RULES: $(cat ~/.claude/workflows/cli-templates/prompts/development/02-implement-feature.txt) | auto=FULL operations
" --skip-git-repo-check -s danger-full-access
```

## 📊 质量监控 (Quality Monitoring)

### 实时质量指标
- **测试覆盖率**: ≥80%
- **TypeScript严格模式**: 100%
- **ESLint警告**: 0
- **Lighthouse性能**: ≥95分
- **API响应时间**: P95 <200ms

### 自动化质量检查
```bash
# 代码质量检查
/cli:analyze 代码质量和技术债务

# 性能分析
/cli:mode:code-analysis 性能瓶颈和优化机会

# 安全评估
/cli:mode:bug-diagnosis 安全漏洞和风险评估
```

## 📚 知识管理 (Knowledge Management)

### 技能包系统
```bash
# 生成项目技能包
/memory:skill-memory cloudflare-edge-next-starter

# 加载特定技能
/memory:load-skill-memory react-dev "React组件开发最佳实践"

# 更新技术栈文档
/memory:tech-research nextjs-15 --regenerate
```

### 经验总结
```bash
# 工作流经验总结
/memory:workflow-skill-memory session-id-123

# 最佳实践更新
/memory:update-related --tool gemini

# 风格技能包生成
/memory:style-skill-memory --package-name ui-components
```

## 🎯 最佳实践 (Best Practices)

### 1. 开始工作前
```bash
# 1. 加载项目上下文
Skill(cloudflare-edge-next-starter)

# 2. 检查当前状态
/workflow:status

# 3. 明确任务目标
/task:create "明确的任务描述"
```

### 2. 开发过程中
```bash
# 1. 定期质量检查
/cli:analyze

# 2. 同步进度
/workflow:status task-id

# 3. 记录重要决策
# (在代码中添加注释和文档)
```

### 3. 完成工作时
```bash
# 1. 质量审查
/workflow:review

# 2. 经验总结
/workflow:session:complete

# 3. 知识更新
/memory:workflow-skill-memory session-id
```

## 🔧 故障排除 (Troubleshooting)

### 常见问题

#### 1. 代理无响应
```bash
# 检查工作流状态
/workflow:status

# 重启工作流会话
/workflow:session:resume

# 查看活跃会话
/workflow:session:list
```

#### 2. 质量检查失败
```bash
# 详细分析问题
/cli:mode:bug-diagnosis "质量检查失败原因"

# 生成修复建议
/cli:execute "修复代码质量问题"

# 重新运行检查
/workflow:tdd-verify
```

#### 3. 性能问题
```bash
# 性能分析
/cli:mode:code-analysis "系统性能问题"

# 生成优化建议
/cli:analyze "性能优化机会"

# 实施优化
/cli:execute "实施性能优化方案"
```

### 获取帮助
```bash
# 查看可用命令
/help

# SDD特定帮助
/sdd --help

# 工作流帮助
/workflow:help
```

## 📈 持续改进 (Continuous Improvement)

### 定期回顾
- **每周**: 代码质量回顾
- **每月**: 架构健康评估
- **每季度**: SDD流程优化
- **每年**: 技术栈升级规划

### 反馈机制
- **即时反馈**: 工作流中的质量门
- **定期反馈**: 团队回顾会议
- **长期反馈**: 年度技术规划

## 🎉 结语 (Conclusion)

SDD框架通过AI代理协作、规范驱动流程和持续质量监控，为Cloudflare Edge Next.js项目提供了完整的开发支持。正确使用SDD将显著提升开发效率、代码质量和团队协作能力。

**记住**: 让规范驱动开发成为我们的标准实践！🚀

---

*文档版本*: v1.0.0
*最后更新*: 2025-11-21
*维护者*: SDD架构师团队