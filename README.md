# nmap-network-scan
# Nmap Network Scan Report

## 1. Objective
To perform a network scan on a local system using Nmap and identify open ports, running services, and potential security risks.

---

## 2. Tool Used
- Nmap (Kali Linux)

---

## 3. Methodology

### Command Used
nmap -sS -sV localhost

- -sS → TCP SYN scan (stealth scan)
- -sV → Service version detection

---

## 4. Scan Results

![Scan Result](nmap -sS -sV after apache.png)

| Port | State | Service | Version |
|------|------|---------|---------|
| 80   | open | http    | Apache 2.4.66 (Debian) |

---

## 5. Additional Findings

- Default Apache web page is enabled
- Server header reveals Apache version information
- Operating System detected as Linux (Kernel 5.x)

---

## 6. Analysis

- Port 80 (HTTP) is open, indicating a running web server.
- HTTP traffic is unencrypted, making it vulnerable to interception (e.g., Man-in-the-Middle attacks).
- The Apache version (2.4.66) is exposed, which may allow attackers to identify known vulnerabilities.
- The presence of a default Apache page suggests the server is not fully hardened.

---

## 7. OS Detection Comparison (Before vs After Service Activation)

### 7.1 Before Starting Apache

**Command:**
nmap -A localhost

**Results:**
- All 1000 scanned ports were closed
- No active services detected
- OS detection was inconclusive

![Scan Result](nmap -A before apache.png)

**Analysis:**
With no running services, the system had a minimal attack surface. Nmap could not accurately fingerprint the operating system due to the absence of exposed services.

---

### 7.2 After Starting Apache

**Command:**
nmap -A localhost

**Results:**
- Port 80 opened (HTTP)
- Apache web server detected
- OS identified as Linux (Kernel 5.x)

![Scan Result](nmap -A after apache.png)

**Analysis:**
Once a service was enabled:
- Nmap successfully detected open ports
- Service version information became visible
- OS fingerprinting became more accurate

---

### 7.3 Comparison Summary

| Condition | Open Ports | OS Detection | Services |
|----------|-----------|-------------|----------|
| Before   | None      | Inconclusive | None     |
| After    | 80        | Linux        | Apache   |

---

### 7.4 Key Insight

This experiment demonstrates that OS detection and service identification depend heavily on exposed services. A system with no open ports provides minimal information to an attacker, whereas active services significantly increase both the attack surface and information disclosure.

---

## 8. Conclusion

The scan successfully identified an active web service running on port 80. While this is expected for a web server, improper configuration and information exposure can introduce security risks. Implementing proper hardening measures and using HTTPS instead of HTTP is recommended to improve security.
