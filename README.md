# DHCP Configuration Lab: Cisco Packet Tracer
 
 
Two-router DHCP lab. An ISP router leases a WAN address to an edge router. The edge router also runs a DHCP server for its own LAN, so it is a DHCP client on one interface and a DHCP server on another. PCs on the LAN receive their addressing automatically.
 
```
ISP-Router (DHCP server, 200.1.1.1/24)
    |
    |  200.1.1.0/24
    |
Edge-Router (WAN: DHCP client, LAN: DHCP server, 192.168.1.1/24)
    |
    |  192.168.1.0/24
    |
PC1, PC2 (DHCP clients)
```
 
## Addressing plan
 
| Device / interface | Address | Assignment | Purpose |
|---|---|---|---|
| ISP-Router Gi0/0/0 | 200.1.1.1/24 | Static | ISP gateway and DHCP server |
| Edge-Router WAN | 200.1.1.2/24 | DHCP (from ISP-POOL) | Address received from the ISP |
| Edge-Router LAN | 192.168.1.1/24 | Static | LAN default gateway and DHCP server |
| LAN-POOL | 192.168.1.11 onwards | DHCP | Client address range (.1 to .10 excluded) |
| PC1 | 192.168.1.11 | DHCP | First client |
| PC2 | 192.168.1.12 | DHCP | Second client |
| DNS (both pools) | 8.8.8.8 | DHCP option | Name resolution |
 
## Documentation
 
| # | Document | Covers |
|---|---|---|
| 1 | [DHCP fundamentals](docs/01-dhcp-fundamentals.md) | What DHCP provides, DORA exchange, address assignment methods |
| 2 | [Topology and addressing](docs/02-topology-and-addressing.md) | Devices, cabling, IP plan, build steps, Layer 1 check |
| 3 | [ISP router as DHCP server](docs/03-isp-router-dhcp-server.md) | Interface, exclusion, pool, save, verify |
| 4 | [Edge router: DHCP client and LAN DHCP server](docs/04-edge-router.md) | WAN client, LAN interface, LAN pool |
| 5 | [Verification](docs/05-verification.md) | `ipconfig /all`, ping tests, bindings, pool statistics |
| 6 | [Troubleshooting](docs/06-troubleshooting.md) | Three problems, causes and fixes |
| 7 | [Command reference](docs/07-command-reference.md) | Commands used and what they do |
 
Full device configurations are in [`configs/`](configs/):
 
- [`isp-router.cfg`](configs/isp-router.cfg)
- [`edge-router.cfg`](configs/edge-router.cfg)
## Results
 
| Test | Result |
|---|---|
| WAN address assignment | Edge-Router received 200.1.1.2 from the ISP router |
| LAN address assignment | PC1 received 192.168.1.11, PC2 received 192.168.1.12 |
| Gateway reachability | PC1 reached the Edge-Router at 192.168.1.1 |
| LAN connectivity | PC1 reached PC2 |
| Binding tables | Both routers listed the expected leases |
| Troubleshooting | Three configuration problems diagnosed and fixed |
 
## Skills demonstrated
 
- Cisco IOS CLI: privileged and configuration modes, interface configuration, DHCP pools
- DHCP server configuration: pools, excluded addresses, default gateway and DNS options
- DHCP client configuration on a router interface (`ip address dhcp`)
- IPv4 addressing plan with separate WAN and LAN subnets
- Verification with `show` commands, `ipconfig /all` and ping
- Bottom-up troubleshooting (interface state, exclusions, both ends of a link)
## Conventions
 
- Router prompts and commands are in code blocks.
- Interface names are written as in the IOS configuration (for example `gigabitEthernet 0/0/0`).
- Spelling follows UK English.
 
