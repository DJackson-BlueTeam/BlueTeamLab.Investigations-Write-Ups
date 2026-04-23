![[Vortext.png]]
Jake, a Transgear Corp Incident Response analyst, delves into an alert from Brianna, who flagged unusual activity on her workstation. A week prior, enticed by an email promising Amazon gift cards, Brianna clicked a link, unknowingly downloading malware. This granted attackers access, enabling espionage: capturing credentials, file copying, and eavesdropping on video calls. Days later, Brianna noticed her workstation lagging and received a LinkedIn login attempt notification from an unfamiliar device. Worried, she reported to the IT help desk. Jake now investigates to find and collect IOCs.

Q1) What time did the suspected user system/browser connect to the malicious website? 

- In Wireshark, I started by filtering for http get request `http.request.method == GET` and the resutls of foriegn destination IP popped up with the victim source IP. Shown below.
- ![[1.1.png]]
- This told me that the IP 45[.]56[.]99[.]101 is the potential adversary IP address. 
- So I then filtered for the ip.dst to see when did the adversary first connected to the website. 
- ![[1.2.png]]
- The screenshot above is the website that the target was redirected to when they clicked on the malicious document. 
- ![[1.3.png]]
- The screen shot above shows a syn communication, which is the Source IP is Communicating to the Destination Ip. 
- The time of connection is shown below. 
- ![[1..png]]
Q2) What is Briana’s IP address? (Format: IP Address) _(2 points)_
- In the same filter, we can see Briana's Ip address constantly communicating to the malicious website.  
- ![[2.1.png]]
- The Answer Shown below
- ![[2..png]]
Q3) What is Briana’s MAC/Ethernet address? What is the vendor name for the MAC address? (Format: MAC, Vendor Name) _(2 points)_

- I figured out the MAC adress on Briana's connection by going to conversation filtering, but reverted to just looking at the output information (the middle panel). Shown below. 
- ![[3.1.png]]
- I then looked up HewletteP and the Vendor was discovered. 
- ![[3.2.png]]
- Answer Shown Below
- ![[3..png]]
Q4) What is Briana’s Windows machine name? (Format: Machine Name) _(2 points)_

- I discovered the windows machine name by filtering SMTP (Simple Message Transfer Protocol), Since this evasion occurred through a phishing email. 
- I was able to track down the IP address of Brianna's machine and follow the digital footprints to identifying the "box.net" communicating to the windows Machine. Shown below.
- ![[4.1.png]]

- Answer shown below. 
- ![[4..png]]

Q5) What is Briana’s Windows username? (Format: username@domain.tld) _(2 points)_

- In the same filter, looking at the output information in the middle panel, I was able to detect the username of Brianna's Windows Machine. Shown Below
- ![[5.1.png]]
- Answer Shown Below.
- ![[5..png]]
Q6) What email address was the attacker sending data to? (Format: name@domain.tld) _(2 points)_

- Looking and the Wireshark logs, There was a from email with a plain text html output. 
- I clicked on it and seen a strange email address that did not seem legitimate. Shown below
- ![[6.1.png]]
- Answer shown below.
- ![[6..png]]
Q7) What type of CPU does Briana’s computer use? (Format: CPU Name) _(2 points)_
- In the same filter of the email, I observe the Machine Name that belong to Brianna,
- Following the strings of the output, I seen the CPU type. Shown below
- ![[7.1.png]]
- Answer shown below
- ![[7..png]]
Q8) How much RAM does Briana’s computer have—in GBs? (Format: XXGB) _(2 points)_

- In the same output in Q7, I seen the Ram of 32165.83 MB, which round up to about 32 GBs.
- ![[8..png]]
Q9) What type of account login data was stolen by the attacker?
-  In the same filter "smtp" I was able to discover Data output and the Data had a size ranging from 615 to 1025 bytes with indicates there information with that network traffic. 
- The screen shot below shows that a Username and a Password was stolen by the adversary.
- ![[9.1.png]]

Q10) What are the username and password related to the Amazon account?
- In the first data set, I observe that an amazon account was signed in with the username and password that was stolen by the adversary. Shown below. 
- ![[10.1.png]]
- Answer: ![[10..png]]
Q11) What username did Briana use to authenticate to webhostbox[.]net? Can you decode it? (Format: Username) _(2 points)_

- Looking at the smtp traffic in acsending order, I noticed the webhost[.]box and it was talking to Brianna's Windows machine. 
- ![[11.1.png]]
- Below was a encrypted base64 hashvalue that needed to be decrypted. 
- I could of went the easy route and used cyberchef, but I decrypted it myself through the terminal myself. shown below
- ![[11.2.png]]
- Answer shown below
- ![[11..png]]
Q12) What password did Briana use to authenticate to webhostbox[.]net? Can you decode it? (Format: Password)
- In the same filter, there was a password that was encrypted in base64. 
- ![[12.1.png]]
- I also decrpyted it to reveal the password. Shown below. 
- ![[12.2.png]]
- Answer shown below 
- ![[12..png]]