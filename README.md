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
