# Computer Networking


## OSI Model
Stands for Open System Interconnect

7.Application Layer<br>6.Presentation Layer<br>5.Session Layer<br>4.Transport Layer<br>3.Network Layer<br>2.Data Link Layer<br>1.Physical Layer<br>

## Encapsulation and the OSI Model

When we want to access a website, that is basically application layer information. Incase of going to a website, we use protocol HTTP[Hypertext Markup Language].
Websites are written in HTMl[Hypertext Markup Language], and we use HTTP to transfer it. When we are working with this, though, these websites tend to be quite large, we need to be able to breakup that website into smaller chunks. So we can successfully get it to the client.
<br><br>
This layer works in conjunction with the transport layer to take that data, break it into smaller pieces, and then add it to a header.<br>
Header is put on the data at the transport layer.<br>

SEGMENT
| Source Port | Destination Port | Flags | Seq# | Ack# | Payload[Data] |
| ----------- | ---------------- | ----- | ---- | ---- | ------------- |


The Transport Layer, since it is setting up a session between out client and our server, we have speceific information in there to allow that to happen.<br>
Flags - General information about what is happening in the transaction.<br>
Seq#, Ack# - Keep track of how much data has been sent and received.<br>
Segment - chunck of data, with a transport layer header [TCP Header]
<br>
This info, allows client and server to set up a session and keep track of what data has been sent and received.
<br><br>
In order to know where we are sending this data, we need to tell it what the source and destination IP addresses are.
So we can know where on the internet or on a network the server and client are.
<br>
So, we take our transport layer information which is going to keep that sesion between our endpoints going, then send it down to network layer.
<br>
<br>
Segment becomes the payload of our network layer, and then we add this header, we add Source IP Address, Destionation IP Address, a value called TTL[Time to Live] and other.<br>
PACKET
| Source IP Address | Destination IP Address | TTL | Other | Payload[Segment] |
| ----------------- | ---------------------- | --- | ----- | ---------------- |

Packet - chunck of data with the network layer header [IP Header]
<br>
This header helps us know what two endpoints on the internet or any network, we are going to send this information to.
<br><br>
Now, in order to get our packet to go from one device to next[from workstation to switch, from switch to router, from router to cable modem, from cable modem out to the internet, and all of the hops that go along the internet], we need a Data Link Layer Header.
<br>
So, we send our network layer packet down to the data link layer and put it in a frame.
<br>
FRAME
| Source MAC Address | Destination MAC Address | Layer 3 Protocol | Payload[Packet] |
| ------------------ | ----------------------- | ---------------- | --------------- |

Frmae - chunk of data, with a DLL Header[Ethernet Header]
<br><br>
We often use Ethernet Frame when we are sending data from our workstation to the switch, from switch to router, from router to cable modem.
<br>Once we get to cable modem, we are going to use different protocols there which require a different frame.<br>Take out this frame and put it into new frame. This happends consistently throughout the transaction as moving the data accross the Internet.<br>
Packet will remain same,frame header will change as it goes from segment to segment to segment.
<br>
In Ethernet Frame, data part can have MTU[Maximum Transmission Unit] for Ethernet.
For Ethernet that is typically 1500 bytes.
<br><br>
Once we have our frame constructed with the source MAC address, destionation MAC Address and layer 3 protocol that we are using, we can then take that frame and send it down to the physical layer.
<br><br>
In physical layer, it will get converted into 0's and 1's and then to signals, signals could be light signal that we send accross fiber optics, it could be an electrical pulse that we send accross a copper wire or it might be electromagnetic signal that we send with wireless.<br><br>
# Application Layer Protocols
## Transferring Data
Whenever we go on our workstation and ask for a website "www.google.com", we are asking an HTML document to be tranferred from the server to our workstation.
<br>
HTTP or HTTPs are used. These protocols allow us to transfer HTML document between server and client.
<br>HTTPs
<br>->SSL[Secure Socket Layer] 
<br>->TLS[Transport Layer Security]
<br>These are literally the same protocol, they changed their name around 2000. These are used to provide encryption when we are using HTTPs.
<br><br>
Not all files that we transfer when we are working with the data network are going to be an HTML files via website. Sometimes we have files on our wokrstation that need to get transferred to a server or to a network device. Maybe there are some specific files that are not HTML files on a server that we need to access and download to our workstation.
<br>
So, when we are working with File Transfer, we need to have several File Transfer Protocol.
<br>->FTP [File Transfer Protocol] [Port no.: 20 & 21]
<br>->sFTP [Secure File Transfer Protocol] [Port no.: 22]
<br>->TFTP [Trivial File Transfer Protocol] [Port no.: 69]
<br>
FTP is somewhat messy protocol, especially if you have to use it through firewall.
<br>
sFTP is FTP with encryption. It operates on port 22 on which operates another utility that use called SSH or Secure Shell. The reason that it is the same port number is that we are actually creating and SSH connection and then using FTP on top of it.
<br>
TPTP can be used to transfer small files[OS File]
<br>
There is one more from Microsoft called SMB[port: 445] which stands for server message block.
If you have shared drive, shared network drive mounted on your workstation, typically SMB is used. It allows us to mount a drive on out windows workstation or other workstation.
With SMB, we can just browse that drive as if it were a local drive on our workstation, yet it is a network drive.<br><br>
## E-mail
It is a way of transferring a file from a server to a client again. We just use different format, in this case, we use email format.
<br>
There are three methods that we need in order to transfer email.
<br>->POP3 [Post Office Protocol version 3]
<br>->IMAP [Internet Message Access Protocol]
<br>These two are for receiving mail from server to client.
<br>->SMTP [Simple Mail Transfer Protocol]
<br>This is for sending mail from client to server.
<br><br>
So, when we are configuring email clients, usually we need to either POP or IMAP, as well as SMTP.
The way we configure them has changed pretty drastically over time.
MAil services like gmail, outlook, yahoo and others have changed the way we configure our devices for email. We just put in username and password, it automatically configures all the protocols for us. These protocols have two transport layer port numbers they can use.
<br>->POP3 : 110(unencrypted), 995(encrypted)
<br>->IMAP: 143(unencrypted), 993(encrypted)
<br>->SMTP : 25(unencrypted), 465(encrypted)
<br><br>

## Authentication

Your settings, desktop, mapped drives and what not will all show up on your client workstation, regardless of which one you are using.
Two protocols are used for this.
<br>->LDAP[Lightweight Directory Access Protocol] (port: 389)
<br>->LDAPs[LDAP Secure] (port: 636)
<br>
We put username and password on the client, we send it to the server, then server will then send a token back saying "yes, this user is authenticated". After that, server may send additional information that has user settings and what not for the client. 

## Network Services
### DHCP [Dynamic Host Configuration Protocol]
Responsible for giving your wokrstation an IP Address when it first is plugged into the network. IP are an identifier for your device on the network. Operates at the network layer.
<br>Instead of having users to configure this or configure them manually, we often times will use a DHCP server to do this.
Cable modem or cable router or wireless access point, all these devices have the capabilities to offer a DHCP server. That way, when you turn on your device or you connect it to the wireless network or you plug into the wired network, it automatically gets and IP address.
<br><br>
So, when we plug-in the client into the network, we are going to send out a discover message. The DHCP server then is going to reply with something called an offer message. Offer message is going to have a IP address, subnet mask, default gateway, DNS server, possibly some other information as well.
Client will respon back and accept that offer. Server then will respond back with acknowledgement.
<br><br>
Port : 67/68
### DNS [Domain Name System]
Also called name server. Allows us to take names like ishita.com, google.com.
Allows us to translate the name google.com into and IP address that we actually use to transfer information at network layer.
<br>When we search www.google.com, it will first send a message to DNS server asking the IP of this domain name and then DNS server will reply with IP address of google.com.
<br><br>Port : 53 [Not encrypted] 443 [encrypted]
<br>Command : nslookup google.com

### NTP [Network Time Protocol]
It is a device on the network that has a clock on it.
That clock is usually synchronized with some government run atomic clock, so it has very precise time.
<br><br>
So, our server on the network would go retrieve the precise time from some atomic time some place on the internet and then synchronize it locally so that when local client need to know how to set their clocks, they can send a message to our sever, NTP server, NTP will reply back with the time.
Now the client can set its time. This will inclue the date on the workstation.
<br><br>
NTP is important because services like encryption will often times validate whether or not a server that we are connection to is valid by checking a certificate and the certificate is often only valid for a specific period of time, so we need some kind of clock to validate that the time of certificate is okay to use.
<br><br>
Also, we have log messages that are stored on clients, servers, network devices, firewalls etc. Those logs need a precise time so that if an event occurs whether it be a technical or security event, we know exactly the right time that is happening so we can cordinate with other devic logs on our network.
<br><br>
Port : 123

## Network Management
Often times we have a device on our network, that we are going to manage from central location.
<br>Two utilities can be used for this.
### Telnet/Secure Shell
<br>->Telnet [Not encrypted] [Port : 23]
<br>->Secure Shell [Encrypted] [Port : 22]
<br>So, this is a way to actually use a command-line interface to access devices around the network, whether it be a server, like a linux server, could be a router or a switch or a firewall or multitude of other devices that we can access with.
<br>
So, on our network administration workstation , we might SSH to a router, or a switch or a server here, or even a firewall. The devices that we are SSHing are going to be the server.The device weare SSHing from becomes our client.

### SNMP [Simple Network MAnagement Protocol]
It is a way of devices to send information back to a centralized information like log messages or information about port up and down, or maybe some other event on our device that we configure to tell our SNMP server about. All these devices sending information about SNMP are client. These clients can report in to the server what is happening with them, or the server can send out message to all the devices to tell it all the information they have about their devices that has SNMP number assigned to it.
<br>These numbers are MIB [Management information base].
<br>These information can be sent out to SNMP sever, this server can them use that information to populate a table of all the events happening on the devices.
<br><br>SNMP Trap - When an event both good or both happens, it can send a message to SNMP server to tell it the event that happened. With the central server, we can configure the central server to send out alerts to the network administrator telling them to fix it.
<br><br>Port : 161 & 162
### Syslog
Mechanism to take the logs on each one of our devices and send them to a centralized syslog server so thay can be correlated with other events on our network.
<br> Port : 514
### RDP [Remote Desktop Protocol]
Allows us to access the graphical user interface of devices on our network when we are not local.
<br>Port : 3389

## Audio/Visual Protocols
Allows us to either have voiceover IP phone calls or video phone between two organizations.
### H.323
Allows for video and audio communication between two devices.
### SIP [Session Initiation Protocol]
Port : 5060 or 5061
<br>Used to transfer voice when we are using our voiceover IP phone to a voice gateway which gets us out of the rest of the telephone system so we can make calls. 

## SQL Databse Protocols 
SQL is a protocol named Structured Query Language and it is actually server[SQL server], language to access ata on that server, protocol[used to communicate accross network to access that database].

# Transport Layer Protocols
This layer is responsible for building a session and maintaining a session between the two endpoints i.e client and server on a data network.
## TCP [Transmission Control Protocol]
Protocol that initiate communication between two devices.<br>
It uses the three way handshake, very precise process that the client and server need to go through before we can send information.
<br>
SYN - First message to the server indicating that client wants to start a conversation.
<br>SYN+ACK - Server replies back. This alerts the client that server is up for the conversation.
<br>ACK - Client responds back with acknowledgement.
<br><br>When the conversation is all done and the website has finished transferring, client will send a message to disconnect.
<br><br>
The four way disconnect, to disconnect the client sends a message to server.
<br>FIN - client wants to disconnect.
<br>FIN+ACK - server acknowledges.
<br>FIN - server sends out fin to client to disconnect.
<br>FIN+ACK - client acknowledges.
<br><br>
TCP RESET - This can be sent from either web server or client, and when TCP reset happens, communication is over.
It can also come from client.
Also, if there is some device in the middle like firewall, that is paying attention to the conversation, watching nefarious activity, it can also send a reset as well.

## UDP [User Datagram Protocol]
Works similar to TCP in that we are going to set up a session between two devices.
However, this time, we are just going to start talking.
Client will say to server to send data. And then server, if it recieves it and it is able to, it will send the data to the client.
<br>There is no mechanism to make sure that the data sent was actually recieved. There is no three way handshake, there is mo four way disconnect, there is no reset, no reliable communication, no sequence number, no acknowledgement numbers.
<br>Used for efficient data transfer.

# Transport Layer Addressing
## Port Numbers
There are two sets of port numbers<br>0-65535
<br>->Server Port Numbers or Well Known/Registered Port Numbers
<br>->Client Port Numbers or Ephemeral Port Numbers
<br>
<br>
### Well known [0-1023]
Typically for applications
<br>HTTP - 80
<br>HTTPs - 443
<br> FTP - 20,21
<br> SSH - 22
<br> Telnet - 23
<br>
### Registered [1024 - 49151]
These are for customer applications "official and un-official". There are many games that would use registered port numbers.
### Ephemeral [49152 - 65535]
Used by client or the PC side of this in order to identify the session that they are sending.

# Network Layer
## IP Addressing 
Mechanism for us to be able to communicate accross long distance on the internet. IP address is a unique identifier for your device on the public internet. There are routing tables on the public internet that allow anybody to communicate with your IP address.<br>Generally, we find out IP address of device by DNS.<br>
Example - 203.0.113.10 [32 bits]
<br> How to identify network portion and host portion?
<br>->Classless Addressing
<br>->CLassfull Addressing

### Classless Addressing
We can identify network portion and host portion by subnet mask.<br>
255.255.255.0
<br>11111111.11111111.11111111.00000000
<br>1's are network portion 
<br>0's are host portion

### Classfull Addressing

| class | IP Range                    |
| ----- | --------------------------- |
|   A   | 0.0.0.0 - 127.255.255.255   |
|   B   | 128.0.0.0 - 191.255.255.255 |
|   C   | 192.0.0.0 - 223.255.255.255 |
|   D   | 224.0.0.0 - 239.255.255.255 |
|   E   | 240.0.0.0 - 255.255.255.255 |

<br>Class A -> N.H.H.H
<br>Class B -> N.N.H.H
<br>Class C -> N.N.N.H
<br>Class D -> N.N.N.N

### IP Address Type
#### Network Address
Identifier for a group of devices. Also known as Network Prefix. <br>Has all 1's in the network portion and has all 0's in the host portion.

#### Broadcast Address
Identifier for all devices on a network.<br> Has all 1's in the host portion.

#### Host Address
Identifies unique devices on the internet.
<br>Has some combination of 1's and 0's in the host portion.
 Neither all 1's or all 0's.

 ### Private IP
 Prior to 1994, there were no private IP addresses. Because we were running out of IP addresses, we changed to classless addressing, which gave us the subnet mask. And private IP address ranges were also introduced.
 <br>Any organization could use these private IP addresses. They would not be routed publically on the internet. This allowed organizations to set up very large IT infrastructure and very large networks using IP addressed without confilicting with other organizations. This really saved the internet and allowed it to expand and grew as much as it did.
 <br> Three ranges of address ->
 <br>A   10.0.0.0    - 10.255.255.255
 <br>B   172.16.0.0  - 172.255.255.255
 <br>C   192.168.0.0 - 192.168.255.255
 <br>This is all documented in Request for comments or RFC.
 <br>APIPA =>162.254.0.0 /16
 <br>Loopback => 127.0.0.1 => localhost
 <br>
 
#### NAT [Network Address Translation]
It allows us to take these private IP addresses, allows us to route out on the public internet by translating it into public IP address for a moment while it routes accross the public internet and then it gets translated back in to a private address when it reaches our internal network.
 ### Subnetting
 ## IPv6 Addressing
 IPv4 size => 32 bits long => 4 octets
 <br>IPv6 size => 128 bits long => 32 nibbles => 8 hextets
 <br>Example : 2001:0DB8:0002:008D:0000:000:00A5:52F5
 <br>In IPv6 we typically use /64 mask on everything.

 <br><br>To make it simpler=>
 <br>->Eliminate leading 0's
 <br>  2001:DB8:2:8D:0:0:A5:52F5
 <br>->Eliminate series of 0's with :: [can only be done once]
 <br>  2001:DB8:2:8D::A5:52F5

 <br><br>
 When we are communicating between devices on the internet, Internet is full of routers that can route IPv6. We are using IPv6 unicast addresses. These addresses are used for global communication.
 <br>Every single devie in our network is going to have two IPv6 addresses.
 <br>-> IPv6 Link Local Address [switch]
 <br>-> Global Communication

 ### Ipv6 Acquisition
 
#### SLAAC
Stateless Address Auto-Configuration. This is a feature that does not exist at all in IPv4.<br>
Let us say router has IP of 2001:DB8:4:A::1. This router is going to periodically send router advertisement. In this, it is going to adverstise what network this particular segment of the network is, so it is going to advertise the network address, so the IPv6 netowkr address as well as some other info that our endpoints of our workstation can use to automatically configure themselves without asking.<br>
So, after sending router advertisement, out in the network. That happens periodically, so we don't have to wait for a new device to come on. That router is just sending those messages out regularly. Workstation will then automatically configure its address.
<br> It knows it has network 2001:DB8:4:A:: with a /64 mask. <br>And now the way the interfacce identifier portion is configured depends upon the Operating System.
<br>If system is windows, it is going to choose random 64 bit interface identifier.
Randomly assign next 64 bits information to become interface identifier.<br>Example - 2001:DB8:4:A:67835FA1:7B4C:A42A /64
<br> It will create two of these [global and link local]. We can configure more than two addresses besides our link local addresses on those interfaces. When windows chooses two of them and applies them to the interface.
<br>If system is Unix/Linux/Mac, modifies EUI-64 address is used.
We are oging to take the MAC address of our network interface card. Split it into two and then add FF:FE in the middle. This will make the address 64 bits long.
<br>Then we take 7th bit in that list and we flip it, and then we convert it back to hexadecimal, now this becomes the interface identifier.
<br>MAC => 000C:29:FC:70A5
<br>=>000C:29:FF:FE:FC:70A5
<br>=>020C:29:FF:FE:FC:70A5
<br>Problem with this is, if we are using MAC address in our interface identifier portion, anybody on the public internet that is recieving traffic from us will know our MAC address.
#### DHCP
Similar to IPv4 DHCP. We have DHCP server on our network. Wen our device comes online, it is going to send out advertisement needing the address. DHCP server will reply with one.
<br>In order to do that, we have set our router up to turn off SLAAC. This allows for a lot more control, it allows for shorter address, especially in our internal network.
### IPv6 Tunneling
One of the problems with IPv6 is not everywhere supports it, not all ISP have full support of it, it is not used globally the way IPv4 is.
<br>Say, we have some IPv6 internet here locally and we want to connect it to a device far away that has an IPv6 address.
<br>We have to find a way to get our IPv6 internet traffic accross IPv4 internet, and those two are not backwards compatible with each other.
<br>So, we build a tunnel.
<br>Tunnel is a mechanism where we can take an IPv6 message, an IPv6 packet and put it inside of IPv4 packet, move it accross IPv4 internet to other device where it will be pulled out of the IPv4 packet and then put back into and IPv6 message and it can be forwarded.
<br>This tunneling allows our IPv6 device to traverse the IPv4 internet and accross a device that has an IPv6 address.

## Network Services
### NAT [Network Address Translation]
It is a network layer function, we need this to make the internet grow how we use it today.
Private adresses which are in the private range, can not be routed on the public internet.<br>
If we send a message into the public internet with a destination of any of these private addresses. Internet will just throw it away. All these routers on the internet are programme to dicard messages with a destination address of one of these ranges.
<br>We send our message from our workstation to the router, we have configured to do our NAT.
Router will remove source IP from the packet and store it in a table. Place sourse IP with IP of our router which is a public routable IP address. We then forward that mesage on to the internet. Now while recieving messages, destination becomes the IP of the router, once our router recieves that message it looks up in the little table that it has set up and replaces the outside public IP with the inside IP address and forwards it to our workstation.
<br>This is how NAT works. NAT is swapping out addresses in our packets in order to make those messages routable on the public internet. This is the primary use of it.
### DHCP
This is an application layer protocol. We need a DHCP server, a device on our network that can hand out addresses to the clients as they come online.
<br>Large organizations have a dedicated DHCP server that hands out the addresses for hte entire organizations. <br>
In our home network, DHCP server is built in to the router.
<br>When we configure our device, we configure our IP properties here and say obtain an IP automatically, this is going to use DHCP to get that address.
<br>Our DHCP server then is set up with a scope. Scope is the parameters of DHCP. We hace range of excluded addresses, often times we put excluded addresses in our DHCP scope that hte server does not hand out these addresses, and we can use them either to statically assign to devices or set up a reservation that is specific for the device.
Usually, these excluded addresses are reserved for static configuration, for things like servers or printer or other storage hardware that may not support DHCP very well.
We need to include our gateway in the scope so that our device know where the default gateway is so that when we are trying to send traffic off of our subnet, our workstation know how to route that traffic appropriately.
<br>We need to configure a DNS server.
<br>Then we have a lease time, amount of time that our workstations are going to hold on to that IP address before asking for a new one.
<br>Now, we need an address, our workstation sens out a discover message, and this message is oging to be recieved by the HCP server, this server is going to make and offer to the workstation, so that it then becomes the IP address of the workstation. The workstation will request this address, and server will send back message of acknowlesgement.
