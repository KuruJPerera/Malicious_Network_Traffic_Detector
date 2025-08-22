# Network Traffic Monitoring Script

## 📌 Overview
This Python script monitors **active network connections** on your system to detect **suspicious or unusual activity**.  
It checks for:
- Connections to **blacklisted IP addresses** (demo list included).
- **Excessive connections** opened by the same process (default: > 20).

Findings are written to a **human-readable log** and a **structured JSON file** for security analysis.

---

## ⚙️ Features
- Uses `psutil` to enumerate current **INET** connections.
- Records key fields for flagged connections:
  - Date & time
  - Process ID (PID)
  - Local IP & port
  - Remote IP & port
  - Reason flagged (`Blacklisted IP` or `Excessive connections`)
- Configurable thresholds and scan interval.
- Saves results to:
  - `network_alerts.log` (standard log)
  - `network_alerts.json` (JSON records)

---

## 📂 Alert Output Example

When a connection hits a **blacklisted IP**:
```json
{
  "timestamp": "2025-08-22 14:35:10",
  "pid": 1234,
  "local_ip": "192.168.1.10",
  "local_port": 50544,
  "remote_ip": "104.22.55.228",
  "remote_port": 80,
  "reason": "Blacklisted IP"
}
```

When a process has **too many connections**:
```json
{
  "timestamp": "2025-08-22 14:40:20",
  "pid": 5678,
  "connections": 45,
  "reason": "Excessive connections"
}
```

---

## 🚀 How to Run

1. **Clone this repository**
   ```bash
   git clone https://github.com/yourusername/network-traffic-monitor.git
   cd network-traffic-monitor
   ```

2. **Make sure you have Python 3 installed**
   ```bash
   python --version
   ```

3. **Install dependencies**
   ```bash
   pip install psutil
   ```
   *(Alternatively create `requirements.txt` with `psutil>=5.9.0` and run `pip install -r requirements.txt`.)*

4. **Run the script**
   ```bash
   python network_monitor.py
   ```
   Replace `network_monitor.py` with your actual filename.

5. **(Optional) Quick demo**
   - The script includes sample blacklisted IPs for training sites (e.g., tryhackme.com).
   - With the script running, visit `http://tryhackme.com` in your browser.
   - You should see a warning in the terminal and entries appended to:
     - `network_alerts.log`
     - `network_alerts.json`

---

## 📄 Where to View Results
- **Terminal:** real-time status (e.g., “No anomalies detected.” or alert details).
- **Log file:** `network_alerts.log` (timestamps + messages).
- **JSON file:** `network_alerts.json` (structured records suitable for ingestion/analysis).

---

## 🛠️ Configuration (inside the script)
- `blacklisted_ips` — set of IPs to flag.
- `connection_limit` — max allowed connections per PID (default: `20`).
- `scan_interval` — seconds between scans (default: `10`).
- `log_file` / `json_file` — output file paths.

---
