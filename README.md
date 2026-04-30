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
- **企业网络友好** — 自动继承 shell 代理 / SSL 证书配置,公司网下也能直连

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

### Step 2 — 启动

```bash
seedex-cli start
```

进程脱离终端在后台跑,关掉终端不死。子进程默认继承当前 shell 的环境变量,公司代理 / API key 之类无需额外配置。

要 **开机自启**(系统服务模式,launchd / systemd 托管):

```bash
seedex-cli service install
```

### Step 3 — 扫码配对 iPhone

```bash
seedex-cli qrcode
```

打开 iPhone 上的 Seedex App,扫码即可建立加密通道。Mac 上的全部 Claude Code 历史会话立即出现在 iPhone 上,从此可以从手机上直接发起或接管对话。

---

## 后台管理

`seedex-cli start` 起的后台:

```bash
seedex-cli status     # 查状态
seedex-cli stop       # 停掉
seedex-cli restart    # 重启
```

`seedex-cli service install` 起的系统服务:

```bash
seedex-cli service status     # 查状态
seedex-cli service stop       # 停止
seedex-cli service restart    # 重启
seedex-cli service uninstall  # 移除
```

## 企业网络 / 代理

如果你的 Mac 出口必须走 HTTP 代理或公司自签 CA(常见于公司网络下访问 Anthropic API),在你的 shell 里 `export` 过 `https_proxy` / `http_proxy` / `SSL_CERT_FILE` / `NODE_EXTRA_CA_CERTS` 等之后:

- **`seedex-cli start`** — daemon 从你 shell fork,自动继承这些变量,**零配置**
- **`seedex-cli service install`** — install 时自动捕获 shell 中的网络 env 写进 plist / systemd unit;代理变了之后跑一次:

  ```bash
  seedex-cli service refresh-env
  ```

不需要手动编辑 plist。

## 升级

```bash
brew update && brew upgrade seedex-cli
```

升级后:

- `start` 模式:

  ```bash
  seedex-cli restart
  ```

- `service` 模式:

  ```bash
  seedex-cli service refresh-env
  ```

  会把 plist / systemd unit 重写成新版的入口和环境,不需要 uninstall + install。

> **v0.1.x → v0.2.0 首次升级**:`service refresh-env` 会自动把老的 `ProgramArguments=["run"]` 切到新的 `daemon --mode service` 入口。

## 卸载

```bash
seedex-cli stop                # 如果在用 start 模式
seedex-cli service uninstall   # 如果在用 service 模式
brew uninstall seedex-cli
```

## License

CLI 二进制为商业闭源发布。
