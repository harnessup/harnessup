<p align="center">
  <a href="README.zh-CN.md"><img src="../assets/banner/banner-zh-CN.svg" alt="HarnessUp" width="100%"></a>
</p>

<p align="center">
  <a href="../INSTALL.md">🇺🇸 English</a> ·
  <a href="INSTALL.pt-BR.md">🇧🇷 Português</a> ·
  <a href="INSTALL.es.md">🇪🇸 Español</a> ·
  <a href="INSTALL.fr.md">🇫🇷 Français</a> ·
  <a href="INSTALL.de.md">🇩🇪 Deutsch</a> ·
  <a href="INSTALL.it.md">🇮🇹 Italiano</a> ·
  <a href="INSTALL.ja.md">🇯🇵 日本語</a> ·
  <a href="INSTALL.ko.md">🇰🇷 한국어</a> ·
  <b>🇨🇳 简体中文</b> ·
  <a href="INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="INSTALL.he.md">🇮🇱 עברית</a> ·
  <a href="INSTALL.hi.md">🇮🇳 हिन्दी</a>
</p>

# 安装指南

无需离开 GitHub，即可安装、检查、更新和卸载 HarnessUp 的全部说明。安装按用户进行，无需管理员权限，也无需系统服务。安装前会使用 SHA-256 校验二进制文件。

## 目录

- [快速选择](#快速选择)
- [npm](#npm)
- [Windows: PowerShell](#windows-powershell)
- [Windows: .exe 安装程序](#windows-exe-安装程序)
- [macOS 与 Linux 脚本](#macos-与-linux-脚本)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [首次使用](#首次使用)
- [更新](#更新)
- [卸载](#卸载)
- [故障排除](#故障排除)
- [即将推出](#即将推出)
- [帮助](#帮助)

<img src="../assets/divider.svg" width="100%">

## 快速选择

| 你的情况 | 推荐方式 |
|---|---|
| 你使用 Node 18+，并在终端中工作 | [npm](#npm) |
| Windows，想一行命令完成，且不装 Node | [PowerShell](#windows-powershell) |
| Windows，更习惯点击"下一步" | [.exe 安装程序](#windows-exe-安装程序) |
| Windows，并且不希望出现 SmartScreen 警告 | [npm](#npm) 或 [PowerShell](#windows-powershell) |
| macOS 或 Linux，没有 Node | [`install.sh` 脚本](#macos-与-linux-脚本)（测试版） |
| macOS 或 Linux，已安装 Node 18+ | [npm](#npm) |
| 你希望下载后核对哈希并解压 | [ZIP](#zip-github-releases) |

<img src="../assets/divider.svg" width="100%">

## npm

**要求**

- Node 18 或更新版本。
- Windows x64、macOS（arm64 或 x64）或 Linux x64。npm 只下载适用于你平台的包。

**命令**

```sh
npm install -g harnessup
```

**会发生什么**

- npm 为你的系统安装对应的包，不会从外部获取其他内容。
- 终端中即可使用 `harnessup` 命令。
- 要将它连接到你的智能体，请继续阅读[首次使用](#首次使用)。

**如何检查**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## Windows: PowerShell

**要求**

- 带有 PowerShell 的 Windows x64。无需 Node，也无需管理员权限。

**命令**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

如果暂时不想连接 Claude Code 进行安装：

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**会发生什么**

- 下载最新版本，并在安装前核对 SHA-256。如果哈希不匹配，什么都不会安装。
- 安装到你的用户文件夹（`%LOCALAPPDATA%\HarnessUp\`），并添加到 PATH。
- 除非使用 `-NoHooks`，否则会连接到 Claude Code。
- 安装后请打开一个新终端，这样才能使用 `harnessup` 命令。

**如何检查**

```powershell
harnessup doctor
```

此方式没有 SmartScreen 警告。

<img src="../assets/divider.svg" width="100%">

## Windows: .exe 安装程序

**要求**

- Windows x64。无需管理员权限。

**步骤**

1. 在 [harnessup.dev/install](https://harnessup.dev/install/) 下载安装程序。
2. 运行文件，并按屏幕提示操作。

**会发生什么**

- 按用户安装，无需管理员权限，安装到 `%LOCALAPPDATA%\HarnessUp\`。
- Windows 可能会显示 SmartScreen 警告。请参见 [SmartScreen](#smartscreen-warns-when-opening-the-exe)。

**如何检查**

打开一个新终端并运行：

```powershell
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## macOS 与 Linux 脚本

> **测试版。** 此方式尚未在真实的 Mac 上测试。

**要求**

- 带有 `curl` 的 macOS（arm64 或 x64）或 Linux x64。

**命令**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**变量**

| 变量 | 作用 |
|---|---|
| `HARNESSUP_DIR` | 安装到的文件夹。 |
| `HARNESSUP_NO_HOOKS=1` | 安装时不连接 Claude Code。 |

示例：

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**如何检查**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**要求**

- Windows x64、macOS（arm64 或 x64）或 Linux x64。无需 Node，也无需管理员权限。

**步骤**

1. 从 [Releases](https://github.com/harnessup/harnessup/releases/latest) 下载适用于你系统的 zip，并一同下载 `SHA256SUMS.txt`。

   | 系统 | 文件 |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. 核对 SHA-256，并与 `SHA256SUMS.txt` 中该文件的那一行比较。如果不匹配，请不要使用：删除后重新下载。

   ```powershell
   Get-FileHash -Algorithm SHA256 <file>
   ```

   ```sh
   shasum -a 256 <file>
   ```

3. 在你自己的文件夹中解压，无需管理员权限：Windows 上类似 `C:\Users\<you>\HarnessUp`；macOS 和 Linux 上为 `~/.local/share/HarnessUp`。
4. 在 macOS 和 Linux 上，如有需要：`chmod +x harnessup harnessupd harnessup-hook`。
5. 将该文件夹加入 PATH，或通过路径调用这些程序。
6. 运行 `harnessup install`，然后运行 `harnessup doctor`。

**zip 中的内容**

- Windows：`harnessup.exe`、`harnessupd.exe`、`harnessup-hook.exe` 和 `harnessup-panel.exe`。
- macOS 和 Linux：`harnessup`、`harnessupd` 和 `harnessup-hook`。

在 Windows 上，可能会出现 SmartScreen 警告。请参见 [SmartScreen](#smartscreen-warns-when-opening-the-exe)。

**更新：** 下载新的 zip。如果文件夹可写，守护进程也会自行更新。

**卸载：** 运行 `harnessup uninstall`，然后删除该文件夹。

<img src="../assets/divider.svg" width="100%">

## 首次使用

通过任意方式安装后，运行一次：

```sh
harnessup install
```

这会将 HarnessUp 连接到 Claude Code，并告诉你它改动过的所有内容。这些内容都不会离开你的电脑。

> 连接需要已安装 Claude Code。如果未安装，安装程序会给出警告并继续。

然后启动守护进程：

```sh
harnessupd
```

检查：

```sh
harnessup doctor
```

`doctor` 会显示连接是否真的已安装、哪些事件实际到达，以及产品能通过本机的哪些渠道与你通信。

<details>
<summary><b><code>doctor</code> 在 <code>[communication channels]</code> 下显示"not tested"</b></summary>

<br>

打开 Claude Code，发送任意消息，会出现一个代码。输入：

```sh
harnessup channels <code>
```

如果代码**没有**出现，那也是一个答案：

```sh
harnessup channels -missing <channel>
```

</details>

<img src="../assets/divider.svg" width="100%">

## 更新

新版本发布时，仪表盘会在任何渠道上告诉你。

| 渠道 | 如何更新 |
|---|---|
| `.exe` 安装程序和 PowerShell | 无需操作。替换会在守护进程下次关闭时自动完成，绝不会在会话中途进行。如果文件夹不可写，仪表盘会提示。 |
| npm | `npm install -g harnessup@latest` |

<img src="../assets/divider.svg" width="100%">

## 卸载

| 渠道 | 如何卸载 |
|---|---|
| `.exe` 安装程序 | Windows"应用和功能"，与其他程序一样。删除文件前会先移除 Claude Code 连接。 |
| npm、PowerShell 和脚本 | `harnessup uninstall` |

```sh
harnessup uninstall
```

移除 Claude Code 连接，并让电脑恢复原样。
<img src="../assets/divider.svg" width="100%">

## 故障排除

<details>
<summary><b>"harnessup" 无法识别 / 找不到命令</b></summary>

<br>

打开一个新终端。PATH 只对安装之后打开的终端生效。如果仍然失败，请在新终端中运行 `harnessup doctor`，并查看它报告的内容。

</details>

<details id="smartscreen-warns-when-opening-the-exe">
<summary><b>打开 .exe 时 SmartScreen 发出警告</b></summary>

<br>

该警告是准确的：`.exe` 目前还没有代码签名证书，因此 Windows 无法识别发布者。这并不表示文件有危险，只是 Windows 无法确认它的来源。

[npm](#npm) 和 [PowerShell](#windows-powershell) 方式没有此类警告。证书到位后，`.exe` 的警告也会消失。

</details>

<details>
<summary><b>Node 版本过旧</b></summary>

<br>

npm 方式需要 Node 18 或更新版本。使用 `node --version` 检查。如果版本较旧，请更新 Node，或使用不需要 Node 的 [PowerShell](#windows-powershell)（Windows）或[脚本](#macos-与-linux-脚本)（macOS 和 Linux）。

</details>

<details>
<summary><b>缺少 Claude Code</b></summary>

<br>

如果未安装 Claude Code，安装程序会给出警告并继续：HarnessUp 已安装，但未与其连接。请安装 Claude Code，然后运行 `harnessup install`。

</details>

<img src="../assets/divider.svg" width="100%">

## 即将推出

暂无日期：winget、Scoop、Chocolatey、Homebrew 和 Snap。

<img src="../assets/divider.svg" width="100%">

## 帮助

- 问题与请求：[Issues](https://github.com/harnessup/harnessup/issues)
- 提问与讨论：[Discussions](https://github.com/harnessup/harnessup/discussions)
- 邮件：[support@harnessup.dev](mailto:support@harnessup.dev)
