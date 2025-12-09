# Clash Verge Service v1.0.5 构建说明

## 版本信息
- **版本**: 1.0.5
- **提交哈希**: ffcccc6095e052534980230f9e0ca97db2675062
- **日期**: 2025年3月24日
- **对应 Clash Verge Rev**: v2.2.3 (2025年4月9日)

## Windows 构建步骤

### 前置要求
1. 安装 Rust: https://rustup.rs/
2. 安装 Visual Studio Build Tools 或完整版 Visual Studio (需要 C++ 工作负载)

### 添加 Windows 目标平台
```bash
# 64位 Windows (推荐)
rustup target add x86_64-pc-windows-msvc

# 32位 Windows
rustup target add i686-pc-windows-msvc

# ARM64 Windows
rustup target add aarch64-pc-windows-msvc
```

### 构建命令

#### 在 Windows 系统上构建:
```bash
# 进入源代码目录
cd clash-verge-service-v1.0.5

# 构建 64位版本 (推荐)
cargo build --release --target x86_64-pc-windows-msvc

# 或 32位版本
cargo build --release --target i686-pc-windows-msvc

# 构建产物位置:
# target/x86_64-pc-windows-msvc/release/clash-verge-service.exe
# target/x86_64-pc-windows-msvc/release/install-service.exe
# target/x86_64-pc-windows-msvc/release/uninstall-service.exe
```

#### 在 macOS/Linux 上交叉编译到 Windows:

**方式1: 使用 cross 工具 (推荐)**
```bash
# 安装 cross (需要 Docker)
cargo install cross

# 构建
cross build --release --target x86_64-pc-windows-msvc
```

**方式2: 使用 cargo-xwin (仅限 Linux/macOS)**
```bash
# 安装 cargo-xwin
cargo install cargo-xwin

# 构建
cargo xwin build --release --target x86_64-pc-windows-msvc
```

## 输出文件

构建成功后,你会得到三个可执行文件:
- `clash-verge-service.exe` - 主服务程序
- `install-service.exe` - 服务安装程序  
- `uninstall-service.exe` - 服务卸载程序

## 故障排除

### 错误: "linker 'link.exe' not found"
- 需要安装 Visual Studio Build Tools
- 下载: https://visualstudio.microsoft.com/visual-cpp-build-tools/

### 错误: OpenSSL 相关
- Windows 上通常不需要 OpenSSL (仅 Linux 需要)
- 如果遇到问题,可以尝试设置环境变量禁用 OpenSSL

## 验证构建

构建完成后,可以运行:
```bash
clash-verge-service.exe --help
```

应该看到版本信息和帮助文本。
