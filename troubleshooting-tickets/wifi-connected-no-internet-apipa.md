# Wi-Fi Connected but No Internet

| Field | Details |
|---|---|
| Scenario | Simulated help-desk ticket |
| Platform | Windows |
| Status | Resolved |
| Root cause | DHCP failure resulting in an APIPA configuration |

## Problem

The user reported problems with her computer's Wi-Fi connection. Although the laptop showed that it was connected to Wi-Fi, websites would not open and Microsoft Teams showed as offline. The connection had worked normally the previous day.

Other devices, including the user's phone and tablet, worked correctly on the same Wi-Fi network. This indicated that the issue was isolated to the laptop rather than affecting the entire network.

## Initial Checks

- **Could other devices access the same Wi-Fi?** Yes
- **First command used:** `ping 1.1.1.1`
- **Result:** Request timed out

```powershell
ping 1.1.1.1
```

Because the test used an IP address rather than a hostname, the timeout showed that the problem was not limited to DNS resolution.

## Diagnosis

I asked the user to run:

```powershell
ipconfig /all
```

The results showed:

- **IPv4 address:** An APIPA address beginning with `169.254`
- **Default gateway:** Missing
- **DNS server:** Missing

Windows had assigned itself an Automatic Private IP Addressing (APIPA) address because it could not obtain network settings from DHCP. DHCP normally provides the device with an IP address, subnet configuration, default gateway, and DNS-server details.

Without a default gateway, the laptop had no route to the internet. The missing DNS-server address also meant it could not translate website names into IP addresses.

## Resolution

1. Asked the user to run `ping 1.1.1.1`; the requests timed out.
2. Asked the user to run `ipconfig /all`.
3. Identified an APIPA address with no default gateway or DNS server.
4. Confirmed that other devices worked on the same Wi-Fi network.
5. Asked the user to disconnect the laptop from Wi-Fi and reconnect it.

Reconnecting caused the laptop to request fresh network configuration from DHCP.

## Verification

After reconnecting to Wi-Fi, the user successfully opened `google.com` in her browser.

I then asked her to run `ipconfig` again. The laptop now had:

- A valid private IPv4 address beginning with `192.168`
- An assigned default gateway
- An assigned DNS server

Internet access and Microsoft Teams connectivity were restored.

## What I Learned

1. A simple action such as disconnecting and reconnecting Wi-Fi can renew network configuration and resolve the issue.
2. `ipconfig` and `ipconfig /all` can be used to inspect Windows TCP/IP settings.
3. `ping` can be used to test basic network connectivity.
4. An address beginning with `169.254` indicates that Windows could not obtain its configuration from DHCP.
5. Testing another device helps determine whether the fault affects one computer or the whole network.
6. Testing an IP address before a domain name helps distinguish general connectivity problems from DNS problems.
