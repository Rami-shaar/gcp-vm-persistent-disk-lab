# ☁️ GCP VM + Persistent Disk Lab

This project demonstrates how to manually build a secure and production-style Google Cloud Platform (GCP) environment by deploying a Linux VM, setting up a web server, and attaching a Persistent Disk for storage.

---

## 📐 Architecture Overview

GCP Project: `cloud-practice-project`

┌─────────────────────────────┐
│    GCP Virtual Network      │
│   (Default VPC used here)   │
│                             │
│  ┌───────────────────────┐  │
│  │   Compute Engine VM   │  │
│  │  gcp-linux-vm         │  │
│  │  Region: us-central1  │  │
│  └───────────────────────┘  │
│          │                  │
│          │ Attached Disk    │
│          ▼                  │
│   🟢 Persistent Disk        │
│   Name: gcp-data-disk      │
│   Size: 10 GB              │
└─────────────────────────────┘

---

## 🔧 What You Set Up

✅ Compute Engine VM  
- Name: `gcp-linux-vm`  
- Machine Type: `e2-micro (Free Tier eligible)`  
- OS: Ubuntu 22.04 LTS (or Debian 12)  
- Boot Disk: 10 GB Balanced Persistent Disk  
- Firewall: HTTP (Port 80) allowed  

✅ Persistent Disk  
- Name: `gcp-data-disk`  
- Size: 10 GB  
- Type: Balanced Persistent Disk  
- Attached to: `gcp-linux-vm`

---

## 🔐 How to Connect & Configure

1. Connect to VM  
GCP Console → Compute Engine → VM instances → SSH → Open in browser window

2. Install Apache Web Server  
sudo apt update  
sudo apt install apache2 -y  
sudo systemctl start apache2

3. Verify Web Server  
Open in your browser:  
http://<your-vm-external-ip>  
You should see the Apache2 Default Page

4. Format & Mount Persistent Disk  
lsblk  
sudo mkfs.ext4 /dev/sdb  
sudo mkdir /mnt/data  
sudo mount /dev/sdb /mnt/data  
df -h

5. (Optional) Make Mount Persistent  
sudo blkid /dev/sdb  
sudo nano /etc/fstab  
Add this line at the end:  
UUID=<your-disk-uuid> /mnt/data ext4 defaults 0 0

---

## 🧠 Skills Practiced

✅ GCP Compute Engine VM creation  
✅ Connecting via browser-based SSH  
✅ Installing Apache Web Server  
✅ Persistent Disk creation & attachment  
✅ Linux disk formatting & mounting  
✅ Real-world cloud storage configuration

