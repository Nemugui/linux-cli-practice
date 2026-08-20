# 🗡️ Daily CLI Practice — Nemugui
**Repository:** linux-cli-practice
**Rule:** I do this every single day before studying. No exceptions.
**Time needed:** 20–30 minutes

---

## How This Works
```
Every phase you complete → new tasks get added
Old tasks stay → builds muscle memory
Do them in order → each one builds on the previous
Document your output → paste results in your daily log
```

---

## 🔥 PHASE 1 PRACTICE — Computer Fundamentals & CLI

### Warm Up (Do this EVERY day, no exceptions)
```bash
# The holy trinity — first 3 commands every session
whoami && pwd && ls -la
```
Expected output: your username, current location, file listing with permissions.

---

### Task 1 — Navigation Gauntlet
```bash
# Go home, list everything, go to root, come back
cd ~ && ls -la && cd / && ls && cd ~ && pwd
```
What you should see: home folder contents, root directory contents, confirm back home.

---

### Task 2 — File Creation Chain
```bash
# Create today's practice folder with the date
mkdir practice-$(date +%Y%m%d) && cd practice-$(date +%Y%m%d) && pwd
```
Then inside it:
```bash
echo "Practice session: $(date)" > session.txt && cat session.txt
```

---

### Task 3 — Folder Structure Building
Build this structure in ONE command (no cd allowed):
```
cyberlab/
├── notes.txt      → "Daily practice notes"
├── tools/
│   └── nmap.txt   → "Tool: Network Scanner"
└── logs/
    └── session.txt → "Session: (today's date)"
```

```bash
mkdir -p cyberlab/tools cyberlab/logs && echo "Daily practice notes" > cyberlab/notes.txt && echo "Tool: Network Scanner" > cyberlab/tools/nmap.txt && echo "Session: $(date)" > cyberlab/logs/session.txt
```

Verify it:
```bash
ls cyberlab/ && ls cyberlab/tools/ && ls cyberlab/logs/
```

---

### Task 4 — File Manipulation
```bash
# Copy, move, rename, delete
cp cyberlab/notes.txt cyberlab/notes-backup.txt && ls cyberlab/
mv cyberlab/notes-backup.txt cyberlab/logs/ && ls cyberlab/logs/
rm cyberlab/logs/notes-backup.txt && ls cyberlab/logs/
```

---

### Task 5 — Echo and Redirection
```bash
# Write multiple lines to a file
echo -e "Name: Josh\nCourse: BSIT\nGoal: Ethical Hacker\nPhase: 2" > cyberlab/profile.txt
cat cyberlab/profile.txt
```

Then append without overwriting:
```bash
echo "Date: $(date)" >> cyberlab/profile.txt && cat cyberlab/profile.txt
```

---

### Task 6 — Piping and Filtering
```bash
# See all running processes, filter for specific ones
ps aux | grep kali
ps aux | head -10
ps aux | wc -l
ls -la | grep "^d"
ls -la | grep "^-"
```

`wc -l` counts lines — tells you total number of processes running.
`^d` filters only directories, `^-` filters only files.

---

### Task 7 — Search and Find
```bash
# Search inside files
grep "Hacker" cyberlab/profile.txt && echo "FOUND" || echo "NOT FOUND"
grep "password" cyberlab/profile.txt ; echo $?
find cyberlab/ -name "*.txt"
find cyberlab/ -name "*.txt" | wc -l
```

---

### Task 8 — Wildcards
```bash
# Display all txt files at different levels
cat cyberlab/*.txt
cat cyberlab/tools/*.txt
cat cyberlab/logs/*.txt
cat cyberlab/*.txt cyberlab/tools/*.txt cyberlab/logs/*.txt
```

---

### Task 9 — System Reconnaissance
```bash
# Know your system
whoami
id
hostname
uname -a
echo $PATH
which nmap
which python3
```

---

### Task 10 — Process Investigation
```bash
# Find what's running
ps aux | grep -v grep | head -20
ps aux --sort=-%cpu | head -5
ps aux --sort=-%mem | head -5
top -bn1 | head -20
```

---

## 🌐 PHASE 2 ADDITIONS — Networking

*(Add these after completing Phase 2 topics)*

### Task 11 — Network Identity Check
```bash
# Always know where you are on the network
ip addr | grep inet
ip route show
cat /etc/resolv.conf
curl ifconfig.me
echo "Private IP check complete"
```

---

### Task 12 — Connectivity Test
```bash
# Test network connectivity
ping -c 3 google.com
ping -c 3 1.1.1.1
ping -c 3 192.168.110.1
traceroute google.com
```

---

### Task 13 — DNS Investigation
```bash
# Daily DNS checks
dig google.com | grep -A1 "ANSWER SECTION"
dig facebook.com | grep -A1 "ANSWER SECTION"
dig -x 8.8.8.8 | grep PTR
dig @1.1.1.1 google.com | grep "Query time"
dig @8.8.8.8 google.com | grep "Query time"
```

---

### Task 14 — Network Scan Practice
```bash
# Scan your home network (legal — your own network)
nmap -sn 192.168.110.0/24
nmap -sV 192.168.110.1
nmap -p 80,443,22,21,53 192.168.110.1
```

---

### Task 15 — Web Reconnaissance
```bash
# Check HTTP headers of websites
curl -I https://google.com
curl -I https://facebook.com
curl -I http://192.168.110.1
curl ifconfig.me && echo ""
```

---

### Task 16 — Active Connections
```bash
# See what your system is connected to
ss -tulnp
netstat -tulnp 2>/dev/null || ss -tulnp
ip route show
arp -a
```

### Task 17 — DNS capture
```bash
sudo tshark -i eth0 -f "port 53" &
dig google.com 
facebook.com 
github.com
kill %1
```

### Task 18 — ARP capture
```bash
sudo tshark -i eth0 -f "arp" &
ping -c 2 192.168.110.1
kill %1
```
### Task 19 — Save and analyze
```bash
sudo timeout 20 tshark -i eth0 -w /tmp/daily.pcap
tshark -r /tmp/daily.pcap | wc -l
tshark -r /tmp/daily.pcap -Y "dns" | head -10
```

---

## 📋 Daily Log Template

After every practice session, document your output:

```bash
# Create today's log automatically
mkdir -p ~/Documents/daily-logs && echo -e "DATE: $(date)\nHOSTNAME: $(hostname)\nUSER: $(whoami)\nIP: $(ip addr | grep 'inet 192' | awk '{print $2}')\nPUBLIC IP: $(curl -s ifconfig.me)\n---\nNOTES: " > ~/Documents/daily-logs/$(date +%Y%m%d).txt && cat ~/Documents/daily-logs/$(date +%Y%m%d).txt
```

---

## 🏆 Challenge Tasks (Do these when you finish the daily tasks)

### Challenge 1 — The Chain Master
Build this entire structure in ONE single chained command:
```
hacklab/
├── recon/
│   ├── targets.txt    → "Target: Home Network 192.168.110.0/24"
│   └── tools.txt      → "Tools: nmap, dig, curl, ping"
├── findings/
│   ├── ports.txt      → "Open ports found: 53, 80, 443"
│   └── services.txt   → "Services: DNS, HTTP, HTTPS"
└── report.txt         → "Report by: Josh | Date: (today)"
```
Then display all files combined using wildcards.

---

### Challenge 2 — The Investigator
```bash
# Find all information about your system in one session
echo "=== SYSTEM INFO ===" && whoami && hostname && uname -a && echo "=== NETWORK INFO ===" && ip addr | grep inet && echo "=== PUBLIC IP ===" && curl -s ifconfig.me && echo "" && echo "=== PROCESSES ===" && ps aux | wc -l && echo "processes running" && echo "=== DISK SPACE ===" && df -h | grep -v tmpfs
```

---

### Challenge 3 — The Log Analyzer
```bash
# Analyze system logs like a real security analyst
sudo grep "Failed" /var/log/auth.log 2>/dev/null | tail -10
sudo grep "Accepted" /var/log/auth.log 2>/dev/null | tail -10
sudo grep "sudo" /var/log/auth.log 2>/dev/null | tail -10
```

---

### Challenge 4 — DNS Enumeration
```bash
# Enumerate DNS records for multiple domains
for domain in google.com facebook.com github.com tryhackme.com; do
  echo "=== $domain ===" && dig $domain A +short
done
```

---

### Challenge 5 — Port Scanner One-liner
```bash
# Quick port check on your router
for port in 21 22 23 25 53 80 443 3306 8080 8443; do
  nmap -p $port --open 192.168.110.1 2>/dev/null | grep "open" && echo "Port $port is OPEN on router" || echo "Port $port closed"
done
```

---

## 📈 Progress Tracker

Mark off when you can do each task WITHOUT looking at the cheat sheet:

```
Phase 1 Tasks:
[ ] Task 1  — Navigation Gauntlet
[ ] Task 2  — File Creation Chain
[ ] Task 3  — Folder Structure Building
[ ] Task 4  — File Manipulation
[ ] Task 5  — Echo and Redirection
[ ] Task 6  — Piping and Filtering
[ ] Task 7  — Search and Find
[ ] Task 8  — Wildcards
[ ] Task 9  — System Reconnaissance
[ ] Task 10 — Process Investigation

Phase 2 Tasks:
[ ] Task 11 — Network Identity Check
[ ] Task 12 — Connectivity Test
[ ] Task 13 — DNS Investigation
[ ] Task 14 — Network Scan Practice
[ ] Task 15 — Web Reconnaissance
[ ] Task 16 — Active Connections

Challenge Tasks:
[ ] Challenge 1 — The Chain Master
[ ] Challenge 2 — The Investigator
[ ] Challenge 3 — The Log Analyzer
[ ] Challenge 4 — DNS Enumeration
[ ] Challenge 5 — Port Scanner One-liner
```

---

## 🔑 The Golden Rule

```
You are not done with daily practice until:
→  you typed every command from memory
→  you understood the output
→  you documented at least one interesting finding
→  you asked yourself "what does this mean for security?"
```

---

## 📅 What Gets Added Each Phase

```
Phase 3  (Linux)      → file permissions, user management,
                        bash scripting, cron jobs, log analysis
Phase 4  (Python)     → run python scripts, automate tasks
Phase 5  (Web)        → curl requests, header analysis,
                        cookie inspection
Phase 6  (Cyber Fund) → hash checking, encryption tools
Phase 7  (Eth Hack)   → metasploit basics, exploitation practice
Phase 8  (Web App)    → burp suite, sql injection practice
Phase 9  (Net Sec)    → wireshark captures, traffic analysis
Phase 10 (Forensics)  → file carving, log investigation
Phase 11 (SOC)        → splunk queries, alert analysis
Phase 12 (Cloud)      → aws cli, cloud enumeration
Phase 13 (Malware)    → sandbox analysis, yara rules
```

---

*Daily practice file by Nemugui | Updated as phases are completed*
*Remember: 20 minutes every day beats 3 hours once a week*
