# Getting Setup

### Requirements

- Windows 10 or 11
- Administrator rights for Install, Update, and Uninstall (UAC)

To build from source, see [docs/build.md](docs/build.md).
Get the latest beta [release](https://github.com/0x7f9/EgressGuard/releases/).

### Uninstall

1. Open Settings, then Service.
2. Click **Uninstall**.

### Install

1. Keep EgressGuard.exe and EgressGuardService.exe in the same folder.
3. Run EgressGuard.exe.
4. Click **Install**.

The first service start creates %ProgramData%\EgressGuard\database.

Optional country codes use a local GeoIP file. Put geoip-country.mmdb in %ProgramData%\EgressGuard\database\. Then restart the EgressGuard service from Settings, Service, **Restart**. Get the file from [DB-IP Country Lite](https://db-ip.com/db/download/ip-to-country-lite).

### Update

Rules and data under %ProgramData%\EgressGuard\ stay in place.

1. Run the new EgressGuard.exe.
3. Keep the new EgressGuardService.exe in the same folder.
4. Open Settings, then Service.
5. Click **Update**.

### Uninstall

1. Open Settings, then Service.
2. Click **Uninstall**.
