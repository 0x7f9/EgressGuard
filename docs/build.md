# Build from source

### Requirements

- Windows 10 or 11
- Current stable Rust (edition 2024). See [rustup](https://rustup.rs/)
- Visual Studio Build Tools with **Desktop development with C++**
- WebView2 Runtime

### Build release binaries

```powershell
cargo build --release -p egressguard-service -p egressguard-ui
```

Outputs:

- target\release\EgressGuardService.exe
- target\release\EgressGuard.exe

To setup, see [docs/setup.md](docs/setup.md).

