# 🖥️ System Monitoring with Netdata (via Docker)
Install and run **Netdata**, a powerful real-time monitoring tool, using Docker to visualize system and application performance metrics such as CPU, memory, disk usage, and Docker container stats.

---

## 🚀 Quick Start

### 🔧 Prerequisites

- Docker installed and running
- Port `19999` available on your system

---

### 🐳 Run Netdata with Docker

```bash
docker run -d --name=netdata \
  -p 19999:19999 \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /etc/os-release:/host/etc/os-release:ro \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  netdata/netdata
