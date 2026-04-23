![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/Nano.png)

### The SOC detected unusual network activity from a critical server. Analysts believe the attack was by Nano by identifying these beaconing patterns and obfuscation techniques. Nano is a newly discovered hacking group that focuses on stealth and persistence. It uses custom obfuscated protocols that mimic legitimate traffic, making it challenging to detect using standard network monitoring tools. Your job is to understand and identify these patterns by looking through captured logs, which will help defend against such advanced threats in the future.

**1. Looking at the RITA HTML Report (Log_2V), what is the IP of the attacker’s C2 server? Provide the number of connections as well.**
- This is a html file that I had to analyze.
- After doing some research, I discovered in order to appropriate analysis, I had to specify grep to only grap the table data "<td>" output.
-  In order to determine the IP of the adversary that exfiltrated the server, I used the `grep` command and filtered out only the first 30 outputs and seens there was a repeated connection with the same IP address. 
- Command Used: `grep -A 5 "<td>" beacons.html | head -n 30`
- **What is Beacons?**
	- In web development, beacons are designed to handle network activity without interfering with the user. 
- **What is `-A 5`?**
	- `-A 5` tell grep to display lines that matches the search terem, including the 5 lines that come after it. 
- **What is `head -n 30`?**
	- This is when we are telling linux to only display the first 30 lines of the output. If not, grep will dispaly the entire output.

  ![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/1.1.png)

- Oberserving the output of the command, I seen an IP that was repeatedly shown which was IP 138[.]197[.]117[.]74 and the port the adversary was connected through to perform their malicious activity; which was Port 8440.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/1..png)
		
**2. What is the cloud infrastructure being used for the C2 server?**
- Since I discovered the IP address, I can go to VirusTotal and search the IP address to see if there any returns. 
- Shown in the screenshot below, the C2 connection may been by Digital Ocean LLC.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/2.2.png)

- The Basic Properties shows the Network (which is the IP I discovered). the Autonomous System Number "14061", and the Autonomous System Label "Digital Ocean"

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/2.1.png)

**3. Looking at the RITA User Agent report, what is the system that corresponds to the connection count in Q1?**
- Here I had to unwrap the user-agent and use a similar command that was uses in Q1 but pipe and grep "user agent" 
- the output is shown below.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/3.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/3..png)



**4. Let’s look at Log_1D, what is the low-profile subdomain with the absurd amount of requests? Provide the number of requests as well.** 
- By time I got to Q4, I realized I can use firefox to provide and structured layout of the html files. by using `firefox "directory"` and went to the DNS file and seen the Domain and the subdomain of the absurd amount request.

 ![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/4.1.png)
 
- In addition, just to verify, I did the manual search the sub domain in the terminal. 
**- what is `- B 2`?**
	- This tell grep to print out 2 line before the preferred search.
- I see the Domain; which is `nanobotninjas.com`
- Following that also saw the subdomain and the request.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/4.2.png)

- Notice that the Domain and the Subdomain have a similar request.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/4..png)

**5. In the Zeek logs (Log_1D), we can see a large number of DNS TXT record requests for a private IP for the subdomain found in Q4.** 
- Looking in the structured layout by firefox, I seen numerous rewuest by the same IP "10[.]234[.]234[.]105" that is also associated with the subdomain "cat.nanobotninjas.com"

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/5.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/5..png)

**6. This is an unusual activity. To avoid cached results on the intermediate DNS server(s), a certain value prepended to the subdomain is being changed. What numeral system is being used for the value that changes?** **It seems like a Base 16 numbering system.**
- Base 16 numering system is usually related to hexidecimal and does not exceed the letter f. 
- In the screen shot, below we can see the hexidecimal and the constant change of it so it does not get detected by the DNS server.

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/6.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/6..png)


**7. Judging from the logs (Log_1D), what tool was the attacker using? A tool to help C2s channel over the DNS protocol.** 
- Since the adversary was utilizing DNS to perform their malicious tool "cat.nanobotninjas.com", I did a little research and search for C2 dns tactics with "cat" and discovered the information shown below.
 
![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/7.1.png)

![alt text](https://github.com/DJackson-BlueTeam/BlueTeamLab.Investigations-Write-Ups/blob/b791ad7c60c71b6f83439ca0dae48c08254a2508/Easy/SOC/2.%20Nano/Nano%20Img/7..png)
