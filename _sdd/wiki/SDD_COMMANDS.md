# SDD 范式命令系统使用指南

## 🎯 命令概览

SDD 范式命令系统提供了一套完整的规范驱动开发工作流，包含 16 个核心命令：

### 🏗️ 主流程命令
| 命令 | 功能描述 | 使用阶段 |
|------|----------|----------|
| `/sdd.init` | 现有项目技术栈分析和初始化 | 项目初始化 |
| `/sdd.constitution` | 制定项目宪法 | 项目启动 |
| `/sdd.specify` | 创建功能规范 | 需求分析 |
| `/sdd.plan` | 制定技术计划 | 技术设计 |
| `/sdd.tasks` | 分解开发任务 | ���务规划 |
| `/sdd.implement` | 执行实现任务 | 开发实现 |

### 🔍 质量保证命令
| 命令 | 功能描述 | 使用阶段 |
|------|----------|----------|
| `/sdd.clarify` | 澄清模糊事项 | 任意阶段 |
| `/sdd.analyze` | 分析一致性 | 质量保证 |
| `/sdd.checklist` | 生成检查清单 | 质量保证 |

### 🚨 错误处理和调试命令
| 命令 | 功能描述 | 使用阶段 |
|------|----------|----------|
| `/sdd.debug.init` | 错误初始化和建档 | 错误发现 |
| `/sdd.debug.analyze` | 深度根因分析 | 错误分析 |
| `/sdd.debug.solutions` | 设计多个解决方案 | 方案设计 |
| `/sdd.debug.validate` | 验证解决方案 | 方案验证 |
| `/sdd.debug.implement` | 实施修复方案 | 实施修复 |
| `/sdd.learn` | 经验学习和知识库更新 | 经验总结 |

### 🧠 智能辅助命令
| 命令 | 功能描述 | 使用阶段 |
|------|----------|----------|
| `/sdd.history.check` | 检查历史思路和解决方案 | 方案设计 |
| `/sdd.patterns.extract` | 提取错误模式 | 持续改进 |
| `/sdd.knowledge.search` | 搜索相关知识库 | 问题解决 |

---

## 🚀 快速开始

### 1. 项目初始化
```bash
# 分析现有项目技术栈并生成 SDD 配置
/sdd.init

# 带参数的初始化
/sdd.init --framework nextjs --strict-mode
/sdd.init --team-size 5 --quality-level high

# 制定项目宪法
/sdd.constitution

# 示例输入：
创建一个高质量的用户管理系统，重视代码质量和安全性，使用 React 和 Node.js 技术栈
```

### 2. 功能开发流程
```bash
# 1. 创建功能规范
/sdd.specify 我想要一个用户登录系统，支持邮箱和密码登录

# 2. 制定技术计划
/sdd.plan 使用 React 18 + TypeScript，Node.js + Express，PostgreSQL 数据库

# 3. 分解开发任务
/sdd.tasks

# 4. 执行实现
/sdd.implement
```

---

## 📋 详细命令说明

### `/sdd.init` - 现有项目技术栈分析和初始化

**功能**：分析现有项目的技术栈、架构模式和开发规范，自动生成适合该项目的 SDD 配置

**使用场景**：
- 现有项目需要引入 SDD 范式
- 需要为现有代码库制定开发规范
- 技术栈迁移和架构优化
- 团队开发流程标准化

**输入格式**：
```bash
/sdd.init [选项]
```

**示例**：
```bash
# 基础用法
/sdd.init

# 指定框架和质量标准
/sdd.init --framework nextjs --strict-mode

# 团队配置
/sdd.init --team-size 5 --quality-level high

# 功能重点
/sdd.init --include-tests --performance-focus
```

**输出**：
- 项目宪法文档（基于现有技术栈）
- 技术方案和开发规范
- SDD 集成建议
- 团队培训计划

**选项说明**：
- `--framework`: 指定主要框架 (nextjs, react, vue, angular)
- `--strict-mode`: 启用严格模式质量标准
- `--team-size`: 团队规模，影响规范复杂度
- `--quality-level`: 质量等级 (basic, standard, high, enterprise)
- `--include-tests`: 包含测试策略生成
- `--performance-focus`: 重点关注性能优化
- `--security-focus`: 重点关注安全规范

---

### `/sdd.constitution` - 项目宪法制定

**功能**：建立项目的根本性规则和原则

**使用场景**：
- 项目启动时
- 项目原则需要更新时
- 团队规范需要调整时

**输入格式**：
```bash
/sdd.constitution [项目原则描述]
```

**示例**：
```bash
/sdd.constitution 创建一个高质量的用户管理系统，重视代码质量和安全性，使用 React 和 Node.js 技术栈，测试覆盖率要求 80% 以上
```

**输出**：
- 项目宪法文档
- 核心原则定义
- 技术约束设定
- 开发规范制定

---

### `/sdd.specify` - 功能规范制定

**功能**：将用户需求转换为结构化的功能规范

**使用场景**：
- 新功能需求分析时
- 功能规范需要更新时
- 需求不明确需要澄清时

**输入格式**：
```bash
/sdd.specify [功能需求描述]
```

**示例**：
```bash
/sdd.specify 创建一个用户登录系统，支持邮箱和密码登录，包含密码重置功能，要求响应时间小于 200ms
```

**输出**：
- 功能规范文档
- 用户故事定义
- 验收标准
- 成功指标
- 澄清问题列表

---

### `/sdd.plan` - 技术计划制定

**功能**：将功能规范转换为详细的技术实现方案

**使用场景**：
- 功能规范完成后
- 技术方案需要设计时
- 架构决策需要制定时

**输入格式**：
```bash
/sdd.plan [技术栈和约束描述]
```

**示例**：
```bash
/sdd.plan 前端使用 React 18 + TypeScript + Tailwind CSS，后端使用 Node.js + Express + TypeScript，数据库使用 PostgreSQL，缓存使用 Redis，认证使用 JWT
```

**输出**：
- 技术实现计划
- 系统架构设计
- 数据模型设计
- API 接口设计
- 安全设计方案

---

### `/sdd.tasks` - 任务分解

**功能**：将技术计划分解为可执行的任务列表

**使用场景**：
- 技术计划完成后
- 开发任务需要规划时
- 工作量需要评估时

**输入格式**：
```bash
/sdd.tasks [开发模式和约束]
```

**示例**：
```bash
/sdd.tasks 使用 TDD 开发模式，重视测试覆盖率，预计工期 2 周
```

**输出**：
- 详细任务清单
- 任务依赖关系
- 时间估算
- 并行执行策略
- 质量检查点

---

### `/sdd.implement` - 实现执行

**功能**：按照任务清单执行所有开发任务

**使用场景**：
- 任务清单完成后
- 开始功能实现时
- 需要自动化实现时

**输入格式**：
```bash
/sdd.implement [执行选项]
```

**示例**：
```bash
/sdd.implement
/sdd.implement --continue
/sdd.implement --from T020
/sdd.implement --skip-tests
```

**输出**：
- 完整功能实现
- 测试用例
- API 文档
- 部署配置

---

### `/sdd.clarify` - 澄清模糊事项

**功能**：识别和解决规范、计划中的模糊事项

**使用场景**：
- 发现文档中有模糊表述时
- 需要明确具体细节时
- 决策需要支持时

**输入格式**：
```bash
/sdd.clarify [澄清范围]
```

**示例**：
```bash
/sdd.clarify
/sdd.clarify spec.md
/sdd.clarify --type performance
```

**输出**：
- 模糊点识别
- 问题分类
- 解决方案建议
- 决策支持

---

### `/sdd.analyze` - 一致性分析

**功能**：检查所有文档间的一致性和完整性

**使用场景**：
- 需要质量检查时
- 文档需要验证时
- 问题需要诊断时

**输入格式**：
```bash
/sdd.analyze [分析选项]
```

**示例**：
```bash
/sdd.analyze
/sdd.analyze --consistency-only
/sdd.analyze --score-only
```

**输出**：
- 一致性检查报告
- 完整性分析结果
- 质量评分
- 改进建议

---

### `/sdd.checklist` - 质量检查清单

**功能**：为各阶段生成质量检查清单

**使用场景**：
- 需要质量保证时
- 制定验收标准时
- 进行代码审查时

**输入格式**：
```bash
/sdd.checklist [清单类型]
```

**示例**：
```bash
/sdd.checklist
/sdd.checklist --stage requirements
/sdd.checklist --type security
/sdd.checklist --update
```

**输出**：
- 需求质量检查清单
- 设计质量检查清单
- 实现质量检查清单
- 安全检查清单

---

## 🔄 完整工作流示例

### 场景：现有项目开发用户认证功能

```bash
# 1. 分析现有项目并初始化 SDD（如果是现有项目）
/sdd.init --framework nextjs --strict-mode

# 2. 制定项目宪法（如果还没有或需要更新）
/sdd.constitution 创建一个高质量的用户管理系统，重视代码质量和安全性，使用 React 和 Node.js 技术栈

# 3. 创建功能规范
/sdd.specify 我想要一个用户认证系统，支持用户注册、登录、密码重置功能，要求安全性高，用户体验好

# 4. 澄清不明确的事项（如果需要）
/sdd.clarify

# 5. 制定技术计划
/sdd.plan 使用 React 18 + TypeScript，Node.js + Express，PostgreSQL 数据库，JWT 认证，Redis 缓存

# 6. 分析一致性
/sdd.analyze

# 7. 分解开发任务
/sdd.tasks

# 8. 生成质量检查清单
/sdd.checklist

# 9. 执行实现
/sdd.implement

# 10. 最终质量检查
/sdd.analyze
```

---

## 🚨 错误处理和调试命令详解

### `/sdd.debug.init` - 错误初始化和建档

**功能**：系统化记录错误信息，建立完整错误档案

**核心价值**：
- 🎯 **避免遗忘**：确保每个错误都被完整记录
- 📊 **统一标准**：建立结构化的错误信息格式
- 🔍 **便于分析**：为后续分析提供完整上下文

**使用场景**：
- 发现新错误或异常
- 需要系统化记录错误信息
- 准备进行错误分析

**输入格式**：
```bash
/sdd.debug.init [错误描���]
/sdd.debug.init --type [错误类型] --severity [严重程度] --context [上下文]
```

**示例**：
```bash
/sdd.debug.init 用户登录接口返回500错误，数据库连接超时
/sdd.debug.init --type database --severity high --context production
```

---

### `/sdd.debug.analyze` - 深度根因分析

**功能**：强制进行深度根因分析，避免急于解决表面问题

**核心价值**：
- 🔍 **深度分析**：使��多种分析方法确保找到根本原因
- 🚫 **防止急于求成**：强制完成分析才能进入方案设计
- 📊 **系统性方法**：提供结构化的分析框架

**分析方法**：
- **5 Whys 分析法**：连续追问根本原因
- **鱼骨图分析**：多维度分析问题
- **时序分析**：分析事件发生的时间序列
- **对比分析**：对比正常和异常状态

**输入格式**：
```bash
/sdd.debug.analyze [错误ID]
/sdd.debug.analyze --deep --method 5whys --error-id [ID]
```

**防错机制**：
- ❌ 禁止直接跳到解决方案
- ✅ 强制完成根因分析
- 🔍 多角度验证分析结果

---

### `/sdd.debug.solutions` - 智能方案设计

**功能**：设计多个解决方案，避免重复设计和过度简化

**核心价值**：
- 🔄 **多方案对比**：至少提供3个解决方案供选择
- 🚫 **防止重复**：自动检查是否已有类似功能
- ✅ **完整性保证**：确保方案不破坏原有设计
- 🎯 **实用导向**：避免过度简化的模拟数据方案

**设计原则**：
- **复用检查**：检查是否已有类似功能
- **完整性检查**：确保方案不破坏原有设计
- **复杂度评估**：避免过度复杂的解决方案

**输入格式**：
```bash
/sdd.debug.solutions [错误ID]
/sdd.debug.solutions --min-options 3 --check-duplicates --no-simplification
```

**智能检查**：
- 🔍 历史方案相似性检查
- 🚫 模拟数据使用检测
- 📊 复杂度风险评估

---

### `/sdd.debug.validate` - 严格方案验证

**功能**：在实施前严格验证解决方案有效性

**核心价值**：
- 🧪 **真实环境验证**：禁止使用模拟数据作为最终验证
- 📊 **全面测试**：功能、性能、安全、集成全方位验证
- 🚪 **质量门禁**：不通过验证不允许实施

**验证层次**：
1. **单元测试** - 验证核心逻辑
2. **集成测试** - 验证系统协作
3. **端到端测试** - 验证完整流程
4. **性能测试** - 验证性能影响
5. **安全测试** - 验证安全性

**输入格式**：
```bash
/sdd.debug.validate [错误ID] [方案编号]
/sdd.debug.validate --prototype --real-data --no-mock --integration-test
```

**质量门禁**：
- ✅ 测试覆盖率 > 90%
- ✅ 性能影响 < 5%
- ✅ 无新的安全风险
- ✅ 兼容性测试通过

---

### `/sdd.learn` - 经验学习和知识库更新

**功能**：将错误处理经验纳入知识库，避免重复犯错

**核心价值**：
- 🧠 **永不遗忘**：所有思路和尝试都被记录
- 🎯 **智能提醒**：自动检测重复的失败思路
- 📊 **模式识别**：从历史中提取有价值的信息
- 🎓 **持续改进**：系统性地改进错误处理能力

**学习内容**：
- **错误模式提取**：识别错误发生的模式
- **解决方案模式**：总结有效的解决方案
- **预防措施**：制定预防类似错误的措施
- **知识更新**：更新开发指南和最佳实践

**输入格式**：
```bash
/sdd.learn [错误ID]
/sdd.learn --extract-patterns --update-guidelines --team-share
```

---

## 🔄 完整错误处理工作流示例

### 场景：数据库性能问题处理

```bash
# 1. 错误发现和建档
/sdd.debug.init --type database --severity high "用户查询响应时间超过30秒"

# 2. 深度根因分析
/sdd.debug.analyze --method 5whys --deep ERR20241020

# 3. 检查历史思路
/sdd.history.check "使用缓存解决数据库问题"
# 输出：⚠️ 该思路在 2024-09-15 已尝试，结果：缓存一致性问题

# 4. 设计多个解决方案
/sdd.debug.solutions --min-options 3 --check-duplicates ERR20241020

# 5. 严格验证最佳方案
/sdd.debug.validate --prototype --real-data --integration-test ERR20241020 2

# 6. 实施修复
/sdd.debug.implement --rollback --monitor ERR20241020 2

# 7. 经验学习和知识库更新
/sdd.learn --extract-patterns --update-guidelines ERR20241020
```

---

## 🎯 最佳实践

### 1. 渐进式采用
- **第一阶段**：先使用 `constitution`、`specify`、`plan`
- **第二阶段**：引入 `tasks`、`implement`
- **第三阶段**：完整的质量保证流程

### 2. 质量门禁
- 每个阶段完成后使用 `analyze` 检查质量
- 使用 `checklist` 生成详细检查清单
- 确保每个阶段的质量达标后再进入下一阶段

### 3. 持续改进
- 定期使用 `analyze` 识别问题
- 使用 `clarify` 解决模糊事项
- 根据反馈调整模板和流程

### 4. 团队协作
- **产品经理**：主导 `constitution`、`specify`
- **技术负责人**：主导 `plan`、`tasks`
- **开发团队**：执行 `implement`
- **质量保证**：使用 `analyze`、`checklist`

### 5. 🚨 错误处理最佳实践
- **立即建档**：发现错误立即使用 `/sdd.debug.init` 建立档案
- **深度分析**：使用 `/sdd.debug.analyze` 强制进行根因分析
- **历史检查**：使用 `/sdd.history.check` 避免重复失败思路
- **多重方案**：使用 `/sdd.debug.solutions` 确保多方案对比
- **严格验证**：使用 `/sdd.debug.validate` 确保方案有效性
- **持续学习**：使用 `/sdd.learn` 将经验纳入知识库

### 6. 🧠 智能防错机制
- **强制根因分析**：不允许跳过分析直接进入解决方案
- **多方案要求**：必须提供至少3个解决方案
- **历史提醒**：自动检测并提醒重复的失败思路
- **质量门禁**：不通过验证不允许实施修复
- **模拟数据禁用**：禁止使用模拟数据作为最终方案

---

## 📊 质量标准

### 通过标准
- **需求阶段**：所有检查项 100% 通过
- **设计阶段**：所有检查项 95% 以上通过
- **实现阶段**：所有检查项 90% 以上通过

### 质量等级
- **优秀**：95-100 分
- **良好**：85-94 分
- **一般**：70-84 分
- **需改进**：50-69 分
- **不合格**：<50 分

---

## 🔧 常见问题

### Q: 如何处理命令执行失败？
A: 检查错误信息，修复问题后使用 `--continue` 选项继续执行。

### Q: 可以跳过某些阶段吗？
A: 不建议跳过，但可以使用 `--from` 选项从特定任务开始。

### Q: 如何自定义模板？
A: 修改 `_sdd/templates/` 目录下的模板文件。

### Q: 如何处理多个功能开发？
A: 为每个功能创建独立的规范目录，使用功能编号区分。

---

## 📚 相关文档

- [SDD 完整指南](../SDD_GUIDE.md)
- [项目结构说明](../_sdd/README.md)
- [模板文档](../_sdd/templates/)

---

**注意**: SDD 范式命令系统旨在提高开发质量和效率，建议团队严格按照流程执行，确保每个阶段的输出质量。