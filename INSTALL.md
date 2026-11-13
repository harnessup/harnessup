<p align="center">
  <a href="README.md"><img src="assets/banner/banner-en.svg" alt="HarnessUp" width="100%"></a>
</p>

<p align="center">
  <b>🇺🇸 English</b> ·
  <a href="i18n/INSTALL.pt-BR.md">🇧🇷 Português</a> ·
  <a href="i18n/INSTALL.es.md">🇪🇸 Español</a> ·
  <a href="i18n/INSTALL.fr.md">🇫🇷 Français</a> ·
  <a href="i18n/INSTALL.de.md">🇩🇪 Deutsch</a> ·
  <a href="i18n/INSTALL.it.md">🇮🇹 Italiano</a> ·
  <a href="i18n/INSTALL.ja.md">🇯🇵 日本語</a> ·
  <a href="i18n/INSTALL.ko.md">🇰🇷 한국어</a> ·
  <a href="i18n/INSTALL.zh-CN.md">🇨🇳 简体中文</a> ·
  <a href="i18n/INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="i18n/INSTALL.he.md">🇮🇱 עברית</a> ·
  <a href="i18n/INSTALL.hi.md">🇮🇳 हिन्दी</a>
</p>

# Installation guide

Everything you need to install, check, update and uninstall HarnessUp without leaving GitHub. Installation is per user, with no administrator and no system service. Binaries are checked with SHA-256 before installing.

## Contents

- [Quick pick](#quick-pick)
- [npm](#npm)
- [Windows: PowerShell](#windows-powershell)
- [Windows: .exe installer](#windows-exe-installer)
- [macOS and Linux: script](#macos-and-linux-script)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [First use](#first-use)
- [Update](#update)
- [Uninstall](#uninstall)
- [Troubleshooting](#troubleshooting)
- [Coming soon](#coming-soon)
- [Help](#help)

<img src="assets/divider.svg" width="100%">

## Quick pick

| Your situation | Recommended channel |
|---|---|
| You use Node 18+ and live in the terminal | [npm](#npm) |
| Windows, you want one line and no Node | [PowerShell](#windows-powershell) |
| Windows, you prefer clicking "next" | [.exe installer](#windows-exe-installer) |
| Windows, and you want no SmartScreen warning | [npm](#npm) or [PowerShell](#windows-powershell) |
| macOS or Linux, no Node | [`install.sh` script](#macos-and-linux-script) (beta) |
| macOS or Linux, with Node 18+ | [npm](#npm) |
| You prefer to download, check the hash and unzip | [ZIP](#zip-github-releases) |

<img src="assets/divider.svg" width="100%">

## npm

**Requirements**

- Node 18 or newer.
- Windows x64, macOS (arm64 or x64) or Linux x64. npm downloads only the package for your platform.

**Command**

```sh
npm install -g harnessup
```

**What happens**

- npm installs the package for your system, without fetching anything else from outside.
- The `harnessup` command becomes available in the terminal.
- To connect it to your agent, continue to [First use](#first-use).

**How to check**

```sh
harnessup doctor
```

<img src="assets/divider.svg" width="100%">

## Windows: PowerShell

**Requirements**

- Windows x64 with PowerShell. No Node and no administrator needed.

**Command**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

To install without connecting to Claude Code right now:

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**What happens**

- Downloads the latest version and checks its SHA-256 before installing. If the hash does not match, nothing is installed.
- Installs into your user folder (`%LOCALAPPDATA%\HarnessUp\`) and adds it to your PATH.
- Connects to Claude Code, unless you use `-NoHooks`.
- Open a new terminal afterwards, so the `harnessup` command exists in it.

**How to check**

```powershell
harnessup doctor
```

This route has no SmartScreen warning.

<img src="assets/divider.svg" width="100%">

## Windows: .exe installer

**Requirements**

- Windows x64. No administrator needed.

**Steps**

1. Download the installer at [harnessup.dev/install](https://harnessup.dev/install/).
2. Run the file and follow the screens.

**What happens**

- Installs per user, with no administrator, into `%LOCALAPPDATA%\HarnessUp\`.
- Windows will show a SmartScreen warning. See [SmartScreen](#smartscreen-warns-when-opening-the-exe).

**How to check**

Open a new terminal and run:

```powershell
harnessup doctor
```

<img src="assets/divider.svg" width="100%">

## macOS and Linux: script

> **Beta.** This route has not been tested on a real Mac yet.

**Requirements**

- macOS (arm64 or x64) or Linux x64, with `curl`.

**Command**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**Variables**

| Variable | What it does |
|---|---|
| `HARNESSUP_DIR` | Folder to install into. |
| `HARNESSUP_NO_HOOKS=1` | Installs without connecting to Claude Code. |

Example:

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**How to check**

```sh
harnessup doctor
```

<img src="assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**Requirements**

- Windows x64, macOS (arm64 or x64) or Linux x64. No Node and no administrator needed.

**Steps**

1. Download the zip for your system from [Releases](https://github.com/harnessup/harnessup/releases/latest), along with `SHA256SUMS.txt`.

   | System | File |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. Check the SHA-256 and compare it with the file's line in `SHA256SUMS.txt`. If it does not match, do not use it: delete it and download again.

   ```powershell
   Get-FileHash -Algorithm SHA256 <file>
   ```

   ```sh
   shasum -a 256 <file>
   ```

3. Unzip into a folder of your own, with no administrator: on Windows, something like `C:\Users\<you>\HarnessUp`; on macOS and Linux, `~/.local/share/HarnessUp`.
4. On macOS and Linux, if needed: `chmod +x harnessup harnessupd harnessup-hook`.
5. Put the folder on your PATH or call the programs by their path.
6. Run `harnessup install` and then `harnessup doctor`.

**What is in the zip**

- Windows: `harnessup.exe`, `harnessupd.exe`, `harnessup-hook.exe` and `harnessup-panel.exe`.
- macOS and Linux: `harnessup`, `harnessupd` and `harnessup-hook`.

On Windows, the SmartScreen warning may appear. See [SmartScreen](#smartscreen-warns-when-opening-the-exe).

**Update:** download the new zip. The daemon also updates itself if the folder is writable.

**Uninstall:** `harnessup uninstall` and delete the folder.

<img src="assets/divider.svg" width="100%">

## First use

After installing through any channel, run once:

```sh
harnessup install
```

This connects HarnessUp to Claude Code and tells you everything it touched. None of it leaves your machine.

> Claude Code must be installed for the connection. Without it, the installer warns and carries on.

Then start the daemon:

```sh
harnessupd
```

Check:

```sh
harnessup doctor
```

`doctor` shows whether the connection is really installed, which events actually arrived, and through which channels the product can talk to you on this machine.

<details>
<summary><b><code>doctor</code> said "not tested" under <code>[communication channels]</code></b></summary>

<br>

Open Claude Code and send any message. A code will appear. Type:

```sh
harnessup channels <code>
```

If the code does **not** appear, that is also an answer:

```sh
harnessup channels -missing <channel>
```

</details>

<img src="assets/divider.svg" width="100%">

## Update

The dashboard tells you when a new version is out, on any channel.

| Channel | How to update |
|---|---|
| `.exe` installer and PowerShell | Nothing to do. The swap happens by itself on the daemon's next shutdown, never in the middle of a session. If the folder is not writable, the dashboard says so. |
| npm | `npm install -g harnessup@latest` |

<img src="assets/divider.svg" width="100%">

## Uninstall

| Channel | How to uninstall |
|---|---|
| `.exe` installer | Windows "Apps and features", like any program. It removes the Claude Code connection before deleting the files. |
| npm, PowerShell and script | `harnessup uninstall` |

```sh
harnessup uninstall
```

Removes the Claude Code connection and leaves the machine as it was.
<img src="assets/divider.svg" width="100%">

## Troubleshooting

<details>
<summary><b>"harnessup" is not recognized / command not found</b></summary>

<br>

Open a new terminal. The PATH only applies to terminals opened after the installation. If it still fails, run `harnessup doctor` from a new terminal and see what it reports.

</details>

<details id="smartscreen-warns-when-opening-the-exe">
<summary><b>SmartScreen warns when opening the .exe</b></summary>

<br>

The warning is accurate: the `.exe` does not have a code-signing certificate yet, so Windows does not know who published it. This does not mean the file is dangerous, only that Windows does not know.

The [npm](#npm) and [PowerShell](#windows-powershell) routes have no such warning. Once the certificate exists, the warning goes away for the `.exe`.

</details>

<details>
<summary><b>Old Node</b></summary>

<br>

The npm route needs Node 18 or newer. Check with `node --version`. If it is older, update Node or use [PowerShell](#windows-powershell) (Windows) or the [script](#macos-and-linux-script) (macOS and Linux), which do not need it.

</details>

<details>
<summary><b>Claude Code missing</b></summary>

<br>

Without Claude Code installed, the installer warns and carries on: HarnessUp is installed but not connected to it. Install Claude Code and run `harnessup install`.

</details>

<img src="assets/divider.svg" width="100%">

## Coming soon

No date: winget, Scoop, Chocolatey, Homebrew and Snap.

<img src="assets/divider.svg" width="100%">

## Help

- Problems and requests: [Issues](https://github.com/harnessup/harnessup/issues)
- Questions and discussion: [Discussions](https://github.com/harnessup/harnessup/discussions)
- Email: [support@harnessup.dev](mailto:support@harnessup.dev)
