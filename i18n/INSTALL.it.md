<p align="center">
  <a href="../README.md"><img src="../assets/banner/banner-it.svg" alt="HarnessUp" width="100%"></a>
</p>

<p align="center">
  <a href="../INSTALL.md">🇺🇸 English</a> ·
  <a href="INSTALL.pt-BR.md">🇧🇷 Português</a> ·
  <a href="INSTALL.es.md">🇪🇸 Español</a> ·
  <a href="INSTALL.fr.md">🇫🇷 Français</a> ·
  <a href="INSTALL.de.md">🇩🇪 Deutsch</a> ·
  <b>🇮🇹 Italiano</b> ·
  <a href="INSTALL.ja.md">🇯🇵 日本語</a> ·
  <a href="INSTALL.ko.md">🇰🇷 한국어</a> ·
  <a href="INSTALL.zh-CN.md">🇨🇳 简体中文</a> ·
  <a href="INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="INSTALL.he.md">🇮🇱 עברית</a> ·
  <a href="INSTALL.hi.md">🇮🇳 हिन्दी</a>
</p>

# Guida all'installazione

Tutto ciò che serve per installare, verificare, aggiornare e disinstallare HarnessUp senza uscire da GitHub. L'installazione è per utente, senza amministratore e senza servizi di sistema. I binari vengono verificati con SHA-256 prima dell'installazione.

## Sommario

- [Scelta rapida](#scelta-rapida)
- [npm](#npm)
- [Windows: PowerShell](#windows-powershell)
- [Windows: installer .exe](#windows-installer-exe)
- [macOS e Linux: script](#macos-e-linux-script)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [Primo utilizzo](#primo-utilizzo)
- [Aggiornamento](#aggiornamento)
- [Disinstallazione](#disinstallazione)
- [Risoluzione dei problemi](#risoluzione-dei-problemi)
- [Prossimamente](#prossimamente)
- [Aiuto](#aiuto)

<img src="../assets/divider.svg" width="100%">

## Scelta rapida

| La tua situazione | Canale consigliato |
|---|---|
| Usi Node 18+ e lavori nel terminale | [npm](#npm) |
| Windows, vuoi una riga e niente Node | [PowerShell](#windows-powershell) |
| Windows, preferisci cliccare "avanti" | [installer .exe](#windows-installer-exe) |
| Windows, e non vuoi l'avviso di SmartScreen | [npm](#npm) o [PowerShell](#windows-powershell) |
| macOS o Linux, senza Node | [script `install.sh`](#macos-e-linux-script) (beta) |
| macOS o Linux, con Node 18+ | [npm](#npm) |
| Preferisci scaricare, verificare l'hash e decomprimere | [ZIP](#zip-github-releases) |

<img src="../assets/divider.svg" width="100%">

## npm

**Requisiti**

- Node 18 o successivo.
- Windows x64, macOS (arm64 o x64) o Linux x64. npm scarica solo il pacchetto per la tua piattaforma.

**Comando**

```sh
npm install -g harnessup
```

**Cosa succede**

- npm installa il pacchetto per il tuo sistema, senza recuperare nient'altro dall'esterno.
- Il comando `harnessup` diventa disponibile nel terminale.
- Per collegarlo al tuo agente, prosegui con [Primo utilizzo](#primo-utilizzo).

**Come verificare**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## Windows: PowerShell

**Requisiti**

- Windows x64 con PowerShell. Non servono Node né amministratore.

**Comando**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

Per installare senza collegarlo subito a Claude Code:

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**Cosa succede**

- Scarica l'ultima versione e verifica il suo SHA-256 prima di installare. Se l'hash non corrisponde, non viene installato nulla.
- Installa nella tua cartella utente (`%LOCALAPPDATA%\HarnessUp\`) e la aggiunge al tuo PATH.
- Collega a Claude Code, a meno che tu non usi `-NoHooks`.
- Apri poi un nuovo terminale, così il comando `harnessup` sarà disponibile.

**Come verificare**

```powershell
harnessup doctor
```

Questo percorso non ha l'avviso di SmartScreen.

<img src="../assets/divider.svg" width="100%">

## Windows: installer .exe

**Requisiti**

- Windows x64. Non serve l'amministratore.

**Passaggi**

1. Scarica l'installer da [harnessup.dev/install](https://harnessup.dev/install/).
2. Esegui il file e segui le schermate.

**Cosa succede**

- Installa per utente, senza amministratore, in `%LOCALAPPDATA%\HarnessUp\`.
- Windows mostrerà un avviso di SmartScreen. Vedi [SmartScreen](#smartscreen-avvisa-all-apertura-dell-exe).

**Come verificare**

Apri un nuovo terminale ed esegui:

```powershell
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## macOS e Linux: script

> **Beta.** Questo percorso non è ancora stato testato su un Mac reale.

**Requisiti**

- macOS (arm64 o x64) o Linux x64, con `curl`.

**Comando**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**Variabili**

| Variabile | Cosa fa |
|---|---|
| `HARNESSUP_DIR` | Cartella in cui installare. |
| `HARNESSUP_NO_HOOKS=1` | Installa senza collegare Claude Code. |

Esempio:

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**Come verificare**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**Requisiti**

- Windows x64, macOS (arm64 o x64) o Linux x64. Non servono Node né amministratore.

**Passaggi**

1. Scarica lo zip per il tuo sistema da [Releases](https://github.com/harnessup/harnessup/releases/latest), insieme a `SHA256SUMS.txt`.

   | Sistema | File |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. Verifica il SHA-256 e confrontalo con la riga del file in `SHA256SUMS.txt`. Se non corrisponde, non usarlo: eliminalo e scaricalo di nuovo.

   ```powershell
   Get-FileHash -Algorithm SHA256 <file>
   ```

   ```sh
   shasum -a 256 <file>
   ```

3. Decomprimi in una cartella tua, senza amministratore: su Windows, qualcosa come `C:\Users\<tu>\HarnessUp`; su macOS e Linux, `~/.local/share/HarnessUp`.
4. Su macOS e Linux, se necessario: `chmod +x harnessup harnessupd harnessup-hook`.
5. Metti la cartella nel tuo PATH oppure richiama i programmi tramite il loro percorso.
6. Esegui `harnessup install` e poi `harnessup doctor`.

**Cosa contiene lo zip**

- Windows: `harnessup.exe`, `harnessupd.exe`, `harnessup-hook.exe` e `harnessup-panel.exe`.
- macOS e Linux: `harnessup`, `harnessupd` e `harnessup-hook`.

Su Windows può comparire l'avviso di SmartScreen. Vedi [SmartScreen](#smartscreen-avvisa-all-apertura-dell-exe).

**Aggiornamento:** scarica il nuovo zip. Il daemon si aggiorna anche da solo se la cartella è scrivibile.

**Disinstallazione:** `harnessup uninstall` e cancella la cartella.

<img src="../assets/divider.svg" width="100%">

## Primo utilizzo

Dopo l'installazione con un qualsiasi canale, esegui una volta:

```sh
harnessup install
```

Questo collega HarnessUp a Claude Code e ti dice tutto ciò che ha toccato. Niente di tutto questo esce dalla tua macchina.

> Claude Code deve essere installato per il collegamento. Senza di esso, l'installer avvisa e prosegue.

Poi avvia il daemon:

```sh
harnessupd
```

Verifica:

```sh
harnessup doctor
```

`doctor` mostra se il collegamento è davvero installato, quali eventi sono effettivamente arrivati e attraverso quali canali il prodotto può parlarti su questa macchina.

<details>
<summary><b><code>doctor</code> ha detto "not tested" sotto <code>[communication channels]</code></b></summary>

<br>

Apri Claude Code e invia un messaggio qualsiasi. Comparirà un codice. Digita:

```sh
harnessup channels <code>
```

Se il codice **non** compare, anche questa è una risposta:

```sh
harnessup channels -missing <channel>
```

</details>

<img src="../assets/divider.svg" width="100%">

## Aggiornamento

La dashboard ti avvisa quando esce una nuova versione, su qualsiasi canale.

| Canale | Come aggiornare |
|---|---|
| Installer `.exe` e PowerShell | Nulla da fare. Lo scambio avviene da solo alla prossima chiusura del daemon, mai nel mezzo di una sessione. Se la cartella non è scrivibile, la dashboard lo segnala. |
| npm | `npm install -g harnessup@latest` |

<img src="../assets/divider.svg" width="100%">

## Disinstallazione

| Canale | Come disinstallare |
|---|---|
| Installer `.exe` | "App e funzionalità" di Windows, come per qualsiasi programma. Rimuove il collegamento con Claude Code prima di cancellare i file. |
| npm, PowerShell e script | `harnessup uninstall` |

```sh
harnessup uninstall
```

Rimuove il collegamento con Claude Code e lascia la macchina com'era.
<img src="../assets/divider.svg" width="100%">

## Risoluzione dei problemi

<details>
<summary><b>"harnessup" non è riconosciuto / command not found</b></summary>

<br>

Apri un nuovo terminale. Il PATH vale solo per i terminali aperti dopo l'installazione. Se continua a non funzionare, esegui `harnessup doctor` da un nuovo terminale e leggi cosa segnala.

</details>

<details id="smartscreen-avvisa-all-apertura-dell-exe">
<summary><b>SmartScreen avvisa all'apertura dell'.exe</b></summary>

<br>

L'avviso è corretto: l'`.exe` non ha ancora un certificato di firma del codice, quindi Windows non sa chi lo ha pubblicato. Questo non significa che il file sia pericoloso, solo che Windows non sa chi lo ha firmato.

I percorsi [npm](#npm) e [PowerShell](#windows-powershell) non hanno questo avviso. Quando il certificato sarà disponibile, l'avviso sparirà per l'`.exe`.

</details>

<details>
<summary><b>Node vecchio</b></summary>

<br>

Il percorso npm richiede Node 18 o successivo. Verifica con `node --version`. Se è più vecchio, aggiorna Node oppure usa [PowerShell](#windows-powershell) (Windows) o lo [script](#macos-e-linux-script) (macOS e Linux), che non ne hanno bisogno.

</details>

<details>
<summary><b>Claude Code mancante</b></summary>

<br>

Senza Claude Code installato, l'installer avvisa e prosegue: HarnessUp viene installato ma non collegato. Installa Claude Code ed esegui `harnessup install`.

</details>

<img src="../assets/divider.svg" width="100%">

## Prossimamente

Senza data: winget, Scoop, Chocolatey, Homebrew e Snap.

<img src="../assets/divider.svg" width="100%">

## Aiuto

- Problemi e richieste: [Issues](https://github.com/harnessup/harnessup/issues)
- Domande e discussioni: [Discussions](https://github.com/harnessup/harnessup/discussions)
- Email: [support@harnessup.dev](mailto:support@harnessup.dev)
