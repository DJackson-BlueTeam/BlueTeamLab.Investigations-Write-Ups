![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/8f611d74a09cac90d8509bb4503fc13805593211/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/Foxy.png)
# Foxy - Write-Up 

## As an Intelligence  Analyst you are tasked with assisting the SOC Analyst with their investigations, providing additional context and information.

**1. The SOC recently observed network connections from 3 internal hosts towards hxxp://45.63.126[.]199/dot.gif (URL has been sanitized). What is this activity likely related to?**
  - I had to read the `.csv` file with `cat` and also used `grep` to by piping `|` it to only look for information with the ip `45[.]63[.]126[.]199`
    
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/1d6f64aa67a9bb2ad1bcfaf0828744be00959155/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/1..png)

  - I was able to get a return, observe that there was a malicious tool "Cobalt Strike": which can be used as a penetration tool.
  - In addition this tool is it used by adversaries and Advance Persistent Threat groups. 
  - I was able to verify this by looking up `Cobalt Strike` and
  - 
3. The SHA256 hash of a file was detected and quarantined on one of the Executives old android phones. We are trying to work out what this file does so we can take next steps. The hash value is 6461851c092d0074150e4e56a146108ae82130c22580fb444c1444e7d936e0b5. Is this file associated with malware? If so, what is the malware name? (as stated by Malware Bazaar)
4. Investigate the reference link for this SHA256 hash value. Submit the threat name (acronym only), the C2 domain, IP, and the domain registrar.
5. Visit https://www.joesandbox.com/analysis/1319345/1/html. Investigate the MITRE ATT&CK Matrix to understand the Collection activities this file can take, and what the potential impact is to the Executives work mobile phone. Submit the 5 Technique names in alphabetical order.
6. A junior analyst was handling an event that involved outbound connections to a private address and didn't perform any further analysis on the IP. What are the two ports used by the IP 192.236.198.236?
7. Use the reference to help you further research the IP. What is the C2 domain?
8. What is the likely delivery method into our organization? Provide the Technique name and Technique ID from ATT&CK.
9. Investigate further and try to find the name of the weaponized Word document, so we can use our EDR to check if it is present anywhere else within the organization.
10. What is the name of the .JAR file dropped by the Word document?
11. A junior analyst was handling an event that involved outbound connections to a private address and didn't perform any further analysis on the IP. What are the two ports used by the IP 192.236.198.236?
12. Looking at all export files, how many rows reference this URL? (include duplicates).
13. Based on this information, what is the name of the malware family that is being widely distributed via Discord?
14. We can proactively use indicators from threat feeds for detection, or for prevention via blocking. When it comes to blocking indicators, it is crucial that they are from a reputable source and have a high level of confidence to prevent blocking legitimate entities. How many rows in the full_urls.csv have a confidence rating of 100, and would likely be safe to block on the web proxy?
15. An analyst has reported activity coming from an IP address using source port 8001, but they don't understand what this IP is trying to achieve. Looking at full_ip-port.csv in Gnumeric, filter on malware_printable = Unknown malware, and find an IP that is using port 8001. What is the IP address value?
16. Investigating the reference material, what is the CVE ID of the vulnerability that this IP has been trying to exploit? And what is the industry nickname for this vulnerability?
