<p align="center">
  <a href="README.ko.md"><img src="../assets/banner/banner-ko.svg" alt="HarnessUp" width="100%"></a>
</p>

<p align="center">
  <a href="../INSTALL.md">🇺🇸 English</a> ·
  <a href="INSTALL.pt-BR.md">🇧🇷 Português</a> ·
  <a href="INSTALL.es.md">🇪🇸 Español</a> ·
  <a href="INSTALL.fr.md">🇫🇷 Français</a> ·
  <a href="INSTALL.de.md">🇩🇪 Deutsch</a> ·
  <a href="INSTALL.it.md">🇮🇹 Italiano</a> ·
  <a href="INSTALL.ja.md">🇯🇵 日本語</a> ·
  <b>🇰🇷 한국어</b> ·
  <a href="INSTALL.zh-CN.md">🇨🇳 简体中文</a> ·
  <a href="INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="INSTALL.he.md">🇮🇱 עברית</a> ·
  <a href="INSTALL.hi.md">🇮🇳 हिन्दी</a>
</p>

# 설치 가이드

GitHub를 벗어나지 않고 HarnessUp을 설치, 확인, 업데이트, 제거할 수 있는 가이드예요. 설치는 사용자별로 이루어지며, 관리자 권한이나 시스템 서비스가 필요 없어요. 바이너리는 설치 전에 SHA-256으로 확인해요.

## 목차

- [빠른 선택](#빠른-선택)
- [npm](#npm)
- [Windows: PowerShell](#windows-powershell)
- [Windows: .exe 설치 프로그램](#windows-exe-설치-프로그램)
- [macOS와 Linux: 스크립트](#macos와-linux-스크립트)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [처음 사용](#처음-사용)
- [업데이트](#업데이트)
- [제거](#제거)
- [문제 해결](#문제-해결)
- [곧 출시](#곧-출시)
- [도움말](#도움말)

<img src="../assets/divider.svg" width="100%">

## 빠른 선택

| 내 상황 | 권장 방법 |
|---|---|
| Node 18 이상을 쓰고 터미널에서 작업해요 | [npm](#npm) |
| Windows에서, Node 없이 한 줄로 끝내고 싶어요 | [PowerShell](#windows-powershell) |
| Windows에서, "다음"을 눌러 설치하는 편이 좋아요 | [.exe 설치 프로그램](#windows-exe-설치-프로그램) |
| Windows에서, SmartScreen 경고가 없었으면 좋겠어요 | [npm](#npm) 또는 [PowerShell](#windows-powershell) |
| macOS 또는 Linux이고, Node가 없어요 | [`install.sh` 스크립트](#macos와-linux-스크립트) (베타) |
| macOS 또는 Linux이고, Node 18 이상이 있어요 | [npm](#npm) |
| 내려받아서 해시를 확인하고 압축을 풀고 싶어요 | [ZIP](#zip-github-releases) |

<img src="../assets/divider.svg" width="100%">

## npm

**요구 사항**

- Node 18 이상.
- Windows x64, macOS(arm64 또는 x64) 또는 Linux x64. npm은 내 플랫폼용 패키지만 내려받아요.

**명령어**

```sh
npm install -g harnessup
```

**진행 내용**

- npm이 내 시스템용 패키지를 설치해요. 외부에서 다른 것은 가져오지 않아요.
- 터미널에서 `harnessup` 명령을 쓸 수 있게 돼요.
- 에이전트와 연결하려면 [처음 사용](#처음-사용)으로 이어서 진행하세요.

**확인 방법**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## Windows: PowerShell

**요구 사항**

- PowerShell이 있는 Windows x64. Node도 관리자 권한도 필요 없어요.

**명령어**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

지금 Claude Code에 연결하지 않고 설치하려면:

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**진행 내용**

- 최신 버전을 내려받고 설치 전에 SHA-256을 확인해요. 해시가 맞지 않으면 아무것도 설치되지 않아요.
- 사용자 폴더(`%LOCALAPPDATA%\HarnessUp\`)에 설치하고 PATH에 추가해요.
- `-NoHooks`를 쓰지 않으면 Claude Code에 연결해요.
- 설치 후 새 터미널을 열어야 `harnessup` 명령을 쓸 수 있어요.

**확인 방법**

```powershell
harnessup doctor
```

이 방법에는 SmartScreen 경고가 없어요.

<img src="../assets/divider.svg" width="100%">

## Windows: .exe 설치 프로그램

**요구 사항**

- Windows x64. 관리자 권한은 필요 없어요.

**단계**

1. [harnessup.dev/install](https://harnessup.dev/install/)에서 설치 프로그램을 내려받으세요.
2. 파일을 실행하고 화면의 안내를 따르세요.

**진행 내용**

- 사용자별로, 관리자 권한 없이 `%LOCALAPPDATA%\HarnessUp\`에 설치돼요.
- Windows에 SmartScreen 경고가 뜰 수 있어요. [SmartScreen](#smartscreen-warns-when-opening-the-exe)을 보세요.

**확인 방법**

새 터미널을 열고 다음을 실행하세요:

```powershell
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## macOS와 Linux: 스크립트

> **베타.** 이 방법은 아직 실제 Mac에서 테스트되지 않았어요.

**요구 사항**

- `curl`이 있는 macOS(arm64 또는 x64) 또는 Linux x64.

**명령어**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**변수**

| 변수 | 역할 |
|---|---|
| `HARNESSUP_DIR` | 설치할 폴더. |
| `HARNESSUP_NO_HOOKS=1` | Claude Code에 연결하지 않고 설치해요. |

예시:

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**확인 방법**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**요구 사항**

- Windows x64, macOS(arm64 또는 x64) 또는 Linux x64. Node도 관리자 권한도 필요 없어요.

**단계**

1. [Releases](https://github.com/harnessup/harnessup/releases/latest)에서 내 시스템용 zip과 `SHA256SUMS.txt`를 함께 내려받으세요.

   | 시스템 | 파일 |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. SHA-256을 확인하고, `SHA256SUMS.txt`에서 해당 파일의 줄과 비교하세요. 맞지 않으면 사용하지 말고, 삭제한 뒤 다시 내려받으세요.

   ```powershell
   Get-FileHash -Algorithm SHA256 <file>
   ```

   ```sh
   shasum -a 256 <file>
   ```

3. 관리자 권한 없이, 내 폴더에 압축을 풀어요. Windows에서는 `C:\Users\<you>\HarnessUp`처럼, macOS와 Linux에서는 `~/.local/share/HarnessUp`에요.
4. macOS와 Linux에서 필요하면: `chmod +x harnessup harnessupd harnessup-hook`.
5. 이 폴더를 PATH에 넣거나, 프로그램을 경로로 호출하세요.
6. `harnessup install`을 실행한 다음 `harnessup doctor`를 실행하세요.

**zip 안의 내용**

- Windows: `harnessup.exe`, `harnessupd.exe`, `harnessup-hook.exe`, `harnessup-panel.exe`.
- macOS와 Linux: `harnessup`, `harnessupd`, `harnessup-hook`.

Windows에서는 SmartScreen 경고가 나타날 수 있어요. [SmartScreen](#smartscreen-warns-when-opening-the-exe)을 보세요.

**업데이트:** 새 zip을 내려받으세요. 폴더에 쓸 수 있으면 데몬도 스스로 업데이트해요.

**제거:** `harnessup uninstall`을 실행한 뒤 폴더를 삭제하세요.

<img src="../assets/divider.svg" width="100%">

## 처음 사용

어떤 방법으로 설치하든, 한 번 다음을 실행하세요:

```sh
harnessup install
```

이 명령은 HarnessUp을 Claude Code에 연결하고, 건드린 모든 항목을 알려 줘요. 그중 무엇도 내 컴퓨터 밖으로 나가지 않아요.

> 연결하려면 Claude Code가 설치되어 있어야 해요. 없으면 설치 프로그램이 경고만 띄우고 계속 진행해요.

그다음 데몬을 시작하세요:

```sh
harnessupd
```

확인하세요:

```sh
harnessup doctor
```

`doctor`는 연결이 실제로 설치되었는지, 어떤 이벤트가 실제로 도착했는지, 그리고 이 컴퓨터에서 제품이 어떤 채널로 나에게 말을 걸 수 있는지 보여 줘요.

<details>
<summary><b><code>doctor</code>가 <code>[communication channels]</code> 아래에서 "not tested"라고 했어요</b></summary>

<br>

Claude Code를 열고 아무 메시지나 보내세요. 코드가 나타나요. 다음을 입력하세요:

```sh
harnessup channels <code>
```

코드가 나타나지 **않으면**, 그것도 답이에요:

```sh
harnessup channels -missing <channel>
```

</details>

<img src="../assets/divider.svg" width="100%">

## 업데이트

새 버전이 나오면, 어떤 채널에서든 대시보드가 알려 줘요.

| 채널 | 업데이트 방법 |
|---|---|
| `.exe` 설치 프로그램과 PowerShell | 할 일이 없어요. 교체는 데몬이 다음에 종료될 때 자동으로 이루어지며, 세션 도중에는 절대 일어나지 않아요. 폴더에 쓸 수 없으면 대시보드가 그렇게 알려 줘요. |
| npm | `npm install -g harnessup@latest` |

<img src="../assets/divider.svg" width="100%">

## 제거

| 채널 | 제거 방법 |
|---|---|
| `.exe` 설치 프로그램 | Windows "앱 및 기능"에서, 다른 프로그램과 같은 방식으로 제거해요. 파일을 지우기 전에 Claude Code 연결을 먼저 제거해요. |
| npm, PowerShell, 스크립트 | `harnessup uninstall` |

```sh
harnessup uninstall
```

Claude Code 연결을 제거하고, 컴퓨터를 원래 상태로 되돌려요.
<img src="../assets/divider.svg" width="100%">

## 문제 해결

<details>
<summary><b>"harnessup"을 인식할 수 없음 / command not found</b></summary>

<br>

새 터미널을 여세요. PATH는 설치 후에 열린 터미널에만 적용돼요. 그래도 실패하면 새 터미널에서 `harnessup doctor`를 실행하고, 무엇을 보고하는지 확인하세요.

</details>

<details id="smartscreen-warns-when-opening-the-exe">
<summary><b>.exe를 열 때 SmartScreen 경고가 떠요</b></summary>

<br>

이 경고는 정확해요. `.exe`에는 아직 코드 서명 인증서가 없어서, Windows가 누가 배포했는지 알 수 없어요. 파일이 위험하다는 뜻이 아니라, Windows가 그것을 모른다는 뜻이에요.

[npm](#npm)과 [PowerShell](#windows-powershell) 방법에는 이런 경고가 없어요. 인증서가 생기면 `.exe`에서도 경고가 사라져요.

</details>

<details>
<summary><b>오래된 Node</b></summary>

<br>

npm 방법에는 Node 18 이상이 필요해요. `node --version`으로 확인하세요. 낮은 버전이면 Node를 업데이트하거나, Node가 필요 없는 [PowerShell](#windows-powershell)(Windows) 또는 [스크립트](#macos와-linux-스크립트)(macOS와 Linux)를 쓰세요.

</details>

<details>
<summary><b>Claude Code가 없음</b></summary>

<br>

Claude Code가 설치되어 있지 않으면, 설치 프로그램은 경고만 띄우고 계속 진행해요. HarnessUp은 설치되지만 Claude Code와는 연결되지 않은 상태가 돼요. Claude Code를 설치하고 `harnessup install`을 실행하세요.

</details>

<img src="../assets/divider.svg" width="100%">

## 곧 출시

날짜는 아직 정해지지 않았어요: winget, Scoop, Chocolatey, Homebrew, Snap.

<img src="../assets/divider.svg" width="100%">

## 도움말

- 문제와 요청: [Issues](https://github.com/harnessup/harnessup/issues)
- 질문과 토론: [Discussions](https://github.com/harnessup/harnessup/discussions)
- 이메일: [support@harnessup.dev](mailto:support@harnessup.dev)
