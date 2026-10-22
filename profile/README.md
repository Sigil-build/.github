<p align="center">
  <a href="https://docs.sigil.build">
    <img src="https://raw.githubusercontent.com/Sigil-build/.github/main/profile/banner.svg?v=3" alt="Sigil.build — Native AOT desktop tools for Windows and Linux: Sigil and Dictum" width="100%">
  </a>
</p>

<p align="center">
  <a href="https://docs.sigil.build"><img src="https://img.shields.io/badge/docs-docs.sigil.build-c9b98a?labelColor=101322" alt="Documentation: docs.sigil.build"></a>
  <img src="https://img.shields.io/badge/.NET-10%20%C2%B7%20Native%20AOT-c9b98a?labelColor=101322" alt=".NET 10, Native AOT">
  <img src="https://img.shields.io/badge/made%20in-Ukraine-c9b98a?labelColor=101322" alt="Made in Ukraine">
</p>

**Sigil.build** makes desktop tools for Windows and Linux. Each one is a single native binary built with .NET 10 Native AOT and Avalonia: it starts at once and needs no runtime. One site documents them all: [docs.sigil.build](https://docs.sigil.build).

## Dictum: voice to text

[![Latest release](https://img.shields.io/github/v/release/Sigil-build/dictum?label=release&color=c9b98a&labelColor=101322)](https://github.com/Sigil-build/dictum/releases/latest)
[![CI](https://github.com/Sigil-build/dictum/actions/workflows/ci.yml/badge.svg)](https://github.com/Sigil-build/dictum/actions/workflows/ci.yml)
[![MIT license](https://img.shields.io/badge/license-MIT-c9b98a?labelColor=101322)](https://github.com/Sigil-build/dictum/blob/main/LICENSE)

Hold a hotkey, speak, and the text appears where you are typing, in any app.

- **Speech recognition runs on your computer** with Whisper, on the GPU through Vulkan when it can. Nothing leaves your machine unless you connect a server yourself.
- **Several languages.** The main language has priority, so your words are not translated by mistake.
- **Your own LLM clean-up.** Optionally, a server you run fixes punctuation and slips.
- **Your setup:** profiles with their own hotkeys, your words, and replace rules.
- **Two programs:** a tray app with a setup wizard, and a command line with `dictum doctor`.

Windows 11 and Linux (x86-64) · open source under the MIT License.

📥 [Download](https://github.com/Sigil-build/dictum/releases/latest) · 📖 [Documentation](https://docs.sigil.build/dictum/) · 🇺🇦 [Українською](https://docs.sigil.build/uk/dictum/) · 🔒 [Privacy](https://docs.sigil.build/dictum/privacy/) · 💻 [Source](https://github.com/Sigil-build/dictum)

## Sigil: ship Windows software from one `sigil.yaml`

[![CI](https://github.com/Sigil-build/sigil/actions/workflows/ci.yml/badge.svg?branch=release%2Fv0.1.0-alpha)](https://github.com/Sigil-build/sigil/actions/workflows/ci.yml)
[![License: Sigil License 1.0](https://img.shields.io/badge/license-Sigil%201.0-c9b98a?labelColor=101322)](https://github.com/Sigil-build/sigil/blob/release/v0.1.0-alpha/LICENSE)
![Status: pre-MVP](https://img.shields.io/badge/status-pre--MVP-a8865a?labelColor=101322)

Sigil packs a desktop app into a branded, self-elevating `Setup.exe`, an MSIX or a ZIP. It signs the result and ships signed updates. All of it comes from one declarative `sigil.yaml` you can review in a pull request, run by a single Native AOT CLI.

| Stage | What it does | Today |
|---|---|---|
| **pack** | `sigil.yaml` → `Setup.exe` wizard, MSIX, or ZIP | ✅ |
| **sign** | Authenticode via `signtool` or Azure Trusted Signing, with an audit log | ✅ |
| **publish** | Hosting and release-channel distribution | 🚧 not built |
| **update** | Signed channel manifests; `/Update` fetches the full new package | ✅ · delta patches deferred |

> **Status: pre-MVP, Windows-first.** Build from source; every `0.x` release may change the manifest schema or the CLI. The code is source-available under the [Sigil License 1.0](https://github.com/Sigil-build/sigil/blob/release/v0.1.0-alpha/LICENSE), not open source; [ADR-016](https://docs.sigil.build/sigil/architecture/adr-016-licensing/) explains why.

📖 [Documentation](https://docs.sigil.build/sigil/) · 🚀 [Getting started](https://docs.sigil.build/sigil/getting-started/) · 📋 [Manifest](https://docs.sigil.build/sigil/manifest-reference/) · ⌨️ [CLI](https://docs.sigil.build/sigil/cli-reference/) · 🩺 [Diagnostics](https://docs.sigil.build/sigil/diagnostics/) · 💻 [Source](https://github.com/Sigil-build/sigil)

## Security

Report a vulnerability privately through each repository's Security tab: [Dictum](https://github.com/Sigil-build/dictum/security/policy) · [Sigil](https://github.com/Sigil-build/sigil/security/policy). How to verify a download is described in each project's documentation.

<p align="center">
  <sub>Made in Ukraine 🇺🇦 · <a href="https://docs.sigil.build">docs.sigil.build</a></sub>
</p>
