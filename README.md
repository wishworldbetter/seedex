# Seedex

Seedex 把你的 Mac 变成一个安全的桥接节点,让你从 iPhone 上无缝使用桌面端的编码会话。所有数据本地存储,所有通信端到端加密。

## 特性

- **端到端加密** — 全程加密,只有你的设备能解密,服务器只是哑通道
- **前向安全** — 每次会话独立密钥,旧密钥泄露不影响历史
- **扫码配对** — 一次扫码,iPhone 立即同步全部桌面历史记录
- **多端同步** — Mac、iPhone 实时双向同步,改在哪一端都立刻生效
- **本地优先** — 数据存在你自己的 Mac 上,不依赖任何第三方云

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

启动桥接守护进程:

```bash
seedex-cli run
```

生成 iPhone 配对二维码:

```bash
seedex-cli qrcode
```

打开 iPhone 上的 Seedex App,扫码即可建立加密通道,桌面历史记录会自动同步过来。

更多命令:

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
