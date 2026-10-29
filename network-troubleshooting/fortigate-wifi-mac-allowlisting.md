FortiGate Wi-Fi MAC Allowlisting — Multi-Site Service Request

Status: Resolved
Category: Network Administration / Wireless Security
Platform: Fortinet FortiGate, FortiOS
Scope: Two sites

Issue

A request was received to allow a new managed tablet to connect to a dedicated corporate tablet Wi-Fi network at two separate locations.

The wireless environment was managed through FortiGate firewalls. Existing authorised tablets were controlled using MAC address objects and an established MAC allowlist.

The objective was to add the new device at both locations without affecting access for existing devices.

Investigation

I accessed the relevant FortiGate firewalls and reviewed the dedicated tablet SSID under:

WiFi & Switch Controller → SSIDs

I then investigated the existing device configuration under:

Policy & Objects → Addresses

Existing tablets were configured as Device (MAC Address) objects using asset identifiers as their object names.

The existing objects were referenced by a MAC address group called:

mac-allow-group

This established the configuration pattern being used for authorised wireless devices.

During the investigation, one FortiGate interface returned a Failed to load data error when attempting to edit the SSID. I therefore used the existing address objects and their references to identify the relevant configuration instead.

Resolution

For each required location:

1. Located the appropriate FortiGate firewall.
2. Created a new Device (MAC Address) object for the tablet.
3. Used the organisation’s existing asset naming convention for the object.
4. Entered the tablet’s MAC address.
5. Located the existing mac-allow-group.
6. Added the new device object to the group.
7. Ensured that all existing authorised devices remained in the group.
8. Saved the configuration.

The requested MAC allowlisting configuration was completed at both locations.

Technical Notes

A FortiGate MAC address object represents the individual device, while the address group allows multiple authorised device objects to be managed together.

Creating the MAC address object alone was therefore not sufficient — the new object also needed to be added to the existing allowlist group.

MAC filtering provides a basic device access-control mechanism but should not be treated as strong authentication because MAC addresses can be spoofed. Higher-security wireless environments can use controls such as WPA2/WPA3-Enterprise, 802.1X authentication, certificates and network segmentation.

Skills Demonstrated

* Fortinet FortiGate administration
* FortiOS navigation
* Wireless network administration
* MAC address filtering
* Firewall address objects
* Address groups
* Multi-site configuration
* Access control
* Network troubleshooting
* Change management

Outcome

The new managed device was successfully added to the required MAC allowlists across both locations and the service request was completed.

⸻

This case study is based on a real support request. Organisation names, locations, device identifiers and MAC addresses have been anonymised to protect client confidentiality.
