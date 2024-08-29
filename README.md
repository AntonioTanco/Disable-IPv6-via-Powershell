<h1>Disabling IPv6 via Powershell - CVE-2024-38063</h1>

This is a simple script creating in Powershell to automate the disabling of the IPv6 Protocol against all NIC's that have IPv6 enabled. This script can be tailored to your specific needs and can serve as a template for larger environments. 

In order to mitigate CVE-2024-38063, IPv6 Protocol should be disabled immediately unless you already rely on IPv6 in your home network or IT environment then prioritize applying all the relevant Windows patches first and consider implementing a network monitoring solution like: Snort (Network Level), Suricata (Network Level) or GlassWire (For home/personal use).

#CVE-2024-38063 - Disabling IPv6 binging.ps1
```
#CVE-2024-38063 - Disabling IPv6 binging.ps1
#Author: Antonio T
#Github: https://github.com/antoniotanco

#Get all the network adapters that are enabled and have IPv6 Protocol enabled
$adapters = Get-NetAdapter | Where-Object {$_.Status -eq "Up" -and (Get-NetAdapterBinding -ComponentID ms_tcpip6).Enabled}

#Interate through each NIC
foreach ($adapter in $adapters) {

    #Disable IPv6 for each network adapter
    Disable-NetAdapterBinding -Name ($adapter.Name) -ComponentID "ms_tcpip6"

    #Print to console the results of what network adapter had IPv6 disabled
    Write-Host "Ipv6 has been disabled for network adapter: $($adapter.Name)"

}
```
