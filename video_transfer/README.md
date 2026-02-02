# Video Transfer (TOS App)

本项目是适配 TerraMaster TOS 系统的 **Video Transfer** 应用包源码。

## 项目简介

Video Transfer 是一个基于 FFmpeg 和 FastAPI 的视频转码工具，支持硬件加速（NVIDIA/Intel/AMD）和 Web 界面管理。

## 目录结构说明

- **`app/`**: 应用核心文件
  - **`docker/`**: 包含 Dockerfile, docker-compose 模板, Python 源码等核心逻辑。详细文档请见 [app/docker/README.md](app/docker/README.md)。
  - **`ui/`**: TOS 桌面图标与 UI 配置文件。
- **`cmd/`**: TOS 应用生命周期管理脚本 (start, stop, install 等)。
- **`wizard/`**: 安装向导配置，用于在安装时收集用户设置（如媒体目录路径）。
- **`manifest`**: 应用元数据描述文件。

## 打包与发布

本项目遵循 TOS 应用包结构标准。
1. 确保 `manifest` 中的版本号正确。
2. 使用 TOS 打包工具将目录打包为 `.tpk` 文件。
3. 在 TOS 应用中心进行安装测试。

## 快速入口

- **核心代码**: [app/docker/main.py](app/docker/main.py)
- **安装脚本**: [app/docker/setup.sh](app/docker/setup.sh)
- **UI 配置**: [app/ui/config](app/ui/config)
