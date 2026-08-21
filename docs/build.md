# Build from source

This document describes how to compile EgressGuard and what Install does on disk.

## Requirements

- Windows 10 or 11
- Administrator rights for Install, Update, and Uninstall (UAC)
- Current stable Rust (edition 2024). See [rustup](https://rustup.rs/)
- Visual Studio Build Tools with **Desktop development with C++**
- WebView2 Runtime

## Build release binaries

```powershell
cargo build --release -p egressguard-service -p egressguard-ui
```

Outputs:

- target\release\EgressGuardService.exe
- target\release\EgressGuard.exe

## Install

1. Put both EXEs in one folder.
2. Run EgressGuard.exe.
3. Click **Install**.

Service name: EgressGuardService. It starts at boot. It depends on the Base Filtering Engine (BFE). Install copies the service binary to C:\Program Files\EgressGuard\. After a successful install, the UI deletes the copy next to the UI.

## Update

1. Put the new EXEs in one folder.
2. Run the new UI.
3. Open Settings, then Service.
4. Click **Update**.

After a successful update, the UI deletes the copy of EgressGuardService.exe next to the UI. Rules and data under %ProgramData%\EgressGuard\ stay.

## Uninstall

1. Open Settings, then Service.
2. Click **Uninstall**.

Uninstall runs an elevated --uninstall-service on a service binary. The UI uses the registered SCM path when that file exists. If that path is missing, it uses the copy next to the UI, then C:\Program Files\EgressGuard\.

The elevated process stops the SCM service when it is present. It then removes WFP objects. Only after WFP cleanup succeeds does it delete the SCM service, remove C:\Program Files\EgressGuard\, and clear %ProgramData%\EgressGuard\ipc-token. It turns off **Start with Windows**. Rules and the database under %ProgramData%\EgressGuard\ stay.

If WFP cleanup fails, Uninstall aborts and leaves the SCM service installed. The service still owns the provider, so you can start it again or retry Uninstall. Do not delete the SCM entry while persistent deny filters remain.

If the Program Files folder stays (rare lock):

```powershell
Remove-Item "C:\Program Files\EgressGuard" -Recurse -Force
# Optional. Wipe all product data: Remove-Item "$env:ProgramData\EgressGuard" -Recurse -Force
```

If SCM is broken but WFP objects remain:

1. Put both EXEs in one folder and run the UI.
2. Open Settings, then Service.
3. Click **Uninstall**, then **Install**.
