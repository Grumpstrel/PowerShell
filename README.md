# PowerShell
Repository for PowerShell scripts.

# New-AzureVM.ps1
Name doesn't matter as long as it's unique.

Location can be found with `Get-AzureRMLocation`

VMSize can be determined with `Get-AzureRMVMSize -Location <location>`
  
  We default to `Standard_D1` since it's super cheap
  
  The largest VM we'd suggest you go with is `Standard_D4s_v3` because of it's unique cost/benefit
  
  For more pricing details: https://azure.microsoft.com/en-us/pricing/details/virtual-machines/windows/


# New-NetworkCapture.ps1
Runs a network capture for 5 minutes by default.

This a PowerShell variant of running `netsh trace start capture=yes tracefile=%temp%\NetworkTrace.etl` in the command prompt.


# TcpPing.ps1
The script will take an IP address (IPv4 or IPv6) or DNS hostname, then will 
test how long it takes to make a TCP socket connection to that IP and port. 

This script produces the following TCP traffic:

-> [SYN]<br />
<- [SYN,ACK]<br />
-> [ACK]<br />
-> [FIN,ACK]<br />
<- [RST,ACK]<br />

Latency is displayed in milliseconds (ms).
```powershell
PS F:\Repo\PowerShell> .\TcpPing.ps1 -HostNameOrIP outlook.office365.com -Port 25 | FT -AutoSize
```
| SourceAddress | RemoteAddress | RemotePort | Connected | Latency | Exception |
| :------------ | :------------ | ---------: | --------: | ------: | --------- |
| 10.131.34.100 | 40.97.119.162 | 25         | True      | 4.6481  |
| 10.131.34.100 | 40.97.119.162 | 25         | True      | 4.6751  |
| 10.131.34.100 | 40.97.119.162 | 25         | True      | 4.8726  |
| 10.131.34.100 | 40.97.119.162 | 25         | True      | 4.8324  |

