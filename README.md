<div align="center">

<img src="https://img.shields.io/badge/version-2.0.0-e8a020?style=for-the-badge" alt="version"/>
<img src="https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="python"/>
<img src="https://img.shields.io/badge/License-MIT-00c9a0?style=for-the-badge" alt="license"/>
<img src="https://img.shields.io/badge/Tests-Passing-00c9a0?style=for-the-badge" alt="tests"/>

<br/><br/>

# 🌿 SecretScript — Jungle Language Converter

### A personal cipher workspace — encode and decode messages using a customizable secret language.
### Inspired by secondary school secret notes. Built into a professional tool.

<br/>

[🚀 Live Demo](#-web-app) · [📦 Installation](#-installation) · [📖 How It Works](#-how-it-works) · [🖥️ CLI Usage](#️-cli-usage) · [🗺️ Roadmap](#️-roadmap)

</div>

---

## 📖 Background

Back in secondary school, passing secret notes meant writing in a made-up cipher that nobody else could quickly read. This project formalises that exact system into a fully-featured Python library, CLI tool, and browser-based web app.

The cipher is deliberately simple — which is what makes it fun:

| Character | Rule | Example |
|-----------|------|---------|
| Vowel (a, e, i, o, u) | Replaced by its number → `a=1 e=2 i=3 o=4 u=5` | `a → 1` |
| Consonant | Kept (lowercased) + suffix appended | `f → fa` |
| Space / punctuation | Passed through unchanged | `! → !` |

```
"finance"    →   fa3na1naca2
"dictionary" →   da3cata34na1raya
"hello"      →   h2lala4
```

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔒 **Encode** | Convert any plain text into Jungle Language |
| 🔓 **Decode** | Reverse any encoded string back to plain text |
| 🎨 **Custom Ciphers** | Design your own vowel mappings and consonant suffixes |
| 🔗 **Shareable Links** | Share your cipher via a single URL — no sign-up needed |
| 🖥️ **CLI Tool** | Full command-line interface with file I/O and stdin support |
| 🌐 **Web App** | Real-time browser interface, works completely offline |
| 💾 **Message History** | Last 8 encoded messages saved locally in browser |
| 📊 **Cipher Strength Meter** | Visual indicator showing how hard your cipher is to crack |
| 🎭 **4 Built-in Presets** | Jungle Classic, Hex Code, Ghost Script, Shadow Lang |
| ✅ **Full Test Suite** | pytest coverage including round-trip verification |
| 🤖 **GitHub Actions CI** | Tests auto-run on every push |

---

## 🎭 Cipher Presets

### 🌿 Jungle Classic *(the original)*
`a=1, e=2, i=3, o=4, u=5` · consonant suffix: `a`
```
finance → fa3na1naca2
```

### 💻 Hex Code
`a=A1, e=E2, i=I3, o=O4, u=U5` · consonant suffix: `x`
```
finance → fxI3nxA1nxcxA1E2
```

### 👻 Ghost Script
`a=@, e=#, i=!, o=*, u=~` · consonant suffix: `o`
```
finance → fo!no@nococ@#
```

### 🕵️ Shadow Lang *(reversed numbers)*
`a=5, e=4, i=3, o=2, u=1` · consonant suffix: `z`
```
finance → fz3nz5nzcz54
```

---

## 🌐 Web App

The `app/index.html` file is a **fully self-contained** browser app — no server, no build step, no dependencies. Just open it.

**Includes:**
- Real-time encode/decode as you type (no button needed)
- Cipher designer with live strength meter
- 4 preset ciphers + fully custom builder
- Generate and share your cipher as a single URL
- Message history saved to browser storage
- Works completely offline

```bash
# Option 1 — open directly
open app/index.html

# Option 2 — serve locally
python -m http.server 8000
# then visit http://localhost:8000/app/
```

---

## 📦 Installation

**Requirements:** Python 3.11 or higher

```bash
# 1. Clone the repo
git clone https://github.com/your-username/jungle-language-converter.git
cd jungle-language-converter

# 2. Install — registers the `jungle` command globally
pip install -e .
```

---

## 🖥️ CLI Usage

### Encode text
```bash
jungle encode "hello world"
#  Encoded →  h2lala4 waw4rarala da

jungle encode "finance"
#  Encoded →  fa3na1naca2
```

### Decode text
```bash
jungle decode "fa3na1naca2"
#  Decoded →  finance
```

### Encode or decode a file
```bash
jungle encode -f message.txt -o secret.txt
jungle decode -f secret.txt -o plain.txt
```

### Quiet mode *(output only — great for piping and scripting)*
```bash
jungle encode -q "hello"
# h2lala4

cat notes.txt | jungle decode -q
```

### Interactive REPL
```bash
jungle
# launches the interactive session
```

```
🌿  SecretScript  —  Interactive Mode

  Commands:  encode <text>  |  decode <text>  |  auto <text>

  jungle> encode finance
  ──────────────────────────────────────
  Encoded →  fa3na1naca2
  ──────────────────────────────────────

  jungle> decode fa3na1naca2
  ──────────────────────────────────────
  Decoded →  finance
  ──────────────────────────────────────

  jungle> exit
  Goodbye! 🌿
```

---

## 📦 Library Usage

```python
from jungle_converter import encode, decode, encode_sentence, decode_sentence

# Single words
encode("finance")       # → 'fa3na1naca2'
decode("fa3na1naca2")   # → 'finance'

# Full sentences (preserves spaces)
encode_sentence("hello world")              # → 'h2lala4 waw4rarala da'
decode_sentence("h2lala4 waw4rarala da")    # → 'hello world'

# Auto-detect whether text is already encoded
from jungle_converter import is_encoded
is_encoded("fa3na1naca2")   # → True
is_encoded("hello world")   # → False
```

---

## 🔢 Cipher Reference

### Vowel Map (Jungle Classic)

| Vowel | Code |
|-------|------|
| A / a | `1` |
| E / e | `2` |
| I / i | `3` |
| O / o | `4` |
| U / u | `5` |

### Consonant Rule

Every consonant is lowercased and has `"a"` appended after it:

```
b→ba  c→ca  d→da  f→fa  g→ga  h→ha  j→ja  k→ka  l→la
m→ma  n→na  p→pa  q→qa  r→ra  s→sa  t→ta  v→va  w→wa
x→xa  y→ya  z→za
```

---

## 📁 Project Structure

```
jungle-language-converter/
│
├── jungle_converter/           # Python package
│   ├── __init__.py             # Public API
│   ├── converter.py            # Core encode / decode logic
│   └── cli.py                  # CLI tool (REPL, flags, file I/O)
│
├── app/
│   └── index.html              # Self-contained web app
│
├── tests/
│   └── test_converter.py       # Full pytest suite (14 tests)
│
├── .github/
│   └── workflows/
│       └── tests.yml           # GitHub Actions CI pipeline
│
├── main.py                     # Direct run entry point
├── pyproject.toml              # Modern Python packaging config
├── LICENSE                     # MIT License
└── README.md                   # You are here
```

---

## ✅ Running the Tests

```bash
pip install pytest
pytest tests/ -v
```

Expected output:

```
tests/test_converter.py::TestEncode::test_encode_all_vowels_lowercase    PASSED
tests/test_converter.py::TestEncode::test_encode_simple_word             PASSED
tests/test_converter.py::TestEncode::test_encode_uppercase               PASSED
tests/test_converter.py::TestDecode::test_decode_simple_word             PASSED
tests/test_converter.py::TestRoundTrip::test_round_trip_words[finance]   PASSED
tests/test_converter.py::TestRoundTrip::test_round_trip_words[python]    PASSED
tests/test_converter.py::TestSentenceHelpers::test_encode_sentence       PASSED
tests/test_converter.py::TestIsEncoded::test_plain_text_returns_false    PASSED
...

14 passed in 0.12s
```

---

## 🗺️ Roadmap

- [x] Core encode / decode engine
- [x] Bug fix — uppercase vowels handled correctly
- [x] Full CLI with file I/O, stdin, quiet mode, interactive REPL
- [x] Browser-based web app (real-time, works offline)
- [x] Custom cipher designer with live preview
- [x] Shareable cipher URLs (no account needed)
- [x] 4 built-in presets (Jungle, Hex, Ghost, Shadow)
- [x] Cipher strength meter
- [x] Message history
- [x] GitHub Actions CI pipeline
- [ ] Flask / FastAPI REST API
- [ ] Export encoded message as a downloadable image
- [ ] Mobile-friendly PWA version
- [ ] Emoji-based cipher preset

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

```bash
# 1. Fork the repo
# 2. Create your feature branch
git checkout -b feature/your-feature

# 3. Make your changes, then commit
git commit -m "Add your feature"

# 4. Push and open a Pull Request
git push origin feature/your-feature
```

---

## 📄 License

Distributed under the **MIT License** — see [LICENSE](LICENSE) for details.

---

<div align="center">

Made with ❤️ — inspired by secondary school secret messages 🌿

**[⬆ Back to top](#)**

</div>
