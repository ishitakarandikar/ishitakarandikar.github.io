# Computer Networking

## What is Data Networking?
System of Hardware, Software and Protocols used to move information from one device to another.

## OSI Model
Stands for Open System Interconnect

7.Application Layer<br>6.Presentation Layer<br>5.Session Layer<br>4.Transport Layer<br>3.Network Layer<br>2.Data Link Layer<br>1.Physical Layer<br>

## Encapsulation and the OSI Model

When we want to access a website, that is basically application layer information. Incase of going to a website, we use protocol HTTP[Hypertext Markup Language].
Websites are written in HTMl[Hypertext Markup Language], and we use HTTP to transfer it. When we are working with this, though, these websites tend to be quite large, we need to be able to breakup that website into smaller chunks. So we can successfully get it to the client.
<br><br>
This layer works in conjunction with the transport layer to take that data, break it into smaller pieces, and then add it to a header.<br>
Header is put on the data at the transport layer.<br>
| Source Port | Destination Port | Flags | Seq# | Ack# | Payload[Data] |
