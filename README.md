# Network Spoofing — IP Spoofing & MAC Spoofing

> **Lab Write-up | Ethical Hacking & Network Security**  
> Tools Used: `ifconfig`, `macchanger`, SMAC, VPN, Tor Browser  
> Platforms: Kali Linux | Windows
## Disclaimer

> This write-up is created strictly for **educational purposes** as part of an ethical hacking learning lab. All techniques demonstrated were performed in a **controlled environment** on devices I own. Spoofing network identities on public or unauthorized networks is **illegal and unethical**. Always practice cybersecurity in legal, authorized environments only.
---

## Table of Contents

- [What is Spoofing?](#what-is-spoofing)
- [IP Spoofing](#ip-spoofing)
  - [IP Spoofing on Kali Linux](#ip-spoofing-on-kali-linux)
- [MAC Spoofing](#mac-spoofing)
  - [MAC Spoofing on Kali Linux](#mac-spoofing-on-kali-linux)
  - [MAC Spoofing on Windows](#mac-spoofing-on-windows)
- [Anonymous Browsing](#anonymous-browsing)
  - [Using VPN](#using-vpn)
  - [Using Tor Browser](#using-tor-browser)
- [Observations](#observations)
- [Disclaimer](#disclaimer)

---

## What is Spoofing?

Spoofing in network security refers to the act of disguising or changing your network identity — such as your IP address or MAC address — to appear as a different device or user on the network. It is a fundamental concept studied in ethical hacking and penetration testing to understand how attackers can mask their identity and how defenders can detect such behavior.

---

## IP Spoofing

An **IP address (Internet Protocol address)** is a unique numerical label assigned to every device on a network. IP spoofing involves altering this address to impersonate another device or to hide your true identity on the network.

### IP Spoofing on Kali Linux

On Kali Linux, we can manually assign a specific IP address to a network interface using the `ifconfig` command.

**Command:**
```bash
sudo ifconfig <interface> <new-ip-address>
```

**Example:**
```bash
sudo ifconfig eth0 192.168.1.100
```

**Steps:**
1. Open a terminal in Kali Linux.
2. Check your current IP address and interface name:
   ```bash
   ifconfig
   ```
3. Assign a new IP address of your choice to the interface:
   ```bash
   sudo ifconfig eth0 192.168.1.100
   ```
4. Verify the change:
   ```bash
   ifconfig eth0
   ```

<img width="733" height="489" alt="Screenshot 2026-06-09 091519" src="https://github.com/user-attachments/assets/ab2b70a3-45f1-4880-b3c1-6ff6bb3eff69" />


---

## MAC Spoofing

A **MAC address (Media Access Control address)** is a hardware identifier assigned to a network interface card (NIC). It is unique to every device at the hardware level. MAC spoofing involves changing this address to bypass MAC-based access controls or to avoid device tracking on a local network.

### MAC Spoofing on Kali Linux

On Kali Linux, MAC spoofing is done using two tools — `ifconfig` (to bring the interface down/up) and `macchanger` (to assign a new MAC address).

**Steps:**

1. Check your current MAC address:
   ```bash
   ifconfig eth0
   ```

2. Bring the interface down (required before changing MAC):
   ```bash
   sudo ifconfig eth0 down
   ```

3. Change the MAC address using `macchanger`:
   ```bash
   # Assign a random MAC address
   sudo macchanger -r eth0

   # Assign a specific MAC address
   sudo macchanger -m XX:XX:XX:XX:XX:XX eth0
   ```

4. Bring the interface back up:
   ```bash
   sudo ifconfig eth0 up
   ```

5. Verify the new MAC address:
   ```bash
   ifconfig eth0
   # or
   macchanger -s eth0
   ```

<img width="713" height="553" alt="Screenshot 2026-06-09 092250" src="https://github.com/user-attachments/assets/577733b9-f534-4582-a06a-a514b7f65fb1" />


---

### MAC Spoofing on Windows

On Windows, MAC spoofing can be done using a GUI tool called **SMAC (Spoofed MAC Address Changer)**. It provides a simple interface to view and change the MAC address of any network adapter without needing command-line knowledge.

**Steps:**

1. Download and install **SMAC** on your Windows machine.
2. Open SMAC — it will list all available network adapters with their current MAC addresses.
3. Select the network adapter you want to spoof.
4. Enter the new MAC address in the provided field.
5. Click **"Update MAC"** to apply the change.
6. Restart the network adapter or reboot if prompted.
7. Verify the new MAC address from the adapter properties or within SMAC itself.

---

## Anonymous Browsing

Beyond IP and MAC spoofing at the network layer, identity masking at the application/browser layer is also widely studied. Two common methods are VPNs and the Tor Browser.

### Using VPN

A **VPN (Virtual Private Network)** encrypts your internet traffic and routes it through a server in a location of your choice, masking your real IP address from websites and services you visit.

**How it works:**
- Your traffic is encrypted and tunneled to a VPN server.
- Websites see the VPN server's IP address, not yours.
- Your ISP can see you're using a VPN but cannot read the traffic.

**Steps (general):**
1. Install a VPN client (e.g., ProtonVPN, OpenVPN).
2. Connect to a server of your choice.
3. Verify your new public IP at [https://whatismyipaddress.com](https://whatismyipaddress.com).


---

### Using Tor Browser

**Tor (The Onion Router)** routes your internet traffic through multiple encrypted relay nodes (entry → middle → exit), making it extremely difficult to trace the traffic back to your real IP address.

**How it works:**
- Traffic is encrypted in multiple layers (like an onion).
- Each relay only knows the previous and next hop — no single node knows both the origin and the destination.
- The exit node sends traffic to the destination, masking your real IP.

**Steps:**
1. Download and install **Tor Browser** from [https://www.torproject.org](https://www.torproject.org).
2. Launch Tor Browser and connect to the Tor network.
3. Browse normally — your traffic is anonymized through the Tor relay network.
4. Verify your IP has changed at [https://check.torproject.org](https://check.torproject.org).

---

## Observations

| Technique | Platform | Tool Used | Purpose |
|---|---|---|---|
| IP Spoofing | Kali Linux | `ifconfig` | Change IP to a specific address |
| MAC Spoofing | Kali Linux | `ifconfig` + `macchanger` | Change MAC randomly or to a specific address |
| MAC Spoofing | Windows | SMAC | GUI-based MAC address change |
| Anonymous Browsing | Any | VPN | Mask real IP via encrypted tunnel |
| Anonymous Browsing | Any | Tor Browser | Multi-hop anonymization via relay nodes |

---

