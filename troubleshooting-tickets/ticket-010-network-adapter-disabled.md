# Ticket 010 – No Network Connection

**Category:** Networking  
**Environment:** Windows 11 VirtualBox VM  
**Status:** Resolved

## Issue
User reported that their computer had suddenly lost network connectivity.

## Investigation
I deliberately disabled the Ethernet adapter to simulate the fault.

I checked the network configuration using:

ipconfig

I then tested connectivity using:

ping 8.8.8.8

The test failed.

I opened Network Connections using:

ncpa.cpl

The Ethernet adapter was shown as disabled.

## Resolution
I right-clicked the Ethernet adapter and selected **Enable**.

## Verification
I ran `ipconfig` again and confirmed that the adapter had network configuration.

I then repeated:

ping 8.8.8.8

to verify connectivity.

## What I Learned
A loss of internet access does not necessarily indicate an ISP or router problem. Troubleshooting should begin with the local device and work outward through the network.

This ticket also demonstrated the difference between:

- Adapter disabled
- Adapter enabled but without a valid IP configuration
- Local network connectivity failure
- Internet connectivity failure
- DNS failure
