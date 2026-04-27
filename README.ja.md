# Seedex

[English](./README.en.md) · **日本語** · [简体中文](./README.md)

**Claude Code 用の iPhone リモコン**。一度 QR コードでペアリングすれば、Mac 上のすべての Claude Code 履歴が iPhone に即座にミラーリングされ、リアルタイムで会話を開始したり引き継いだりできます。Claude Code の公式リモート機能を完全に置き換え、データは常にあなた自身の Mac に保管されます。

## 特徴

- **ログイン不要** — QR コードを 1 回スキャンするだけ。アカウントもクラウドサービスも不要
- **履歴の完全同期** — Mac 上のすべての Claude Code プロジェクトとセッションを iPhone にミラー
- **双方向リアルタイムセッション** — Mac の Claude Code の進行状況を iPhone で即時確認;iPhone から開始した会話も Mac 側にリアルタイム反映
- **エンドツーエンド暗号化** — 通信はすべて暗号化され、中継サーバーは内容を一切読めない単なるパイプ
- **前方秘匿性** — セッションごとに独立した鍵を使用。鍵が漏洩しても過去のセッションは解読されません
- **ローカルファースト** — すべてのデータはあなたの Mac 上にあり、iPhone は暗号化されたビューに過ぎません

## クイックスタート

### Step 1 — インストール

```bash
brew install wishworldbetter/tap/seedex-cli
```

または curl で:

```bash
curl -fsSL https://github.com/wishworldbetter/seedex/releases/latest/download/install.sh | sh
```

macOS(Intel / Apple Silicon)と Linux(x86_64 / arm64)に対応。

### Step 2 — バックグラウンドサービスを起動

```bash
seedex-cli service install
seedex-cli service start
```

Mac のバックグラウンドで常駐し、起動時に自動で立ち上がります。

### Step 3 — iPhone をペアリング

```bash
seedex-cli qrcode
```

iPhone の Seedex アプリを開いて QR コードをスキャンするだけ。暗号化チャネルが確立され、Mac 上のすべての Claude Code 履歴が iPhone に表示され、これ以降は iPhone から直接会話を開始したり引き継いだりできます。

---

## サービス管理

```bash
seedex-cli service status     # 状態を確認
seedex-cli service stop       # 停止
seedex-cli service restart    # 再起動
seedex-cli service uninstall  # 削除
```

## アップグレード

```bash
brew upgrade seedex-cli
```

## アンインストール

```bash
seedex-cli service uninstall
brew uninstall seedex-cli
```

## ライセンス

CLI バイナリは商用クローズドソースとして配布されています。
