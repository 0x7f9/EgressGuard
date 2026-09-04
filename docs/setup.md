# Setup

### Requirements

- Windows 10 or 11
- Administrator rights for Install, Update, and Uninstall (UAC)

Get the latest beta [release](https://github.com/0x7f9/EgressGuard/releases/), or [build from source](build.md).

### Install

1. Keep EgressGuard.exe and EgressGuardService.exe in the same folder.
2. Run EgressGuard.exe.
3. Click **Install**.

Optional country codes. Put geoip-country.mmdb in %ProgramData%\EgressGuard\database\. Then restart the EgressGuard service from Settings, Service, **Restart**. Get the file from [DB-IP Country Lite](https://db-ip.com/db/download/ip-to-country-lite).

### Update

1. Run the new EgressGuard.exe.
2. Keep the new EgressGuardService.exe in the same folder.
3. Open Settings, then Service.
4. Click **Update**.

### Uninstall

1. Open Settings, then Service.
2. Click **Uninstall**.

Rules and data under %ProgramData%\EgressGuard\ stay in place. You can remove with:

```powershell
Remove-Item "C:\ProgramData\EgressGuard" -Recurse -Force
```