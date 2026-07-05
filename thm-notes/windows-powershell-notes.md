# Windows PowerShell - TryHackMe Room Notes

**Room:** Windows PowerShell  
**Difficulty:** Easy  
**Time:** 60min  

---

## Recon & Basics

| Command | What It Does | Key Output |
|---------|--------------|------------|
| `powershell` | Switch from cmd to PS | PS prompt |
| `Get-Command` | List all cmdlets | Functions, aliases, cmdlets |
| `Get-Help Get-Date` | Show cmdlet help | Syntax, examples, parameters |
| `Get-Alias` | Show command shortcuts | dir = Get-ChildItem, cd = Set-Location |

---

## Key Commands Used

| Command | Purpose |
|---------|---------|
| `Get-ChildItem` | List files/folders (like dir/ls) |
| `Set-Location` | Change directory (like cd) |
| `New-Item` | Create files/folders |
| `Remove-Item` | Delete files/folders |
| `Get-Content` | Read file contents |
| `Where-Object` | Filter output |
| `Select-Object` | Select specific properties |
| `Get-Process` | List running processes |
| `Get-Service` | List services |
| `Get-NetTCPConnection` | Show network connections |
| `Get-FileHash` | Calculate file hash |

---

## What I Learned

- **PowerShell uses Verb-Noun naming** like `Get-ChildItem`, `Set-Location`
- **`Get-Help`** is the first thing to run when stuck on any cmdlet
- **Piping (`|`)** passes real objects, not just text. Much more powerful than cmd
- **`Get-Command`** when you don't know what exists
- **`Get-Process`**, **`Get-Service`**, **`Get-NetTCPConnection`** give instant system visibility
- **`Get-FileHash`** is useful for checking file integrity

---

## Useful Aliases

| Alias | Full Command |
|-------|--------------|
| `dir` | `Get-ChildItem` |
| `ls` | `Get-ChildItem` |
| `cd` | `Set-Location` |
| `echo` | `Write-Output` |
| `cat` | `Get-Content` |

---

## Example Workflow

```powershell
# Check what commands exist
Get-Command *process*

# Get help on a command
Get-Help Get-Process -Detailed

# List all processes and filter
Get-Process | Where-Object {$_.CPU -gt 100}

# Read a file
Get-Content .\file.txt

# Get file hash
Get-FileHash .\file.txt -Algorithm SHA256
