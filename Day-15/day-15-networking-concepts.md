# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## Objective

Learn the networking fundamentals required for DevOps engineering:

* DNS Resolution
* IP Addressing
* CIDR & Subnetting
* Network Ports
* Basic Troubleshooting

---

# 1. DNS (Domain Name System)

## What is DNS?

DNS translates human-readable domain names into IP addresses.

### Example

When a user enters `google.com` in a browser:

1. Browser sends a DNS query.
2. DNS resolver finds the IP address.
3. IP address is returned.
4. Browser connects to the server using that IP.
5. Website is displayed.

---

## Common DNS Record Types

| Record | Purpose                               |
| ------ | ------------------------------------- |
| A      | Maps a domain name to an IPv4 address |
| AAAA   | Maps a domain name to an IPv6 address |
| CNAME  | Creates an alias for another domain   |
| MX     | Specifies mail servers for a domain   |
| NS     | Specifies authoritative DNS servers   |

### Verify DNS

```bash
dig google.com
```

Look for:

* A Record → IP Address
* TTL (Time To Live) → Cache duration in seconds

---

# 2. IP Addressing

## What is an IPv4 Address?

An IPv4 address uniquely identifies a device on a network.

Example:

```text
192.168.1.10
```

### IPv4 Structure

* 32 bits
* 4 octets
* Each octet ranges from 0–255

Example:

```text
192.168.1.10
```

---

## Public vs Private IP

| Public IP                    | Private IP                   |
| ---------------------------- | ---------------------------- |
| Accessible from the Internet | Used inside private networks |
| Globally unique              | Can be reused                |
| Assigned by ISP              | Assigned internally          |

### Examples

Public IP:

```text
8.8.8.8
```

Private IP:

```text
192.168.1.10
```

---

## Private IP Ranges

| Range                         | CIDR           |
| ----------------------------- | -------------- |
| 10.0.0.0 – 10.255.255.255     | 10.0.0.0/8     |
| 172.16.0.0 – 172.31.255.255   | 172.16.0.0/12  |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 |

### Check Your IP

```bash
ip addr show
```

Identify whether your IP belongs to one of the private ranges.

---

# 3. CIDR & Subnetting

## What is CIDR?

CIDR (Classless Inter-Domain Routing) defines how many bits belong to the network portion of an IP address.

Example:

```text
192.168.1.0/24
```

Here:

* Network Bits = 24
* Host Bits = 8

Subnet Mask:

```text
255.255.255.0
```

---

## Why Do We Subnet?

Subnetting helps:

* Reduce network congestion
* Improve security
* Organize networks efficiently
* Control IP address allocation
* Improve performance

---

## CIDR Quick Reference

| CIDR | Subnet Mask     | Total IPs | Usable Hosts |
| ---- | --------------- | --------- | ------------ |
| /24  | 255.255.255.0   | 256       | 254          |
| /16  | 255.255.0.0     | 65,536    | 65,534       |
| /28  | 255.255.255.240 | 16        | 14           |

### Formula

```text
Usable Hosts = (2^Host Bits) - 2
```

---

## Interview Tip

Remember:

```text
/24 = 254 Hosts
/16 = 65,534 Hosts
/28 = 14 Hosts
```

---

# 4. Ports

## What is a Port?

A port is a logical endpoint used by applications to communicate over a network.

Think of:

* IP Address = Building Address
* Port = Door Number

Example:

```text
192.168.1.10:80
```

---

## Common Ports

| Port  | Service |
| ----- | ------- |
| 22    | SSH     |
| 53    | DNS     |
| 80    | HTTP    |
| 443   | HTTPS   |
| 3306  | MySQL   |
| 6379  | Redis   |
| 27017 | MongoDB |

---

## Check Listening Ports

```bash
ss -tulpn
```

Example:

```bash
ss -tulpn | grep 22
```

Output indicates SSH is listening on Port 22.

---

# 5. OSI Model vs TCP/IP Model

| OSI Layer    | TCP/IP Layer | Example Protocols |
| ------------ | ------------ | ----------------- |
| Application  | Application  | HTTP, HTTPS, DNS  |
| Presentation | Application  | SSL/TLS           |
| Session      | Application  | Sessions          |
| Transport    | Transport    | TCP, UDP          |
| Network      | Internet     | IP                |
| Data Link    | Link         | Ethernet          |
| Physical     | Link         | Cables, Wi-Fi     |

---

# Protocol Placement

| Protocol | Layer       |
| -------- | ----------- |
| HTTP     | Application |
| HTTPS    | Application |
| DNS      | Application |
| TCP      | Transport   |
| UDP      | Transport   |
| IP       | Internet    |
| Ethernet | Link        |

---

# Real Example

Command:

```bash
curl https://example.com
```

Network Flow:

```text
HTTPS
 ↓
TCP
 ↓
IP
 ↓
Ethernet/Wi-Fi
```

Meaning:

Application Layer → Transport Layer → Internet Layer → Link Layer

---

# Troubleshooting Scenarios

## Scenario 1

### Command

```bash
curl http://myapp.com:8080
```

### Concepts Involved

* DNS resolves `myapp.com`
* IP routing finds destination server
* TCP establishes connection
* Port 8080 identifies application
* HTTP transfers data

Flow:

```text
HTTP → TCP → IP
```

---

## Scenario 2

### Problem

Application cannot connect to:

```text
10.0.1.50:3306
```

### Checks

1. Verify connectivity

```bash
ping 10.0.1.50
```

2. Verify database service

```bash
systemctl status mysql
```

3. Verify listening port

```bash
ss -tulpn | grep 3306
```

4. Verify firewall rules

```bash
ufw status
```

5. Verify application configuration

* Correct IP
* Correct Port
* Correct Credentials

---

# Interview Revision Sheet

### DNS Records

* A → IPv4
* AAAA → IPv6
* CNAME → Alias
* MX → Mail Server
* NS → Name Server

### Private IP Ranges

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

### Important CIDRs

```text
/24 = 254 Hosts
/16 = 65,534 Hosts
/28 = 14 Hosts
```

### Important Ports

```text
22    SSH
53    DNS
80    HTTP
443   HTTPS
3306  MySQL
6379  Redis
27017 MongoDB
```

### Networking Stack

```text
Application → HTTP/HTTPS/DNS
Transport   → TCP/UDP
Internet    → IP
Link        → Ethernet/Wi-Fi
```
