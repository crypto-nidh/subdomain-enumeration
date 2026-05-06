# subdomain-enumeration
subdomain enumeration commands 

# 🔍 Passive Reconnaissance Guide

This repository contains commands and tools for **passive reconnaissance** and **subdomain enumeration** without directly interacting with the target.

---

## 🧠 1. Passive Reconnaissance (No Direct Interaction)

### 📜 Certificate Transparency Logs

#### Using crt.sh
```bash
curl -s "https://crt.sh/?q=%.target.com&output=json" | jq -r '.[].name_value' | sort -u
