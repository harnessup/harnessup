<p align="center">
  <a href="README.ja.md"><img src="../assets/banner/banner-ja.svg" alt="HarnessUp" width="100%"></a>
</p>

<p align="center">
  <a href="../INSTALL.md">🇺🇸 English</a> ·
  <a href="INSTALL.pt-BR.md">🇧🇷 Português</a> ·
  <a href="INSTALL.es.md">🇪🇸 Español</a> ·
  <a href="INSTALL.fr.md">🇫🇷 Français</a> ·
  <a href="INSTALL.de.md">🇩🇪 Deutsch</a> ·
  <a href="INSTALL.it.md">🇮🇹 Italiano</a> ·
  <b>🇯🇵 日本語</b> ·
  <a href="INSTALL.ko.md">🇰🇷 한국어</a> ·
  <a href="INSTALL.zh-CN.md">🇨🇳 简体中文</a> ·
  <a href="INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="INSTALL.he.md">🇮🇱 עברית</a> ·
  <a href="INSTALL.hi.md">🇮🇳 हिन्दी</a>
</p>

# インストールガイド

GitHub を離れることなく、HarnessUp のインストール、確認、更新、アンインストールができるガイドです。インストールはユーザーごとに行われ、管理者権限もシステムサービスも不要です。バイナリはインストール前に SHA-256 で検証されます。

## 目次

- [かんたんな選び方](#かんたんな選び方)
- [npm](#npm)
- [Windows: PowerShell](#windows-powershell)
- [Windows: .exe インストーラー](#windows-exe-インストーラー)
- [macOS と Linux: スクリプト](#macos-と-linux-スクリプト)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [初回の使い方](#初回の使い方)
- [更新](#更新)
- [アンインストール](#アンインストール)
- [トラブルシューティング](#トラブルシューティング)
- [近日公開](#近日公開)
- [ヘルプ](#ヘルプ)

<img src="../assets/divider.svg" width="100%">

## かんたんな選び方

| あなたの状況 | おすすめの方法 |
|---|---|
| Node 18 以上を使っていて、ターミナルで作業する | [npm](#npm) |
| Windows で、Node なしで一行で済ませたい | [PowerShell](#windows-powershell) |
| Windows で、「次へ」をクリックして進めたい | [.exe インストーラー](#windows-exe-インストーラー) |
| Windows で、SmartScreen の警告を出したくない | [npm](#npm) または [PowerShell](#windows-powershell) |
| macOS または Linux で、Node はない | [`install.sh` スクリプト](#macos-と-linux-スクリプト)（ベータ） |
| macOS または Linux で、Node 18 以上がある | [npm](#npm) |
| ダウンロードして、ハッシュを確認し、解凍したい | [ZIP](#zip-github-releases) |

<img src="../assets/divider.svg" width="100%">

## npm

**必要条件**

- Node 18 以降。
- Windows x64、macOS（arm64 または x64）、または Linux x64。npm はお使いのプラットフォーム用のパッケージだけをダウンロードします。

**コマンド**

```sh
npm install -g harnessup
```

**何が起きるか**

- npm が、お使いのシステム用のパッケージをインストールします。外部からほかの何かを取得することはありません。
- `harnessup` コマンドがターミナルで使えるようになります。
- エージェントに接続するには、[初回の使い方](#初回の使い方)に進んでください。

**確認方法**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## Windows: PowerShell

**必要条件**

- PowerShell が使える Windows x64。Node も管理者権限も不要です。

**コマンド**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

Claude Code にすぐには接続せずにインストールするには：

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**何が起きるか**

- 最新バージョンをダウンロードし、インストール前に SHA-256 を確認します。ハッシュが一致しなければ、何もインストールされません。
- ユーザーフォルダ（`%LOCALAPPDATA%\HarnessUp\`）にインストールし、PATH に追加します。
- `-NoHooks` を使わない限り、Claude Code に接続します。
- そのあとで新しいターミナルを開くと、`harnessup` コマンドが使えるようになります。

**確認方法**

```powershell
harnessup doctor
```

この方法には SmartScreen の警告はありません。

<img src="../assets/divider.svg" width="100%">

## Windows: .exe インストーラー

**必要条件**

- Windows x64。管理者権限は不要です。

**手順**

1. [harnessup.dev/install](https://harnessup.dev/install/) からインストーラーをダウンロードします。
2. ファイルを実行し、画面の指示に従います。

**何が起きるか**

- ユーザーごとにインストールされ、管理者権限は不要で、`%LOCALAPPDATA%\HarnessUp\` に入ります。
- Windows が SmartScreen の警告を表示する場合があります。[SmartScreen](#smartscreen-warns-when-opening-the-exe) を参照してください。

**確認方法**

新しいターミナルを開き、次を実行します：

```powershell
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## macOS と Linux: スクリプト

> **ベータ版。** この方法は、まだ実物の Mac では検証されていません。

**必要条件**

- `curl` が使える macOS（arm64 または x64）または Linux x64。

**コマンド**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**変数**

| 変数 | 働き |
|---|---|
| `HARNESSUP_DIR` | インストール先のフォルダ。 |
| `HARNESSUP_NO_HOOKS=1` | Claude Code に接続せずにインストールします。 |

例：

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**確認方法**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**必要条件**

- Windows x64、macOS（arm64 または x64）、または Linux x64。Node も管理者権限も不要です。

**手順**

1. お使いのシステム用の zip を [Releases](https://github.com/harnessup/harnessup/releases/latest) からダウンロードし、あわせて `SHA256SUMS.txt` も取得します。

   | システム | ファイル |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. SHA-256 を確認し、`SHA256SUMS.txt` の該当ファイルの行と比べます。一致しなければ使わず、削除して再度ダウンロードしてください。

   ```powershell
   Get-FileHash -Algorithm SHA256 <file>
   ```

   ```sh
   shasum -a 256 <file>
   ```

3. 管理者権限なしで、自分のフォルダに解凍します。Windows では `C:\Users\<you>\HarnessUp` のような場所、macOS と Linux では `~/.local/share/HarnessUp` です。
4. macOS と Linux で必要な場合：`chmod +x harnessup harnessupd harnessup-hook`。
5. フォルダを PATH に追加するか、プログラムをパスで呼び出します。
6. `harnessup install` を実行し、続けて `harnessup doctor` を実行します。

**zip の中身**

- Windows：`harnessup.exe`、`harnessupd.exe`、`harnessup-hook.exe`、`harnessup-panel.exe`。
- macOS と Linux：`harnessup`、`harnessupd`、`harnessup-hook`。

Windows では SmartScreen の警告が出る場合があります。[SmartScreen](#smartscreen-warns-when-opening-the-exe) を参照してください。

**更新：** 新しい zip をダウンロードします。フォルダに書き込みできる場合は、デーモンも自分で更新します。

**アンインストール：** `harnessup uninstall` を実行してから、フォルダを削除します。

<img src="../assets/divider.svg" width="100%">

## 初回の使い方

どの方法でインストールしても、一度だけ次を実行します：

```sh
harnessup install
```

これで HarnessUp が Claude Code に接続され、触ったものすべてが表示されます。どれもお使いのマシンの外には出ません。

> 接続には Claude Code のインストールが必要です。ない場合、インストーラーは警告を出して先に進みます。

次に、デーモンを起動します：

```sh
harnessupd
```

確認します：

```sh
harnessup doctor
```

`doctor` は、接続が実際にインストールされているか、どのイベントが実際に届いているか、そしてこのマシンでどのチャネルを通じて製品があなたに話しかけられるかを表示します。

<details>
<summary><b><code>doctor</code> が <code>[communication channels]</code> の下で「not tested」と表示した場合</b></summary>

<br>

Claude Code を開いて、任意のメッセージを送ってください。コードが表示されます。次のように入力します：

```sh
harnessup channels <code>
```

コードが**表示されない**場合も、それが答えです：

```sh
harnessup channels -missing <channel>
```

</details>

<img src="../assets/divider.svg" width="100%">

## 更新

新しいバージョンが出ると、どのチャネルでもダッシュボードが知らせます。

| チャネル | 更新方法 |
|---|---|
| `.exe` インストーラーと PowerShell | 何もする必要はありません。入れ替えは、デーモンが次に終了するときに自動で行われ、セッションの途中で行われることはありません。フォルダに書き込みできない場合は、ダッシュボードがその旨を表示します。 |
| npm | `npm install -g harnessup@latest` |

<img src="../assets/divider.svg" width="100%">

## アンインストール

| チャネル | アンインストール方法 |
|---|---|
| `.exe` インストーラー | Windows の「アプリと機能」から、ほかのプログラムと同じように行います。ファイルを削除する前に、Claude Code との接続を取り除きます。 |
| npm、PowerShell、スクリプト | `harnessup uninstall` |

```sh
harnessup uninstall
```

Claude Code との接続を取り除き、マシンを元の状態に戻します。
<img src="../assets/divider.svg" width="100%">

## トラブルシューティング

<details>
<summary><b>「harnessup」が認識されません / コマンドが見つかりません</b></summary>

<br>

新しいターミナルを開いてください。PATH は、インストール後に開かれたターミナルにだけ適用されます。それでも失敗する場合は、新しいターミナルから `harnessup doctor` を実行し、表示された内容を確認してください。

</details>

<details id="smartscreen-warns-when-opening-the-exe">
<summary><b>.exe を開くと SmartScreen が警告する</b></summary>

<br>

この警告は正確です。`.exe` にはまだコード署名証明書がないため、Windows はそれを誰が公開したのか把握できません。ファイルが危険だという意味ではなく、Windows がそれを知らないというだけです。

[npm](#npm) と [PowerShell](#windows-powershell) の方法には、そのような警告はありません。証明書ができると、`.exe` についてもこの警告はなくなります。

</details>

<details>
<summary><b>古い Node</b></summary>

<br>

npm の方法には Node 18 以上が必要です。`node --version` で確認してください。古い場合は、Node を更新するか、Node を必要としない [PowerShell](#windows-powershell)（Windows）または [スクリプト](#macos-と-linux-スクリプト)（macOS と Linux）を使ってください。

</details>

<details>
<summary><b>Claude Code がない</b></summary>

<br>

Claude Code がインストールされていない場合、インストーラーは警告を出して先に進みます。HarnessUp はインストールされますが、Claude Code には接続されていない状態です。Claude Code をインストールし、`harnessup install` を実行してください。

</details>

<img src="../assets/divider.svg" width="100%">

## 近日公開

日付は未定です：winget、Scoop、Chocolatey、Homebrew、Snap。

<img src="../assets/divider.svg" width="100%">

## ヘルプ

- 問題とリクエスト：[Issues](https://github.com/harnessup/harnessup/issues)
- 質問と議論：[Discussions](https://github.com/harnessup/harnessup/discussions)
- メール：[support@harnessup.dev](mailto:support@harnessup.dev)
