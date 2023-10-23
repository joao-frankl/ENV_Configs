## Table of Contents

- [Bashrc](#Bashrc)
- [Windows Terminal](#WT)
- [Powershell](#Powershell)
- [Disclaimer](#disclaimer)

## Bashrc
### and some "alias" for .bahsrc!

 ```sh
PS1='\n\n<\#> \[\e[1m\][\[\e[0;4m\]\u\[\e[0;1m\]]\[\e[0;2m\] - \[\e[0;1m\][\[\e[0m\]\w\[\e[1m\]]\[\e[0;2m\] - \[\e[0;1m\]|\[\e[0;97;2m\]$(ip route get 1.1.1.1 | awk -F"src " '"'"'NR == 1{ split($2, a," ");print a[1]}'"'"')\[\e[0;1m\]|\n\[\e[2m\]>_\[\e[0m\]'
```

```sh
alias ls='ls -al --color=auto'
```

```sh
alias dir='dir --color=auto'
```

```sh
alias vdir='vdir -a --color=auto'
```

```sh
alias cat='batcat'
```

```sh
alias npp='/mnt/c/Program\ Files/Notepad++/Notepad++.exe'
```


## WT
### settings.json for windows terminal

```json
{
    "$help": "https://aka.ms/terminal-documentation",
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "actions": 
    [
        {
            "command": 
            {
                "action": "copy",
                "singleLine": false
            },
            "keys": "ctrl+c"
        },
        {
            "command": "paste",
            "keys": "ctrl+v"
        },
        {
            "command": "find",
            "keys": "ctrl+shift+f"
        },
        {
            "command": 
            {
                "action": "splitPane",
                "split": "auto",
                "splitMode": "duplicate"
            },
            "keys": "alt+shift+d"
        },
		{
			"command":
			{
				"action":"wt",
				"commandline":"new-tab wsl.exe 'zap';split-pane wsl.exe 'disc'"
			},
			"keys":"alt+s",
			"name":"chats"
		}
    ],
    "alwaysShowNotificationIcon": true,
    "centerOnLaunch": true,
    "copyFormatting": "none",
    "copyOnSelect": false,
    "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
    "disableAnimations": true,
    "newTabMenu": 
    [
        {
            "type": "remainingProfiles"
        }
    ],
    "profiles": 
    {
        "defaults": 
        {
            "cursorShape": "vintage",
            "elevate": true,
            "useAtlasEngine": true
        },
        "list": 
        [
            {
                "commandline": "%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": false,
                "name": "Windows PowerShell"
            },
            {
                "commandline": "%SystemRoot%\\System32\\cmd.exe",
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "name": "Prompt de comando"
            },
            {
                "bellStyle": 
                [
                    "audible",
                    "taskbar"
                ],
                "closeOnExit": "never",
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "name": "PowerShell 7",
                "source": "Windows.Terminal.PowershellCore"
            },
            {
                "guid": "{17bf3de4-5353-5709-bcf9-835bd952a95e}",
                "hidden": true,
                "name": "Ubuntu-22.04",
                "source": "Windows.Terminal.Wsl"
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": false,
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            },
            {
                "guid": "{aab79973-318f-43b6-a9bc-b4096493753f}",
                "hidden": false,
                "name": "Nushell",
                "source": "nu"
            },
            {
                "guid": "{d7b20cea-47a9-518c-95a4-c8bd91e2e1c6}",
                "hidden": false,
                "name": "Ubuntu 22.04.2 LTS",
                "source": "CanonicalGroupLimited.Ubuntu22.04LTS_79rhkp1fndgsc"
            },
            {
                "commandline": "ssh joao.frankl@172.25.10.201",
                "guid": "{1490783e-22d0-477e-81b0-b03a94f8fb2e}",
                "hidden": false,
                "name": "SSH AD01",
                "startingDirectory": "%USERPROFILE%",
                "tabTitle": "AD01"
            },
            {
                "bellStyle": "taskbar",
                "commandline": "wt Ubuntu2204 ; split-pane -V -p wt Ubuntu2204 ",
                "guid": "{9707be55-6a3a-45c1-a173-0dd48d5a29d4}",
                "hidden": false,
                "name": "Chats",
                "startingDirectory": "~",
                "tabTitle": "Chats"
				
            }
        ]
    },   
```

## Powershell
### Microsoft.PowerShell_profile.ps1 settings for $PROFILE powershell

 ```ps1

## Customize the prompt
function prompt {
    $identity = [Security.Principal.WindowsIdentity]::GetCurrent()
    $principal = [Security.Principal.WindowsPrincipal] $identity
    $adminRole = [Security.Principal.WindowsBuiltInRole]::Administrator

    $prefix = $(if (Test-Path variable:/PSDebugContext) { '[DBG]: ' }
                elseif ($principal.IsInRole($adminRole)) { "PS | [ADMIN] - " } 
                else { '' })
    $body = '[' + $(Get-Location) + ']'
	Write-Host ""
    $suffix = $(if ($NestedPromptLevel -ge 1) { '>>' }) + '>_ '
    $prefix + $body + "`n"+ $suffix
	Write-Host ""
}


## Function			Set-ExecutionPolicy
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope Process -Force 

##function Get-SystemInfo {
##    $osInfo = Get-CimInstance Win32_OperatingSystem
##    $cpuInfo = Get-CimInstance Win32_Processor
##    $memoryInfo = Get-CimInstance Win32_PhysicalMemory
##
##    Write-Host "Sistema Operacional: $($osInfo.Caption) $($osInfo.Version)"
##    ##Write-Host "Nome do Computador: $($osInfo.CSName)"
##    Write-Host "Processador: $($cpuInfo.Name)"
##    
##    # Somar a capacidade total da memória física
##    $totalMemory = $memoryInfo | Measure-Object -Property Capacity -Sum
##    $totalMemoryGB = [math]::Round($totalMemory.Sum / 1GB, 2)
##    
##    Write-Host "Memória RAM Total: ${totalMemoryGB} GB"
##	Write-Host ""
##}
##
##Get-SystemInfo

New-Alias -Name 'npp' -Value 'C:\Program Files\Notepad++\notepad++.exe' -Description 'Launch Notepad++'
# New-Alias -Name 'scriptyes' -Value 'Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope Process -Force'
```
