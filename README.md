# PulseAI (墨诊) · 跨文化 AI 中医导诊工作台

> **AI Product Manager Portfolio Project**  
> 一款面向入境外国人士与在华外籍居民的 AI 中医导诊助手。通过 LLM 意图识别、中医病机映射与结构化 RAG 检索，解决外籍患者“病症表达难、科室匹配准度低、现场医患沟通瘫痪”的三大核心痛点。

---

## 📌 项目背景与痛点 (Problem Statement)

随着入境免签政策扩展与海外社交平台（TikTok/YouTube）上“东方神秘力量”（拔罐、针灸、中药调理）的爆火，越来越多的外国游客和在华外企员工产生看中医的需求。然而，跨文化中医就医面临极高壁垒：
1. **语言与概念鸿沟**：外国患者使用西医或口语化英文描述（如 "brain fog", "bloating", "cold feet"），难以转化为中医特有概念（如“脾虚湿阻”、“阳气不达”）。
2. **科室对不准**：国内中医医院科室细分（治未病科、针灸科、推拿科、脾胃病科），外籍患者无法准确挂号。
3. **现场沟通中断**：国内名老中医多不具备流利英文沟通能力，现场诊疗效率极低。

---

## 🚀 核心功能与五步就医闭环 (Core Capabilities)

`PulseAI` 采用 **Multi-Agent 协作架构** 与 **极轻量工具切入策略**，实现完整的导诊闭环：
---

## 🛠️ 架构设计与 Agent System Prompt

### 1. Multi-Agent 编排与 Guardrails (安全护栏)

* **Intent Intake Agent**：解析自然语言口语，提取关键病症字段。若主诉缺失关键要素，自动触发追问。
* **Domain Mapping Agent**：连接中医知识库，完成中西医概念转换与科室映射。
* **RAG Generator Agent**：检索预构建的机构数据库，并按 strict JSON Schema 强制输出《就诊沟通卡》。
* **Medical Guardrail**：全流程注入医疗免责声明（Medical Disclaimer），强行拦截违禁处方药开具请求。

### 2. Core System Prompt 概览

```text
# Role: PulseAI - Cross-Cultural TCM Guide Agent

## Profile
You are an expert AI Assistant specialized in Traditional Chinese Medicine (TCM) cross-cultural navigation. Your task is to bridge the language and conceptual gap for foreign patients seeking TCM treatment in China.

## Directives
1. Analyze user input (English/natural language) and extract chief complaints.
2. Map Western symptoms into TCM concepts (e.g., "brain fog & fatigue" -> "Spleen Qi Deficiency with Dampness / 脾虚湿阻").
3. Recommend corresponding TCM departments (e.g., Acupuncture Department, Preventive Medicine).
4. Output a structured bilingual Doctor Communication Card for local Chinese physicians.
5. Strict Guardrails: Always enforce medical disclaimers; NEVER prescribe specific herbal medication.
📂 项目结构 (Project Structure)
Plaintext
pulse-ai-portfolio/
├── index.html        # 包含 Executive Dark Minimalist UI、模拟 Agent 状态机与卡片生成器的单文件 MVP
├── README.md         # 项目产品设计与架构文档
└── LICENSE           # MIT 开源许可证
