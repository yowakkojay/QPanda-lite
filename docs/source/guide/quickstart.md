# 快速上手

本指南帮助你在完成安装后立即运行第一个量子线路示例，体验构建线路 → 本地模拟 → 查看结果的全流程。若尚未安装，请先参考 [安装指南](installation.md) 完成环境配置。

## 构建量子线路

第一个示例将让你看到如何创建量子线路并添加量子门。建议重点关注：
- 如何使用 `Circuit` 创建空线路
- 如何添加量子门（如 `h`、`cnot`）
- 如何添加测量指令 `measure`

```python
from qpandalite.circuit_builder import Circuit

# 创建线路
circuit = Circuit()

# 添加量子门
circuit.h(0)          # Hadamard 门
circuit.cnot(0, 1)    # CNOT 门
circuit.measure(0, 1) # 测量

# 查看 OriginIR 格式
print(circuit.originir)
```

运行上述代码后，你将看到线路的 OriginIR 文本表示，这是 QPanda-lite 用于描述量子线路的标准格式。

## 本地模拟

接下来使用本地模拟器运行线路并观察结果。建议重点关注：
- 如何使用 `OriginIR_Simulator` 创建模拟器
- 如何调用 `simulate_pmeasure` 获取测量概率分布
- 输出结果的含义（概率分布）

```python
from qpandalite.simulator import OriginIR_Simulator

sim = OriginIR_Simulator()

# 概率测量
prob = sim.simulate_pmeasure(circuit.originir)
print("测量概率分布:", prob)
```

输出将显示各测量结果的概率值，例如 `{'00': 0.5, '11': 0.5}` 表示两种结果各占一半概率。

## 下一步

完成本示例后，建议按以下顺序继续阅读：
- [构建量子线路](circuit.md) —— 详细了解线路构建 API 与更多量子门
- [本地模拟](simulation.md) —— 模拟器功能详解与不同后端选项
- [提交任务](submit_task.md) —— 将线路提交到真机运行
