** ACL On CentOS Terminal (NO Extra Firewall Installation Separately)  (Bridged Or NAT Should Be AnyOne,Both Should Match)
On 1st Machine 
sudo yum install squid -y

sudo nano /etc/squid/squid.conf
#To Insert Below Insert your Own Rules Here To Allow Access From Your Client (Line 50)
Save and Close (Only Check Default Rules)

sudo systemctl start squid
sudo systemctl status squid

sudo firewall-cmd --add-port=3128/tcp --permanent  (Squid Port 3128)

On 2nd Machine 
ip -br a (100.10)

Browser Settings From CentOS -->Settings --> Proxy -->  Give 1st Machine Where Squid Is Installed
Port 3128 
Both Should Ping Each Other 

On 1st Machine (Squid)
sudo nano /etc/squid/squid.conf (Line 50)
Enter --> acl comp1 src 192.168.80 (To Allow Or Deny ,Other Client IP) 
acl cdac dstdomain cdac.in
http_access deny cdac comp1  (save and Close)

sudo systemctl reload squid

On 2nd Machine 

Go To Browser and It Will Deny (Error)
