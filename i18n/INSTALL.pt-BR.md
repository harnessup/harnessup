<p align="center">
  <a href="../README.md"><img src="../assets/banner/banner-pt-BR.svg" alt="HarnessUp" width="100%"></a>
</p>

<p align="center">
  <a href="../INSTALL.md">🇺🇸 English</a> ·
  <b>🇧🇷 Português</b> ·
  <a href="INSTALL.es.md">🇪🇸 Español</a> ·
  <a href="INSTALL.fr.md">🇫🇷 Français</a> ·
  <a href="INSTALL.de.md">🇩🇪 Deutsch</a> ·
  <a href="INSTALL.it.md">🇮🇹 Italiano</a> ·
  <a href="INSTALL.ja.md">🇯🇵 日本語</a> ·
  <a href="INSTALL.ko.md">🇰🇷 한국어</a> ·
  <a href="INSTALL.zh-CN.md">🇨🇳 简体中文</a> ·
  <a href="INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="INSTALL.he.md">🇮🇱 עברית</a> ·
  <a href="INSTALL.hi.md">🇮🇳 हिन्दी</a>
</p>

# Guia de instalação

Tudo o que você precisa para instalar, conferir, atualizar e desinstalar o HarnessUp sem sair do GitHub. A instalação é por usuário, sem administrador e sem serviço de sistema. Os binários são verificados com SHA-256 antes de instalar.

## Sumário

- [Escolha rápida](#escolha-rápida)
- [npm](#npm)
- [Windows: PowerShell](#windows-powershell)
- [Windows: instalador .exe](#windows-instalador-exe)
- [macOS e Linux: script](#macos-e-linux-script)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [Primeiro uso](#primeiro-uso)
- [Atualização](#atualização)
- [Desinstalação](#desinstalação)
- [Solução de problemas](#solução-de-problemas)
- [Em breve](#em-breve)
- [Ajuda](#ajuda)

<img src="../assets/divider.svg" width="100%">

## Escolha rápida

| Sua situação | Canal recomendado |
|---|---|
| Você usa Node 18+ e vive no terminal | [npm](#npm) |
| Windows, você quer uma linha e sem Node | [PowerShell](#windows-powershell) |
| Windows, você prefere clicar em "próximo" | [instalador .exe](#windows-instalador-exe) |
| Windows, e você não quer o aviso do SmartScreen | [npm](#npm) ou [PowerShell](#windows-powershell) |
| macOS ou Linux, sem Node | [script `install.sh`](#macos-e-linux-script) (beta) |
| macOS ou Linux, com Node 18+ | [npm](#npm) |
| Você prefere baixar, conferir o hash e descompactar | [ZIP](#zip-github-releases) |

<img src="../assets/divider.svg" width="100%">

## npm

**Requisitos**

- Node 18 ou mais recente.
- Windows x64, macOS (arm64 ou x64) ou Linux x64. O npm baixa apenas o pacote da sua plataforma.

**Comando**

```sh
npm install -g harnessup
```

**O que acontece**

- O npm instala o pacote para o seu sistema, sem buscar nada mais fora.
- O comando `harnessup` fica disponível no terminal.
- Para conectar ao seu agente, continue em [Primeiro uso](#primeiro-uso).

**Como conferir**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## Windows: PowerShell

**Requisitos**

- Windows x64 com PowerShell. Não precisa de Node nem de administrador.

**Comando**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

Para instalar sem conectar ao Claude Code agora:

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**O que acontece**

- Baixa a versão mais recente e confere o SHA-256 antes de instalar. Se o hash não bater, nada é instalado.
- Instala na sua pasta de usuário (`%LOCALAPPDATA%\HarnessUp\`) e adiciona ao seu PATH.
- Conecta ao Claude Code, a menos que você use `-NoHooks`.
- Abra um novo terminal depois, para que o comando `harnessup` exista nele.

**Como conferir**

```powershell
harnessup doctor
```

Esta rota não tem aviso do SmartScreen.

<img src="../assets/divider.svg" width="100%">

## Windows: instalador .exe

**Requisitos**

- Windows x64. Não precisa de administrador.

**Passos**

1. Baixe o instalador em [harnessup.dev/install](https://harnessup.dev/install/).
2. Execute o arquivo e siga as telas.

**O que acontece**

- Instala por usuário, sem administrador, em `%LOCALAPPDATA%\HarnessUp\`.
- O Windows vai mostrar um aviso do SmartScreen. Veja [SmartScreen](#smartscreen-avisa-ao-abrir-o-exe).

**Como conferir**

Abra um novo terminal e rode:

```powershell
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## macOS e Linux: script

> **Beta.** Esta rota ainda não foi testada em um Mac real.

**Requisitos**

- macOS (arm64 ou x64) ou Linux x64, com `curl`.

**Comando**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**Variáveis**

| Variável | O que faz |
|---|---|
| `HARNESSUP_DIR` | Pasta onde instalar. |
| `HARNESSUP_NO_HOOKS=1` | Instala sem conectar ao Claude Code. |

Exemplo:

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**Como conferir**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**Requisitos**

- Windows x64, macOS (arm64 ou x64) ou Linux x64. Não precisa de Node nem de administrador.

**Passos**

1. Baixe o zip do seu sistema em [Releases](https://github.com/harnessup/harnessup/releases/latest), junto com `SHA256SUMS.txt`.

   | Sistema | Arquivo |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. Confira o SHA-256 e compare com a linha do arquivo em `SHA256SUMS.txt`. Se não bater, não use: apague e baixe de novo.

   ```powershell
   Get-FileHash -Algorithm SHA256 <arquivo>
   ```

   ```sh
   shasum -a 256 <arquivo>
   ```

3. Descompacte em uma pasta sua, sem administrador: no Windows, algo como `C:\Users\<você>\HarnessUp`; no macOS e Linux, `~/.local/share/HarnessUp`.
4. No macOS e Linux, se precisar: `chmod +x harnessup harnessupd harnessup-hook`.
5. Coloque a pasta no seu PATH ou chame os programas pelo caminho.
6. Rode `harnessup install` e depois `harnessup doctor`.

**O que tem no zip**

- Windows: `harnessup.exe`, `harnessupd.exe`, `harnessup-hook.exe` e `harnessup-panel.exe`.
- macOS e Linux: `harnessup`, `harnessupd` e `harnessup-hook`.

No Windows, o aviso do SmartScreen pode aparecer. Veja [SmartScreen](#smartscreen-avisa-ao-abrir-o-exe).

**Atualização:** baixe o novo zip. O daemon também se atualiza sozinho se a pasta for gravável.

**Desinstalação:** `harnessup uninstall` e apague a pasta.

<img src="../assets/divider.svg" width="100%">

## Primeiro uso

Depois de instalar por qualquer canal, rode uma vez:

```sh
harnessup install
```

Isso conecta o HarnessUp ao Claude Code e informa tudo o que ele tocou. Nada disso sai da sua máquina.

> O Claude Code precisa estar instalado para a conexão. Sem ele, o instalador avisa e segue em frente.

Depois, inicie o daemon:

```sh
harnessupd
```

Confira:

```sh
harnessup doctor
```

`doctor` mostra se a conexão está realmente instalada, quais eventos chegaram de fato e por quais canais o produto consegue falar com você nesta máquina.

<details>
<summary><b><code>doctor</code> disse "not tested" em <code>[canais de fala]</code></b></summary>

<br>

Abra o Claude Code e envie qualquer mensagem. Um código vai aparecer. Digite:

```sh
harnessup channels <code>
```

Se o código **não** aparecer, essa também é uma resposta:

```sh
harnessup channels -missing <channel>
```

</details>

<img src="../assets/divider.svg" width="100%">

## Atualização

O painel avisa quando uma nova versão sai, em qualquer canal.

| Canal | Como atualizar |
|---|---|
| Instalador `.exe` e PowerShell | Nada a fazer. A troca acontece sozinha no próximo desligamento do daemon, nunca no meio de uma sessão. Se a pasta não for gravável, o painel avisa. |
| npm | `npm install -g harnessup@latest` |

<img src="../assets/divider.svg" width="100%">

## Desinstalação

| Canal | Como desinstalar |
|---|---|
| Instalador `.exe` | "Aplicativos e recursos" do Windows, como qualquer programa. Ele remove a conexão com o Claude Code antes de apagar os arquivos. |
| npm, PowerShell e script | `harnessup uninstall` |

```sh
harnessup uninstall
```

Remove a conexão com o Claude Code e deixa a máquina como estava.
<img src="../assets/divider.svg" width="100%">

## Solução de problemas

<details>
<summary><b>"harnessup" não é reconhecido / command not found</b></summary>

<br>

Abra um novo terminal. O PATH só vale para os terminais abertos depois da instalação. Se ainda falhar, rode `harnessup doctor` em um novo terminal e veja o que ele informa.

</details>

<details id="smartscreen-avisa-ao-abrir-o-exe">
<summary><b>O SmartScreen avisa ao abrir o .exe</b></summary>

<br>

O aviso está certo: o `.exe` ainda não tem certificado de assinatura de código, então o Windows não sabe quem o publicou. Isso não quer dizer que o arquivo é perigoso, só que o Windows não sabe quem o assinou.

As rotas [npm](#npm) e [PowerShell](#windows-powershell) não têm esse aviso. Quando o certificado existir, o aviso desaparece para o `.exe`.

</details>

<details>
<summary><b>Node antigo</b></summary>

<br>

A rota npm precisa do Node 18 ou mais recente. Confira com `node --version`. Se for mais antigo, atualize o Node ou use o [PowerShell](#windows-powershell) (Windows) ou o [script](#macos-e-linux-script) (macOS e Linux), que não precisam dele.

</details>

<details>
<summary><b>Claude Code ausente</b></summary>

<br>

Sem o Claude Code instalado, o instalador avisa e segue: o HarnessUp fica instalado, mas não conectado a ele. Instale o Claude Code e rode `harnessup install`.

</details>

<img src="../assets/divider.svg" width="100%">

## Em breve

Sem data: winget, Scoop, Chocolatey, Homebrew e Snap.

<img src="../assets/divider.svg" width="100%">

## Ajuda

- Problemas e pedidos: [Issues](https://github.com/harnessup/harnessup/issues)
- Dúvidas e discussão: [Discussions](https://github.com/harnessup/harnessup/discussions)
- E-mail: [support@harnessup.dev](mailto:support@harnessup.dev)
