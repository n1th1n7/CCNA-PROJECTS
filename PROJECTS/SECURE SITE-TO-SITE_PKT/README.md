# Project 2 – Secure Site-to-Site Network (Packet Tracer)

This project is a **secure two-site network design** built in **Cisco Packet Tracer**, connecting:

- **Montreal LAN (MTL)** – `192.168.51.0/24`
- **Toronto LAN (TOR)** – `172.31.51.0/24`
- An **ISP / Internet segment** – `209.165.51.0/28`

It focuses on **routing, services, security, and VPN** between the two sites.

## Key Technologies Demonstrated

- IPv4 addressing and default gateways for all LAN devices.
- **DHCP** for MTL LAN and ISP subnet.
- **OSPF** routing in a single area for internal networks.
- **NAT overload** (PAT) for Internet access from the internal TOR network.
- **DNS, NTP, and Syslog** servers.
- **SSH** remote management on routers and switches.
- **Port security** on access switch ports.
- **802.1X / AAA (RADIUS)** authentication for users on TOR-SW.
- **Zone-Based Firewall (ZBF)** on TOR-RT, with zones for INTERNAL and INTERNET and an inspect policy for typical user traffic.
- **IPsec site-to-site VPN** between MTL-RT and TOR-RT, protecting traffic between the two LANs over the WAN.

## Folder Structure

- `packet-tracer/`
  - `PART 1.pkt` – Base addressing, routing, and core services.
  - `PART 2.pkt` – Device hardening, SSH, port security, and 802.1X/AAA.
  - `PART 3.pkt` – Zone-Based Firewall configuration on TOR-RT.
  - `PART 4.pkt` – IPsec site-to-site VPN between MTL and TOR.
- `configs/`
  - `CONFIG.txt` – Core router and switch configuration snippets.
  - `MTL LAN.txt` – Detailed addressing plan for the Montreal LAN.
  - `TOR LAN.txt` – Detailed addressing plan for the Toronto LAN and ISP segment.
  - `PART 3 and 4.txt` – ZBF firewall and IPsec VPN configuration commands.
- `docs/`
  - `CCNA.docx` – Additional written documentation for the project (as provided).

## High-Level Scenario

1. **Basic Connectivity & Services**
   - MTL-RT and TOR-RT act as default gateways for their LANs.
   - DHCP, DNS, and NTP servers are configured for end-user devices.
   - OSPF provides dynamic routing between internal networks and the edge.

2. **Internet Access via TOR-RT**
   - TOR-RT connects to an ISP network using `209.165.51.0/28`.
   - NAT overload translates internal addresses so TOR hosts can browse the Internet and reach an HTTP server on the ISP segment.

3. **Secure Switching & Management**
   - SSH v2 is enabled on routers and switches for secure remote access.
   - MTL-SW uses port security to limit MAC addresses per port.
   - TOR-SW implements 802.1X with RADIUS (AAA) for user authentication, pointing to an AAA/Syslog server in the TOR LAN.

4. **Firewall Protection (ZBF)**
   - TOR-RT defines `INTERNAL_ZONE` (LAN side) and `INTERNET_ZONE` (WAN side).
   - A class-map matches typical traffic (HTTP, HTTPS, DNS, ICMP, FTP, Telnet, SMTP, POP3).
   - A policy-map inspects this traffic between the zones to provide stateful firewall behavior.

5. **IPsec Site-to-Site VPN**
   - MTL-RT and TOR-RT establish an IPsec tunnel over the WAN link.
   - ISAKMP policies, transform sets, ACLs, and crypto maps are configured.
   - Only traffic between the two LANs is encrypted; general Internet traffic from TOR still uses NAT and the firewall.

## How to Use

1. Open **Cisco Packet Tracer**.
2. Load the `.pkt` file for the part you want to study (e.g. `PART 1.pkt` through `PART 4.pkt`).
3. Use the configurations in the `configs/` folder to understand or rebuild the setup.
4. Test connectivity:
   - Ping between MTL and TOR hosts.
   - Test access to the ISP HTTP server.
   - Verify authentication, firewall behavior, and the IPsec VPN.

This project is designed as a compact **security-focused CCNA-level portfolio piece** that demonstrates not only connectivity, but also layered security and VPN technologies.
