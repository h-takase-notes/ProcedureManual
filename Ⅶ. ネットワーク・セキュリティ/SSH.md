---
created: 2026-10-28
tags:
  - ProcedureManual-SSH
  - SSH
---
## 0.パッケージを更新
##### パッケージ一覧を更新
```bash
sudo apt update
```
##### インストール済みパッケージを更新
```bash
sudo apt upgrade
```
## 1.SSHをインストール
```bash
sudo apt install openssh-server
```
> [!NOTE]
> SSHクライアントとSSHサーバーは別の役割です。
> ・`openssh-client`　他のPC・サーバーへSSH接続する
　・`openssh-server`　他のPCからSSH接続を受け付ける
## 2.SSHサーバーを起動
```bash
sudo service ssh start
```
```bash
sudo service ssh status
```
> [!WARNING]
> `Active: active (running)` と表示されれば、SSHサーバーが稼働

## 3. SSHの待ち受けポートを確認
```bash
sudo ss -lntp | grep ':22'
```
## 4. SSH接続確認
##### Ubuntuのユーザー名を確認
```bash
whoami
```
##### PowerShellから接続
```powershell
ssh user@localhost
```
> [!NOTE]
> `user` の部分は、確認したユーザー名に置き換えてください。
> 初回接続時にホスト鍵の確認が表示された場合は、接続先を確認して `yes` と入力します。
> その後、Ubuntuユーザーのパスワードを入力します
## 5. 接続先の確認
##### ホスト名を表示
```bash
hostname
```
##### ユーザ名を表示
```bash
whoami
```
##### 現在の完全パスを表示
```bash
pwd
```
## 6. SSHサーバーを自動起動\\\\\\\\\\\\\\\lll^uuuuuuuuu:nnrf5;
```bash
sudo systemctl enable --now ssh
```
確認
```bash
systemctl is-enabled ssh
```
```bash
systemctl is-active ssh
```

## 7. 接続できない場合の確認
### 7.1. 構文検証
```bash
sudo sshd -t
```
### 7.2. トラブル一覧

| 症状                           | 確認すること                          |
| ---------------------------- | ------------------------------- |
| `Connection refused`         | SSHサーバーが起動しているか、22番ポートで待ち受けているか |
| `Permission denied`          | Ubuntuのユーザー名・パスワード、SSH認証設定      |
| `Could not resolve hostname` | 接続先の入力ミス                        |
| `Connection timed out`       | 接続先IP、ポート転送、ファイアウォールなど          |