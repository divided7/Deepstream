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

对于 数据中心 GPU（如 NVIDIA Tesla T4、Hopper 等）：需要 535.183.06 或更高版本
。
对于 RTX GPU（如 NVIDIA RTX 3080、RTX 4080 等）：需要 560.35.03 或更高版本。

CUDA 版本：12.6

TensorRT 版本：10.3.0.26 或更高。

## Docker Pull
```bash
docker pull ubuntu:22.04
docker run -it --name Deepstream ubuntu:22.04 /bin/bash # 下次启动使用:docker start -ai Deepstream
cat /etc/os-release # 查看系统信息
```

