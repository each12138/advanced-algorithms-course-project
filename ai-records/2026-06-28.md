# AI 交互记录

## 2026-06-28

### 背景

对 FLP 不可能性结果的 review（main.tex）进行审阅，与论文原文（1985-flp）逐项对比，检查正确性和完整性。

### 审阅发现的问题

#### 需要修正的错误

1. **Output register 取值精度不足**（L91）
   - 原文说 "所有未崩溃的 process 的 output register y_p ∈ {0, 1}"
   - 论文定义 y_p ∈ {b, 0, 1}，b 表示未决定
   - 修正为：在做出决策后取值为 {0, 1}（初始值为 b，表示未决定）

2. **Theorem 2 中 k 的计数表述不准确**（L206）
   - 原文说 "收齐 k = ⌈(n+1)/2⌉ 个其他进程的回复"
   - 论文原文 "including itself"，所以是包含自己在内共 k 个
   - 修正为：等待收到至少 k-1 个其他进程的回复（连同自己共计 k 个）

#### 不够精确需补充的部分

3. **Lemma 2 中 deciding run 的存在性前提未说明**（L130）
   - 原文仅说 "执行一个 admissible 且 deciding 的运行"
   - 缺少前提：该 deciding run 的存在依赖"协议 P 是单故障下完全正确的"（定理 1 的反证假设）
   - 修正：补充了反证假设说明

4. **缺乏 Event / Schedule / Run 的形式化定义**
   - 论文在 Section 2 中明确定义了 step (event)、schedule、run
   - 修正：在 Configuration 与 Admissible run 之间新增三项定义

5. **Lemma 3 中 valency 保序性未显式写出**（L157）
   - "0-valent 的后继也是 0-valent"缺少形式化依据
   - 修正：补充 "由 valency 的保序性（若配置 C 是 v-valent，则从 C 出发可到达的任何配置也是 v-valent）"

6. **Lemma 3 情况 2 中 deciding run 的构造缺少完全正确性前提**（L161）
   - 修正：补充 "由完全正确性（每个 admissible run 都是 deciding run）"

7. **模型节缺失 write-once 属性定义**
   - 论文显式说明 output register 是 write-once 的
   - 修正：在模型节（L97）补充 "进程的转移函数在进入决策状态后不能再改变输出寄存器中的值"

### 修改执行情况

| No. | 内容 | 状态 |
|-----|------|------|
| 1 | Output register 精度修正 | 已修改 |
| 2 | Theorem 2 k 值修正 | 已修改 |
| 3 | Lemma 2 deciding run 前提补充 | 已修改 |
| 4 | Event / Schedule / Run 定义新增 | 已修改 |
| 5 | Lemma 3 valency 保序性补充 | 已修改 |
| 6 | Lemma 3 完全正确性引用补充 | 已修改 |
| 7 | write-once 定义补充 | 已修改 |