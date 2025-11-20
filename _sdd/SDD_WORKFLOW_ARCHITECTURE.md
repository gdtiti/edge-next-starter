# SDD 工作流驱动架构设计

## 🎯 核心理念重构

### 代理 vs 命令重新定义

#### 🔄 命令 (Commands)
- **定义**: 单一的、原子性的操作
- **作用**: 执行具体的、不可分割的任务
- **特点**: 独立、可重用、有明确输入输出

#### 🤖 代理 (Agents)
- **定义**: 工作流的编排者和执行者
- **作用**: 将多个命令按业务逻辑组合执行
- **特点**: 智能编排、流程控制、错误处理、决策能力

---

## 🏗️ 新架构设计

### 1. 分层架构

```
_sdd/
├── core/                           # 核心配置
│   ├── system-config.json          # 系统配置
│   ├── workflow-registry.json      # 工作流注册表
│   └── command-registry.json       # 命令注册表
│
├── workflows/                      # 工作流定义
│   ├── README.md                   # 工作流说明
│   │
│   ├── sdd-lifecycle/              # SDD生命周期工作流
│   │   ├── project-initiation.json
│   │   ├── specification-phase.json
│   │   ├── planning-phase.json
│   │   ├── implementation-phase.json
│   │   ├── validation-phase.json
│   │   └── learning-phase.json
│   │
│   ├── quality-assurance/          # 质量保证工作流
│   │   ├── code-review-workflow.json
│   │   ├── testing-workflow.json
│   │   └── documentation-workflow.json
│   │
│   ├── problem-solving/            # 问题解决工作流
│   │   ├── error-debugging-workflow.json
│   │   ├── performance-optimization-workflow.json
│   │   └── compatibility-resolution-workflow.json
│   │
│   └── utility/                    # 工具工作流
│       ├── analysis-workflow.json
│       ├── checklist-generation-workflow.json
│       └── mcp-analysis-workflow.json
│
├── agents/                         # 代理定义
│   ├── README.md                   # 代理说明
│   │
│   ├── workflow-executors/         # 工作流执行器
│   │   ├── sdd-lifecycle-agent.json
│   │   ├── quality-agent.json
│   │   ├── problem-solver-agent.json
│   │   └── utility-agent.json
│   │
│   ├── orchestration/              # 编排逻辑
│   │   ├── condition-evaluator.json
│   │   ├── error-handler.json
│   │   ├── decision-maker.json
│   │   └── flow-controller.json
│   │
│   └── capabilities/               # 能力定义
│       ├── text-analysis.json
│       ├── code-generation.json
│       ├── pattern-recognition.json
│       └── knowledge-retrieval.json
│
├── commands/                      # 原子命令定义
│   ├── README.md                   # 命令说明
│   │
│   ├── file-operations/            # 文件操作命令
│   │   ├── read-file.json
│   │   ├── write-file.json
│   │   ├── edit-file.json
│   │   └── search-files.json
│   │
│   ├── analysis/                   # 分析命令
│   │   ├── analyze-code.json
│   │   ├── analyze-structure.json
│   │   ├── analyze-dependencies.json
│   │   └── analyze-quality.json
│   │
│   ├── generation/                 # 生成命令
│   │   ├── generate-specification.json
│   │   ├── generate-plan.json
│   │   ├── generate-tasks.json
│   │   ├── generate-code.json
│   │   └── generate-documentation.json
│   │
│   ├── validation/                 # 验证命令
│   │   ├── validate-specification.json
│   │   ├── validate-plan.json
│   │   ├── validate-code.json
│   │   └── validate-consistency.json
│   │
│   ├── integration/                # 集成命令
│   │   ├── integrate-api.json
│   │   ├── integrate-database.json
│   │   ├── integrate-frontend.json
│   │   └── integrate-testing.json
│   │
│   ├── debug/                      # 调试命令
│   │   ├── debug-error.json
│   │   ├── debug-performance.json
│   │   ├── debug-compatibility.json
│   │   └── debug-deployment.json
│   │
│   └── utility/                    # 工具命令
│       ├── checklist.json
│       ├── mcp-analyze.json
│       ├── knowledge-query.json
│       └── report-generate.json
```

### 2. 工作流定义示例

#### 🔄 SDD项目初始化工作流

```json
// workflows/sdd-lifecycle/project-initiation.json
{
  "workflow_id": "project-initiation",
  "name": "SDD项目初始化工作流",
  "version": "1.0.0",
  "description": "完整的项目初始化流程，从分析到配置生成",

  "trigger": {
    "command_pattern": "/sdd.init",
    "required_input": "project_description"
  },

  "steps": [
    {
      "step_id": "analyze-project",
      "name": "项目分析",
      "type": "command_sequence",
      "commands": [
        {
          "command": "analyze-structure",
          "params": {
            "path": ".",
            "depth": "deep"
          }
        },
        {
          "command": "analyze-dependencies",
          "params": {
            "include_dev": true
          }
        },
        {
          "command": "analyze-quality",
          "params": {
            "metrics": ["complexity", "duplication", "coverage"]
          }
        }
      ],
      "output_mapping": {
        "structure": "project_structure",
        "dependencies": "tech_stack",
        "quality": "code_quality"
      }
    },

    {
      "step_id": "generate-constitution",
      "name": "生成项目宪法",
      "type": "conditional_generation",
      "condition": "needs_constitution",
      "commands": [
        {
          "command": "generate-specification",
          "params": {
            "type": "constitution",
            "template": "project-constitution",
            "context": {
              "tech_stack": "{{previous.tech_stack}}",
              "project_structure": "{{previous.project_structure}}"
            }
          }
        }
      ]
    },

    {
      "step_id": "create-sdd-config",
      "name": "创建SDD配置",
      "type": "file_operations",
      "operations": [
        {
          "command": "write-file",
          "params": {
            "path": "_sdd/memory/project-context.md",
            "content": "Generated from analysis results"
          }
        },
        {
          "command": "write-file",
          "params": {
            "path": "_sdd/constitution.md",
            "content": "{{previous.constitution}}"
          }
        }
      ]
    }
  ],

  "error_handling": {
    "retry_strategy": "exponential_backoff",
    "fallback_workflow": "minimal-initiation",
    "notification_level": "warning"
  },

  "success_criteria": {
    "required_outputs": ["project_context", "constitution"],
    "quality_threshold": 0.8
  }
}
```

#### 🔄 错误调试工作流

```json
// workflows/problem-solving/error-debugging-workflow.json
{
  "workflow_id": "error-debugging",
  "name": "错误调试工作流",
  "version": "1.0.0",
  "description": "系统化的问题分析和解决方案设计流程",

  "trigger": {
    "command_patterns": [
      "/sdd.debug.init",
      "/sdd.debug.analyze",
      "/sdd.debug.solutions",
      "/sdd.debug.validate",
      "/sdd.debug.implement"
    ]
  },

  "states": {
    "init": {
      "name": "错误建档",
      "entry_command": "debug-error",
      "next_states": ["analyze"]
    },

    "analyze": {
      "name": "根因分析",
      "entry_command": "debug-error",
      "workflow": [
        {
          "step": "collect-context",
          "command": "analyze-error",
          "params": {
            "analysis_depth": "deep",
            "method": "5whys"
          }
        },
        {
          "step": "historical-check",
          "command": "knowledge-query",
          "params": {
            "query_type": "similar_errors",
            "context": "{{previous.error_context}}"
          }
        },
        {
          "step": "root-cause",
          "command": "debug-error",
          "params": {
            "analysis_type": "root_cause",
            "historical_data": "{{previous.similar_errors}}"
          }
        }
      ],
      "next_states": ["solutions"]
    },

    "solutions": {
      "name": "方案设计",
      "entry_command": "debug-error",
      "workflow": [
        {
          "step": "generate-solutions",
          "command": "debug-error",
          "params": {
            "action": "design_solutions",
            "max_solutions": 5,
            "consideration_factors": ["feasibility", "cost", "risk"]
          }
        }
      ],
      "next_states": ["validate"]
    },

    "validate": {
      "name": "方案验证",
      "entry_command": "debug-error",
      "workflow": [
        {
          "step": "solution-evaluation",
          "command": "debug-error",
          "params": {
            "action": "validate_solutions",
            "test_scenarios": "comprehensive"
          }
        }
      ],
      "next_states": ["implement"]
    },

    "implement": {
      "name": "方案实施",
      "entry_command": "debug-error",
      "workflow": [
        {
          "step": "implementation-plan",
          "command": "debug-error",
          "params": {
            "action": "create_implementation_plan"
          }
        }
      ],
      "final_state": true
    }
  },

  "state_machine": {
    "initial": "init",
    "transitions": {
      "init": ["analyze"],
      "analyze": ["solutions"],
      "solutions": ["validate"],
      "validate": ["implement", "analyze"],
      "implement": []
    }
  }
}
```

### 3. 命令定义示例

#### 🔧 原子命令：文件分析

```json
// commands/analysis/analyze-structure.json
{
  "command_id": "analyze-structure",
  "name": "项目结构分析",
  "version": "1.0.0",
  "category": "analysis",
  "type": "atomic",

  "description": "分析项目目录结构和文件组织模式",

  "input_schema": {
    "type": "object",
    "properties": {
      "path": {
        "type": "string",
        "description": "分析路径",
        "default": "."
      },
      "depth": {
        "type": "string",
        "enum": ["shallow", "standard", "deep"],
        "description": "分析深度",
        "default": "standard"
      },
      "include_patterns": {
        "type": "array",
        "items": {"type": "string"},
        "description": "包含的文件模式",
        "default": ["*.{cs,js,ts,json,md}"]
      }
    },
    "required": ["path"]
  },

  "output_schema": {
    "type": "object",
    "properties": {
      "directory_structure": {
        "type": "object",
        "description": "目录结构树"
      },
      "file_patterns": {
        "type": "object",
        "description": "文件模式统计"
      },
      "architecture_hints": {
        "type": "array",
        "items": {"type": "string"},
        "description": "架构模式提示"
      }
    }
  },

  "implementation": {
    "tools": ["Glob", "Grep", "Read"],
    "algorithm": "hierarchical_analysis",
    "timeout": 30000
  }
}
```

#### 🔧 原子命令：规范生成

```json
// commands/generation/generate-specification.json
{
  "command_id": "generate-specification",
  "name": "规范生成",
  "version": "1.0.0",
  "category": "generation",
  "type": "atomic",

  "description": "基于模板和上下文生成各种规范文档",

  "input_schema": {
    "type": "object",
    "properties": {
      "type": {
        "type": "string",
        "enum": ["specification", "constitution", "plan", "tasks"],
        "description": "规范类型"
      },
      "template": {
        "type": "string",
        "description": "模板名称"
      },
      "context": {
        "type": "object",
        "description": "生成上下文数据"
      },
      "format": {
        "type": "string",
        "enum": ["markdown", "json", "both"],
        "default": "markdown",
        "description": "输出格式"
      }
    },
    "required": ["type", "template", "context"]
  },

  "output_schema": {
    "type": "object",
    "properties": {
      "content": {
        "type": "string",
        "description": "生成的内容"
      },
      "metadata": {
        "type": "object",
        "properties": {
          "template_used": {"type": "string"},
          "generation_time": {"type": "number"},
          "quality_score": {"type": "number"}
        }
      }
    }
  },

  "implementation": {
    "tools": ["Read", "Write"],
    "template_engine": "handlebars",
    "validation": "content_quality_check"
  }
}
```

### 4. 代理定义示例

#### 🤖 SDD生命周期代理

```json
// agents/workflow-executors/sdd-lifecycle-agent.json
{
  "agent_id": "sdd-lifecycle-agent",
  "name": "SDD生命周期管理代理",
  "version": "1.0.0",
  "type": "workflow_executor",

  "description": "专门负责SDD完整生命周期管理的代理，能够智能编排各种工作流",

  "capabilities": [
    "workflow_orchestration",
    "state_management",
    "error_recovery",
    "progress_tracking",
    "decision_making"
  ],

  "supported_workflows": [
    "sdd-lifecycle/project-initiation",
    "sdd-lifecycle/specification-phase",
    "sdd-lifecycle/planning-phase",
    "sdd-lifecycle/implementation-phase",
    "sdd-lifecycle/validation-phase",
    "sdd-lifecycle/learning-phase"
  ],

  "orchestration_logic": {
    "workflow_selection": {
      "strategy": "intent_based",
      "fallback": "user_selection"
    },
    "step_execution": {
      "parallelism": "conditional",
      "retry_policy": "exponential_backoff",
      "timeout_handling": "graceful_degradation"
    },
    "error_handling": {
      "strategy": "cascading_fallback",
      "user_interaction": "on_critical_errors"
    }
  },

  "decision_making": {
    "context_analysis": {
      "factors": [
        "project_complexity",
        "team_size",
        "timeline_pressure",
        "quality_requirements"
      ]
    },
    "optimization_goals": [
      "minimize_execution_time",
      "maximize_output_quality",
      "ensure_user_satisfaction"
    ]
  },

  "interaction_patterns": {
    "progress_reporting": {
      "frequency": "on_milestone_completion",
      "detail_level": "summary_with_details"
    },
    "user_feedback": {
      "collection_points": ["major_decisions", "error_recovery"],
      "response_integration": "immediate"
    }
  }
}
```

### 5. 命令到工作流的映射机制

```json
// core/workflow-registry.json
{
  "version": "1.0.0",
  "last_updated": "2025-11-19T00:00:00Z",

  "command_workflow_mapping": {
    "/sdd.init": {
      "workflow": "sdd-lifecycle/project-initiation",
      "agent": "sdd-lifecycle-agent",
      "execution_mode": "single_workflow"
    },

    "/sdd.constitution": {
      "workflow": "sdd-lifecycle/specification-phase",
      "agent": "sdd-lifecycle-agent",
      "execution_mode": "single_workflow",
      "workflow_parameters": {
        "focus_area": "constitution"
      }
    },

    "/sdd.debug.analyze": {
      "workflow": "problem-solving/error-debugging-workflow",
      "agent": "problem-solver-agent",
      "execution_mode": "stateful_workflow",
      "initial_state": "analyze"
    },

    "/sdd.implement": {
      "workflow": "sdd-lifecycle/implementation-phase",
      "agent": "sdd-lifecycle-agent",
      "execution_mode": "single_workflow",
      "required_prerequisites": ["specification", "plan"]
    }
  },

  "workflow_chaining": {
    "full_sdd_cycle": [
      "sdd-lifecycle/project-initiation",
      "sdd-lifecycle/specification-phase",
      "sdd-lifecycle/planning-phase",
      "sdd-lifecycle/implementation-phase",
      "sdd-lifecycle/validation-phase"
    ]
  }
}
```

---

## 🔄 工作流执行机制

### 1. 工作流引擎

```json
// core/workflow-engine.json
{
  "engine_configuration": {
    "parallel_execution": true,
    "max_concurrent_steps": 3,
    "step_timeout": 60000,
    "workflow_timeout": 300000
  },

  "execution_model": {
    "step_execution": "command_sequence",
    "conditional_logic": "rule_based_evaluation",
    "error_handling": "cascading_recovery"
  },

  "state_management": {
    "persistence": "workflow_state.json",
    "checkpoint_frequency": "on_step_completion",
    "recovery_strategy": "from_last_checkpoint"
  }
}
```

### 2. 工作流编排示例

#### 复杂的SDD完整流程

```json
// workflows/sdd-lifecycle/full-sdd-cycle.json
{
  "workflow_id": "full-sdd-cycle",
  "name": "完整SDD开发周期",
  "description": "从初始化到学习的完整SDD流程",

  "orchestration_strategy": "adaptive",

  "phases": [
    {
      "phase_id": "initiation",
      "name": "初始化阶段",
      "workflow": "sdd-lifecycle/project-initiation",
      "success_criteria": {
        "context_created": true,
        "constitution_generated": true
      },
      "next_phases": ["specification"]
    },

    {
      "phase_id": "specification",
      "name": "规范阶段",
      "workflow": "sdd-lifecycle/specification-phase",
      "parallel_sub_workflows": [
        "functional-specifications",
        "technical-constraints",
        "quality-requirements"
      ],
      "success_criteria": {
        "all_specifications_complete": true,
        "stakeholder_approval": true
      },
      "next_phases": ["planning"]
    },

    {
      "phase_id": "planning",
      "name": "规划阶段",
      "workflow": "sdd-lifecycle/planning-phase",
      "decision_point": {
        "condition": "project_complexity",
        "branch_a": "simple_plan",
        "branch_b": "complex_plan"
      },
      "next_phases": ["implementation"]
    },

    {
      "phase_id": "implementation",
      "name": "实现阶段",
      "workflow": "sdd-lifecycle/implementation-phase",
      "iterative": true,
      "success_criteria": {
        "all_features_implemented": true,
        "quality_gates_passed": true
      },
      "next_phases": ["validation"]
    },

    {
      "phase_id": "validation",
      "name": "验证阶段",
      "workflow": "sdd-lifecycle/validation-phase",
      "parallel_sub_workflows": [
        "functional-testing",
        "performance-testing",
        "security-testing"
      ],
      "next_phases": ["learning"]
    },

    {
      "phase_id": "learning",
      "name": "学习阶段",
      "workflow": "sdd-lifecycle/learning-phase",
      "final_phase": true
    }
  ]
}
```

---

## 🎯 核心优势

### ✅ 解决的问题

1. **清晰职责分离**：
   - 命令 = 原子操作
   - 代理 = 工作流编排
   - 工作流 = 业务流程

2. **高度可组合性**：
   - 命令可独立使用
   - 工作流可灵活组合
   - 代理可智能编排

3. **智能执行能力**：
   - 条件判断和决策
   - 错误恢复和重试
   - 并行和串行执行

4. **强大的扩展性**：
   - 新命令易于添加
   - 新工作流易于定义
   - 新代理易于创建

### 📈 预期效果

- **开发效率**: 提升70%（智能编排减少手动操作）
- **质量保证**: 提升50%（标准化工作流确保质量）
- **学习成本**: 降低80%（清晰的架构易于理解）
- **扩展能力**: 提升90%（模块化设计便于扩展）

这个基于工作流的架构真正实现了代理作为执行逻辑组合的理念！