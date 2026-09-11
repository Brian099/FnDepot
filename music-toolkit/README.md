# 飞牛 NAS 原生应用 (FnOS App) 打包说明

本文档记录如何维护与打包 `music-toolkit.fpk` 飞牛官方格式应用包。

## 目录结构

- `manifest`: 飞牛应用清单文件（版本号、架构、名称、桌面入口等）
- `fnpack.exe`: 飞牛官方 Windows 端打包工具命令行程序
- `app/`:
  - `music-toolkit-linux-amd64`: Linux 平台运行的主程序二进制（已内嵌 Web 前端）
  - `bin/`: 内置静态依赖二进制（`ffmpeg`、`ffprobe`、`fpcalc`）
  - `ui/`: 应用桌面快捷方式及配置
- `cmd/`:
  - `main`: 飞牛后台服务启动与停止控制脚本（已配置挂载目录识别与环境变量导出）
  - `install_init`, `install_callback`, `uninstall_init`, `upgrade_callback` 等生命周期钩子
- `config/`: 权限与应用配置
- `wizard/`: 安装向导配置
- `ICON.PNG`, `ICON_256.PNG`: 应用图标

---

## 本地打包流程 (PowerShell)

在项目根目录下依次执行：

```powershell
# 1. 编译最新的 Linux AMD64 二进制 (无 CGo 纯静态)
$env:CGO_ENABLED="0"; $env:GOOS="linux"; $env:GOARCH="amd64"; go build -ldflags="-s -w" -o music-toolkit-linux-amd64 .

# 2. 将编译出的二进制覆盖复制到应用 app 目录
Copy-Item -Path music-toolkit-linux-amd64 -Destination .\飞牛应用\app\music-toolkit-linux-amd64 -Force

# 3. 进入飞牛应用目录调用打包工具
cd 飞牛应用
.\fnpack.exe build
cd ..
```

执行后，将在当前目录生成最新的 `music-toolkit.fpk`，可直接在飞牛 NAS 的【应用中心】->【手动安装】中上传使用。
