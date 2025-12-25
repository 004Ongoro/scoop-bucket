# scoop-bucket (004Ongoro/scoop-bucket)

Scoop bucket containing Scoop manifests for open-source projects maintained here. This README explains how to install Scoop (if needed), add this bucket, find and install apps from it, and common maintenance/troubleshooting commands.

> Quick summary:
- Install Scoop (one-liner).
- Add this bucket: scoop bucket add 004Ongoro https://github.com/004Ongoro/scoop-bucket
- Install apps: scoop install <app-name>
- Update: scoop update && scoop update * && scoop cleanup

---

## Requirements
- Windows 10 / 11 (or compatible) with PowerShell (PowerShell 5+ recommended). PowerShell Core (7+) also works.
- A working internet connection.
- Scoop installs per-user by default (no admin rights required). If you prefer a system-wide setup, you must run PowerShell as Administrator and manage paths/permissions yourself.

---

## 1) Install Scoop (if you don't already have it)
Open PowerShell (recommended: run as normal user). Run:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
irm get.scoop.sh | iex
```

Notes:
- The script will set up Scoop in your user profile (default: %USERPROFILE%\scoop) and add the scoop shims to your PATH.
- If you run into execution policy errors, ensure you used the `-Scope CurrentUser` flag or run in an elevated session only if you understand the implications.

Verify Scoop is installed:

```powershell
scoop --version
```

If you see a version number, Scoop is ready.

---

## 2) Add this bucket (004Ongoro/scoop-bucket)
After installing Scoop, add this bucket so Scoop can find manifests stored here:

```powershell
scoop bucket add 004Ongoro https://github.com/004Ongoro/scoop-bucket
```

You can confirm the bucket was added:

```powershell
scoop bucket list
```

This should show `004Ongoro` in the list.

---

## 3) See what apps are available in this bucket
- Browse the bucket on GitHub: https://github.com/004Ongoro/scoop-bucket to see available manifests (recommended).
- Or search with Scoop after adding the bucket:

```powershell
scoop search <name-or-partial-name>
# Example:
scoop search editor
```

To inspect details about a specific manifest:

```powershell
scoop info <app-name>
```

If you want to list all known apps across all buckets, use:

```powershell
scoop search *
```

(For large result sets, narrow the search with a name fragment.)

---

## 4) Install an app from this bucket
Once you know the app name (manifest file name), install it with:

```powershell
scoop install <app-name>
# Example:
scoop install mytool
```

If an app exists in multiple buckets, Scoop will choose based on manifest precedence; specifying the bucket name is not usually necessary after you've added it.

Verify installation:

```powershell
scoop list
# or check the app version:
<app-name> --version
```

Scoop installs executables as "shims" (shortcuts) in %USERPROFILE%\scoop\shims and adds that folder to your PATH automatically.

---

## 5) Update apps and bucket
To update Scoop itself and all installed apps:

```powershell
scoop update
scoop update *
```

To update a single app:

```powershell
scoop update <app-name>
```

To update this bucket's manifests (if you want to refresh manifest list):

```powershell
scoop bucket update 004Ongoro
```

---

## 6) Uninstall / Remove
Uninstall an app:

```powershell
scoop uninstall <app-name>
```

Remove the bucket (will not remove apps already installed from it):

```powershell
scoop bucket rm 004Ongoro
```

If you want to uninstall and remove leftover files:

```powershell
scoop uninstall <app-name>
scoop cleanup
```

---

## 7) Troubleshooting & tips
- PATH issues: Ensure %USERPROFILE%\scoop\shims is in your PATH. Restart your terminal after installing Scoop.
- Permissions: Scoop is designed for per-user installs and usually does not require admin rights. If installation fails due to permissions, try running PowerShell as Administrator only if you understand the implications, or check file permissions in %USERPROFILE%\scoop.
- Missing dependencies: Some manifests require common tools (e.g., 7zip, unzip). Scoop typically installs needed dependencies automatically, but if a manifest fails, inspect `scoop info <app-name>` or the manifest file in the bucket.
- Logs: For more detail, re-run the failing command with `-v` (verbose) or check the PowerShell error message.
- If `irm get.scoop.sh | iex` is blocked in your environment, follow your organization’s policies or install Scoop manually by cloning the repo and adding shims to PATH.

---

## 8) Contributing
Contributions to this bucket (new manifests, updates, fixes) are welcome:
- Fork the repository on GitHub.
- Add or update a manifest under a clear filename (manifest format should follow Scoop manifest conventions).
- Open a pull request with a description and any relevant notes (checks, sources, verification steps).

Manifest authoring resources:
- Scoop manifest guidelines (see official Scoop docs and existing manifests in this bucket for examples).

---

## 9) License and repository info
This bucket is hosted at: https://github.com/004Ongoro/scoop-bucket

See the repository for license information (LICENSE file) and contribution guidelines.
