# AnyDesk Quick Cleanup 

This removes AnyDesk service, running process, and leftover data folders.

---

## Version 1 — Command Prompt (CMD)

```cmd
sc stop AnyDesk >nul 2>&1 & timeout /t 2 >nul & taskkill /f /im anydesk.exe >nul 2>&1 & rmdir /s /q "%AppData%\AnyDesk" 2>nul & rmdir /s /q "%LocalAppData%\AnyDesk" 2>nul & rmdir /s /q "C:\ProgramData\AnyDesk" 2>nul & echo AnyDesk cleanup completed.
```

---

## Version 2 — PowerShell

```powershell
Stop-Service -Name "AnyDesk" -Force -ErrorAction SilentlyContinue; Start-Sleep 2; Stop-Process -Name "AnyDesk" -Force -ErrorAction SilentlyContinue; Remove-Item "$env:AppData\AnyDesk","$env:LocalAppData\AnyDesk","C:\ProgramData\AnyDesk" -Recurse -Force -ErrorAction SilentlyContinue; Write-Host "AnyDesk cleanup completed."
```

---
