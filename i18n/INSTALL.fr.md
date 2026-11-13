<p align="center">
  <a href="README.fr.md"><img src="../assets/banner/banner-fr.svg" alt="HarnessUp" width="100%"></a>
</p>

<p align="center">
  <a href="../INSTALL.md">🇺🇸 English</a> ·
  <a href="INSTALL.pt-BR.md">🇧🇷 Português</a> ·
  <a href="INSTALL.es.md">🇪🇸 Español</a> ·
  <b>🇫🇷 Français</b> ·
  <a href="INSTALL.de.md">🇩🇪 Deutsch</a> ·
  <a href="INSTALL.it.md">🇮🇹 Italiano</a> ·
  <a href="INSTALL.ja.md">🇯🇵 日本語</a> ·
  <a href="INSTALL.ko.md">🇰🇷 한국어</a> ·
  <a href="INSTALL.zh-CN.md">🇨🇳 简体中文</a> ·
  <a href="INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="INSTALL.he.md">🇮🇱 עברית</a> ·
  <a href="INSTALL.hi.md">🇮🇳 हिन्दी</a>
</p>

# Guide d'installation

Tout ce qu'il faut pour installer, vérifier, mettre à jour et désinstaller HarnessUp sans quitter GitHub. L'installation se fait par utilisateur, sans administrateur et sans service système. Les binaires sont vérifiés avec SHA-256 avant l'installation.

## Sommaire

- [Choix rapide](#choix-rapide)
- [npm](#npm)
- [Windows : PowerShell](#windows--powershell)
- [Windows : installateur .exe](#windows--installateur-exe)
- [macOS et Linux : script](#macos-et-linux--script)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [Première utilisation](#première-utilisation)
- [Mise à jour](#mise-à-jour)
- [Désinstallation](#désinstallation)
- [Dépannage](#dépannage)
- [Bientôt disponible](#bientôt-disponible)
- [Aide](#aide)

<img src="../assets/divider.svg" width="100%">

## Choix rapide

| Votre situation | Canal recommandé |
|---|---|
| Vous utilisez Node 18+ et vivez dans le terminal | [npm](#npm) |
| Windows, vous voulez une seule ligne et pas de Node | [PowerShell](#windows--powershell) |
| Windows, vous préférez cliquer sur « suivant » | [installateur .exe](#windows--installateur-exe) |
| Windows, et vous ne voulez aucun avertissement SmartScreen | [npm](#npm) ou [PowerShell](#windows--powershell) |
| macOS ou Linux, sans Node | [script `install.sh`](#macos-et-linux--script) (bêta) |
| macOS ou Linux, avec Node 18+ | [npm](#npm) |
| Vous préférez télécharger, vérifier le hash puis décompresser | [ZIP](#zip-github-releases) |

<img src="../assets/divider.svg" width="100%">

## npm

**Prérequis**

- Node 18 ou plus récent.
- Windows x64, macOS (arm64 ou x64) ou Linux x64. npm ne télécharge que le paquet de votre plateforme.

**Commande**

```sh
npm install -g harnessup
```

**Ce qui se passe**

- npm installe le paquet pour votre système, sans rien récupérer d'autre à l'extérieur.
- La commande `harnessup` devient disponible dans le terminal.
- Pour la connecter à votre agent, passez à [Première utilisation](#première-utilisation).

**Comment vérifier**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## Windows : PowerShell

**Prérequis**

- Windows x64 avec PowerShell. Ni Node ni administrateur ne sont nécessaires.

**Commande**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

Pour installer sans se connecter à Claude Code tout de suite :

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**Ce qui se passe**

- Télécharge la dernière version et vérifie son SHA-256 avant l'installation. Si le hash ne correspond pas, rien n'est installé.
- Installe dans votre dossier utilisateur (`%LOCALAPPDATA%\HarnessUp\`) et l'ajoute à votre PATH.
- Se connecte à Claude Code, sauf si vous utilisez `-NoHooks`.
- Ouvrez ensuite un nouveau terminal, pour que la commande `harnessup` y soit disponible.

**Comment vérifier**

```powershell
harnessup doctor
```

Ce canal n'affiche pas d'avertissement SmartScreen.

<img src="../assets/divider.svg" width="100%">

## Windows : installateur .exe

**Prérequis**

- Windows x64. Aucun administrateur nécessaire.

**Étapes**

1. Téléchargez l'installateur sur [harnessup.dev/install](https://harnessup.dev/install/).
2. Lancez le fichier et suivez les écrans.

**Ce qui se passe**

- Installe par utilisateur, sans administrateur, dans `%LOCALAPPDATA%\HarnessUp\`.
- Windows affichera un avertissement SmartScreen. Voir [SmartScreen](#smartscreen-warns-when-opening-the-exe).

**Comment vérifier**

Ouvrez un nouveau terminal et exécutez :

```powershell
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## macOS et Linux : script

> **Bêta.** Ce canal n'a pas encore été testé sur un vrai Mac.

**Prérequis**

- macOS (arm64 ou x64) ou Linux x64, avec `curl`.

**Commande**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**Variables**

| Variable | Ce qu'elle fait |
|---|---|
| `HARNESSUP_DIR` | Dossier dans lequel installer. |
| `HARNESSUP_NO_HOOKS=1` | Installe sans se connecter à Claude Code. |

Exemple :

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**Comment vérifier**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**Prérequis**

- Windows x64, macOS (arm64 ou x64) ou Linux x64. Ni Node ni administrateur nécessaires.

**Étapes**

1. Téléchargez le zip de votre système depuis [Releases](https://github.com/harnessup/harnessup/releases/latest), avec `SHA256SUMS.txt`.

   | Système | Fichier |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. Vérifiez le SHA-256 et comparez-le avec la ligne du fichier dans `SHA256SUMS.txt`. S'il ne correspond pas, n'utilisez pas le fichier : supprimez-le et téléchargez-le à nouveau.

   ```powershell
   Get-FileHash -Algorithm SHA256 <fichier>
   ```

   ```sh
   shasum -a 256 <fichier>
   ```

3. Décompressez dans un dossier à vous, sans administrateur : sous Windows, quelque chose comme `C:\Users\<vous>\HarnessUp` ; sous macOS et Linux, `~/.local/share/HarnessUp`.
4. Sous macOS et Linux, si besoin : `chmod +x harnessup harnessupd harnessup-hook`.
5. Ajoutez le dossier à votre PATH ou appelez les programmes par leur chemin.
6. Exécutez `harnessup install`, puis `harnessup doctor`.

**Contenu du zip**

- Windows : `harnessup.exe`, `harnessupd.exe`, `harnessup-hook.exe` et `harnessup-panel.exe`.
- macOS et Linux : `harnessup`, `harnessupd` et `harnessup-hook`.

Sous Windows, l'avertissement SmartScreen peut apparaître. Voir [SmartScreen](#smartscreen-warns-when-opening-the-exe).

**Mise à jour :** téléchargez le nouveau zip. Le daemon se met aussi à jour tout seul si le dossier est accessible en écriture.

**Désinstallation :** `harnessup uninstall`, puis supprimez le dossier.

<img src="../assets/divider.svg" width="100%">

## Première utilisation

Après l'installation par n'importe quel canal, exécutez une fois :

```sh
harnessup install
```

Cela connecte HarnessUp à Claude Code et vous indique tout ce qu'il a touché. Rien de cela ne quitte votre machine.

> Claude Code doit être installé pour la connexion. Sans lui, l'installateur affiche un avertissement et poursuit.

Démarrez ensuite le daemon :

```sh
harnessupd
```

Vérifiez :

```sh
harnessup doctor
```

`doctor` indique si la connexion est vraiment installée, quels événements sont effectivement arrivés, et par quels canaux le produit peut vous parler sur cette machine.

<details>
<summary><b><code>doctor</code> a indiqué « not tested » sous <code>[communication channels]</code></b></summary>

<br>

Ouvrez Claude Code et envoyez un message quelconque. Un code apparaîtra. Tapez :

```sh
harnessup channels <code>
```

Si le code n'apparaît **pas**, c'est aussi une réponse :

```sh
harnessup channels -missing <canal>
```

</details>

<img src="../assets/divider.svg" width="100%">

## Mise à jour

Le tableau de bord vous indique quand une nouvelle version est disponible, sur n'importe quel canal.

| Canal | Comment mettre à jour |
|---|---|
| Installateur `.exe` et PowerShell | Rien à faire. Le remplacement se fait tout seul à l'arrêt suivant du daemon, jamais au milieu d'une session. Si le dossier n'est pas accessible en écriture, le tableau de bord le signale. |
| npm | `npm install -g harnessup@latest` |

<img src="../assets/divider.svg" width="100%">

## Désinstallation

| Canal | Comment désinstaller |
|---|---|
| Installateur `.exe` | « Applications et fonctionnalités » de Windows, comme pour tout programme. Il supprime la connexion à Claude Code avant d'effacer les fichiers. |
| npm, PowerShell et script | `harnessup uninstall` |

```sh
harnessup uninstall
```

Supprime la connexion à Claude Code et laisse la machine comme elle était.
<img src="../assets/divider.svg" width="100%">

## Dépannage

<details>
<summary><b>« harnessup » n'est pas reconnu / command not found</b></summary>

<br>

Ouvrez un nouveau terminal. Le PATH ne s'applique qu'aux terminaux ouverts après l'installation. Si cela échoue encore, exécutez `harnessup doctor` depuis un nouveau terminal et regardez ce qu'il signale.

</details>

<details id="smartscreen-warns-when-opening-the-exe">
<summary><b>SmartScreen avertit à l'ouverture du .exe</b></summary>

<br>

L'avertissement est exact : le `.exe` n'a pas encore de certificat de signature de code, donc Windows ne sait pas qui l'a publié. Cela ne signifie pas que le fichier est dangereux, seulement que Windows ne le connaît pas.

Les voies [npm](#npm) et [PowerShell](#windows--powershell) n'ont pas cet avertissement. Une fois le certificat en place, l'avertissement disparaîtra pour le `.exe`.

</details>

<details>
<summary><b>Node trop ancien</b></summary>

<br>

La voie npm nécessite Node 18 ou plus récent. Vérifiez avec `node --version`. S'il est plus ancien, mettez Node à jour ou utilisez [PowerShell](#windows--powershell) (Windows) ou le [script](#macos-et-linux--script) (macOS et Linux), qui n'en ont pas besoin.

</details>

<details>
<summary><b>Claude Code absent</b></summary>

<br>

Sans Claude Code installé, l'installateur affiche un avertissement et poursuit : HarnessUp est installé mais pas connecté à lui. Installez Claude Code et exécutez `harnessup install`.

</details>

<img src="../assets/divider.svg" width="100%">

## Bientôt disponible

Sans date : winget, Scoop, Chocolatey, Homebrew et Snap.

<img src="../assets/divider.svg" width="100%">

## Aide

- Problèmes et demandes : [Issues](https://github.com/harnessup/harnessup/issues)
- Questions et discussions : [Discussions](https://github.com/harnessup/harnessup/discussions)
- E-mail : [support@harnessup.dev](mailto:support@harnessup.dev)
