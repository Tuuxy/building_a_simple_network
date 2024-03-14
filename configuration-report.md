Cisco Packet Tracer - Build a Simple Network


For this project :

- Added 3 computers (PC-PT)
- Added 1 switch (2960)
- Added 1 router (Router-PT)

I started by linking the 3 computers to the switch like this :

PC1 to switch : fastethernet0 to fastethernet0/1 using copper straight-through
PC2 to switch : fastethernet0 to fastethernet0/2 using copper straight-through
PC3 to switch : fastethernet0 to fastethernet0/3 using copper straight-through
switch to router : fastethernet0/24 to fastethernet0/0 using copper cross-over

I added notes for the IP configurations so that my work would stay organized and I attributed them as such : 

Router : 192.168.1.1 255.255.255.0 - Gateway
PC 1 : 192.168.1.10 255.255.255.0
PC 2 : 192.168.1.11 255.255.255.0
PC 3 : 192.168.1.12 255.255.255.0

Then I went to the router CLI to configure the connections of the network and I typed those command:

router> enable
router# configure terminal
router# interface fastethernet0/0
router# ip address 192.168.1.1 255.255.255.0
router# no shutdown
router# exit

Then I went to the PCs ip configuration panels and I set them up as explained in my notes: 

PC 1 : 192.168.1.10 255.255.255.0 - 192.168.1.1 as Gateway
PC 2 : 192.168.1.11 255.255.255.0 - 192.168.1.1 as Gateway
PC 3 : 192.168.1.12 255.255.255.0 - 192.168.1.1 as Gateway

Then I tested the connections by pinging each hosts :

-- PUT PING SCREENSHOTS -- 

All pings succeeded ! 

Now, to simulate internet I create a different network.

I added a second router, the "google" router, I connect it to a switch by copper cross-over cable and connect a server to the switch by copper straight-through.

On the google router CLI i did :

router> enable
router# configure terminal
router# interface fastethernet0/0
router# ip address 192.168.2.1 255.255.255.0
router# no shutdown
router# exit

Then I configured the server as such :

192.168.2.10 255.255.255.0 - 192.168.2.1 as Gateway - 192.168.2.10 as DNS address

I activated the DNS service and I assigned : 

google
google.com
www.google.com 

as A Record to the ip 192.168.2.10

I also activated the http service and deleted all the default pages except index.html. I used chatgpt to generate a google-like page and uploaded it.

Then I connected the 2 routers together with a copper cross-over cable.

On hacker's poulette's router : 

router> enable
router# configure terminal
router# interface fastethernet1/0
router# ip address 192.168.0.2 255.255.255.0
router# no shutdown

On google's router: 

router> enable
router# configure terminal
router# interface fastethernet1/0
router# ip address 192.168.0.4 255.255.255.0
router# no shutdown

Then I just had to create the ip routes on the 2 routers like that :

Hacker's Poulette's router:
ip route 192.168.2.0 255.255.255.0 192.168.0.4

Google's router:
ip route 192.168.1.0 255.255.255.0 192.168.0.2

Now I can verify that Hacker's Poulette's network is connected to the internet by accessing the site www.google.com on any of their PC, and voilà.





