# Prerequisites:

## Install choco :
  [REFER HERE](https://chocolatey.org/docs/installation)

### Install with cmd.exe
* Run the following command:

```
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

### Install with PowerShell.exe
* With PowerShell, there is an additional step. You must ensure Get-ExecutionPolicy is not Restricted. We suggest using Bypass to bypass the policy to get things installed or AllSigned for quite a bit more security.

* Run Get-ExecutionPolicy. If it returns Restricted, then run Set-ExecutionPolicy AllSigned or Set-ExecutionPolicy Bypass -Scope Process.
* Now run the following command:

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

### Install Mobaxterm : [REFER HERE](https://community.chocolatey.org/packages/MobaXTerm)
```
choco install mobaxterm
```

### Install Git : [REFER HERE](https://chocolatey.org/packages/git.install)
```
choco install git.install
```

### Install visualStudioCode : [REFER HERE](https://chocolatey.org/packages/vscode)
```
choco install vscode
```
### AWS free tier account [REFER HERE](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc)

![preview](../MAR-2021/images/A1.png)
![preview](../MAR-2021/images/A2.png)
![preview](../MAR-2021/images/A3.png)
![preview](../MAR-2021/images/A4.png)
![preview](../MAR-2021/images/A5.png)
![preview](../MAR-2021/images/A6.png)
![preview](../MAR-2021/images/A7.png)
![preview](../MAR-2021/images/A8.png)
![preview](../MAR-2021/images/A9.png)
![preview](../MAR-2021/images/A10.png)
![preview](../MAR-2021/images/A11.png)
![preview](../MAR-2021/images/A12.png)
![preview](../MAR-2021/images/A13.png)
![preview](../MAR-2021/images/A14.png)
![preview](../MAR-2021/images/A15.png)


