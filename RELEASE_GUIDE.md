# 发布指南

## ✅ 已完成

1. ✓ 代码已推送到 GitHub: https://github.com/z0fans/clash-verge-service.git
2. ✓ 分支: `v1.0.5-release`
3. ✓ 标签: `v1.0.5`
4. ✓ GitHub Actions 配置已存在

## 🚀 触发自动构建和发布

### 方法 1: 通过 GitHub 网页手动触发

1. 访问: https://github.com/z0fans/clash-verge-service/actions
2. 点击左侧的 "Release CI"
3. 点击右侧的 "Run workflow" 按钮
4. 选择分支: `v1.0.5-release`
5. 点击绿色的 "Run workflow" 按钮

### 方法 2: 使用 GitHub CLI (gh)

```bash
# 确保已登录 gh
gh auth login

# 进入仓库目录
cd /Users/yuu/Downloads/clash-verge-rev-2.2.3/clash-verge-service-v1.0.5

# 手动触发工作流
gh workflow run "Release CI" --ref v1.0.5-release
```

## 📦 构建说明

GitHub Actions 将自动构建以下平台的二进制文件:

### Windows
- x86_64-pc-windows-msvc (64位)
- i686-pc-windows-msvc (32位)
- aarch64-pc-windows-msvc (ARM64)

### Linux
- x86_64-unknown-linux-gnu (64位)
- i686-unknown-linux-gnu (32位)
- aarch64-unknown-linux-gnu (ARM64)
- armv7-unknown-linux-gnueabihf (ARMv7)

### macOS
- aarch64-apple-darwin (Apple Silicon)
- x86_64-apple-darwin (Intel)

## 🔑 注意事项

### macOS 代码签名
工作流配置中包含 macOS 代码签名步骤,需要以下 GitHub Secrets:
- `APPLE_CERTIFICATE` - Base64 编码的证书
- `APPLE_CERTIFICATE_PASSWORD` - 证书密码
- `APPLE_SIGNING_IDENTITY` - 签名标识

**如果没有配置这些 secrets,macOS 构建会失败。** 解决方案:
1. 配置证书 (推荐)
2. 或者暂时注释掉 `.github/workflows/release.yml` 中的 CodeSign 步骤

### Linux 交叉编译
Linux 构建使用 Docker 容器进行交叉编译,已在配置中处理。

## 📥 下载构建产物

构建完成后:

1. 访问: https://github.com/z0fans/clash-verge-service/releases
2. 每个平台会创建一个对应的 Release (例如 `x86_64-pc-windows-msvc`)
3. 下载所需平台的二进制文件

## 🎯 Windows 版本快速获取

如果你只需要 Windows 版本:

1. 等待 GitHub Actions 完成(大约 10-20 分钟)
2. 访问: https://github.com/z0fans/clash-verge-service/releases/tag/x86_64-pc-windows-msvc
3. 下载:
   - clash-verge-service.exe
   - install-service.exe
   - uninstall-service.exe

## 🔧 本地构建 (备选方案)

如果 GitHub Actions 遇到问题,可以本地构建:

### Windows 环境
```bash
rustup target add x86_64-pc-windows-msvc
cargo build --release --target x86_64-pc-windows-msvc
```

### 使用 Docker (Linux/macOS)
```bash
docker run --rm -v $(pwd):/workspace -w /workspace rust:latest bash -c "
  rustup target add x86_64-pc-windows-msvc && \
  apt-get update && apt-get install -y mingw-w64 && \
  cargo build --release --target x86_64-pc-windows-msvc
"
```

## 📝 下一步

1. 在 GitHub 上手动触发工作流
2. 等待构建完成
3. 从 Releases 页面下载 Windows 二进制文件
4. 将文件复制到 Clash Verge Rev 项目的 `src-tauri/resources/` 目录
5. 重新打包 Clash Verge Rev
