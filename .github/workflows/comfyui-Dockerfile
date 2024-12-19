# 使用更小的基础镜像
FROM ubuntu:25.04

# 设置环境变量以避免交互式提示
ENV DEBIAN_FRONTEND=noninteractive
ENV HSA_OVERRIDE_GFX_VERSION=10.3.0

# 安装基础依赖和 Git、Python 环境
RUN apt-get update && apt-get install -y --no-install-recommends \
    git python3 python3-pip wget && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# 克隆 ComfyUI 项目
RUN git clone https://github.com/comfyanonymous/ComfyUI.git /ComfyUI

# 安装 PyTorch，指定 ROCm 相关包
RUN pip3 install --no-cache-dir torch torchvision torchaudio \
    --index-url https://download.pytorch.org/whl/rocm6.3

# 安装 ComfyUI 项目依赖
WORKDIR /ComfyUI
RUN pip3 install --no-cache-dir -r requirements.txt

# 暴露服务端口并设置默认启动命令
EXPOSE 8188
CMD ["python3", "main.py"]
