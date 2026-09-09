<p align="center">
  <a href="https://github.com/Sigil-build/sigil">
    <img src="https://raw.githubusercontent.com/Sigil-build/.github/main/profile/banner.svg?v=2" alt="Sigil — pack, sign, publish, update from one sigil.yaml" width="100%">
  </a>
</p>

<p align="center">
  <a href="https://github.com/Sigil-build/sigil/actions/workflows/ci.yml"><img src="https://github.com/Sigil-build/sigil/actions/workflows/ci.yml/badge.svg" alt="CI"></a>
  <a href="https://github.com/Sigil-build/sigil/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-c9b98a?labelColor=101322" alt="MIT license"></a>
  <img src="https://img.shields.io/badge/.NET-10%20%C2%B7%20Native%20AOT-c9b98a?labelColor=101322" alt=".NET 10, Native AOT">
  <img src="https://img.shields.io/badge/status-pre--MVP-a8865a?labelColor=101322" alt="Status: pre-MVP">
  <a href="https://sigil.build"><img src="https://img.shields.io/badge/web-sigil.build-c9b98a?labelColor=101322" alt="sigil.build"></a>
</p>

**Sigil** is an open-source CLI that replaces NSIS, Inno Setup, and WiX with one
declarative `sigil.yaml`. It packs your Windows app into a branded, self-elevating
`Setup.exe` (or MSIX / ZIP), signs it with a local certificate or Azure Trusted
Signing, and ships a signed full-package update engine — all from a single
Native AOT binary with no runtime to install.

> **Status: pre-MVP, Windows-first.** No published binaries yet; build from
> source. The `publish` stage is not built, and delta updates are deferred.
> Every `0.x` release may break the manifest schema or CLI flags.

## The pipeline

| Stage | What it does | Today |
|---|---|---|
| **pack** | `sigil.yaml` → `Setup.exe` wizard, MSIX, or ZIP | ✅ shipping |
| **sign** | Authenticode via `signtool` or Azure Trusted Signing, with an audit log | ✅ shipping |
| **publish** | Hosting + release-channel distribution | 🚧 not built |
| **update** | Signed channel manifests, `/Update` fetches the full new package | ✅ shipping · delta patches deferred |

## What a manifest looks like

```yaml
spec: v1.0

app:
  id: com.example.HelloSigil
  name: HelloSigil
  version: 1.0.0
  publisher: Example, Inc.

build:
  source: ./payload

package:
  formats: [exe]
  architectures: [x64]

install_steps:
  - id: copy-app
    type: file_copy
    from: payload/**
    to: "{install_dir}"
  - id: start-menu
    type: shortcut_create
    target: "{install_dir}\app.exe"
    location: start_menu
    name: HelloSigil
```

```bash
sigil init                      # scaffold a sigil.yaml (prompts, or pass flags)
sigil validate                  # JSON-schema + typed diagnostics (SIG0xxx)
sigil pack                      # → dist/HelloSigil-1.0.0-x64-Setup.exe
sigil sign                      # always last: stamping invalidates a signature
```

Every install step is journaled, so a failed or cancelled install rolls back
files, registry writes, shortcuts, services, and COM registrations in reverse.
The wizard is themed from two manifest colours, supports install-time
parameters and `when:` conditions, and produces an `uninstall.exe` plus an
Add/Remove Programs entry for free. Silent mode is one flag: `/S`.

## Start here

- 📦 [**sigil**](https://github.com/Sigil-build/sigil) — the CLI, install engine, and installer host
- 🚀 [Getting started](https://github.com/Sigil-build/sigil/blob/main/docs/getting-started.md) — `init` → `validate` → `pack` in five minutes
- 📖 [Manifest reference](https://github.com/Sigil-build/sigil/blob/main/docs/manifest-reference.md) · [CLI reference](https://github.com/Sigil-build/sigil/blob/main/docs/cli-reference.md) · [setup.exe flags](https://github.com/Sigil-build/sigil/blob/main/docs/setup-exe-reference.md)
- 🧩 [Install steps](https://github.com/Sigil-build/sigil/blob/main/docs/guides/install-steps.md) · [Installer wizard](https://github.com/Sigil-build/sigil/blob/main/docs/guides/installer-wizard.md) · [Signing](https://github.com/Sigil-build/sigil/blob/main/docs/guides/signing.md) · [Updates](https://github.com/Sigil-build/sigil/blob/main/docs/guides/updates.md)
- 🗺️ [Changelog and known limitations](https://github.com/Sigil-build/sigil/blob/main/CHANGELOG.md) · [Architecture decisions](https://github.com/Sigil-build/sigil/tree/main/docs/architecture)
- 🤝 [Contributing](https://github.com/Sigil-build/sigil/blob/main/CONTRIBUTING.md) · [Security policy](https://github.com/Sigil-build/sigil/blob/main/SECURITY.md) · [Issues](https://github.com/Sigil-build/sigil/issues)

## Why another installer tool?

Desktop installer tooling makes you choose between expensive GUI suites and
free-but-painful XML or Pascal scripting. Sigil sits in the middle: a
readable manifest you can review in a pull request, headless cloud signing
that fits CI, and an update path that verifies signatures before it runs
anything.

<p align="center">
  <sub>MIT licensed · built with .NET 10 and Avalonia · made in Ukraine 🇺🇦</sub>
</p>
