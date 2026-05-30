# 🛰️ ONU Pro Tool v2.0
### One button, 4 seconds, magical configuration ⚡

---

## Why this tool ❓
Manual ONU provisioning in the field is often:
* **Slow:** Taking 5–10 minutes per device.
* **Error-prone:** High chance of manual IP and VLAN input mistakes.
* **Cumbersome:** Requires dragging laptops, config cables, and complex setups into tight spaces.
* **Non-scalable:** Unfriendly for field technicians dealing with dozens of unknown  and different routers .

## The Solution 💡 
**ONU Pro Tool** transforms provisioning into a fully automated workflow using an **Orange Pi** (or similar micro-computers). By moving from heavy UI automation (Selenium) to pure **HTTP API Requests**, the tool communicates directly with the ONU hardware level.
* ⚡ **Average provisioning time:** ~4 seconds.
* 🤖 **Interaction:** 2% Manual input required (Just enter VLAN & PPPoE credentials).
* 🪶 **Ultra-Lightweight:** Runs seamlessly on low-cost single-board computers.

---

## 🧩 System Architecture & Logic
The automation follows a streamlined, highly optimized lifecycle:
1. **Micro-Server Boot:** Orange Pi auto-boots and broadcasts a local secure Hotspot (`10.42.0.1`).
2. **Device Handshake:** Once connected via LAN, the tool continuously pings and bridges the static IP to reach the ONU gateway (`192.168.100.1`).
3. **Smart Token Extraction:** Scrapes the login tokens (`GetRandCnt` & `x.X_HW_Token`) on-the-fly using regex, bypassing GUI rendering entirely.
4. **Execution Streams:** Sends asynchronous `POST` configuration requests to trigger LAN mapping, WAN profile writing, and remote management access (WAN ACL).
5. **Instant Field Logging:** Uses **Server-Sent Events (SSE)** to stream logs back to the tech's phone screen line-by-line in real-time.

---

## 🛠️ Key Features
* 🚀 **Plug & Play:** Starts automatically on system boot via `systemd`.
* 🧠 **Pure HTTP API Layer:** 10x faster than legacy Selenium-based scrapers.
* 🌐 **Dual Action:** Supports both **Automatic XML Configuration Upload** and **Instant Manual Custom Configuration** (VLAN + PPPoE User/Pass).
* 🖥️ **Live Monitoring Console:** Beautiful, responsive web panel built with SSE to trace the field process.

---

## 📂 Project Structure
To keep the repository modular and clean, the source codes are isolated inside structured folders:
```text
ONU-Pro-Tool/
├── src/
│   ├── app.py               # Core Flask API & Network Automation logic
├── templates/
│   └── index.html           # Live Web Console Dashboard UI
├── config/
│   └── hw_ctree.xml         # XML Configuration Template for Huawei ONUs
├── scripts/
│   └── onu_automation.service # Systemd service for auto-booting
└── README.md                # Documentation
```
## 〽️Installation & Setup
​1. Clone the repository
```bash
git clone [https://github.com/ahmed95i/auto-onu-programming-.git](https://github.com/ahmed95i/auto-onu-programming-.git)
cd auto-onu-programming-
```
2. Install dependencies
```bash
pip3 install flask requests
```
3. Setup systemd service for Headless Field Booting.
```bash
sudo cp scripts/onu_automation.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable onu_automation
sudo systemctl start onu_automation
```
## 🔑How it Works (Field View)

* **Connect:** Power the Orange Pi via a small power bank, and hook up a patch cord from the Pi's LAN port to the Huawei ONU.
* **​Access:** Connect your smartphone to the ONU-Tool-Pro Wi-Fi network and browse to http://10.42.0.1:5000.
* **Or:** download app onu pro tool.
​* **Execute:** Trigger the script from the web UI, watch the log stream finish in 4 seconds
## ​🔮Future Improvements
* **​[✅️]** Migrated from Selenium to raw HTTP requests for instant speed.
* **​[☑️]** Multi-vendor ONU support (ZTE / FiberHome / Nokia).
* **​[☑️]** Smart retry loop algorithms for unstable physical connections.
* **​[☑️]** Remote management over net to onu or routers 
