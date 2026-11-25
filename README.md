# Small Office / Home Office Network

_Level: foundation — Enterprise Campus & LAN — Static Addressing · Default Route · DHCP · Switching_

**Status: In progress.** A work-in-progress snapshot; the project is not complete.

Snapshot taken 2026-11-25. Built in a simulation — no physical or production equipment was involved.

## Scenario

Hollis & Fane, a two-person bookkeeping practice, is moving into a converted shop with a fibre line and no network. Give them the smallest network that works: one router, one switch, the two staff PCs, addresses handed out automatically, and a route to the internet.

### Why it matters

Every larger design is this one repeated. Getting a gateway, a subnet and a default route right for a client who just wants their PCs online is what makes the next twenty projects readable.

## Requirements

| # | Requirement | Status | Checked by |
|---|---|---|---|
| 1 | Place a router, a switch and at least two PCs, cabled into one LAN. | Passed | Sandbox check |
| 2 | Address the LAN from a single /24 and give the router the first usable address. | Passed | Sandbox check |
| 3 | Hand out host addresses from a DHCP pool on the router, excluding the gateway. | Not yet passing | Sandbox check |
| 4 | Give the router a default route toward the ISP. | Passed | Sandbox check |

## Topology

![Topology diagram](topology.svg)

## Addressing

| Device | Interface | Address | Mask | Mode | Gateway |
|---|---|---|---|---|---|
| PC-1 | Eth0 | 192.168.1.10/24 | 255.255.255.0 | VLAN 1 | 192.168.1.1 |
| PC-2 | Eth0 | 192.168.1.11/24 | 255.255.255.0 | VLAN 1 | 192.168.1.1 |
| ISP_Jio | Gi0/0 | 10.0.0.1/8 | 255.0.0.0 | routed |  |
| PC-3 | Eth0 | 192.168.2.11/24 | 255.255.255.0 | VLAN 1 | 192.168.2.1 |
| PC-4 | Eth0 | 192.168.2.10/24 | 255.255.255.0 | VLAN 1 | 192.168.2.1 |
| Router-1 | Gi0/0 | 192.168.1.1/24 | 255.255.255.0 | routed |  |
| Router-1 | Gi0/1 | 10.0.0.2/8 | 255.0.0.0 | routed |  |
| Router-1 | Gi0/2 | 192.168.2.1/24 | 255.255.255.0 | routed |  |

## Device configurations

Running-configs as `show running-config` prints them in the BuildTheNet sandbox. Passwords, secrets, keys and SNMP communities are replaced with `<removed>`.

- [Switch-1](configs/Switch-1.txt)
- [Switch-2](configs/Switch-2.txt)
- [Router-1](configs/Router-1.txt)

---

Built on [BuildTheNet](https://www.buildthenet.io/projects/proj-pt-01-soho)
