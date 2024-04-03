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
## Application Layer Protocols
# Transferring Data
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
# E-mail
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

# Authentication






