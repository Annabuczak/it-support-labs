# Ticket 07 — Troubleshooting Network Paths with Tracert

## Objective

Use the Windows `tracert` command to examine the path traffic takes to a destination and understand how traceroute information can be used when troubleshooting network connectivity.

I compared results from my Windows 11 VirtualBox VM with results from my main Windows laptop.

---

## Lab Environment

### Windows 11 VM

- Oracle VirtualBox
- NAT networking
- IPv4 address: 10.0.2.15
- Default gateway: 10.0.2.2

### Main Windows Laptop

- Windows 11
- Connected to my home network
- Local gateway: 192.168.0.1

---

## Testing a Route to an External IP Address

I first ran the following command from my Windows VM:

tracert 8.8.8.8

The destination was successfully reached, but the VM displayed `8.8.8.8` as the first hop.

📸 **Screenshot — tracert 8.8.8.8 from VirtualBox VM**

This was different from what I expected from a normal physical network.

Because the VM is using VirtualBox NAT, VirtualBox handles the VM's external network traffic and the trace does not expose the physical Internet route in the same way as my main computer.

This demonstrated that virtual networking can affect what networking tools display.

---

## Running Tracert from the Main Windows Laptop

I then ran:

tracert 8.8.8.8

from my main Windows laptop.

This produced a much more detailed route.

The trace reached `8.8.8.8` in 8 hops.

The first hop was:

192.168.0.1

This is my local router/default gateway.

The trace then continued through several other routers before successfully reaching:

dns.google [8.8.8.8]

📸 **Screenshot — tracert 8.8.8.8 from main Windows laptop**

---

## Understanding a Hop

A hop represents a routing step along the path towards a destination.

A simplified route could look like:

My PC  
↓  
Default Gateway  
↓  
ISP Router  
↓  
Other Routers  
↓  
Destination

`tracert` helps show these routing steps.

This makes it different from `ping`.

`ping` helps answer:

Can I reach the destination?

`tracert` helps answer:

What path is my traffic taking towards the destination?

---

## Understanding the Three Response Times

For each hop, `tracert` normally sends three probes.

For example:

16 ms    13 ms    15 ms

These values show the round-trip response time for each probe.

They can help identify changes in latency along a network path, although an individual slow response does not automatically mean there is a network fault.

---

## Understanding Request Timed Out

Some hops in my trace displayed:

*    *    *    Request timed out.

However, later hops responded and the final destination was successfully reached.

For example, my trace contained timeouts at intermediate hops but eventually reached:

dns.google [8.8.8.8]

This showed me that a timeout at one intermediate hop does not automatically mean the route has failed.

Some routers may not respond to traceroute probes or may limit/deprioritise those responses while still forwarding normal traffic.

The important point is to look at what happens after the timeout.

If later hops respond and the destination is reached, the individual timeout is not necessarily a connectivity problem.

---

## Tracing a Hostname

I then tested:

tracert bbc.co.uk

The command first resolved the hostname to an IPv4 address before tracing the route.

On my main laptop the output showed:

Tracing route to bbc.co.uk [151.101.128.81]

The route then passed through:

192.168.0.1

followed by ISP/network infrastructure before successfully reaching the destination.

📸 **Screenshot — tracert bbc.co.uk from main Windows laptop**

---

## DNS and Tracert

Running:

tracert bbc.co.uk

also demonstrated that DNS is involved when I provide a hostname.

Before Windows can trace the route, it needs to determine the IP address associated with `bbc.co.uk`.

The line:

Tracing route to bbc.co.uk [151.101.128.81]

shows that hostname resolution was successful.

By comparison:

tracert 8.8.8.8

already provides the destination IP address, so DNS is not required to determine the destination address.

This gives me another useful troubleshooting comparison.

If tracing an IP works but a hostname cannot be resolved, I would investigate DNS rather than immediately assuming that general network connectivity has failed.

---

## Comparing VM and Physical Network Results

The VirtualBox VM and main laptop produced very different traces.

### VirtualBox VM

The external destination appeared as hop 1.

### Main Windows Laptop

The trace showed the local gateway followed by multiple routers before reaching the destination.

This helped demonstrate that the network environment matters when interpreting troubleshooting results.

VirtualBox NAT abstracts parts of the real network path, so I should not assume that a traceroute from a NAT VM will look the same as a trace from a physical device.

---

## Useful Command

tracert <destination>

Examples:

tracert 8.8.8.8

tracert bbc.co.uk

---

## Troubleshooting Lessons

`ping` and `tracert` answer different troubleshooting questions.

`ping` helps determine whether a destination can be reached.

`tracert` helps investigate the route towards that destination.

A single `* * * Request timed out` does not automatically mean there is a fault.

If later hops respond and the destination is reached, traffic is still progressing through the route.

If a trace repeatedly stops at a particular point and never reaches the destination, I would combine that information with other tests such as:

ipconfig /all

ping <default-gateway>

ping <external-IP>

nslookup <hostname>

I would use the combined results to determine whether the problem is local configuration, the default gateway, DNS, or somewhere further along the network path.

---

## What I Learned

I learned how to use `tracert` to examine the route between my computer and a remote destination.

I can now identify hops, understand the three response times shown for each hop, and recognise that an intermediate timeout does not necessarily mean the connection has failed.

I also understand the difference between tracing an IP address and tracing a hostname, and how DNS resolution is involved when a hostname is used.

Most importantly, I learned that `tracert` should be used alongside other troubleshooting commands rather than as a standalone diagnosis.
