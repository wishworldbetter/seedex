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

---

## macOS

### 安装

```bash
brew install wishworldbetter/tap/seedex-cli
```

### 启动

```bash
seedex-cli service install   # 注册到 launchd
seedex-cli service start     # 启动 + 健康检查
```

第一次启动会弹 **"Allow Seedex in Background"**,允许即可。

### 配对 iPhone

```bash
seedex-cli qrcode
```

打开 iPhone 上的 Seedex App,扫码即可。

> 出于安全考虑,**二维码扫描一次后立即失效**,下次配对需要重新跑 `seedex-cli qrcode` 生成新的。

### 升级

```bash
brew update && brew upgrade seedex-cli
seedex-cli service stop
seedex-cli service uninstall
seedex-cli service install
seedex-cli service start
```

跨大版本(比如 v0.1.x → v0.2.x)plist 的 ProgramArguments / EnvVars 段都要换,完整重装比 `service restart` in-place 更稳。小版本之间(v0.2.x 互升)可以直接 `service restart`。

### 卸载

```bash
seedex-cli service stop
seedex-cli service uninstall
brew uninstall seedex-cli
```

---

## Linux

### 安装

```bash
curl -fsSL https://github.com/wishworldbetter/seedex/releases/latest/download/install.sh | sh
```

支持 x86_64 / arm64,需要 systemd(几乎所有现代发行版都满足)。

### 启动

```bash
seedex-cli service install   # 写 ~/.config/systemd/user/seedex.service
seedex-cli service start     # 启动 + 健康检查
```

如果你**完全登出**(关 SSH、退出 GUI)后仍想让它跑,启用 lingering:

```bash
loginctl enable-linger "$USER"
```

### 配对手机

```bash
seedex-cli qrcode
```

> 出于安全考虑,**二维码扫描一次后立即失效**,下次配对需要重新跑 `seedex-cli qrcode` 生成新的。

### 升级

重新跑一次安装脚本,然后:

```bash
seedex-cli service stop
seedex-cli service uninstall
seedex-cli service install
seedex-cli service start
```

跨大版本完整重装比 `service restart` in-place 更稳。小版本之间(v0.2.x 互升)可以直接 `service restart`。

### 卸载

```bash
seedex-cli service stop
seedex-cli service uninstall
rm -f /usr/local/bin/seedex-cli   # 或 ~/.local/bin/seedex-cli, 看 install.sh 装哪
```

---

## Windows

当前只支持 **WSL2 (Ubuntu)**,在 WSL distro 里跑。

### 安装

```bash
curl -fsSL https://github.com/wishworldbetter/seedex/releases/latest/download/install.sh | sh
```

### 启动

```bash
seedex-cli start
```

WSL2 上不走 systemd user service(`loginctl enable-linger` 在 WSL 里行为不稳定),直接用 `start` 模式后台跑。WSL distro 不 shutdown 就一直在。

### 配对手机

```bash
seedex-cli qrcode
```

> 出于安全考虑,**二维码扫描一次后立即失效**,下次配对需要重新跑 `seedex-cli qrcode` 生成新的。

### 升级

重新跑一次安装脚本,然后:

```bash
seedex-cli restart
```

### 卸载

```bash
seedex-cli stop
rm -f /usr/local/bin/seedex-cli   # 或 ~/.local/bin/seedex-cli
```

---

## 高级:不要开机自启

如果只是临时跑、CI、或者不想注册系统服务:

```bash
seedex-cli start              # 后台跑,继承当前 shell env,关机就停
seedex-cli stop               # 停
seedex-cli restart            # 重启
seedex-cli status             # 查状态
```

跟 `service install` 的区别:这条路径**不写 plist / systemd unit**,纯 self-daemonize,关机就停;但好处是 macOS 上**不触发** Background Items 系统权限弹窗,适合快速验证或不希望开机自启的场景。

---

## 企业网络 / 代理

```bash
seedex-cli service restart
```

---

## License

CLI 二进制为商业闭源发布。
