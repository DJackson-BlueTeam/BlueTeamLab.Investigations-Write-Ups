![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/8f611d74a09cac90d8509bb4503fc13805593211/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/Foxy.png)
# Foxy - Write-Up 

## As an Intelligence  Analyst you are tasked with assisting the SOC Analyst with their investigations, providing additional context and information.

**1. The SOC recently observed network connections from 3 internal hosts towards hxxp://45.63.126[.]199/dot.gif (URL has been sanitized). What is this activity likely related to?**
- I had to read the `.csv` file with `cat` and also used `grep` to by piping `|` it to only look for information with the ip `45[.]63[.]126[.]199`
    
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/1d6f64aa67a9bb2ad1bcfaf0828744be00959155/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/1..png)

- I was able to get a return, observe that there was a malicious tool "Cobalt Strike": which can be used as a penetration tool.
- In addition this tool is it used by adversaries and Advance Persistent Threat groups. 
- I was able to verify this by looking up `Cobalt Strike`.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/6f96b6d72f350bceb6bf5870b9af915ea169f451/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/1.1.png)

**2. How many URLs are using the same endpoint 'dot.gif', across all export files?**
- I had to get the total number of urls that have the similar endpoint of `dot.gif` within the "Threat Fox" directory.
- I used `cat *` with the wild car to read all of the files and output with `grep -c` and telling grep to only retreive and show the totals .dotgif urls.
- which was a total of 568 urls with `.dotgif`.
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/6f96b6d72f350bceb6bf5870b9af915ea169f451/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/2..png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/6f96b6d72f350bceb6bf5870b9af915ea169f451/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/2.1.png)

**3. The SHA256 hash of a file was detected and quarantined on one of the Executives old android phones. We are trying to work out what this file does so we can take next steps. The hash value is 6461851c092d0074150e4e56a146108ae82130c22580fb444c1444e7d936e0b5. Is this file associated with malware? If so, what is the malware name? (as stated by Malware Bazaar)**
- With the hash that was provided, I was able to `cat` the `SHA256.csv` file and grep the hash value

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/6f96b6d72f350bceb6bf5870b9af915ea169f451/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/3.1.png)

- In the 10th cloumn you can see a which seems to be malicious file that was executed in the host machine.
- You can see that it is a spyware executable.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/e83612fcb15489bf02f5dfd525f64b341d09ed4b/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/IRATA.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/6f96b6d72f350bceb6bf5870b9af915ea169f451/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/3..png)

**4. Investigate the reference link for this SHA256 hash value. Submit the threat name (acronym only), the C2 domain, IP, and the domain registrar.**
- The link that was in the Q3 had a twitter link attached to the SHA256 hashvalue

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/6f96b6d72f350bceb6bf5870b9af915ea169f451/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/3.1.png)

- The link then directed to to a twitter post by `@onecert_ir`

![alt](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/748f9264f62917944bb6dc1cac39f3028b91612e/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/4..png)

**5. Visit https://www.joesandbox.com/analysis/1319345/1/html. Investigate the MITRE ATT&CK Matrix to understand the Collection activities this file can take, and what the potential impact is to the Executives work mobile phone. Submit the 5 Technique names in alphabetical order.**

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/748f9264f62917944bb6dc1cac39f3028b91612e/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/5..png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/748f9264f62917944bb6dc1cac39f3028b91612e/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/5.1.png)

**6. A junior analyst was handling an event that involved outbound connections to a private address and didn't perform any further analysis on the IP. What are the two ports used by the IP 192.236.198.236?**
- To figure out the port that used by IP 192[.]236[.]198[.]236, I used `cat` to read the `full_ip-port.csv` and grep for the ip address and with the colon `192.236.198.236:`

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/748f9264f62917944bb6dc1cac39f3028b91612e/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/6..png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/748f9264f62917944bb6dc1cac39f3028b91612e/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/6.1.png)


**7. Use the reference to help you further research the IP. What is the C2 domain?**
- The reference we will be using it the IP `192.236.198.236` in virus total.
- Using virus total will inform us is the ip address have malicious activities associatd with it.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/748f9264f62917944bb6dc1cac39f3028b91612e/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/7..png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/748f9264f62917944bb6dc1cac39f3028b91612e/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/7.1.png)

**8. What is the likely delivery method into our organization? Provide the Technique name and Technique ID from ATT&CK.**
- Since we know that IRATA was a malicious file that uses phishing tactics, I would conclude that the delivery method was Phishing T1566
[MITRE ATT&CK](https://attack.mitre.org/techniques/T1566/)


**9. Investigate further and try to find the name of the weaponized Word document, so we can use our EDR to check if it is present anywhere else within the organization.
**
- We can use joesandbox and paste the ID of the payload.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/9..png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/9.1.png)

**10. What is the name of the .JAR file dropped by the Word document?**
- On the same ID of the payload, the `.Jar` file will be shown in the Process Tress Section
- In addition, there is a command line that the `javaw[.]exe,` executable int the @Appdata Directory.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/10.1.png)

**11. A junior analyst was handling an event that involved outbound connections to a private address and didn't perform any further analysis on the IP. What are the two ports used by the IP 192.236.198.236?**
- When there is a outbound connection occuring, this indicates that the malware is attempting to execute or download a second payload for another website.
- I grep for `cat full_urls.csv | grep github | head -n 5`  grithub and then `cat full_urls.csv | grep discord | head -n 5` discord to see if there are related URLs.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/11.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/11..png)



**12. Looking at all export files, how many rows reference this URL? (include duplicates).**
- To display the number and references from the url with the discord domain, I had to read `cat` the file  `full_url.csv`, `grep` and then get grep to count `-c` the numbr of time the URL appeared.
  
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/12.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/12..png)

**13. Based on this information, what is the name of the malware family that is being widely distributed via Discord?**
- To see what is the malware family I had to have grep only out put the discord but also only dispay the 6 colomun to see the number of time the malware appeared.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/13.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/13..png)

**14. We can proactively use indicators from threat feeds for detection, or for prevention via blocking. When it comes to blocking indicators, it is crucial that they are from a reputable source and have a high level of confidence to prevent blocking legitimate entities. How many rows in the full_urls.csv have a confidence rating of 100, and would likely be safe to block on the web proxy?**

- We can grep the number of time `100` was rated for each url.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/14.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/14..png)

**15. An analyst has reported activity coming from an IP address using source port 8001, but they don't understand what this IP is trying to achieve. Looking at full_ip-port.csv in Gnumeric, filter on malware_printable = Unknown malware, and find an IP that is using port 8001. What is the IP address value?**
- We have the port number and the name "Unknown Malware"
- We can use `cat full_url.csv` and `grep :8001` and also `grep Unknown malware`
- This will return the IP address that is associated with the filter.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/15.1.png)

![alt](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/15..png)

**16. Investigating the reference material, what is the CVE ID of the vulnerability that this IP has been trying to exploit? And what is the industry nickname for this vulnerability?**

- In Q15, we can see name log4j that is linked to the CVE-2021-44228.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/15..png)

- So I search for log4j
- and the Industry Nickname is LogShell

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/16.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/86e14377be1bf6464c52a67be0e0b2cc51c02dcb/Easy/SOC/1.%20Foxy%20Write-Up/Foxy/16..png)
