# Network+ — Wireless Technologies, Networking, and Encryption

## Topics Covered

- Wireless Technologies
- Wireless Networking
- Network Types
- Wireless Encryption
- SSID and BSSID
- Access Points
- Guest Networks
- Captive Portals
- WPA2, WPA3, WEP
- Rogue Access Points
- Evil Twin Attacks
- Kali Wireless Interface Check

---

## 2.4 GHz vs 5 GHz Wi-Fi

Wi-Fi commonly works on different frequency bands.

The two common bands are:

- 2.4 GHz
- 5 GHz

### 2.4 GHz

2.4 GHz provides better range but usually lower speed.

Important points:

- Better range
- Travels farther
- Better through walls compared to 5 GHz
- More interference
- Fewer non-overlapping channels
- Usually slower than 5 GHz

### 5 GHz

5 GHz usually provides better speed but shorter range.

Important points:

- Higher speed
- Shorter range
- More channels
- Less interference compared to 2.4 GHz
- Does not travel through walls as well as 2.4 GHz

Memory line:

- 2.4 GHz = better range
- 5 GHz = better speed

---

## Wi-Fi Standards

Common Wi-Fi standards:

- 802.11a
- 802.11b
- 802.11g
- 802.11n
- 802.11ac
- 802.11ax

Simple mapping:

- Wi-Fi 4 = 802.11n
- Wi-Fi 5 = 802.11ac
- Wi-Fi 6 = 802.11ax

Higher Wi-Fi standards usually improve speed, efficiency, and performance.

---

## Wireless Interference

Wireless interference means signal disruption caused by other wireless signals, devices, or physical obstacles.

Common sources of interference:

- Other Wi-Fi networks
- Microwave ovens
- Bluetooth devices
- Cordless phones
- Baby monitors
- Thick walls
- Metal objects
- Too many nearby access points using overlapping channels

Interference can cause:

- Slow Wi-Fi
- Weak signal
- Packet loss
- Connection drops
- High latency

---

## SSID

SSID stands for Service Set Identifier.

The SSID is the Wi-Fi network name users see when connecting.

Examples:

- Office-WiFi
- Guest-WiFi
- Home_5G
- Cafe_WiFi

Memory line:

- SSID = Wi-Fi network name

---

## BSSID

BSSID stands for Basic Service Set Identifier.

The BSSID is usually the MAC address of the wireless access point radio.

Memory line:

- SSID = Wi-Fi name
- BSSID = AP radio MAC address

Example:

- SSID: Office-WiFi
- BSSID: 00:11:22:33:44:55

A single SSID can have multiple BSSIDs when multiple access points broadcast the same Wi-Fi network.

---

## Wireless Access Point

A wireless access point allows wireless clients to connect to a wired network.

Examples of wireless clients:

- Laptop
- Mobile phone
- Tablet
- Printer
- Camera
- IoT device

Simple flow:

```text
Wireless client → Access Point → Wired network → Internet / internal network
```

---

## Infrastructure Mode

Infrastructure mode means wireless clients connect through an access point.

Example:

```text
Laptop → Access Point → Switch → Router → Internet
```

This is the most common Wi-Fi mode used in homes, offices, hotels, schools, and companies.

Memory line:

- Infrastructure mode = AP-based wireless network

---

## Ad Hoc Mode

Ad hoc mode means wireless devices connect directly to each other without an access point.

Example:

```text
Laptop ↔ Laptop
Phone ↔ Laptop
```

Memory line:

- Ad hoc = device-to-device wireless without AP

---

## Mesh Network

A mesh network uses multiple wireless nodes or access points that communicate with each other to extend coverage.

Example:

```text
Mesh AP 1 ↔ Mesh AP 2 ↔ Mesh AP 3
```

Use cases:

- Large house
- Office floor
- Hotel
- Warehouse
- Campus

Important correction:

- Mesh does not mean every end device connects directly to every other device.
- Mesh means multiple mesh access points or nodes work together to extend coverage.

---

## Guest Network

A guest network gives visitors internet access while keeping them separated from the internal private network.

Example:

```text
Corporate Wi-Fi → internal systems, printers, servers
Guest Wi-Fi     → internet only
```

Why companies use guest networks:

- Security
- Network separation
- Protect internal systems
- Limit guest access
- Reduce risk from unknown devices

---

## Captive Portal

A captive portal is a web page shown before internet access is allowed.

It may ask for:

- Username and password
- Phone number
- Email address
- Voucher code
- Terms and conditions acceptance
- Payment

Common places:

- Hotels
- Airports
- Cafes
- Colleges
- Guest Wi-Fi networks
- Public Wi-Fi

---

## Wireless Encryption

Wireless encryption protects traffic between the wireless client and the access point.

Common wireless security standards:

- WEP
- WPA
- WPA2
- WPA3

---

## WEP

WEP stands for Wired Equivalent Privacy.

WEP is old and insecure.

Why WEP is insecure:

- Weak encryption
- Cryptographic weaknesses
- Can be cracked easily
- Should not be used today

Memory line:

- WEP = old and broken

---

## WPA2

WPA2 stands for Wi-Fi Protected Access 2.

WPA2 provides authentication and encryption for Wi-Fi networks.

Important point:

- WPA2 commonly uses AES/CCMP encryption.

---

## WPA3

WPA3 is the newer Wi-Fi security standard.

It improves security compared to WPA2.

Important point:

- WPA3-Personal uses SAE instead of the older PSK handshake method.

SAE stands for:

```text
Simultaneous Authentication of Equals
```

Memory line:

- WPA3 = newer and stronger than WPA2

---

## PSK

PSK stands for Pre-Shared Key.

It means one shared Wi-Fi password is used by users or devices.

Examples:

- Home Wi-Fi password
- Small office Wi-Fi password

---

## WPA-Personal vs WPA-Enterprise

### WPA-Personal

WPA-Personal uses a shared password.

Example:

- Everyone connects using the same Wi-Fi password.

Common use:

- Home Wi-Fi
- Small office Wi-Fi

### WPA-Enterprise

WPA-Enterprise authenticates users individually.

It commonly uses:

- 802.1X
- RADIUS
- Individual usernames/passwords or certificates

Common use:

- Corporate Wi-Fi
- Universities
- Large organizations

Memory line:

- WPA-Personal = shared password
- WPA-Enterprise = individual authentication

---

## 802.1X

802.1X is used for network access authentication.

It is commonly used in enterprise Wi-Fi and wired networks.

Purpose:

- Authenticate users or devices before allowing network access.

Common components:

- Supplicant = client device
- Authenticator = switch or access point
- Authentication server = usually RADIUS

---

## Rogue Access Point

A rogue access point is an unauthorized access point connected to or operating inside an organization’s network.

Example:

- An employee plugs in a personal Wi-Fi router inside the office without IT approval.

Risks:

- Bypasses security controls
- Creates unknown entry point
- May expose internal network
- Can cause interference
- Can be used by attackers

---

## Evil Twin Attack

An evil twin is a fake wireless access point that copies the name of a legitimate Wi-Fi network.

Example:

```text
Real Wi-Fi: Cafe_WiFi
Fake Wi-Fi: Cafe_WiFi
```

Risks:

- Credential theft
- Traffic interception
- Man-in-the-middle attacks
- Fake login pages
- Session hijacking

Memory line:

- Evil twin = fake AP copying a real SSID

---

## Open Wi-Fi vs Encrypted Wi-Fi

### Open Wi-Fi

Open Wi-Fi has no wireless encryption.

Risks:

- Traffic can be easier to capture
- No Wi-Fi password required
- Users may connect to unsafe networks

### Encrypted Wi-Fi

Encrypted Wi-Fi protects traffic between the client and access point.

Important note:

- Even on encrypted Wi-Fi, HTTPS is still needed for end-to-end website security.

---

## Why Guest Wi-Fi Should Be Separated

Companies should separate guest Wi-Fi from internal corporate Wi-Fi.

Reason:

- Guests should access the internet but not internal systems.

Guest users should not access:

- Internal servers
- File shares
- Printers
- Employee laptops
- Network devices
- Corporate applications

---

## Kali Practical — Wireless Interface Check

Today I checked whether my Kali VM has a wireless interface.

Commands used:

```bash
ip -br a
nmcli dev status
iw dev
rfkill list
```

Observed output:

```text
eth0    ethernet  connected
lo      loopback  connected
```

Meaning:

- eth0 = wired/virtual Ethernet adapter
- lo = loopback interface
- No wlan0 interface was visible

Conclusion:

- My Kali VM currently does not have a wireless adapter attached.

For real Wi-Fi labs, I will need:

- Compatible USB Wi-Fi adapter
- Monitor mode support
- Packet injection support
- USB adapter passed into Kali VM

---

## Key Takeaways

- 2.4 GHz gives better range but usually lower speed and more interference.
- 5 GHz gives better speed but shorter range.
- SSID is the Wi-Fi network name.
- BSSID is usually the MAC address of the AP radio.
- Infrastructure mode uses an access point.
- Ad hoc mode is device-to-device wireless without an AP.
- Mesh networks use multiple nodes/access points to extend coverage.
- Guest networks separate visitors from internal private networks.
- Captive portals control access before allowing internet use.
- WEP is insecure and should not be used.
- WPA2 commonly uses AES/CCMP.
- WPA3 is newer and stronger than WPA2.
- WPA-Personal uses a shared password.
- WPA-Enterprise uses individual authentication with 802.1X/RADIUS.
- Rogue AP means unauthorized AP.
- Evil twin means fake AP copying a real SSID.
- Real Wi-Fi labs in Kali require a compatible USB Wi-Fi adapter.

---

## Interview Lines

2.4 GHz provides better range, while 5 GHz usually provides better speed.

SSID is the Wi-Fi network name, while BSSID is usually the MAC address of the access point radio.

Infrastructure mode uses an access point, while ad hoc mode allows direct device-to-device wireless communication.

A guest network separates visitors from the internal corporate network.

WPA2 provides Wi-Fi authentication and encryption, commonly using AES/CCMP.

WPA3 is newer and stronger than WPA2 and uses SAE in WPA3-Personal.

802.1X is used for enterprise network authentication, commonly with RADIUS.

A rogue access point is an unauthorized AP, while an evil twin is a fake AP that copies a legitimate SSID.
