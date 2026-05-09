# 🔍 Passive Reconnaissance Guide

This repository contains commands and tools for **passive reconnaissance** and **subdomain enumeration** without directly interacting with the target.

---

## 🧠 1. Passive Reconnaissance (No Direct Interaction)

### 📜 Certificate Transparency Logs

#### Using crt.sh
```bash
curl -s "https://crt.sh/?q=%.target.com&output=json" | jq -r '.[].name_value' | sort -u
```

#### Using subfinder
```bash
subfinder -d target.com -o subdomains.txt
```

---

## 🛰️ 2. OSINT Tools

### Amass (Passive Mode)
```bash
amass enum -passive -d target.com -o amass_passive.txt
```

### theHarvester
```bash
theHarvester -d target.com -b all -f results.html
```

---

## 🌐 3. Online Sources

- crt.sh → SSL Certificate logs  
- Shodan, Censys, FOFA → Internet-wide scan data  
- VirusTotal, SecurityTrails, BufferOver → Domain intelligence  

---

## 🌍 4. Subdomain Discovery / Bruteforce

### Gobuster
```bash
gobuster dns -d target.com \
-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt \
-t 50
```

### ffuf
```bash
ffuf -u https://FUZZ.target.com \
-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

### dnsrecon
```bash
dnsrecon -d target.com -t brt \
-D /usr/share/wordlists/dnsmap.txt
```

### massdns (High-Speed)
```bash
massdns -r resolvers.txt -t A -o S -w results.txt wordlist.txt
```

---

## 🔐 5. DNS Zone Transfer

```bash
dig axfr @ns1.target.com target.com
host -l target.com ns1.target.com
dnsrecon -d target.com -t axfr
```

---

## 🔗 6. Merge Results

```bash
cat amass_passive.txt assetfinder.txt subdomains.txt | sort -u > all_subdomains.txt
```

---

## 🌐 7. Find Live Hosts

### Using httprobe
```bash
cat all_subdomains.txt | httprobe > live_hosts.txt
```

### Using httpx
```bash
cat all_subdomains.txt | httpx -silent -status-code -title -o live_results.txt
```

---

## ⚙️ 8. Installation

### Install via APT
```bash
sudo apt update
sudo apt install amass gobuster dnsrecon seclists -y
```

### Install Go Tools
```bash
go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install github.com/tomnomnom/assetfinder@latest
go install github.com/projectdiscovery/httpx/cmd/httpx@latest
go install github.com/tomnomnom/httprobe@latest
```

---

## ⚠️ Disclaimer

- Use this only on authorized targets.
- Replace `target.com` with your actual target.
- Educational purposes only.

---

## ⭐ Contribution

Feel free to fork and improve this repo.
