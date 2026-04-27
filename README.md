# Seedex

[English](./README.en.md) · [日本語](./README.ja.md) · **简体中文**

**Claude Code 的 iPhone 远程控制器**。一次扫码配对,iPhone 上立刻拿到 Mac 上的全部 Claude Code 历史会话,并能实时发起 / 接管新的对话。彻底替代官方 Claude Code 的远程方案,数据始终在你自己的 Mac 上。

## 特性

- **免登录** — 一次扫码配对就能用,不用注册、不用任何云服务
- **完整历史同步** — Mac 上所有 Claude Code 项目和会话自动镜像到 iPhone
- **实时双向会话** — Mac 上 Claude Code 跑到哪一步 iPhone 同步看到;iPhone 上发起的对话 Mac 端也实时呈现
- **端到端加密** — 通信全程加密,中继服务器只做哑转发,看不到任何明文
- **前向安全** — 每次会话独立密钥,旧密钥泄露不影响历史会话
- **本地优先** — 所有数据存你自己的 Mac,iPhone 只是个加密视图层

## 快速开始

### Step 1 — 安装

```bash
brew install wishworldbetter/tap/seedex-cli
```

或用 curl:

```bash
curl -fsSL https://github.com/wishworldbetter/seedex/releases/latest/download/install.sh | sh
```

支持 macOS(Intel / Apple Silicon)和 Linux(x86_64 / arm64)。

### Step 2 — 启动后台服务

```bash
seedex-cli service install
seedex-cli service start
```

服务会在 Mac 后台常驻,开机自动启动。

### Step 3 — 扫码配对 iPhone

```bash
seedex-cli qrcode
```

打开 iPhone 上的 Seedex App,扫码即可建立加密通道。Mac 上的全部 Claude Code 历史会话立即出现在 iPhone 上,从此可以从手机上直接发起或接管对话。

---

## 服务管理

```bash
seedex-cli service status     # 查状态
seedex-cli service stop       # 停止
seedex-cli service restart    # 重启
seedex-cli service uninstall  # 移除
```

## 升级

```bash
brew upgrade seedex-cli
```

## 卸载

```bash
seedex-cli service uninstall
brew uninstall seedex-cli
```

## License

CLI 二进制为商业闭源发布。
