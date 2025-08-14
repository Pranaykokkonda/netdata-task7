# 🖥️ System Monitoring with Netdata (via Docker)
Install and run **Netdata**, a powerful real-time monitoring tool, using Docker to visualize system and application performance metrics such as CPU, memory, disk usage, and Docker container stats.

---

## 🚀 Quick Start

### 🔧 Prerequisites

- 🐳Docker is installed and actively running on the system.
- 🔓Ensure port `19999` is open and accessible on your system's firewall or security group to allow external access to the Netdata dashboard.


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
```

### 🔍Breakdown

| Command                                                                                              | Explanation                                                                                    |
| -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `docker run -d`                                                                                    | Runs the container in **detached mode** (in the background).                                   |
| `--name=netdata`                                                                                   | Names the container `netdata` for easier reference.                                            |
| `-p 19999:19999`                                                                                   | Maps port **19999** on your host to the container (Netdata's web dashboard runs on this port). |
| `-v /etc/passwd:/host/etc/passwd:ro`<br>`-v /etc/group:/host/etc/group:ro`                         | Provides read-only access to host user and group information.                                  |
| `-v /proc:/host/proc:ro`<br>`-v /sys:/host/sys:ro`<br>`-v /etc/os-release:/host/etc/os-release:ro` | Mounts system information for accurate monitoring of the host.                                 |
| `-v /var/run/docker.sock:/var/run/docker.sock:ro`                                                  | Lets Netdata access Docker engine data to monitor running containers.                          |
| `--cap-add SYS_PTRACE`                                                                             | Grants extra permissions needed for deeper system inspection (e.g. per-process metrics).       |
| `--security-opt apparmor=unconfined`                                                               | Disables AppArmor profile restrictions (needed for full access on some systems).               |
| `netdata/netdata`                                                                                  | The official Netdata Docker image.                                                             |

---
### 🌐 Access the Netdata Dashboard

Browse the netdata dashboard with:
**ip-address:19999**

**You'll see a real-time dashboard with:**
- CPU Usage
- Memory
- Disk I/O
- Docker Containers
  
---
### Logs 📁 
View Netdata Logs with below command:
```bash
docker exec -it netdata bash
cat /var/log/netdata/error.log
```

---
### 🧹 Cleanup

To stop and remove Netdata:

```bash
docker stop netdata
docker rm netdata
```

---
##  ✅Deliverable Output:

### Netdata Dashboard Usage:
![image alt](https://github.com/Pranaykokkonda/netdata-task7/blob/830128075d57998199e945fe55108502f89336bd/01-usage-dashboard.PNG)

### Docker Images:
![image alt](https://github.com/Pranaykokkonda/netdata-task7/blob/c886b071b3e0ecac905a95fc0fbd228ff0097a95/02-docker-images.png)

### Docker Containers:
![image alt](https://github.com/Pranaykokkonda/netdata-task7/blob/c886b071b3e0ecac905a95fc0fbd228ff0097a95/03-d-container.png)
![image alt](https://github.com/Pranaykokkonda/netdata-task7/blob/c886b071b3e0ecac905a95fc0fbd228ff0097a95/04-d-containers.png)

### Docker Summary:
![image alt](https://github.com/Pranaykokkonda/netdata-task7/blob/c886b071b3e0ecac905a95fc0fbd228ff0097a95/05-d-summary.png)

---
