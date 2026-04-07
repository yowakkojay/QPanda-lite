.. QPanda-lite documentation master file

欢迎来到 QPanda-lite!
=======================================

QPanda-lite 是一个 Python 原生、轻量且强调透明性的量子计算框架，提供量子线路构建、本地模拟、多平台任务提交，以及 OriginIR / OpenQASM 2.0 相关能力。

.. image:: https://badge.fury.io/gh/Agony5757%2FQPanda-lite.svg?icon=si%3Agithub
    :target: https://badge.fury.io/gh/Agony5757%2FQPanda-lite

.. image:: https://readthedocs.org/projects/qpanda-lite/badge/?version=latest
   :target: https://qpanda-lite.readthedocs.io/en/latest/?badge=latest
   :alt: Documentation Status

.. image:: https://badge.fury.io/py/qpandalite.svg?icon=si%3Apython
   :target: https://badge.fury.io/py/qpandalite
   :alt: PyPI version

.. image:: https://github.com/Agony5757/QPanda-lite/actions/workflows/build_and_test.yml/badge.svg?branch=main
   :target: https://github.com/Agony5757/QPanda-lite/actions/workflows/build_and_test.yml
   :alt: Build and Test

顶部简介
--------

如果你希望以较低心智负担完成“构建量子线路 -> 本地验证 -> 接入不同后端”的工作流，QPanda-lite 提供了一套偏轻量、偏工程落地的入口。

项目定位
--------

- 面向希望快速编写量子线路、完成本地模拟、再接入云平台或真机任务的用户。
- 聚焦 Python 侧的易用性与透明性，不以“大而全平台”作为目标。
- 适合作为量子程序构建、本地验证、多平台提交流程中的轻量入口。

核心能力概览
------------

- **量子线路构建**：通过 ``Circuit`` 以 Python API 构建量子线路。
- **本地模拟**：支持 OriginIR、QASM 与底层 opcode 相关模拟能力，并提供带噪声模拟路径。
- **任务提交**：支持对接 OriginQ、Quafu、IBM 等平台的任务提交流程。
- **格式与语言支持**：支持 OriginIR，并提供 OpenQASM 2.0 相关能力与格式转换路径。

能力边界与当前状态
------------------

.. note::

   当前文档统一将 QPanda-lite 视为**持续演进中的可用项目**：已经具备安装、线路构建、模拟和部分平台接入能力，但接口、平台成熟度与文档内容仍在持续完善中。使用前请优先关注已知限制与对应页面说明。

- **语言边界**：支持 OriginIR，与 OpenQASM 2.0 相关能力已提供，但 QASM 支持目前仍是不完整支持。
- **平台边界**：多平台任务提交通路已提供，但成熟度并不完全一致；其中 **IBM 相关内容目前仍处于 coming soon 阶段**，不应默认其已达到与其他平台相同的完备度。
- **运行时边界**：既可以使用纯 Python 方式安装，也可以启用 C++ 模拟器；两种方式在依赖和体验上不同。
- **已知限制**：在 density matrix 后端下，``crx``、``crz``、``cy`` 在多门组合时存在已知问题，``controlled_by`` 的模拟结果也不正确。涉及带噪声模拟或 density matrix 路径时，请先阅读安装与模拟文档中的限制说明。

推荐阅读路径
------------

**如果你是第一次接触 QPanda-lite：**

1. :doc:`source/guide/installation`
2. :doc:`source/guide/quickstart`
3. :doc:`source/guide/circuit`
4. :doc:`source/guide/simulation`

**如果你准备提交到云平台或真机：**

1. :doc:`source/guide/installation`
2. :doc:`source/guide/quickstart`
3. :doc:`source/guide/submit_task`

**如果你想先理解语言规范：**

- :doc:`source/guide/originir`
- :doc:`source/guide/qasm`

**如果你更关心底层能力与分析：**

- :doc:`source/advanced/opcode`
- :doc:`source/advanced/noise_simulation`
- :doc:`source/advanced/circuit_analysis`

.. toctree::
   :maxdepth: 2
   :caption: 教程

   source/guide/installation
   source/guide/quickstart
   source/guide/circuit
   source/guide/simulation
   source/guide/submit_task

.. toctree::
   :maxdepth: 2
   :caption: 语言规范

   source/guide/originir
   source/guide/qasm

.. toctree::
   :maxdepth: 2
   :caption: 进阶

   source/advanced/opcode
   source/advanced/noise_simulation
   source/advanced/circuit_analysis

查阅型 API 参考
---------------

以下内容更适合作为按模块检索和补充查阅使用；如果你是第一次接触项目，建议优先阅读上方导览路径，再按需进入 API 参考。

.. toctree::
   :maxdepth: 2
   :caption: API 参考

   source/qpandalite.rst
   source/qpandalite.circuit_builder
   source/qpandalite.simulator
   source/qpandalite.originir
   source/qpandalite.qasm
   source/qpandalite.transpiler
   source/qpandalite.analyzer
   source/qpandalite.qcloud_config
   source/qpandalite.task
   source/qpandalite.task.ibm
   source/qpandalite.task.quafu
   source/qpandalite.task.originq
   source/qpandalite.task.originq_dummy
   source/qpandalite.task.origin_qcloud
   source/qpandalite.task.platform_template

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
