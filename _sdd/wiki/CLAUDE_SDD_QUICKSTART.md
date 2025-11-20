# Claude SDD 快速上手指南

## 🚀 5分钟开始使用 SDD

### 步骤1：启动 SDD 系统
```bash
/sdd
```

### 步骤2：项目初始化（新项目或引入SDD）
```bash
# 转换为初始化架构师
*agent init-architect

# 执行项目初始化任务
*task project-initialization
```

### 步骤3：功能开发流程
```bash
# 需求分析阶段
*agent planner
*task specification-creation

# 技术设计阶段
*agent planner
*task technical-planning

# 开发实现阶段
*agent implementer
*task implementation-execution

# 质量保证阶段
*agent analyzer
*task quality-analysis
```

### 步骤4：遇到问题时
```bash
# 转换为调试专家
*agent debugger
*task problem-diagnosis
```

## 📋 常用指令速查

### 系统控制
```bash
/sdd                           # 启动 SDD 编排器
*help                          # 显示所有可用命令
*agent                         # 列出所有可用代理
*task                          # 列出所有可用任务
*checklist                     # 列出所有可用检查清单
```

### 代理转换
```bash
*agent init-architect          # 转换为初始化架构师
*agent planner                 # 转换为规划专家
*agent implementer             # 转换为实现专家
*agent analyzer                # 转换为分析专家
*agent debugger                # 转换为调试专家
*agent learner                 # 转换为学习专家
```

### 任务执行
```bash
*task project-initialization    # 项目初始化
*task specification-creation    # 创建功能规范
*task technical-planning        # 技术方案规划
*task implementation-execution  # 代码实现执行
*task quality-analysis          # 质量分析
*task problem-diagnosis         # 问题诊断
*task lessons-capture           # 经验捕获
```

### 质量检查
```bash
*checklist requirements         # 需求检查清单
*checklist code-quality         # 代码质量检查清单
*checklist architecture         # 架构检查清单
*checklist security             # 安全检查清单
*checklist performance          # 性能检查清单
```

### 扩展功能
```bash
# 创建新的专业代理（参考CLAUDE_SDD_GUIDE.md中的扩展指南）
# 创建新的可执行任务
# 创建新的检查清单
```

## 🎯 SDD 解决的核心问题

### 1. 规范驱动开发
- **问题**: 开发缺乏统一规范，质量参差不齐
- **SDD方案**: 通过项目宪法和标准化流程确保一致性
- **使用**: `*agent init-architect` → `*task project-initialization`

### 2. 质量内建
- **问题**: 质量检查滞后，修复成本高
- **SDD方案**: 在每个阶段内建质量检查点
- **使用**: `*checklist [类型]` 进行阶段性质量验证

### 3. 经验积累
- **问题**: 错误重复出现，经验无法传承
- **SDD方案**: 系统化的错误处理和知识管理
- **使用**: `*agent learner` → `*task lessons-capture`

## 🔧 系统扩展指南

### 添加新代理
1. 在 `.claude/commands/SDD/agents/` 创建新的代理文件
2. 遵循标准的代理结构（角色定义、核心能力、命令集）
3. 参考现有代理的格式和风格

### 添加新任务
1. 在 `.claude/commands/SDD/tasks/` 创建任务文件
2. 定义任务目标、前置条件、执行步骤
3. 指定输出要求和验收标准

### 添加新检查清单
1. 在 `.claude/commands/SDD/checklists/` 创建检查清单
2. 定义检查目标和检查项目
3. 设置评估标准和改进建议

## 📁 文档资源

- **[CLAUDE_SDD_GUIDE.md](./CLAUDE_SDD_GUIDE.md)** - 完整的扩展指南
- **[SDD_GUIDE.md](./SDD_GUIDE.md)** - SDD方法论详解
- **[SDD_MCP_INTEGRATION_GUIDE.md](./SDD_MCP_INTEGRATION_GUIDE.md)** - MCP集成指南
- **[.claude/commands/SDD/README.md](../../.claude/commands/SDD/README.md)** - 系统架构说明

## 💡 最佳实践

### 1. 渐进式采���
- 从单个功能开始试用SDD
- 逐步扩展到整个项目
- 团队培训和经验分享

### 2. 质量优先
- 严格遵循SDD流程
- 不跳过质量检查环节
- 持续改进和优化

### 3. 工具配合
- 结合版本控制系统
- 使用自动化测试工具
- 建立持续集成流程

## ⚠️ 重要提醒

- **完整性**: 确保每个阶段都有完整的输出文档
- **一致性**: 保持团队对SDD流程的理解一致
- **持续性**: 建立持续改进机制
- **协作性**: 促进跨职能团队的有效协作

**通过SDD系统，让AI辅助开发更加规范、高效、可控！**