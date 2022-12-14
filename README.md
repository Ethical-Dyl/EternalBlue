# EternalBlue
This is a writeup on how to exploit the ever popular RCE vulnerability.


# Initial Enumeration 

Starting with an nmap scan I targeted the windows instance with the following syntax:
  "nmap -T4 -v -sC -sV -sT --script vuln $IP"
  
The scan revelead the following information:

<img width="640" alt="image" src="https://user-images.githubusercontent.com/66540055/193915411-ff34d4ba-3bca-4801-bd7e-35190936804e.png">

Woot! Right off the bat I see that the machine is vulnerable to MS17-010, which is a SMB RCE exploit. Which in layman terms is a Server Message Block remote code execution exploit. 

# Initial Foothold

Using the exploit/windows/smb/ms17_010_eternalblue module I defined the RHOSTS and began the exploit which provided my initial foothold into the system:

<img width="754" alt="image" src="https://user-images.githubusercontent.com/66540055/193917585-96b36ab4-8e50-4ee6-8918-249d5ef66844.png">

# Aquiring hashes
Now that I have my foothold into the system I used the hashdump command in my meterpreter session to query the passwords stored in the SAM database:

<img width="693" alt="image" src="https://user-images.githubusercontent.com/66540055/193964503-8a48b95f-09b4-4795-b219-35d10da312ea.png">

# Passing the hash

Now that I have the hashes of the users of the machine I will attempt to pass the hash aka log on to the machine with the hash of a user, for this I will be using the Metasploit module 'windows/smb/psexec' after setting all the parameters I will now run the exploit:

<img width="720" alt="image" src="https://user-images.githubusercontent.com/66540055/193964677-349f6fe1-3ab5-4535-873b-11ef889acde4.png">

Awesome! It works and I now have another foothold into the system without having to run a hefty exploit. 

Thanks for reading! I am looking to do a livestream here soon of some live CTF hacking, if there are any reccomendations let me know!

