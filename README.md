# Deepstream

步骤 1：确认系统要求

 ~/.local/bin/ 已添加到 ~/.bashrc 或 ~/.profile 中的环境变量 PATH

确保系统运行 Ubuntu 22.04。

安装支持的 NVIDIA GPU 驱动程序（适用于 DeepStream SDK 7.1，推荐 GPU 驱动程序版本 **>= 525.xx**）。

已安装 **CUDA Toolkit 12.x**（兼容的版本可以在 NVIDIA 文档中确认）。

安装前置要求

在安装 DeepStream SDK 之前，您需要确保以下组件已正确安装：

操作系统

Ubuntu 22.04

GStreamer 版本：1.20.3

NVIDIA 驱动程序

对于 数据中心 GPU（如 NVIDIA Tesla T4、Hopper 等）：需要 535.183.06 或更高版本。对于 RTX GPU（如 NVIDIA RTX 3080、RTX 4080 等）：需要 560.35.03 或更高版本。

CUDA 版本：12.6

TensorRT 版本：10.3.0.26 或更高。

# Docker配置
## 拉取ubuntu22.04镜像，创建容器 `Deepstream`
```bash
docker pull ubuntu:22.04
docker run -it --name Deepstream ubuntu:22.04 /bin/bash # 下次启动使用:docker start -ai Deepstream
cat /etc/os-release # 查看系统信息
```
## 如果直接使用系统环境，则下面所有代码前面要加`sudo`
## 进入容器配置GStreamer
```bash
apt update
apt install -y \
    build-essential \
    meson \
    ninja-build \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    libglib2.0-dev \
    libgirepository1.0-dev \
    liborc-dev \
    libx11-dev \
    libx264-dev \
    libx265-dev
gst-inspect-1.0 --version # 查看Gstreamer版本
```

## Install Nvidia driver
在 Docker 容器内直接安装 NVIDIA 驱动是不推荐的，因为 NVIDIA 驱动通常是需要直接与宿主机的硬件进行交互的，而 Docker 容器是为了提供与宿主机隔离的运行环境。安装 NVIDIA 驱动程序通常是宿主机操作系统的任务，而不是容器内的任务。

正确的做法：通过 nvidia-container-tooklit 和 NVIDIA 驱动支持 GPU

为了让 Docker 容器使用 NVIDIA GPU，你需要在宿主机上安装 NVIDIA 驱动程序并配置 nvidia-container-tooklit 工具。容器中的 GPU 访问是通过宿主机的 NVIDIA 驱动和 nvidia-container-toolkit 实现的。

1. 确保宿主机安装了nvidia驱动 (nvidia-smi检查）

2. 安装 NVIDIA Docker（nvidia-container-toolkit） （安装参考: https://github.com/NVIDIA/nvidia-container-toolkit） (使用指令检查是否安装好: nvidia-container-tooklit --version）

3. 关闭容器`Deepstream`, 使用带gpu的方式启动
   ```bash
   sudo docker stop Deepstream
   sudo docker start -i --gpus all Deepstream
   ```

5.  

6.  
