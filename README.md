# Wifi connection to Marcel

Marcel provides its own open wifi hotspot called "Marcel0". 
On this interface, the robot has the static IP address 192.168.1.1
You can open a ssh connection to the robot by typing (the default password is marcel)
````
ssh marcel@192.168.1.1
````

# Ethernet (wired) connection to Marcel

You can also connect to the robot using an ethernet cable. 
One end goes to your computer, and the other one to the ethernet plug of the robot.
Then you have to configure your computer's interface :
````
sudo ifconfig eth0 192.168.2.2
````
And then you can directly connect through ssh (note that the IP address is not the same)
````
ssh marcel@192.168.2.1
````

# Accessing the Internet from Marcel through a computer Internet connection

Here we assume you connected the robot to your computer using an ethernet cable (eth0), and have an available internet connection on the wifi interface wlan0

On your computer, edit /etc/sysctl.conf and add the following line:
````
net.ipv4.ip_forward=1
````
To enable IP masquerading, enter following set of commands in the computer's terminal:
````
sudo iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT
````
If you want to do the other way round (forwarding a wired internet connection through the robot's wifi AP), do the converse:
````
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i wlan0 -o eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o wlan0 -j ACCEPT
````
