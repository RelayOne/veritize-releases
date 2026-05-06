# Veritize public binary releases

Public mirror for Veritize binary releases. Hosts platform-specific archives for [`veritize-local`](https://veritize.app/local) (the offline content fact-checker) and [`veritize-desktop`](https://veritize.app/surfaces) (the system-tray GUI wrapper).

The canonical source for Veritize lives at <https://github.com/RelayOne/veritize> (private). This repo's only purpose is to host signed, downloadable binaries that anyone on the internet can install without a Veritize account.

## Install

### macOS / Linux

```sh
PLATFORM=darwin-arm64   # or: darwin-amd64, linux-amd64, linux-arm64
curl -L "https://github.com/RelayOne/veritize-releases/releases/latest/download/veritize-local-${PLATFORM}-v0.1.2.tar.gz" \
  | tar -xz
chmod +x veritize-local
./veritize-local --help
```

### Windows (PowerShell)

```powershell
Invoke-WebRequest "https://github.com/RelayOne/veritize-releases/releases/latest/download/veritize-local-windows-amd64-v0.1.2.zip" -OutFile veritize-local.zip
Expand-Archive veritize-local.zip
.\veritize-local\veritize-local.exe --help
```

### Verify checksums

```sh
curl -L https://github.com/RelayOne/veritize-releases/releases/latest/download/SHA256SUMS-archives.txt | sha256sum -c --ignore-missing
```

## Signed update channel

Every release is signed with the embedded Ed25519 public key (rotated 2026-05-04 per VZ-140d, fingerprint `be1376ce…`). Run `veritize-local update --check` to fetch the latest signed manifest from `api.veritize.app/v1/latest-version` — the binary refuses any update whose signature doesn't verify against the embedded pubkey.

## Other ways to install Veritize

- **TypeScript/JavaScript SDK:** <https://github.com/RelayOne/veritize-sdk> — `npm install github:RelayOne/veritize-sdk#v0.2.0`
- **Microsoft Word add-in:** sideload `https://addin.veritize.app/manifest.xml` (AppSource submission in progress)
- **Cloud SaaS:** <https://app.veritize.app> — sign in, paste a document, get per-claim verdicts

## License

Binaries shipped here are released under FSL-1.1-Apache-2.0. See [LICENSE](LICENSE).
