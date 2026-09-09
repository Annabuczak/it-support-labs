# Network Troubleshooting Labs

Practical networking exercises and service-desk troubleshooting records completed in a Windows lab environment.

## Topics covered

- IPv4 addresses and subnet masks
- Default gateways and routing basics
- DHCP and automatic addressing
- DNS name resolution
- MAC addresses and ARP
- Private and public IP addresses
- Loopback and APIPA addresses
- VirtualBox NAT networking

## Diagnostic commands

```powershell
ipconfig
ipconfig /all
getmac
arp -a
ping
nslookup
tracert
```

## Troubleshooting approach

1. Confirm the user’s symptoms and scope of the issue.
2. Check the physical or virtual network connection.
3. Inspect the IP configuration.
4. Test the local TCP/IP stack and default gateway.
5. Test internet connectivity by IP address.
6. Test DNS name resolution.
7. Apply the appropriate fix.
8. Retest and document the outcome.

## Evidence

Individual labs include the reported issue, investigation, commands used, resolution, verification, and supporting screenshots where appropriate.
