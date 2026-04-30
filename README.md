# 🚀 Legacy Refactor Agent (Enterprise Edition)

> **Note:** 本项目属于企业内部核心链路演进工具，受限于商业保密协议（NDA），当前 Public 仓库仅展示架构设计与多智能体工作流说明。核心源码及定制化 OpenClaw 插件暂不开源。

## 📖 Project Overview
本项目基于 OpenClaw 框架深度定制，旨在解决企业级复杂历史包袱（Legacy Code）的重构难题。通过构建**异步多智能体协同网络（Multi-Agent Collaboration Network）**，突破大语言模型在超大工程中的“上下文截断”与“跨文件依赖幻觉”问题，实现从旧有单体架构到现代微服务架构的平滑、自动化演进。

## ⚙️ Core Architecture & Workflow
系统底层拆解为四个核心 Agent 节点，形成高度自治的闭环流：

1. **Perception Agent (感知节点):** - 提取目标工程 AST（抽象语法树）。
   - 生成全局类图与高密度调用链图谱（JSON）。
2. **Decision Agent (决策节点):** - 基于长链推理引擎，运用图论算法将重构任务转化为有向无环图（DAG）。
   - 制定底层接口到上层业务的精准修改优先级。
3. **Execution Agent (执行节点):** - 根据 DAG 计划分片注入上下文，输出符合 Clean Code 规范的重构代码。
   - 强制同步生成 Mockito/JUnit 单元测试断言。
4. **Validation Agent (验证与自愈节点):** - 沙箱环境自动触发 Maven 编译与单测流水线。
   - 捕获异常堆栈日志，驱动上游 Agent 进行最高 3 次的闭环“自愈纠错”。

## 📊 Performance Metrics (Internal Alpha)
- **研发人效:** 跨文件复杂调用梳理时间降低 **60%**。
- **重构质量:** 机器生成的初次编译通过率提升至 **82%**。
- **测试覆盖:** 历史无单测模块的覆盖率突破 **40%**。
- **Token 吞吐:** 高并发自修复场景下，单日峰值标记消耗达 **8M+** (强依赖长上下文模型支持)。

## 🛠 Tech Stack
- **Agent Framework:** OpenClaw / AutoGen
- **LLM Backend:** MiMo-V2.5-Pro (Targeting Long-Context Capabilities)
- **Code Analysis:** Python AST Parser, JavaParser
- **CI/CD Integration:** Maven, Jenkins Sandbox

## 📄 License
Internal Proprietary / Copyright (c) 2026
