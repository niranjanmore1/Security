# Assignment 6 – tcpdump Commands

> Interface in the screenshots reads `eno1`; machine IP reads `192.168.76.17`. Replace both with your own (`ip -br a`).

## Task 1 – Capture packets where your machine IP is the source (ping test)

**Terminal 1 – capture:**

```bash
sudo tcpdump -i eno1 src host 192.168.76.17
```

**Terminal 2 – generate traffic (Ctrl+C to stop):**

```bash
ping 192.168.72.20
```

## Task 2 – Capture packets going to port 443 (curl test)

**Terminal 1 – capture:**

```bash
sudo tcpdump -i eno1 dst port 443
```

**Terminal 2 – generate traffic:**

```bash
curl https://www.cdac.in
curl https://www.google.com
```

## Task 3 – Capture to a file, run nslookup, read back per domain

**Terminal 1 – capture to file (Ctrl+C to stop after Terminal 2 is done):**

```bash
sudo tcpdump -i eno1 -w dns_capture.pcap
```

**Terminal 2 – DNS lookups:**

```bash
nslookup cdac.in
nslookup micromax.in
nslookup wikipedia.org
```

**Read the file and display packets for each domain:**

```bash
tcpdump -r dns_capture.pcap 'udp port 53' | grep -i "cdac.in"
tcpdump -r dns_capture.pcap 'udp port 53' | grep -i "micromax.in"
tcpdump -r dns_capture.pcap 'udp port 53' | grep -i "wikipedia.org"
```

## Quick Reference

| Command | Purpose |
|---|---|
| `-i eno1` | Capture on interface `eno1` |
| `src host <IP>` | Filter: source IP |
| `dst port 443` | Filter: destination port 443 (HTTPS) |
| `-w file.pcap` | Write capture to file |
| `-r file.pcap` | Read capture from file |
| `'udp port 53'` | Filter: DNS traffic |
