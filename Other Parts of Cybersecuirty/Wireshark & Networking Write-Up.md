I wanted to learn more about DNS, TCP, packets, and networking on Linux so I made sure to install wireshark and ran through a little exercise in order to learn better.

The first thing I did was use Wireshark in order to capture all of the traffic coming unto my ethernet port on my computer. So I captured all the traffic and will go through each explaining what I got and why.

### DNS
Looking through the DNS packets, I can see the names of certain websites that I either queryed and then got a reponse from being stuff like brave.com, chatgpt, gutenberg in order to get a pdf. I can physically see the bytedata that stores that info. With sites like ssl.gstaic.com or www.scripts.com or archive.org.  Whilst in the DNS packet, I can see the source being my own computer to the destitation. Eventually I can see the repsonses to each query that I captured with wireshark

### TCP
In this exercise, I will look through the TCP packets that I captured in the capture.
Syn- This is the client, asking to establish a TCP connection
[Syn,ACk]- This acknowledges the client's request and asks to establish its side of the connection
[Ack]- This is the client responding  and the connection is now estbalish

I then was able to look at the TCP stream and ssee the certain contents inside of the file
Also I am able to expand the packet and see the different protocol layers and see the different information that was coming out of that using Wireshark as well like with the Internet Protocol Version 4 and also look at the Transmission Control Protoctol 

```bash 
┌─────────────────────────────┐
│ Ethernet                    │
├─────────────────────────────┤
│ IP                          │
├─────────────────────────────┤
│ TCP                         │
├─────────────────────────────┤
│ HTTP / Application data     │
└─────────────────────────────┘
```
Each layer provides information used by the layer below it
PSH- Means push, it tells the TCP stack that the sender wants data delivered to the applcation right now rather than waiting for more data to accumulate
FIN- It mean's Im done. IT is used when one side wants gracefully close its side of TCP connection.
RST- stops this connection immediatley, means reset 

#### Strace
socket()- This is where the program asks linux for a TCP socket
connect()- This represents the program attempting to establish a connection to the remote server. Wireshark observes the packets on the network side, while strace observes system calls made by the program
send or sendto()- Depending on the application and libraries invloved, indicate data being passed toward the network
recv()- These are associated with receving data
openat()- Open at is involved with opening files.
write()- This is a system call used to write data to a file, terminal, sokce , or another file descriptor.

| Tool       | What you're observing                            |
| ---------- | ------------------------------------------------ |
| `strace`   | What the program asks the operating system to do |
| Wireshark  | Packets traveling through the network            |
| DNS filter | Name-resolution traffic                          |
| TCP filter | TCP communication                                |
| TCP Stream | Data exchanged in a TCP connection               |
DNS definiton- translates human-friendly domain names into IP addresses.
IPv4- Internet Protocol Version 4 (this is the traditional IP addressing system)
192.168.1.25
IPv6- Internet Protocol Version 6 (This is the newer replacement to IPv4)
It looks like this 2607:f8b0:4004:c1b::65

They haven't switched over because it takes a long ass fucking time to switch over the entire internet. Also Nat prolonged it since, instead of one public IPv4 for each device its uses nat.

Nat lets a bunch of devices share one public IPv4 address.
Nat64 acts as a translator turning Ipv6 to Ipv4 shit and the same goes for DNS64Oka


CNAME- Canoical Name which is basically an alias
going from www.example.com -> points to another domain name which eventually gets to the ip address
MX- Mail Exchange(tells you where email for a domain should go)
TXT-Text record (allows a domain to store text-based information in DNS)

TCP- Transmission Control Protocol sits above IP
Ip gets the packets from one place to another, but IP by itself doesn't guarantee that everything arrives correctly.
TCP adds things like:
Connection Establishment
Ordering 
acknowledgements
retransmission
flow control 
reliable delivery

Ports- identifies a network service/ application endpoint on that device.
Common Ports
20/21 FTP- Tranfers files
22 SSH - Secure remote computer access
25 SMTP-  Sends Email
53 DNS - Resolves domain names 
80 HTTP-Regular/unencryped websites
443 HTTPS- Encryped websites
110 POP3-Downloads email from a server
143 IMAP- Access/Manages email on a server
3389 RDP-Remote access to Windows Computer


TCP vs UDP
Tcp- good for things where losing data is a problem, web traffic, SSH, File transfer, Email.
TCP is for reliability 

UDP- is much simpiler, here's data send it
It doesn't have tcp style connection and doesn't provide tcp's bulit in reliable delivery
It's useful when speed and low overhead matter or the application handles relaibility itself
Examples include:
DNS 
DHCP
streaming 
online game s
Voip


TLS "Encrypt the communication"
Provides Encryption
Provides Authentication
Provides Integerity

```bash
HTTP
  ↓
TLS
  ↓
TCP
  ↓
IP
  ↓
Ethernet/Wi-Fi
```

DHCP "Give my device network configuration"
A classic DHCP exchange is called Dora
D-DIscover- Computer broadcasts to the world
O-Offer- A DHCP server repsonds
R-Request- Computer says it can use that
A-Acknowledge- Server says its all yours
ICMP " Network diagnostic/control"

ARP  "What's the mac address for this local IP"
Ethernet/Wifi needs a MAC address for the local Layer-2 Delivery

