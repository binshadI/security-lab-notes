Performing a Man-in-the-Middle (MITM) Attack Using ARP Spoofing

Lab Setup
This demonstration is performed inside a controlled lab environment for learning and security testing purposes.

Machines Used
1. Attacker Machine
OS: Kali Linux
Purpose: Performs the ARP spoofing attack.
2. Victim Machine
OS: Metasploitable 2
Purpose: Target machine whose traffic will be intercepted.
3. Optional Server Machine
Purpose: Used to observe services like Telnet traffic from the victim machine.
Step 1 — Find the Default Gateway

First, we need to identify the gateway IP address of the network.

On the attacker machine, run:

ip route

Example output:

default via 192.168.1.1 dev eth0

Here:

192.168.1.1 → Default Gateway
eth0 → Network Interface

You can also use:

ip a

to view your network interfaces and IP addresses.

Output

(Insert Screenshot Here)

Step 2 — Discover Devices on the Network

Now we scan the network to identify connected devices.

Command:

sudo netdiscover -r 192.168.1.0/24
Explanation
-r → Specifies the IP range to scan
192.168.1.0/24 → Scans the entire subnet

After scanning, we can identify:

Victim IP
Gateway IP
Other active devices

Example:

Device	IP Address
Gateway	192.168.1.1
Victim	192.168.1.190
Output

(Insert Screenshot Here)

Step 3 — Enable IP Forwarding

To successfully act as a middleman, the attacker machine must forward packets between the victim and the router.

Enable IP forwarding using:

sudo sysctl -w net.ipv4.ip_forward=1
Verify
cat /proc/sys/net/ipv4/ip_forward

If it returns:

1

then forwarding is enabled.

Step 4 — Start ARP Spoofing

Now we trick the victim into believing that the attacker machine is the router.

Spoof the Victim

Command:

sudo arpspoof -i eth0 -t 192.168.1.190 192.168.1.1
What Happens Here?

The victim (192.168.1.190) thinks:

“The attacker machine is the router.”

So the victim starts sending traffic to the attacker.

Step 5 — Spoof the Router

Now we also trick the router into believing that the attacker is the victim.

Open a second terminal and run:

sudo arpspoof -i eth0 -t 192.168.1.1 192.168.1.190
Why This Step Matters

Without this step:

The victim sends traffic to the attacker
But the router does not know how to send responses back properly

This second spoof creates a full Man-in-the-Middle connection.

Traffic Flow After Spoofing
Victim  --->  Attacker  --->  Router
Router  --->  Attacker  --->  Victim

The attacker can now observe unencrypted traffic passing between both systems.

Step 6 — Verify Using Wireshark

Open Wireshark on the attacker machine and start capturing packets on eth0.

You should now see traffic flowing between:

Victim machine
Router
Other network devices

If Telnet is used, usernames and passwords may appear in plaintext because Telnet does not encrypt traffic.

Wireshark Output

(Insert Screenshot Here)

Important Concepts
What is ARP?

ARP (Address Resolution Protocol) maps:

IP Address  --->  MAC Address

Devices use ARP to communicate inside a local network.

What is ARP Spoofing?

ARP spoofing sends fake ARP replies to devices so they associate the attacker’s MAC address with another device’s IP address.

Example:

Gateway IP (192.168.1.1)
        ↓
Attacker MAC Address

This redirects traffic through the attacker machine.

Notes
This attack mainly works inside the same local network.
Encrypted protocols like HTTPS and SSH greatly reduce what an attacker can read.
Older protocols like Telnet, FTP, and HTTP are vulnerable because they transmit data in plaintext.
Tools Used
Kali Linux
Metasploitable 2
Wireshark
arpspoof
netdiscover
