
# 🖥️ Task : Monitor System Resources Using Netdata

## 📌 Objective
Install **Netdata** using Docker to monitor **system and application performance metrics** in real-time, and capture screenshots of the dashboard.

---

## 🛠️ Tools Used
- **Netdata** — Free, open-source, real-time performance monitoring tool  
- **Docker** — To run Netdata in an isolated container environment  

---

## 🚀 Steps to Run Netdata

### **1️⃣ Pull & Run Netdata Container**

docker run -d \
  --name=netdata \
  -p 19999:19999 \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  netdata/netdata


**Explanation:**

* `-p 19999:19999` → Maps Netdata dashboard to host machine
* Mounts (`-v ...`) → Give Netdata access to system and Docker metrics
* `--cap-add SYS_PTRACE` → Allows Netdata to collect advanced process info

---

### **2️⃣ Check if Netdata is Running**

docker ps


Example:


CONTAINER ID   IMAGE             STATUS        PORTS                     NAMES
abcd1234efgh   netdata/netdata   Up 5 seconds  0.0.0.0:19999->19999/tcp   netdata


---

### **3️⃣ Access the Dashboard**

* Local Machine:


  http://localhost:19999

* Remote Server:


  http://<server-ip>:19999


---

### **4️⃣ Explore Metrics**

* **System Metrics:** CPU, RAM, Disk I/O, Network Traffic
* **Docker Metrics:** Per-container CPU, memory, I/O, network usage
* **Alerts:** View warnings & critical alerts in real-time

To quickly find Docker stats, use the dashboard search bar and type **"docker"**.

---

### **5️⃣ View Logs**


docker exec -it netdata /bin/bash
cd /var/log/netdata
ls


* `error.log` → Netdata errors
* `access.log` → Dashboard access logs
* `health.log` → Alert & health check logs

---

### **6️⃣ Stop and Remove Netdata**


docker stop netdata
docker rm netdata


---


## ⚠️ Troubleshooting

* **Port already in use** → Stop existing Netdata container or change to a different port:


docker run -d --name=netdata -p 29999:19999 netdata/netdata


* **Dashboard not loading on AWS EC2** → Open port `19999` (or custom port) in **Security Group**.

---

