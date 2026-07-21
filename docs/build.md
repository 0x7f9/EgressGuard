# Build and manual installation

This document shows how to build from source and install with the CLI or UI.

### Requirements

- Windows 10 or 11
- Admin rights for service install, WFP, and Protection toggles
- Rust installed see [rustup](https://rustup.rs/) 
- Visual Studio Build Tools with **Desktop development with C++**

Optional: put `geoip-country.mmdb` in `%ProgramData%\EgressGuard\database\` for country codes.

### Build release binaries

```powershell
cargo build --release -p egressguard-service -p egressguard-ui
```

Outputs:

- `target\release\EgressGuardService.exe`
- `target\release\EgressGuard.exe`

## Manual install

Preferred path:

1. Put both EXEs in one folder
2. Run `EgressGuard.exe`
3. Click **Install service**

CLI alternative:

```powershell
$installDir = "C:\Program Files\EgressGuard"
New-Item -ItemType Directory -Force -Path $installDir | Out-Null
Move-Item target\release\EgressGuardService.exe $installDir
# UI stays wherever you run it from - no need to copy EgressGuard.exe into Program Files

& "$installDir\EgressGuardService.exe" --install-service
& "$installDir\EgressGuardService.exe" --start-service
```

Service name: `EgressGuardService`. It starts at boot. It depends on BFE.

Protection stays off until you set it to on in the UI. When you close the UI, filtering does not stop. Only the service stops filtering.

## Uninstall

1. Open Settings, then Service.
2. Click **Uninstall**.

Uninstall runs the installed Program Files binary. It stops and deletes the SCM service. It removes WFP objects. It deletes `C:\Program Files\EgressGuard\`. It clears `%ProgramData%\EgressGuard\ipc-token`. Rules and the database under `%ProgramData%\EgressGuard\` stay.

If the Program Files folder stays (rare lock):

```powershell
Remove-Item "C:\Program Files\EgressGuard" -Recurse -Force
# optional full data wipe: Remove-Item "$env:ProgramData\EgressGuard" -Recurse -Force
```

If SCM is broken but WFP objects remain:

1. Run `--wfp-uninstall`.
2. Install and start again from the correct directory.

Set **Start with Windows** to off in the UI before you delete the binaries. You can also remove `EgressGuard` from `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`.
