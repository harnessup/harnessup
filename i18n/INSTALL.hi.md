<p align="center">
  <a href="README.hi.md"><img src="../assets/banner/banner-hi.svg" alt="HarnessUp" width="100%"></a>
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
  <a href="INSTALL.zh-CN.md">🇨🇳 简体中文</a> ·
  <a href="INSTALL.ar.md">🇸🇦 العربية</a> ·
  <a href="INSTALL.he.md">🇮🇱 עברית</a> ·
  <b>🇮🇳 हिन्दी</b>
</p>

# इंस्टॉलेशन गाइड

HarnessUp को GitHub छोड़े बिना इंस्टॉल, जाँचने, अपडेट और अनइंस्टॉल करने के लिए जो कुछ चाहिए, वह यहाँ है। इंस्टॉलेशन हर उपयोगकर्ता के लिए होता है, बिना एडमिन और बिना सिस्टम सेवा के। इंस्टॉल से पहले binaries की SHA-256 से जाँच होती है।

## सामग्री

- [त्वरित चुनाव](#त्वरित-चुनाव)
- [npm](#npm)
- [Windows: PowerShell](#windows-powershell)
- [Windows: .exe इंस्टॉलर](#windows-exe-इंस्टॉलर)
- [macOS और Linux: स्क्रिप्ट](#macos-और-linux-स्क्रिप्ट)
- [ZIP (GitHub Releases)](#zip-github-releases)
- [पहली बार उपयोग](#पहली-बार-उपयोग)
- [अपडेट](#अपडेट)
- [अनइंस्टॉल](#अनइंस्टॉल)
- [समस्या-निवारण](#समस्या-निवारण)
- [जल्द आ रहा है](#जल्द-आ-रहा-है)
- [मदद](#मदद)

<img src="../assets/divider.svg" width="100%">

## त्वरित चुनाव

| आपकी स्थिति | सुझाया गया तरीका |
|---|---|
| आप Node 18+ इस्तेमाल करते हैं और terminal में काम करते हैं | [npm](#npm) |
| Windows, आपको एक लाइन चाहिए और Node नहीं | [PowerShell](#windows-powershell) |
| Windows, आप "अगला" दबाकर इंस्टॉल करना पसंद करते हैं | [.exe इंस्टॉलर](#windows-exe-इंस्टॉलर) |
| Windows, और आपको SmartScreen चेतावनी नहीं चाहिए | [npm](#npm) या [PowerShell](#windows-powershell) |
| macOS या Linux, बिना Node | [`install.sh` स्क्रिप्ट](#macos-और-linux-स्क्रिप्ट) (beta) |
| macOS या Linux, Node 18+ के साथ | [npm](#npm) |
| आप डाउनलोड करके hash जाँचकर unzip करना चाहते हैं | [ZIP](#zip-github-releases) |

<img src="../assets/divider.svg" width="100%">

## npm

**ज़रूरतें**

- Node 18 या नया।
- Windows x64, macOS (arm64 या x64) या Linux x64। npm केवल आपके platform का पैकेज डाउनलोड करता है।

**कमांड**

```sh
npm install -g harnessup
```

**क्या होता है**

- npm आपके सिस्टम के लिए पैकेज इंस्टॉल करता है, बाहर से और कुछ नहीं लाता।
- `harnessup` कमांड terminal में उपलब्ध हो जाती है।
- इसे अपने एजेंट से जोड़ने के लिए [पहली बार उपयोग](#पहली-बार-उपयोग) पर जाएँ।

**कैसे जाँचें**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## Windows: PowerShell

**ज़रूरतें**

- PowerShell वाला Windows x64। न Node चाहिए, न एडमिन।

**कमांड**

```powershell
irm https://harnessup.dev/install.ps1 | iex
```

Claude Code से अभी न जोड़ते हुए इंस्टॉल करने के लिए:

```powershell
& ([scriptblock]::Create((irm https://harnessup.dev/install.ps1))) -NoHooks
```

**क्या होता है**

- नवीनतम संस्करण डाउनलोड होता है और इंस्टॉल से पहले उसका SHA-256 जाँचा जाता है। hash मेल न खाए तो कुछ इंस्टॉल नहीं होता।
- आपके उपयोगकर्ता फ़ोल्डर (`%LOCALAPPDATA%\HarnessUp\`) में इंस्टॉल होता है और उसे PATH में जोड़ता है।
- `-NoHooks` इस्तेमाल न करने पर Claude Code से जुड़ता है।
- बाद में नया terminal खोलें, ताकि उसमें `harnessup` कमांड मिले।

**कैसे जाँचें**

```powershell
harnessup doctor
```

इस रास्ते पर SmartScreen चेतावनी नहीं आती।

<img src="../assets/divider.svg" width="100%">

## Windows: .exe इंस्टॉलर

**ज़रूरतें**

- Windows x64। एडमिन की ज़रूरत नहीं।

**चरण**

1. [harnessup.dev/install](https://harnessup.dev/install/) से इंस्टॉलर डाउनलोड करें।
2. फ़ाइल चलाएँ और स्क्रीन के निर्देश मानें।

**क्या होता है**

- हर उपयोगकर्ता के लिए बिना एडमिन के `%LOCALAPPDATA%\HarnessUp\` में इंस्टॉल होता है।
- Windows SmartScreen चेतावनी दिखाएगा। देखें [SmartScreen](#smartscreen-warns-when-opening-the-exe)।

**कैसे जाँचें**

नया terminal खोलें और चलाएँ:

```powershell
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## macOS और Linux: स्क्रिप्ट

> **Beta।** यह रास्ता अभी असली Mac पर परखा नहीं गया है।

**ज़रूरतें**

- macOS (arm64 या x64) या Linux x64, `curl` के साथ।

**कमांड**

```sh
curl -fsSL https://harnessup.dev/install.sh | sh
```

**वेरिएबल**

| वेरिएबल | क्या करता है |
|---|---|
| `HARNESSUP_DIR` | इंस्टॉल करने वाला फ़ोल्डर। |
| `HARNESSUP_NO_HOOKS=1` | Claude Code से जोड़े बिना इंस्टॉल करता है। |

उदाहरण:

```sh
HARNESSUP_NO_HOOKS=1 curl -fsSL https://harnessup.dev/install.sh | sh
```

**कैसे जाँचें**

```sh
harnessup doctor
```

<img src="../assets/divider.svg" width="100%">

## ZIP (GitHub Releases)

**ज़रूरतें**

- Windows x64, macOS (arm64 या x64) या Linux x64। न Node चाहिए, न एडमिन।

**चरण**

1. अपने सिस्टम का zip [Releases](https://github.com/harnessup/harnessup/releases/latest) से `SHA256SUMS.txt` के साथ डाउनलोड करें।

   | सिस्टम | फ़ाइल |
   |---|---|
   | Windows x64 | `harnessup-1.0.2-windows-amd64.zip` |
   | macOS arm64 | `harnessup-1.0.2-darwin-arm64.zip` |
   | macOS x64 | `harnessup-1.0.2-darwin-amd64.zip` |
   | Linux x64 | `harnessup-1.0.2-linux-amd64.zip` |

2. SHA-256 जाँचें और उसकी तुलना `SHA256SUMS.txt` की उस फ़ाइल वाली लाइन से करें। मेल न खाए तो उसे इस्तेमाल न करें: मिटाकर फिर से डाउनलोड करें।

   ```powershell
   Get-FileHash -Algorithm SHA256 <फ़ाइल>
   ```

   ```sh
   shasum -a 256 <फ़ाइल>
   ```

3. अपने एक फ़ोल्डर में unzip करें, बिना एडमिन के: Windows पर जैसे `C:\Users\<आप>\HarnessUp`; macOS और Linux पर `~/.local/share/HarnessUp`।
4. macOS और Linux पर, ज़रूरत हो तो: `chmod +x harnessup harnessupd harnessup-hook`।
5. फ़ोल्डर को PATH में रखें या programs को उनके path से बुलाएँ।
6. `harnessup install` और फिर `harnessup doctor` चलाएँ।

**zip में क्या है**

- Windows: `harnessup.exe`, `harnessupd.exe`, `harnessup-hook.exe` और `harnessup-panel.exe`।
- macOS और Linux: `harnessup`, `harnessupd` और `harnessup-hook`।

Windows पर SmartScreen चेतावनी आ सकती है। देखें [SmartScreen](#smartscreen-warns-when-opening-the-exe)।

**अपडेट:** नया zip डाउनलोड करें। फ़ोल्डर लिखने योग्य हो तो daemon भी खुद को अपडेट करता है।

**अनइंस्टॉल:** `harnessup uninstall` और फिर फ़ोल्डर मिटाएँ।

<img src="../assets/divider.svg" width="100%">

## पहली बार उपयोग

किसी भी रास्ते से इंस्टॉल करने के बाद एक बार चलाएँ:

```sh
harnessup install
```

यह HarnessUp को Claude Code से जोड़ता है और बताता है कि उसने क्या-क्या छुआ। इनमें से कुछ भी आपकी मशीन से बाहर नहीं जाता।

> कनेक्शन के लिए Claude Code इंस्टॉल होना चाहिए। उसके बिना इंस्टॉलर चेतावनी देता है और आगे बढ़ जाता है।

फिर daemon शुरू करें:

```sh
harnessupd
```

जाँचें:

```sh
harnessup doctor
```

`doctor` बताता है कि कनेक्शन सच में इंस्टॉल है या नहीं, कौन-से events असल में पहुँचे, और इस मशीन पर product किन channels से आपसे बात कर सकता है।

<details>
<summary><b><code>doctor</code> ने <code>[communication channels]</code> के नीचे "not tested" कहा</b></summary>

<br>

Claude Code खोलें और कोई भी संदेश भेजें। एक कोड दिखेगा। लिखें:

```sh
harnessup channels <code>
```

अगर कोड **नहीं** दिखता, तो वह भी एक जवाब है:

```sh
harnessup channels -missing <channel>
```

</details>

<img src="../assets/divider.svg" width="100%">

## अपडेट

जब कोई नया संस्करण आता है, डैशबोर्ड हर channel पर बताता है।

| Channel | कैसे अपडेट करें |
|---|---|
| `.exe` इंस्टॉलर और PowerShell | कुछ करने की ज़रूरत नहीं। बदलाव daemon के अगले shutdown पर अपने-आप होता है, कभी session के बीच में नहीं। अगर फ़ोल्डर लिखने योग्य नहीं है, तो डैशबोर्ड यह बताता है। |
| npm | `npm install -g harnessup@latest` |

<img src="../assets/divider.svg" width="100%">

## अनइंस्टॉल

| Channel | कैसे अनइंस्टॉल करें |
|---|---|
| `.exe` इंस्टॉलर | Windows "Apps and features", किसी भी प्रोग्राम की तरह। फ़ाइलें मिटाने से पहले यह Claude Code कनेक्शन हटा देता है। |
| npm, PowerShell और स्क्रिप्ट | `harnessup uninstall` |

```sh
harnessup uninstall
```

Claude Code कनेक्शन हटाता है और मशीन को वैसा ही छोड़ता है जैसी वह थी।
<img src="../assets/divider.svg" width="100%">

## समस्या-निवारण

<details>
<summary><b>"harnessup" पहचाना नहीं गया / command not found</b></summary>

<br>

नया terminal खोलें। PATH केवल इंस्टॉलेशन के बाद खुले terminals पर लागू होता है। फिर भी विफल हो, तो नए terminal से `harnessup doctor` चलाएँ और देखें कि वह क्या बताता है।

</details>

<details id="smartscreen-warns-when-opening-the-exe">
<summary><b>.exe खोलते समय SmartScreen चेतावनी देता है</b></summary>

<br>

चेतावनी सही है: `.exe` के पास अभी code-signing certificate नहीं है, इसलिए Windows को नहीं पता कि इसे किसने प्रकाशित किया। इसका मतलब यह नहीं कि फ़ाइल खतरनाक है, बस इतना कि Windows उसे नहीं जानता।

[npm](#npm) और [PowerShell](#windows-powershell) रास्तों पर ऐसी चेतावनी नहीं है। certificate आने के बाद `.exe` के लिए भी चेतावनी चली जाएगी।

</details>

<details>
<summary><b>पुराना Node</b></summary>

<br>

npm रास्ते को Node 18 या नया चाहिए। `node --version` से जाँचें। पुराना हो तो Node अपडेट करें, या [PowerShell](#windows-powershell) (Windows) या [स्क्रिप्ट](#macos-और-linux-स्क्रिप्ट) (macOS और Linux) इस्तेमाल करें, जिन्हें इसकी ज़रूरत नहीं।

</details>

<details>
<summary><b>Claude Code नहीं है</b></summary>

<br>

Claude Code इंस्टॉल न हो तो इंस्टॉलर चेतावनी देता है और आगे बढ़ जाता है: HarnessUp इंस्टॉल तो हो जाता है, पर उससे जुड़ा नहीं होता। Claude Code इंस्टॉल करें और `harnessup install` चलाएँ।

</details>

<img src="../assets/divider.svg" width="100%">

## जल्द आ रहा है

कोई तारीख नहीं: winget, Scoop, Chocolatey, Homebrew और Snap।

<img src="../assets/divider.svg" width="100%">

## मदद

- समस्याएँ और अनुरोध: [Issues](https://github.com/harnessup/harnessup/issues)
- सवाल और चर्चा: [Discussions](https://github.com/harnessup/harnessup/discussions)
- ईमेल: [support@harnessup.dev](mailto:support@harnessup.dev)
