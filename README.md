# Seedex

**Claude Code 的 iPhone 远程控制器**。无需登录任何账号,一次扫码配对,iPhone 上立刻拿到 Mac 本地 `~/.claude/projects/` 下的全部历史会话,并能实时发起 / 接管新的 Claude Code 对话。彻底替代官方 Claude Code 的远程方案,数据始终在你自己的 Mac 上。

## 特性

- **零账号** — 不用 Anthropic 账号、不用任何云服务,一次扫码就完事
- **完整历史同步** — `~/.claude/projects/` 下所有项目和会话自动镜像到 iPhone
- **实时双向会话** — Mac 上 Claude Code 跑到哪一步 iPhone 同步看到;iPhone 上发起的对话 Mac 端也实时呈现
- **端到端加密** — 通信全程加密,中继服务器只做哑转发,看不到任何明文
- **前向安全** — 每次会话独立密钥,旧密钥泄露不影响历史会话
- **本地优先** — 所有数据存你自己的 Mac,iPhone 只是个加密视图层

## 安装

### Homebrew(推荐)

```bash
brew install wishworldbetter/tap/seedex-cli
```

### curl 一键安装

```bash
curl -fsSL https://github.com/wishworldbetter/seedex/releases/latest/download/install.sh | sh
```

支持平台:macOS(Intel / Apple Silicon)、Linux(x86_64 / arm64)。

## 使用

### 前台运行(快速试用)

```bash
seedex-cli run
```

终端关掉就停了,适合首次试用或调试。

### 后台服务(推荐,长期使用)

注册为用户级系统服务(macOS 用 launchd,Linux 用 systemd),开机自启、终端关掉照样跑:

```bash
seedex-cli service install   # 注册服务
seedex-cli service start     # 启动
seedex-cli service status    # 查状态
```

其他常用命令:

```bash
seedex-cli service stop      # 停止
seedex-cli service restart   # 重启
seedex-cli service uninstall # 移除
```

### 配对 iPhone

服务跑起来后,生成配对二维码:

```bash
seedex-cli qrcode
```

打开 iPhone 上的 Seedex App,扫码即可建立加密通道,桌面历史记录会自动同步过来。

### 更多命令

```bash
seedex-cli --help
```

## 升级

```bash
brew upgrade seedex-cli
# 或
curl -fsSL https://github.com/wishworldbetter/seedex/releases/latest/download/install.sh | sh
```

## 卸载

```bash
brew uninstall seedex-cli
# 或
sudo rm /usr/local/bin/seedex-cli
```

## License

CLI 二进制为商业闭源发布。
