<p align="center">
  <a href="README.de.md"><img src="../assets/banner/banner-de.svg" alt="HarnessUp" width="100%"></a>
</p>

<p align="center">
  <a href="../INSTALL.md">🇺🇸 English</a> ·
  <a href="INSTALL.pt-BR.md">🇧🇷 Português</a> ·
  <a href="INSTALL.es.md">🇪🇸 Español</a> ·
  <a href="INSTALL.fr.md">🇫🇷 Français</a> ·
  <b>🇩🇪 Deutsch</b> ·
  <a href="INSTALL.it.md">🇮🇹 Italiano</a> ·
  <a href="INSTALL.ja.md">🇯🇵 日本語</a> ·
  <a href="INSTALL.ko.md">🇰🇷 한국어</a> ·
  <a href="INSTALL.zh-CN.md">🇨🇳 简体中文</a> ·
  <a href="INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="INSTALL.he.md">🇮🇱 עברית</a> ·
  <a href="INSTALL.hi.md">🇮🇳 हिन्दी</a>
</p>

# Installationsanleitung

Alles, was du brauchst, um HarnessUp zu installieren, zu prüfen, zu aktualisieren und zu deinstallieren, ohne GitHub zu verlassen. Die Installation erfolgt pro Benutzer, ohne Administrator und ohne Systemdienst. Binaries werden vor der Installation mit SHA-256 geprüft.

## Inhalt

- [Schnellauswahl](#schnellauswahl)
- [npm](#npm)
- [Windows: PowerShell](#windows-powershell)
- [Windows: .exe-Installer](#windows-exe-installer)
- [macOS und Linux: Skript](#macos-und-linux-skript)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [Erste Verwendung](#erste-verwendung)
- [Aktualisierung](#aktualisierung)
- [Deinstallation](#deinstallation)
- [Fehlerbehebung](#fehlerbehebung)
- [Demnächst verfügbar](#demnächst-verfügbar)
- [Hilfe](#hilfe)

<img src="../assets/divider.svg" width="100%">

## Schnellauswahl

| Deine Situation | Empfohlener Weg |
|---|---|
| Du nutzt Node 18+ und arbeitest im Terminal | [npm](#npm) |
| Windows, du willst eine Zeile und kein Node | [PowerShell](#windows-powershell) |
| Windows, du klickst lieber auf „Weiter“ | [.exe-Installer](#windows-exe-installer) |
| Windows, und du willst keine SmartScreen-Warnung | [npm](#npm) oder [PowerShell](#windows-powershell) |
| macOS oder Linux, ohne Node | [`install.sh`-Skript](#macos-und-linux-skript) (Beta) |
| macOS oder Linux, mit Node 18+ | [npm](#npm) |
| Du lädst lieber herunter, prüfst den Hash und entpackst | [ZIP](#zip-github-releases) |

<img src="../assets/divider.svg" width="100%">

## npm

**Voraussetzungen**

- Node 18 oder neuer.
- Windows x64, macOS (arm64 oder x64) oder Linux x64. npm lädt nur das Paket für deine Plattform.

**Befehl**

```sh
npm install -g harnessup
```

**Was passiert**

- npm installiert das Paket für dein System, ohne etwas anderes von außen zu laden.
- Der Befehl `harnessup` wird im Terminal verfügbar.
- Um ihn mit deinem Agenten zu verbinden, geh weiter zu [Erste Verwendung](#erste-verwendung).

**So prüfst du es**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## Windows: PowerShell

**Voraussetzungen**

- Windows x64 mit PowerShell. Kein Node und kein Administrator nötig.

**Befehl**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

Zum Installieren ohne sofortige Verbindung zu Claude Code:

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**Was passiert**

- Lädt die neueste Version herunter und prüft ihren SHA-256, bevor installiert wird. Stimmt der Hash nicht, wird nichts installiert.
- Installiert in deinen Benutzerordner (`%LOCALAPPDATA%\HarnessUp\`) und fügt ihn zu deinem PATH hinzu.
- Verbindet sich mit Claude Code, außer du nutzt `-NoHooks`.
- Öffne danach ein neues Terminal, damit der Befehl `harnessup` darin existiert.

**So prüfst du es**

```powershell
harnessup doctor
```

Dieser Weg hat keine SmartScreen-Warnung.

<img src="../assets/divider.svg" width="100%">

## Windows: .exe-Installer

**Voraussetzungen**

- Windows x64. Kein Administrator nötig.

**Schritte**

1. Lade den Installer unter [harnessup.dev/install](https://harnessup.dev/install/) herunter.
2. Starte die Datei und folge den Bildschirmen.

**Was passiert**

- Installiert pro Benutzer, ohne Administrator, nach `%LOCALAPPDATA%\HarnessUp\`.
- Windows zeigt eine SmartScreen-Warnung. Siehe [SmartScreen](#smartscreen-warns-when-opening-the-exe).

**So prüfst du es**

Öffne ein neues Terminal und führe aus:

```powershell
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## macOS und Linux: Skript

> **Beta.** Dieser Weg wurde noch nicht auf einem echten Mac getestet.

**Voraussetzungen**

- macOS (arm64 oder x64) oder Linux x64, mit `curl`.

**Befehl**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**Variablen**

| Variable | Was sie tut |
|---|---|
| `HARNESSUP_DIR` | Ordner, in den installiert wird. |
| `HARNESSUP_NO_HOOKS=1` | Installiert ohne Verbindung zu Claude Code. |

Beispiel:

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**So prüfst du es**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**Voraussetzungen**

- Windows x64, macOS (arm64 oder x64) oder Linux x64. Kein Node und kein Administrator nötig.

**Schritte**

1. Lade das ZIP für dein System von [Releases](https://github.com/harnessup/harnessup/releases/latest) herunter, zusammen mit `SHA256SUMS.txt`.

   | System | Datei |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. Prüfe den SHA-256 und vergleiche ihn mit der Zeile der Datei in `SHA256SUMS.txt`. Stimmt er nicht überein, verwende die Datei nicht: lösche sie und lade sie erneut herunter.

   ```powershell
   Get-FileHash -Algorithm SHA256 <datei>
   ```

   ```sh
   shasum -a 256 <datei>
   ```

3. Entpacke in einen eigenen Ordner ohne Administrator: unter Windows etwa `C:\Users\<du>\HarnessUp`; unter macOS und Linux `~/.local/share/HarnessUp`.
4. Unter macOS und Linux, falls nötig: `chmod +x harnessup harnessupd harnessup-hook`.
5. Lege den Ordner in deinen PATH oder rufe die Programme über ihren Pfad auf.
6. Führe `harnessup install` und danach `harnessup doctor` aus.

**Inhalt des ZIPs**

- Windows: `harnessup.exe`, `harnessupd.exe`, `harnessup-hook.exe` und `harnessup-panel.exe`.
- macOS und Linux: `harnessup`, `harnessupd` und `harnessup-hook`.

Unter Windows kann die SmartScreen-Warnung erscheinen. Siehe [SmartScreen](#smartscreen-warns-when-opening-the-exe).

**Aktualisierung:** lade das neue ZIP herunter. Der Daemon aktualisiert sich außerdem selbst, wenn der Ordner beschreibbar ist.

**Deinstallation:** `harnessup uninstall` und dann den Ordner löschen.

<img src="../assets/divider.svg" width="100%">

## Erste Verwendung

Führe nach der Installation über einen beliebigen Weg einmal aus:

```sh
harnessup install
```

Das verbindet HarnessUp mit Claude Code und zeigt dir alles, was es angefasst hat. Nichts davon verlässt deine Maschine.

> Für die Verbindung muss Claude Code installiert sein. Ohne es warnt der Installer und macht weiter.

Starte dann den Daemon:

```sh
harnessupd
```

Prüfe:

```sh
harnessup doctor
```

`doctor` zeigt, ob die Verbindung wirklich installiert ist, welche Ereignisse tatsächlich angekommen sind und über welche Kanäle das Produkt auf diesem Rechner mit dir sprechen kann.

<details>
<summary><b><code>doctor</code> meldete „not tested“ unter <code>[communication channels]</code></b></summary>

<br>

Öffne Claude Code und sende eine beliebige Nachricht. Ein Code erscheint. Tippe:

```sh
harnessup channels <code>
```

Wenn der Code **nicht** erscheint, ist auch das eine Antwort:

```sh
harnessup channels -missing <kanal>
```

</details>

<img src="../assets/divider.svg" width="100%">

## Aktualisierung

Das Dashboard meldet dir, wenn eine neue Version erschienen ist, auf jedem Kanal.

| Kanal | So aktualisierst du |
|---|---|
| `.exe`-Installer und PowerShell | Nichts zu tun. Der Austausch passiert beim nächsten Herunterfahren des Daemons von selbst, nie mitten in einer Sitzung. Ist der Ordner nicht beschreibbar, meldet das Dashboard es. |
| npm | `npm install -g harnessup@latest` |

<img src="../assets/divider.svg" width="100%">

## Deinstallation

| Kanal | So deinstallierst du |
|---|---|
| `.exe`-Installer | Windows „Apps und Features“, wie bei jedem Programm. Es entfernt die Verbindung zu Claude Code, bevor die Dateien gelöscht werden. |
| npm, PowerShell und Skript | `harnessup uninstall` |

```sh
harnessup uninstall
```

Entfernt die Verbindung zu Claude Code und lässt den Rechner so, wie er war.
<img src="../assets/divider.svg" width="100%">

## Fehlerbehebung

<details>
<summary><b>„harnessup“ wird nicht erkannt / command not found</b></summary>

<br>

Öffne ein neues Terminal. Der PATH gilt nur für Terminals, die nach der Installation geöffnet wurden. Wenn es immer noch fehlschlägt, führe `harnessup doctor` in einem neuen Terminal aus und lies, was es meldet.

</details>

<details id="smartscreen-warns-when-opening-the-exe">
<summary><b>SmartScreen warnt beim Öffnen der .exe</b></summary>

<br>

Die Warnung ist zutreffend: Die `.exe` hat noch kein Code-Signing-Zertifikat, daher weiß Windows nicht, wer sie veröffentlicht hat. Das heißt nicht, dass die Datei gefährlich ist, nur dass Windows sie nicht kennt.

Die Wege [npm](#npm) und [PowerShell](#windows-powershell) haben keine solche Warnung. Sobald das Zertifikat existiert, verschwindet die Warnung für die `.exe`.

</details>

<details>
<summary><b>Altes Node</b></summary>

<br>

Der npm-Weg braucht Node 18 oder neuer. Prüfe es mit `node --version`. Ist es älter, aktualisiere Node oder nutze [PowerShell](#windows-powershell) (Windows) oder das [Skript](#macos-und-linux-skript) (macOS und Linux), die es nicht brauchen.

</details>

<details>
<summary><b>Claude Code fehlt</b></summary>

<br>

Ohne installiertes Claude Code warnt der Installer und macht weiter: HarnessUp ist installiert, aber nicht mit ihm verbunden. Installiere Claude Code und führe `harnessup install` aus.

</details>

<img src="../assets/divider.svg" width="100%">

## Demnächst verfügbar

Kein Datum: winget, Scoop, Chocolatey, Homebrew und Snap.

<img src="../assets/divider.svg" width="100%">

## Hilfe

- Probleme und Anfragen: [Issues](https://github.com/harnessup/harnessup/issues)
- Fragen und Diskussion: [Discussions](https://github.com/harnessup/harnessup/discussions)
- E-Mail: [support@harnessup.dev](mailto:support@harnessup.dev)
