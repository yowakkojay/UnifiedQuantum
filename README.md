<p align="center">
  <img src="banner_uniq.png" alt="UnifiedQuantum Banner" width="100%">
</p>

# UnifiedQuantum

[![PyPI version](https://badge.fury.io/py/unified-quantum.svg?icon=si%3Apython)](https://badge.fury.io/py/unified-quantum)
[![codecov](https://codecov.io/github/IAI-USTC-Quantum/UnifiedQuantum/graph/badge.svg?token=PFQ6F7HQY7)](https://codecov.io/github/IAI-USTC-Quantum/UnifiedQuantum)
[![Build and Test](https://github.com/IAI-USTC-Quantum/UnifiedQuantum/actions/workflows/build_and_test.yml/badge.svg?branch=main)](https://github.com/IAI-USTC-Quantum/UnifiedQuantum/actions/workflows/build_and_test.yml)

**UnifiedQuantum** — A unified, non-commercial quantum computing aggregation framework.

UnifiedQuantum is a lightweight Python framework that provides a **unified interface** for quantum circuit construction, simulation, and cloud execution across multiple quantum computing platforms. It aggregates backends including OriginQ, Quafu, and IBM Quantum under one consistent API.

---

## 核心工作流

UnifiedQuantum 围绕一个简洁的工作流设计：**任意方式构建线路 → CLI 统一执行**。

### 1. 安装

```bash
pip install unified-quantum
```

### 2. 构建线路（支持原生 API 或任意第三方工具）

```python
from uniq.circuit_builder import Circuit

c = Circuit()
c.h(0)
c.cnot(0, 1)
c.measure(0, 1)

# 输出 OriginIR 格式，可供 CLI 使用
open('circuit.ir', 'w').write(c.originir)
```

> 你也可以使用 Qiskit、Cirq 等工具构建线路，只需最终输出 OriginIR 或 OpenQASM 2.0 格式。

### 3. CLI 统一执行

```bash
# 本地模拟
uniq simulate circuit.ir --shots 1000

# 提交到云端
uniq submit circuit.ir --platform originq --shots 1000

# 查询任务结果
uniq result <task_id>
```

---

## 设计理念

UnifiedQuantum 是一个**非商业性**的开源项目，致力于：

- **聚合**：整合多种量子云平台（OriginQ、Quafu、IBM Quantum），提供统一接口
- **统一**：一致的 API 设计，屏蔽各平台差异
- **透明**：清晰的量子程序组装与执行方式，无隐藏行为
- **轻量**：纯 Python 实现，安装简单，集成方便

| 线路构建 | 原生 API 或任意工具，输出 OriginIR / QASM2 |
| CLI 执行 | 统一接口：模拟、云端、任务管理 |
| 结果分析 | 原生 Python 结构，易于集成 |

---

## Features

| 特性 | 说明 |
|------|------|
| **多后端聚合** | 统一接口支持 OriginQ、Quafu、IBM Quantum 等多种量子云平台 |
| **本地模拟** | 内置 OriginIR Simulator、QASM Simulator |
| **透明** | 清晰的量子程序组装与执行方式 |
| **Python 原生** | 纯 Python 实现，安装简单，集成方便 |
| **同步/异步** | 支持同步和异步两种任务提交模式 |
| **可扩展** | 易于添加新的量子门、操作符和模拟后端 |

**核心概念：**

- **Circuit** — 量子线路构建器，支持 OriginIR / OpenQASM 格式输出
- **Backend** — 量子模拟器或真实量子计算机
- **Result** — 测量结果以原生 Python 数据结构返回（dict / list / ndarray）

---

## Installation

### Supported Platforms

- Windows / Linux / macOS

### Requirements

- Python 3.10 – 3.13

### pip（推荐）

```bash
pip install unified-quantum
```

### Build from Source

**纯 Python（无 C++ 依赖）：**

```bash
git clone https://github.com/IAI-USTC-Quantum/UnifiedQuantum.git
cd UnifiedQuantum
pip install . --no-cpp
```

**开发模式：**

```bash
pip install -e .
```

**含 C++ 模拟器（需 CMake）：**

```bash
git clone --recurse-submodules https://github.com/IAI-USTC-Quantum/UnifiedQuantum.git
cd UnifiedQuantum
pip install .
```

### Optional Dependencies

核心依赖（包括 `scipy`）在默认安装中已包含。以下为可选功能依赖：

| 功能 | 安装命令 |
|------|---------|
| OriginQ 云平台 | `pip install unified-quantum[originq]` |
| Quafu 执行后端 | `pip install unified-quantum[quafu]` |
| Qiskit 执行后端 | `pip install unified-quantum[qiskit]` |
| 高级模拟 (QuTiP) | `pip install unified-quantum[simulation]` |
| 可视化 | `pip install unified-quantum[visualization]` |
| PyTorch 集成 | `pip install unified-quantum[pytorch]` |
| 安装所有可选依赖 | `pip install unified-quantum[all]` |

---

## CLI Quick Reference

```bash
# 查看帮助
uniq --help

# 本地模拟
uniq simulate circuit.ir --shots 1000

# 提交到云端（支持 originq / quafu / ibm / dummy）
uniq submit circuit.ir --platform originq --shots 1000

# 查询任务结果
uniq result <task_id>

# 配置云平台 Token
uniq config init
uniq config set originq.token YOUR_TOKEN

# 也可以用 python -m 调用
python -m uniq simulate circuit.ir
```

---

## Examples

📁 [examples/](examples/README.md) — Runnable demonstrations

### Getting Started

| Example | Description |
|---------|-------------|
| [Circuit Remapping](examples/getting-started/1_circuit_remap.py) | Build a circuit and remap qubits for real hardware |
| [Dummy Server](examples/getting-started/2_dummy_server.py) | Submit tasks to the local dummy simulator |
| [Result Post-Processing](examples/getting-started/3_result_postprocess.py) | Convert and analyze results |

### Algorithms

| Example | Description |
|---------|-------------|
| [Grover Search](examples/algorithms/grover.md) | Unstructured search with quadratic speedup |
| [Quantum Phase Estimation](examples/algorithms/qpe.md) | Eigenvalue phase estimation |

---

## Documentation

📖 [GitHub Pages](https://iai-ustc-quantum.github.io/UnifiedQuantum/)

---

## Status

🚧 Actively developing. API may change.
