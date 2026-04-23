![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/Vortext.png)

## Jake, a Transgear Corp Incident Response analyst, delves into an alert from Brianna, who flagged unusual activity on her workstation. A week prior, enticed by an email promising Amazon gift cards, Brianna clicked a link, unknowingly downloading malware. This granted attackers access, enabling espionage: capturing credentials, file copying, and eavesdropping on video calls. Days later, Brianna noticed her workstation lagging and received a LinkedIn login attempt notification from an unfamiliar device. Worried, she reported to the IT help desk. Jake now investigates to find and collect IOCs.

**1. What time did the suspected user system/browser connect to the malicious website?**
- In Wireshark, I started by filtering for http get request `http.request.method == GET` and the resutls of foriegn destination IP popped up with the victim source IP. Shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/1.1.png)

- This told me that the IP 45[.]56[.]99[.]101 is the potential adversary IP address. 
- So I then filtered for the ip.dst to see when did the adversary first connected to the website.
 
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/1.2.png)

- The screenshot above is the website that the target was redirected to when they clicked on the malicious document.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/1.3.png)

- The screen shot above shows a syn communication, which is the Source IP is Communicating to the Destination Ip. 
- The time of connection is shown below.
 
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/1..png)

**2. What is Briana’s IP address?**
- In the same filter, we can see Briana's Ip address constantly communicating to the malicious website.
 
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/2.1.png)

- The Answer Shown below

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/2..png)

**3. What is Briana’s MAC/Ethernet address? What is the vendor name for the MAC address?**

- I figured out the MAC adress on Briana's connection by going to conversation filtering, but reverted to just looking at the output information (the middle panel). Shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/3.1.png)

- I then looked up HewletteP and the Vendor was discovered.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/3.2.png)

- Answer Shown Below

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/3..png)

**4. What is Briana’s Windows machine name?**
- I discovered the windows machine name by filtering SMTP (Simple Message Transfer Protocol), Since this evasion occurred through a phishing email. 
- I was able to track down the IP address of Brianna's machine and follow the digital footprints to identifying the "box.net" communicating to the windows Machine. Shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/4.1.png)

- Answer shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/4..png)

**5. What is Briana’s Windows username?**
- In the same filter, looking at the output information in the middle panel, I was able to detect the username of Brianna's Windows Machine. Shown Below

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/5.1.png)

- Answer Shown Below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/5..png)

**6. What email address was the attacker sending data to?**

- Looking and the Wireshark logs, There was a from email with a plain text html output. 
- I clicked on it and seen a strange email address that did not seem legitimate. Shown below

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/6.1.png)

- Answer shown below.

- ![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/6..png)

**7. What type of CPU does Briana’s computer use?**
- In the same filter of the email, I observe the Machine Name that belong to Brianna,
- Following the strings of the output, I seen the CPU type. Shown below

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/7.1.png)

- Answer shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/7..png)

**8. How much RAM does Briana’s computer have—in GBs?**

- In the same output in Q7, I seen the Ram of 32165.83 MB, which round up to about 32 GBs.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/8..png)

**9. What type of account login data was stolen by the attacker?**
-  In the same filter "smtp" I was able to discover Data output and the Data had a size ranging from 615 to 1025 bytes with indicates there information with that network traffic. 
- The screen shot below shows that a Username and a Password was stolen by the adversary.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/9.1.png)

**10. What are the username and password related to the Amazon account?**
- In the first data set, I observe that an amazon account was signed in with the username and password that was stolen by the adversary. Shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/10.1.png)

- Answer shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/10..png)

**11. What username did Briana use to authenticate to webhostbox[.]net? Can you decode it?**
- Looking at the smtp traffic in acsending order, I noticed the webhost[.]box and it was talking to Brianna's Windows machine.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/11.1.png)

- Below was a encrypted base64 hashvalue that needed to be decrypted. 
- I could have went the easy route and used cyberchef, however, I decrypted it through the terminal. Shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/11.2.png)

- Answer shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/11..png)

**12. What password did Briana use to authenticate to webhostbox[.]net? Can you decode it?**
- In the same filter, there was a password that was encrypted in base64.
 
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/12.1.png)

- I also decrpyted it to reveal the password. Shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/12.2.png)

- Answer shown below

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/3709a77d81c2598ae763bb7cf01e77616d40696e/Easy/SOC/3.%20Vortex/Vortex%20Img/12..png)
