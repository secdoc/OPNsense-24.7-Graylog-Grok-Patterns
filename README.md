# OPNsense - 24.7 Graylog Grok Patterns
Grok Patterns for Graylog to Support OPNsense 24.7

**NOTE:**
**As of Aug 7 2024 Graylog released version 6.0.5 which broke the filterlog Grok Pattern that worked with version 6.0.4. I have updated the associated files to include both 6.0.4 and 6.0.5.**

With the update to new version of software or platforms can come some technical adjustments. One such example is with the change from OPNsense to OPNsense 24.7. The new version changes the logging format of the filterlogs and suricata logs.

If you are parsing the logs into Graylog or any other logging or SIEM system, it will be necessary to to update any parsers or regex/grok patterns. In my case, I utilize Graylog, so it was necessary to update the parsing to properly be used with dashboards and other visualizations or search queries.

If you use Graylog, this repository has updated Grok Patterns for the filterlog and suricata logs. 

 - [input_extractor_filterlog.grok](https://github.com/secdoc/OPNsense-24.7-Graylog-Grok-Patterns/blob/main/input_extractor_filterlog.grok)
 - [suricata_grok_pattern.grok](https://github.com/secdoc/OPNsense-24.7-Graylog-Grok-Patterns/blob/main/suricata_grok_pattern.grok)

In addition, the repository includes a Graylog Content Packs for Dashboards and Suricata Pipeline and the specific Suricata Parse Pipeline Rule.

 - [ontent-pack-opnsense247-dashboards.json](https://github.com/secdoc/OPNsense-24.7-Graylog-Grok-Patterns/blob/main/content-pack-opnsense247-dashboards.json)
 - [content-pack-opnsense247-suricata-pipeline.json](https://github.com/secdoc/OPNsense-24.7-Graylog-Grok-Patterns/blob/main/content-pack-opnsense247-suricata-pipeline.json)
 - [opnsense247_suricata_pipeline_rule](https://github.com/secdoc/OPNsense-24.7-Graylog-Grok-Patterns/blob/main/opnsense247_suricata_pipeline_rule)

## Example Graylog Filterlog (FW) Dashboards

![image](https://github.com/user-attachments/assets/96ea9cad-eb50-4832-9c74-e3d2230fea5a)

![image](https://github.com/user-attachments/assets/47c7a84c-5917-4485-955b-cdcce7b84a9e)

## Example Graylog IDS (Suricata) Dashboard

![image](https://github.com/user-attachments/assets/ceb8f6ec-700f-4fda-8eb9-90393333171d)


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
## Explanation
As you can see when looking at the old and new log format, there has been adjustment to the date formatting, old `Jul 26 13:17:32` and new format `2024-08-05T23:17:15+00:00`, as well as, the inclusion of the `meta sequenceId=` field.
## Key Changes:
 - Date Format: The old format used a more condensed representation (e.g., "Jul 26 13:17:32"), while the new format adopts the ISO 8601 standard (e.g., "2024-08-05T23:17:15+00:00"), including timezone information.
 - Meta Sequence ID: The new format introduces a [meta sequenceId="XXXXXXX"] field, which can be useful for tracking log sequence and detecting missing logs.
 - Structure: The overall structure of the log entries has been modified to align with more standardized logging practices, potentially improving compatibility with log analysis tools.
