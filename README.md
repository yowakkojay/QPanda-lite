# QPanda-lite

[![GitHub version](https://badge.fury.io/gh/Agony5757%2FQPanda-lite.svg?icon=si%3Agithub)](https://badge.fury.io/gh/Agony5757%2FQPanda-lite)
[![Documentation Status](https://readthedocs.org/projects/qpanda-lite/badge/?version=latest)](https://qpanda-lite.readthedocs.io/en/latest/?badge=latest)
[![PyPI version](https://badge.fury.io/py/qpandalite.svg?icon=si%3Apython)](https://badge.fury.io/py/qpandalite)
[![codecov](https://codecov.io/github/Agony5757/QPanda-lite/graph/badge.svg?token=PFQ6F7HQY7)](https://codecov.io/github/Agony5757/QPanda-lite)
[![Build and Test](https://github.com/Agony5757/QPanda-lite/actions/workflows/build_and_test.yml/badge.svg?branch=main)](https://github.com/Agony5757/QPanda-lite/actions/workflows/build_and_test.yml)

**QPanda**: **Q**uantum **P**rogramming **A**rchitecture for **N**ISQ **D**evice **A**pplication

QPanda-lite is a simple, easy-to-use, and transparent Python-native version of QPanda.

## Quick Example

```python
from qpandalite.circuit_builder import Circuit
from qpandalite.simulator import OriginIR_Simulator

circuit = Circuit()
circuit.h(0)
circuit.cnot(0, 1)
circuit.measure(0, 1)

sim = OriginIR_Simulator()
print(sim.simulate_shots(circuit.originir, shots=1000))
```

第一次使用？建议先阅读 [快速上手](https://qpanda-lite.readthedocs.io/en/latest/source/guide/quickstart.html) 指南。

## Status

🚧 Actively developing. API may change.

### Known Issues

- **`crx`/`crz`/`cy` bug**：Density matrix 后端的受控旋转门在多门组合时计算结果错误。单门测试正常。如需带噪声模拟，请规避这三个门。
- `controlled_by` simulation for density matrix is incorrect, including `backend='density_operator'` and `backend='density_operator_qutip'`.

---

## Design Principles

- **Transparent** — a clear way to assemble and execute quantum programs
- **Sync & Async** — support both modes for execution on quantum hardware
- **Clear errors** — helpful error messages when things go wrong
- **Well documented** — full, high-quality documentation
- **Visualizable** — visualization of quantum programs
- **Portable** — migrate to different quantum backends
- **Extensible** — support more quantum operations and simulation backends

### Core Concepts

| Concept | Type | Description |
|---------|------|-------------|
| **Opcode** | `Tuple` | A tuple representing a quantum operation: name, qubits, parameters, etc. [📖 Docs](https://qpanda-lite.readthedocs.io/en/latest/source/advanced/opcode.html) |
| **Circuit** | `Circuit` | A collection of opcodes representing a quantum program. Can be converted to OriginIR/QASM. [📖 Docs](https://qpanda-lite.readthedocs.io/en/latest/source/guide/circuit.html) |
| **Circuit String** | `str` | A string in [OriginIR](https://qpanda-lite.readthedocs.io/en/latest/source/guide/originir.html) or [QASM](https://qpanda-lite.readthedocs.io/en/latest/source/guide/qasm.html) format, ready for backend execution. |
| **Backend** | `Backend` | A [quantum simulator](https://qpanda-lite.readthedocs.io/en/latest/source/guide/simulation.html) or hardware that executes a circuit. |
| **Result** | `dict` / `list` / `ndarray` | Execution results (measurements, states) in native Python data structures. |

---

## Installation

### pip (Recommended)

```bash
pip install qpandalite
```

Python 3.9 – 3.12 supported.

详细安装方式与可选依赖见 [安装指南](https://qpanda-lite.readthedocs.io/en/latest/source/guide/installation.html)。

### Build from Source

**Minimum (pure Python):**

```bash
git clone https://github.com/Agony5757/QPanda-lite.git
cd QPanda-lite
pip install . --no-cpp
```

**Development mode:**

```bash
git clone https://github.com/Agony5757/QPanda-lite.git
cd QPanda-lite
pip install -e .
```

**With C++ simulator (requires CMake in PATH):**

```bash
git clone --recurse-submodules https://github.com/Agony5757/QPanda-lite.git
cd QPanda-lite
pip install .
```

---

### 项目结构

完整项目结构与各模块说明请参见 [在线文档](https://qpanda-lite.readthedocs.io/)。

---

## 任务提交与结果处理概览

以下是最常见的任务提交用法概览，更多进阶内容请参见 [快速上手](https://qpanda-lite.readthedocs.io/en/latest/source/guide/quickstart.html)。

### Run on Quantum Devices / Simulators

| Function | Code | Note |
|----------|------|------|
| Import platform | `import qpandalite.task.originq as originq` | Platforms are under `qpandalite.task` |
| Submit task | `taskid = originq.submit_task(circuits)` | `circuits`: `str` or `List[str]` |
| Query (sync) | `results = originq.query_by_taskid_sync(taskid)` | Blocks until done; returns `list` |
| Query (async) | `res = originq.query_by_taskid(taskid)` | Returns immediately; check `res['status']` |
| Convert result | `originq.convert_originq_result(results, style='keyvalue', prob_or_shots='prob', key_style='bin')` | Styles: `keyvalue` / `list` |
| Expectation | `calculate_expectation(result, ['ZII', 'IZI', 'IIZ'])` | Diagonal Hamiltonians only |

各平台（OriginQ / Quafu / IBM）的详细配置与提交方式请参见 [提交任务指南](https://qpanda-lite.readthedocs.io/en/latest/source/guide/submit_task.html)。

更多模拟器选项与噪声模型请参见 [本地模拟指南](https://qpanda-lite.readthedocs.io/en/latest/source/guide/simulation.html)。

---

## Documentation

📖 **[Read the Docs](https://qpanda-lite.readthedocs.io/)**

### OpenQASM 2.0 Support

[OpenQASM 2.0 Guide](https://qpanda-lite.readthedocs.io/en/latest/source/guide/qasm.html)

### Build Docs Locally

```bash
cd docs
pip install -r requirements.txt
sphinx-apidoc -o docs/source qpandalite
make html
```
