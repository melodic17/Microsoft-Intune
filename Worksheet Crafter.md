# 📖 Deployment: Worksheet Crafter via Intune (Win32-App)  

## 1. Preparation  

### **Download the installer**  
Get the official Worksheet Crafter installer:  
➡️ [Worksheet Crafter – Full Version Download](https://worksheetcrafter.com/de/downloads/vollversion)  

Save the file as:  
Worksheet_Crafter_Setup_Full.exe



---

### **Create helper scripts**

#### **install.ps1**
```powershell
Param (
    [parameter(Mandatory = $true)]
    [String[]] $param
)

$PackageName = "WorksheetCrafter"

Start-Transcript -Path "$env:ProgramData\Microsoft\IntuneManagementExtension\Logs\$PackageName-install.log" -Force

Start-Process 'Worksheet_Crafter_Setup_Full.exe' -ArgumentList $param -Wait

Stop-Transcript

```


#### **uninstall.ps1**
```powershell
$PackageName = "WorksheetCrafter"

Start-Transcript -Path "$env:ProgramData\Microsoft\IntuneManagementExtension\Logs\$PackageName-uninstall.log" -Force

Start-Process '"C:\Program Files\Worksheet Crafter\unins000.exe"' -ArgumentList '/SILENT /SUPPRESSMSGBOXES /LOG=c:\temp\uninstall.log' -Wait

Stop-Transcript
