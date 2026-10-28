---
created: 2026-10-27
tags:
  - ProcedureManual-WSL2
  - WSL2
---
## 0. コマンドプロンプトの起動
1. Windows+Rで「ファイル名を指定して実行」を起動
2. 『cmd』を入力しOKを押下
3. cmd(コマンドプロンプト)が起動
## 1. WSL2をインストール
```powershell
wsl.exe --install
```
　　↓Enter　※管理者権限が必要
```
任意のキーを押して Linux 用 Windows サブシステムをインストールします。
キャンセルするには、ESC キーまたは CTRL-C を押します。
このプロンプトは 60 秒後にタイムアウトします。
要求された操作には管理者特権が必要です。
ダウンロード中: Linux 用 Windows サブシステム 3.0.3
インストール中: Linux 用 Windows サブシステム 3.0.3
Linux 用 Windows サブシステム 3.0.3 はインストールされました。
Windows オプション コンポーネントをインストールしています: VirtualMachinePlatform

展開イメージのサービスと管理ツール
バージョン: 10.0.26100.9549

イメージのバージョン: 10.0.26200.9711

機能を有効にしています

[==========================100.0%==========================]
操作は正常に完了しました。
要求された操作は正常に終了しました。変更を有効にするには、システムを再起動する必要があります。
Linux 用 Windows サブシステムにインストールされているディストリビューションはありません。
この問題を解決するには、以下の手順に従ってディストリビューションをインストールしてください:

'wsl.exe --list --online' を使用して利用可能な配布を一覧表示する
および 'wsl.exe --install <Distro>' を使用してインストールしてください。
```
## 2. インストールできる有効なディストリビューションの一覧を確認
```powershell
wsl.exe --list --online
```
　　↓Enter
```
インストールできる有効なディストリビューションの一覧を次に示します。
'wsl.exe --install <Distro>' を使用してインストールします。

NAME                            FRIENDLY NAME
Ubuntu                          Ubuntu
Ubuntu-26.04                    Ubuntu 26.04 LTS
Ubuntu-24.04                    Ubuntu 24.04 LTS
Ubuntu-22.04                    Ubuntu 22.04 LTS
openSUSE-Tumbleweed             openSUSE Tumbleweed
openSUSE-Leap-16.0              openSUSE Leap 16.0
RLCPlus-9                       Rocky Linux Plus 9 (CIQ)
RLCPlus-10                      Rocky Linux Plus 10 (CIQ)
SUSE-Linux-Enterprise-15-SP7    SUSE Linux Enterprise 15 SP7
SUSE-Linux-Enterprise-16.0      SUSE Linux Enterprise 16.0
kali-linux                      Kali Linux Rolling
Debian                          Debian GNU/Linux
AlmaLinux-8                     AlmaLinux OS 8
AlmaLinux-9                     AlmaLinux OS 9
AlmaLinux-Kitten-10             AlmaLinux OS Kitten 10
AlmaLinux-10                    AlmaLinux OS 10
archlinux                       Arch Linux
FedoraLinux-44                  Fedora Linux 44
FedoraLinux-43                  Fedora Linux 43
eLxr                            eLxr 12.12.0.0 GNU/Linux
OracleLinux_7_9                 Oracle Linux 7.9
OracleLinux_8_10                Oracle Linux 8.10
OracleLinux_9_5                 Oracle Linux 9.5
SUSE-Linux-Enterprise-15-SP6    SUSE Linux Enterprise 15 SP6
```
## 3. ディストリビューションをインストール
例：Ubuntu-24.04　Ubuntu 24.04 LTS　をインストール
```powershell
wsl.exe --install Ubuntu-24.04
```
　　↓Enter
```
ダウンロードしています: Ubuntu 24.04 LTS
インストールしています: Ubuntu 24.04 LTS
ディストリビューションが正常にインストールされました。'wsl.exe -d Ubuntu-24.04' を使用して起動できます
Ubuntu-24.04 を起動しています...
Provisioning the new WSL instance Ubuntu-24.04
This might take a while...
Create a default Unix user account: user
New password:
Retype new password:
passwd: password updated successfully
To run a command as 3;administrator (user "root"), use "sudo <command>"
```

```bash
user@DESKTOP-7MRL954:/mnt/c/Users/user$
```

## 4.確認
### 4.1.WSL関連コンポーネントのバージョン
```powershell
wsl.exe --version
```
　　↓Enter
```
WSL バージョン: 3.0.3.0
カーネル バージョン: 6.18.54.1-1
WSLg バージョン: 1.0.79
MSRDC バージョン: 1.2.7391
Direct3D バージョン: 1.611.1-81528511
DXCore バージョン: 10.0.26100.1-240331-1435.ge-release
Windows バージョン: 10.0.26200.9711
```
### 4.2.WSLの全体的な状態や既定の設定
```powershell
wsl.exe --status
```
　　↓Enter
```
既定のディストリビューション: Ubuntu-24.04
既定のバージョン: 2
WSL1 は、現在のマシン構成ではサポートされていません。
WSL1 を使用するには、"Linux 用 Windows サブシステム" オプション コンポーネントを有効にしてください。
```

### 4.3.インストール済みLinuxと稼働状態
```powershell
wsl.exe --list --verbose
```
　　↓Enter
```
  NAME            STATE           VERSION
* Ubuntu-24.04    Stopped         2
```

> [!TIP] <!--easygit-callout:original=tip,collapse=-->
> `VERSION` が `2` であればWSL2です。
> もし `1` と表示された場合は、次のコマンドで変更できます。
> ```powershell
> wsl.exe --set-version Ubuntu-24.04 2
> ```
> 今後インストールするディストリビューションもWSL2に統一したい場合は、次を実行
> ```powershell
> wsl --set-default-version 2
> ```

## 5. systemdの設定
### 5.1. 設定ファイルに追記
```bash
sudo nano /etc/wsl.conf
```
既存の設定がある場合は消さずに、次のセクションを追加・統合してください。
```ini
[boot]
systemd=true
```
保存方法は `Ctrl + O` → Enter → `Ctrl + X`
### 5.2. WSL2を再起動
WindowsのPowerShellで実行します。
```PowerShell
wsl.exe --shutdown
```