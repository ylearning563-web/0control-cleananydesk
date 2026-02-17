# AnyDesk Quick Cleanup 

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

# AnyDesk Fresh Install

---

## Version 1 — Command Prompt (CMD)

```cmd
sc stop AnyDesk >nul 2>&1 & taskkill /f /im anydesk.exe >nul 2>&1 & powershell -Command "Get-Package -Name 'AnyDesk' -ErrorAction SilentlyContinue | Uninstall-Package -Force" & rmdir /s /q "%AppData%\AnyDesk" 2>nul & rmdir /s /q "%LocalAppData%\AnyDesk" 2>nul & rmdir /s /q "C:\ProgramData\AnyDesk" 2>nul & powershell -Command "Invoke-WebRequest 'https://download.anydesk.com/AnyDesk.exe' -OutFile $env:TEMP\AnyDesk.exe" & "%TEMP%\AnyDesk.exe" --install "C:\Program Files (x86)\AnyDesk" --start-with-win --silent & echo AnyDesk reinstalled successfully.
```

---

## Version 2 — PowerShell

```powershell
Stop-Service -Name "AnyDesk" -Force -ErrorAction SilentlyContinue; 
Stop-Process -Name "AnyDesk" -Force -ErrorAction SilentlyContinue; 
Get-Package -Name "AnyDesk" -ErrorAction SilentlyContinue | Uninstall-Package -Force; 
Remove-Item "$env:AppData\AnyDesk","$env:LocalAppData\AnyDesk","C:\ProgramData\AnyDesk" -Recurse -Force -ErrorAction SilentlyContinue; 
Invoke-WebRequest "https://download.anydesk.com/AnyDesk.exe" -OutFile "$env:TEMP\AnyDesk.exe"; 
Start-Process "$env:TEMP\AnyDesk.exe" -ArgumentList "--install `"C:\Program Files (x86)\AnyDesk`" --start-with-win --silent" -Wait; 
Write-Host "AnyDesk reinstalled successfully."
```

---
