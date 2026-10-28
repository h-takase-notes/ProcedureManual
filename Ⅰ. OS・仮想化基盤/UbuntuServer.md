---
created: 2026-10-27
tags:
  - ProcedureManual-UbuntuServer
  - UbuntuServer
---
## 0.ダウンロード・準備

## 1.インストール

## 2.初期設定
### 2.1.バージョンと状態を確認
##### Ubuntuのバージョン
```bash
lsb_release -a
```
##### Linuxカーネルの情報
```bash
uname -a
```
##### 現在のユーザー
```bash
whoami
```
##### ユーザーIDと所属グループ
```bash
id
```
##### ディスクの空き容量
```bash
df -h /
```
##### メモリの使用状況
```bash
free -h
```
### 2.2.最新の状態にする
##### パッケージ一覧を更新
```bash
sudo apt update
```
##### インストール済みパッケージを更新
```bash
sudo apt upgrade
```
##### パッケージを整理
```bash
sudo apt autoremove
```
### 2.3.基本的な開発ツールをインストール
#### 2.3.1.共通
##### ディレクトリ構造の表示
```bash
sudo apt install tree
```
```bash
tree --version
```
##### CPU・メモリ・プロセスの確認
```bash
sudo apt install htop
```
```bash
htop --version
```
#### 2.3.2.用途別
##### Web APIへのアクセス
```bash
sudo apt install curl
```
```bash
curl --version
```
##### HTTPS通信に必要な証明書
```bash
sudo apt install ca-certificates
```
```bash
ca-certificates --version
```
##### JSONデータの解析・整形
```bash
sudo apt install jq
```
```bash
jq --version
```

### 2.4.日本語環境・時刻の設定
```bash
timedatectl
```
`Asia/Tokyo` になっていれば、変更不要です。異なる場合は以下を実行。
```bash
sudo timedatectl set-timezone Asia/Tokyo
```
```bash
date
```
### 2.5.日本語入力・文字化け対策
```bash
locale
locale -a
```
`C.UTF-8` や `ja_JP.utf8` などを確認します。日本語ロケールが必要なら次を実行。
```bash
sudo apt install -y language-pack-ja
```
```bash
sudo update-locale LANG=ja_JP.UTF-8
```
