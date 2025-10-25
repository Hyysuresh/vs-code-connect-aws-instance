

aws ec2 instace (ubuntu) connect vs code
Got error from ssh: spawn C:\Program Files\Google\Chrome\Application\ssh.exe ENOENT
Checking ssh with "C:\WINDOWS\system32\ssh.exe -V"
Got error from ssh: spawn C:\WINDOWS\system32\ssh.exe ENOENT
Checking ssh with "C:\WINDOWS\ssh.exe -V"
Got error from ssh: spawn C:\WINDOWS\ssh.exe ENOENT 
Checking ssh with "C:\WINDOWS\System32\Wbem\ssh.exe -V" 
Got error from ssh: spawn C:\WINDOWS\System32\Wbem\ssh.exe ENOENT
Checking ssh with "C:\WINDOWS\System32\WindowsPowerShell\v1.0\ssh.exe -V"
Got error from ssh: spawn C:\WINDOWS\System32\WindowsPowerShell\v1.0\ssh.exe ENOENT
ssh with "C:\WINDOWS\System32\OpenSSH\ssh.exe -V"
> OpenSSH_for_Windows_9.5p2, LibreSSL 3.8.2
> Running script with connection command: "C:\WINDOWS\System32\OpenSSH\ssh.exe" -T -D 49784 "ec2-52-24-173-150.us-west-2.compute.amazonaws.com" bash
> Generated SSH command: 'type "C:\Users\dell\AppData\Local\Temp\vscode-linux-multi-line-command-ec2-52-24-173-150.us-west-2.compute.amazonaws.com-159172969.sh" | "C:\WINDOWS\System32\OpenSSH\ssh.exe" -T -D 49784 "ec2-52-24-173-150.us-west-2.compute.amazonaws.com" bash'
> Using connect timeout of 17 seconds
> Terminal shell path: C:\WINDOWS\System32\cmd.exe 

------------------- solution ----------------------------------------------
Stap.1 - sudo apt-get update && sudo apt-get install -y openssh-server
Stap.2 - sudo sed -i 's/^#PermitTTY yes/PermitTTY yes/' /etc/ssh/sshd_config
Stap.3 - sudo systemctl restart ssh

open - C:\Users\dell\.ssh\config ( config file open)
edit -
Host SSH3
    HostName 54.187.213.238
    User ubuntu
    IdentityFile C:/Users/dell/.ssh/id_ed25519
    IdentitiesOnly yes
    ServerAliveInterval 60
    ServerAliveCountMax 3
    LogLevel DEBUG3
open settings ya ctrl+,
settings.json me
edit -
{
    "files.autoSave": "afterDelay",
    "window.menuBarVisibility": "compact",
    "files.exclude": {
        "**/.git": false
    },
    "azureTerraform.survey": {
        "surveyPromptDate": "2025-11-07T02:00:41.454Z",
        "surveyPromptIgnoredCount": 2
    },
    "terminal.integrated.tabs.defaultIcon": "vm",

    "remote.SSH.showLoginTerminal": true,
    "remote.SSH.useLocalServer": true,
    "terminal.integrated.defaultProfile.windows":"PowerShell",
    "remote.SSH.useExecServer": false,
    "remote.SSH.enableRemoteCommand": true,
    "remote.SSH.remotePlatform": {
    "SSH3": "linux"
    },
    "remote.SSH.path": "C:\\WINDOWS\\System32\\OpenSSH\\ssh.exe",
    "remote.SSH.configFile": "C:\\Users\\dell\\.ssh\\config",
    "remote.SSH.connectTimeout": 60
    

}



VS Code me:
➡️ Ctrl + Shift + P
➡️ Type: Remote-SSH: Settings
➡️ “Remote.SSH: Use Local Server” ✅ enable kar do

EC2 me --- rm -rf ~/.vscode-server

chmod 400 permission for windows
- icacls "ssh-key.pem" /inheritance:r
- icacls "ssh-key.pem" /grant:r "%USERNAME%":(R)

install commends -
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

VS Code →
File → Preferences → Settings
Search: remote.ssh.path
Phir ye path set karo: C:\Windows\System32\OpenSSH\ssh.exe
            ya
use commend - setx PATH "$env:PATH;C:\Windows\System32\OpenSSH"
Ensure - echo $env:PATH

 commend - where ssh 
 output - kuchh nhi aaye 
       manually add path
- PowerShell (Admin) open karo
Type karo:
$env:Path += ";C:\Windows\System32\OpenSSH"
[Environment]::SetEnvironmentVariable("Path", $env:Path, [EnvironmentVariableTarget]::User)

PowerShell close → naya PowerShell/CMD open karo
Test karo:
-where ssh
-ssh -V

commend =] wsl --list --verbose
install nhi hai to
commend = wsl --install -d Ubuntu
commend = wsl --setdefault Ubuntu

open - C:\Users\dell\.ssh\config ( config file open)
edit -
Host SSH3
    HostName 54.187.213.238
    User ubuntu
    IdentityFile C:/Users/dell/.ssh/id_ed25519
    IdentitiesOnly yes
    ServerAliveInterval 60
    ServerAliveCountMax 3
    LogLevel DEBUG3
