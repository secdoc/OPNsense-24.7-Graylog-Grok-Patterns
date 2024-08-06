# OPNsense - 24.7 Graylog Grok Patterns
Grok Patterns for Graylog to Support OPNsense 24.7

With the update to new version of software or platforms can come some technical adjustments. One such example is with the change from OPNsense to OPNsense 24.7. The new version changes the logging format of the filterlogs and suricata logs.

## Example
Old filterlog - 
```
<134>Jul 16 06:36:52 xxxx.acme.tech filterlog[40156]: 85,,,9f96d956119c25145fc2ce221237f3a5,bridge0,match,pass,out,4,0x0,,64,63281,0,DF,17,udp,52,10.13.37.156,8.8.8.8,36444,53,32
```
New filterlog - 
```
<134>1 2024-08-05T12:05:54+00:00 xxxx.acme.tech filterlog 54802 - [meta sequenceId="2763892"] 85,,,9f96d956119c25145fc2ce221237f3a5,bridge0,match,pass,out,4,0x0,,63,11771,0,DF,6,tcp,60,10.13.37.156,193.0.6.135,43802,43,0,S,1404651214,,64240,,mss;sackOK;TS;nop;wscale
```
Likewise, here are the differences with the suricata logs:
Old suricata log - 
```
<173>Jul 26 13:17:32 xxxx.acme.tech suricata[48264]: [1:2017928:4] ET POLICY check.torproject.org IP lookup/Tor Usage check over TLS with SNI [Classification: Device Retrieving External IP Address Detected] [Priority: 2] {TCP} 192.168.200.69:1247 -> 116.202.120.181:443
```
New suricata log - 
```
<173>1 2024-08-05T23:17:15+00:00 xxxx.acme.tech suricata 23296 - [meta sequenceId="1335381"] [1:2024364:4] ET SCAN Possible Nmap User-Agent Observed [Classification: Web Application Attack] [Priority: 1] {TCP} 192.168.2.141:56840 -> 192.168.88.2:80
```
