# NVIDIA Jetson 边缘 AI 计算平台

> **摘要**：NVIDIA Jetson 系列是专为边缘 AI 计算设计的嵌入式平台，广泛应用于机器人、智能摄像头、工业检测等场景。  
> 
> **标签**：`Jetson` `边缘计算` `AI` `嵌入式` `GPU`  
> **状态**：📝 持续更新中

---

## Jetson主要产品系列简介

### 产品定位与应用场景

NVIDIA Jetson 平台将 GPU、CPU、内存和高速接口集成于小型模组，为边缘设备提供强大的 AI 推理与训练能力。主要应用领域包括：

- **智能机器人**：自主导航、机械臂控制、人机交互
- **智能视觉**：目标检测、人脸识别、行为分析
- **工业自动化**：缺陷检测、质量控制、预测性维护
- **智慧医疗**：影像分析、辅助诊断、手术机器人
- **智慧零售**：客流统计、智能货架、无人结算

### Jetson Orin 系列（最新一代）

| 型号 | GPU 架构 | CUDA 核心数 | AI 算力 (TOPS) | 内存 | 典型功耗 | 适用场景 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Jetson AGX Orin** | Ampere | 2048 | 275 | 64GB LPDDR5 | 15-60W | 高端机器人、工业 AI |
| **Jetson Orin NX** | Ampere | 1024 | 100 | 16GB LPDDR5 | 10-25W | 中端边缘设备 |
| **Jetson Orin Nano** | Ampere | 512 | 40 | 8GB LPDDR5 | 5-15W | 入门级 AI 应用 |

### Jetson Xavier 系列（上一代）

| 型号 | GPU 架构 | AI 算力 (TOPS) | 内存 | 典型功耗 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Jetson AGX Xavier** | Volta | 32 | 32GB | 10-30W | 曾为旗舰产品 |
| **Jetson Xavier NX** | Volta | 21 | 8GB | 10-15W | 性价比突出 |

### Jetson Nano / TX2 系列（经典款）

| 型号 | GPU 架构 | AI 算力 (TOPS) | 内存 | 典型功耗 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Jetson Nano** | Maxwell | 0.5 | 4GB | 5-10W | 学习入门首选 |
| **Jetson TX2** | Pascal | 1.3 | 8GB | 7.5-15W | 已逐步停产 |

### 产品选型建议

1. **入门学习/原型开发**：Jetson Nano / Orin Nano（低成本、社区资源丰富）
2. **中型项目/边缘设备**：Jetson Orin NX（性能与功耗平衡）
3. **高端应用/工业场景**：Jetson AGX Orin（最大算力、完整功能）
4. **成本敏感项目**：Xavier NX（上一代旗舰，性价比优异）

---

## 主要工具及软件包汇总

### JetPack SDK

**JetPack** 是 NVIDIA 为 Jetson 平台提供的完整软件开发套件，包含以下核心组件：

- **操作系统**：基于 Ubuntu Linux 的定制化系统
- **CUDA Toolkit**：GPU 并行计算平台和编程模型
- **cuDNN**：深度神经网络加速库
- **TensorRT**：高性能深度学习推理优化器
- **VisionWorks**：计算机视觉和图像处理库
- **Multimedia API**：视频编解码和摄像头接口
- **OpenCV**：开源计算机视觉库（预编译版本）

> 💡 **安装方式**：可通过 SDK Manager（推荐）或 SD 卡镜像方式安装

### 开发环境与工具链

#### 1. SDK Manager

NVIDIA 官方提供的图形化安装工具，用于：

- 刷写 Jetson 系统镜像
- 安装 JetPack SDK 组件
- 管理交叉编译工具链
- 固件更新

```bash
# Ubuntu 主机安装 SDK Manager
sudo apt update
sudo apt install ./sdkmanager_[version].deb
sdkmanager
```

#### 2. 交叉编译工具链

| 工具 | 用途 | 说明 |
| :--- | :--- | :--- |
| **aarch64-linux-gnu-gcc** | ARM64 交叉编译 | 在 x86 主机上编译 Jetson 程序 |
| **nvcc** | CUDA 编译器 | 编译 GPU 加速代码 |
| **CMake** | 构建系统 | 跨平台项目构建 |
| **catkin** | ROS 构建系统 | 机器人操作系统专用 |

#### 3. 容器化部署

- **Docker**：支持 ARM64 架构的容器运行时
- **NVIDIA Container Runtime**：GPU 容器支持
- **L4T Base Image**：官方提供的基础容器镜像

### AI 框架支持

| 框架 | 版本支持 | 特性 |
| :--- | :--- | :--- |
| **TensorFlow** | 2.x | 官方适配 Jetson 版本 |
| **PyTorch** | 1.x/2.x | 社区预编译包 |
| **ONNX Runtime** | 最新 | 跨平台推理引擎 |
| **Apache TVM** | 最新 | 模型编译优化框架 |

### 常用软件包与库

#### 计算机视觉

- **OpenCV**：`sudo apt install libopencv-dev`
- **GStreamer**：多媒体处理框架（预装）
- **V4L2**：Video4Linux2 摄像头接口

#### 深度学习推理

- **TensorRT**：模型量化与加速推理
- **DeepStream SDK**：视频分析流水线框架
- **Triton Inference Server**：多模型服务部署

#### 机器人开发

- **ROS / ROS2**：机器人操作系统
- **Isaac SDK**：NVIDIA 机器人开发平台
- **ZED SDK**：立体视觉摄像头支持

### 开发资源与文档

- **官方文档**：[NVIDIA Jetson 文档中心](https://docs.nvidia.com/jetson/)
- **开发者论坛**：[NVIDIA Developer Forums](https://forums.developer.nvidia.com/)
- **GitHub 示例**：[jetson-inference](https://github.com/dusty-nv/jetson-inference)
- **SDK 下载**：[NVIDIA SDK Manager](https://developer.nvidia.com/embedded/jetpack)

### 实用命令参考

```bash
# 查看 Jetson 系统信息
jtop

# 查看 GPU 使用情况
tegrastats

# 查看 CUDA 版本
nvcc --version

# 查看 TensorRT 版本
dpkg -l | grep tensorrt

# 查看已安装的 JetPack 版本
cat /etc/nv_tegra_release
```

---

> **备注**：本文档持续完善中，后续将补充更多具体型号的对比分析和实际部署经验。

## Jetson Orin NX

### 资料参考

- [NVIDIA Jetson Orin NX 入门指南](https://zhuanlan.zhihu.com/p/668191700)
- [PyTorch for Jetson - NVIDIA 开发者论坛](https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048)
- [在 Jetson 平台上安装 PyTorch - 官方文档](https://docs.nvidia.com/deeplearning/frameworks/install-pytorch-jetson-platform/index.html)