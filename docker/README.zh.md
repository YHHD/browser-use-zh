# Browser-Use 的 Docker 设置

此目录包含 browser-use 的优化 Docker 构建系统，实现 < 30 秒的构建。

## 快速开始

```bash
# 构建基础镜像（仅在第一次需要或依赖项更改时）
./docker/build-base-images.sh

# 构建 browser-use
docker build -f Dockerfile.fast -t browseruse .

# 或使用标准 Dockerfile（较慢但独立）
docker build -t browseruse .
```

## 文件

- `Dockerfile` - 标准独立构建（~2 分钟）
- `Dockerfile.fast` - 使用预构建基础镜像的快速构建（~30 秒）
- `docker/` - 基础镜像定义和构建脚本
  - `base-images/system/` - Python + 最小系统依赖项
  - `base-images/chromium/` - 添加 Chromium 浏览器
  - `base-images/python-deps/` - 添加 Python 依赖项
  - `build-base-images.sh` - 构建所有基础镜像的脚本

## 性能

| 构建类型 | 时间 |
|------------|------|
| 标准 Dockerfile | ~2 分钟 |
| 快速构建（有基础镜像） | ~30 秒 |
| 代码更改后重新构建 | ~16 秒 |
