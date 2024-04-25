![image](https://github.com/vulonggg/Documents/assets/167597317/307b53ce-b928-4151-854b-fa4df3496791)

- Check whether your computer’s external interface (usually designated as either eth0 or em0) has an IP address:	ifconfig / ip a

- If it does, that probably means you’ve been successfully connected to your DHCP server, so the problem must lie farther afield. If you don’t have an IP address, you might want to use dmesg to confirm that the network interface itself was picked up by your system:		
dmesg | grep eth0


- your router address will usually be the same as your DHCP address, but with a 1 in the final field, rather than whatever number you had. Ping, by the way, uses the ICMP transmission protocol to send lots of very small data packets to the specified address, requesting that the host echoes the packets back.
  ping 192.168.0.1

- let’s assume that you can successfully ping your router. The problem must be a bit farther out. Try pinging the DNS name for a known web site:
ping google.com

- If that fails, there might be a problem with your Internet provider (which will require a friendly phone call, assuming your phone still works). But it’s also possible that your DNS address translation isn’t working. To find out, ping the IP address of an external service that you know should work. My favorite for these times is Google’s DNS server,	
ping 8.8.8.8


- If that works (even though ping google.com did not), then you know it’s a DNS issue, which is discussed in the last section of this chapter.

- If it doesn’t work, it might be your Internet provider’s fault, but it can still be helpful to narrow down the location of the blockage.

- Traceroute (or its IPv6 cousin, traceroute6) can help fill in some of the gaps. Running traceroute against a known address will show you each step your packets took along the route to a destination, including the one right before things failed:
  traceroute 8.8.8.8

- Tracepath, by the way, delivers much the same function as traceroute. And both traceroute and tracepath have their IPv6 equivalents: traceroute6 and tracepath6
  
