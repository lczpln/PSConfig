# Powershell configs:

First type ``notepad $Profile.CurrentUserAllHosts`` to open config list

#### Default dracula
```js
Set-PSReadlineOption -Color @{
"Command" = [ConsoleColor]::Green
"Parameter" = [ConsoleColor]::Gray
"Operator" = [ConsoleColor]::Magenta
"Variable" = [ConsoleColor]::White
"String" = [ConsoleColor]::Yellow
"Number" = [ConsoleColor]::Blue
"Type" = [ConsoleColor]::Cyan
"Comment" = [ConsoleColor]::DarkCyan
}
Import-Module posh-git
Import-Module PSReadLine
$GitPromptSettings.DefaultPromptPrefix.Text = "$([char]0x2192) " # arrow unicode symbol
$GitPromptSettings.DefaultPromptPrefix.ForegroundColor = [ConsoleColor]::Green
$GitPromptSettings.DefaultPromptPath.ForegroundColor =[ConsoleColor]::Cyan
$GitPromptSettings.DefaultPromptSuffix.Text = " $([char]0x203A) " # chevron unicode symbol
$GitPromptSettings.DefaultPromptSuffix.ForegroundColor = [ConsoleColor]::Magenta
$GitPromptSettings.BeforeStatus.ForegroundColor = [ConsoleColor]::Blue
$GitPromptSettings.BranchColor.ForegroundColor = [ConsoleColor]::Blue
$GitPromptSettings.AfterStatus.ForegroundColor = [ConsoleColor]::Blue
```
![alt text](https://ibb.co/3MNxNjr)

#### or Spaceship zsh
```js
Set-PSReadlineOption -Color @{
    "Command" = [ConsoleColor]::Green
    "Parameter" = [ConsoleColor]::Gray
    "Operator" = [ConsoleColor]::Magenta
    "Variable" = [ConsoleColor]::White
    "String" = [ConsoleColor]::Yellow
    "Number" = [ConsoleColor]::Blue
    "Type" = [ConsoleColor]::Cyan
    "Comment" = [ConsoleColor]::DarkCyan
}

function prompt {
  $username=( ( Get-WMIObject -class Win32_ComputerSystem | Select-Object -ExpandProperty username ) -split '\\' )[1]
  $currentPathAndGitSeparator = "$(if(git rev-parse --git-dir 2> $null) {" on "})"
  $gitWasModified = if(git rev-parse --git-dir 2> $null) {
    if(git diff --staged --name-only){
      " [+]"
    } 
    elseif(git status --porcelain |Where {$_ -notmatch '^\?\?'}) {
      " [!]"
    }
    else {
      ""
    }
  }
  $gitWasModifiedColor = if(git diff --staged --name-only){
    "Green"
  } 
  elseif(git status --porcelain |Where {$_ -notmatch '^\?\?'}) {
    "Red"
  }
  else {
    "White"
  }
  $git = "$(if(git rev-parse --git-dir 2> $null) {" $(git branch --show-current)"})"
  $prefix = "`n❯"

  $dirSep = [IO.Path]::DirectorySeparatorChar
    $pathComponents = $PWD.Path.Split($dirSep)
    $displayPath = if ($pathComponents.Count -le 3) {
      $PWD.Path
    } else {
      '…{0}{1}' -f $dirSep, ($pathComponents[-2,-1] -join $dirSep)
    }

Write-Host "$($username)" -NoNewline -ForegroundColor "Yellow"
Write-Host " in " -NoNewline
Write-Host "$($displayPath)" -NoNewline -ForegroundColor "Cyan"
Write-Host "$($currentPathAndGitSeparator)" -NoNewline
Write-Host "$($git)" -NoNewline -ForegroundColor "Magenta"
Write-Host "$($gitWasModified)" -NoNewline -ForegroundColor "$($gitWasModifiedColor)"
Write-Host "$($prefix)" -NoNewline -ForegroundColor "Green"
return " "
}

Import-Module posh-git
Import-Module PSReadLine
```
![alt text](https://i.ibb.co/7v8VQDm/image.png)

## Git Posh

https://github.com/dahlbyk/posh-git

install with this command line:

```
PowerShellGet\Install-Module posh-git -Scope CurrentUser -AllowPrerelease -Force
```

## Git PSReadLine

```
Install-Module PSReadLine
```

## Git PSReadLine Addon

```
powershell.exe -noni -nop -c "iwr -useb https://git.io/InstallPSReadlineAutocompleteBeta.ps1 | iex"
```

## Windows Terminal
```
https://www.microsoft.com/pt-br/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab
```

### list
```js
"list": [
  {
  // Make changes here to the powershell.exe profile.
    "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
    "name": "Windows PowerShell",
    "commandline": "powershell.exe -nologo",
    "hidden": false,
    "colorScheme": "Dracula",
    "fontFace": "Fira Code Retina"
  },
...
]
```
### scheme
```js
"schemes": [
  {
    "name": "Dracula",
    "background": "#272935",
    "black": "#21222C",
    "blue": "#BD93F9",
    "cyan": "#8BE9FD",
    "foreground": "#F8F8F2",
    "green": "#50FA7B",
    "purple": "#FF79C6",
    "red": "#FF5555",
    "white": "#F8F8F2",
    "yellow": "#FFB86C",
    "brightBlack": "#6272A4",
    "brightBlue": "#D6ACFF",
    "brightCyan": "#A4FFFF",
    "brightGreen": "#69FF94",
    "brightPurple": "#FF92DF",
    "brightRed": "#FF6E6E",
    "brightWhite": "#F8F8F2",
    "brightYellow": "#FFFFA5"
  }
]
```
