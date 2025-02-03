# 📋 Enabling Copy-Paste in VirtualBox

Copy-paste (clipboard sharing) between **host** and **guest** OS is disabled by default in VirtualBox. Follow these steps to enable it.

---

## ✅ 1️⃣ Enable Clipboard Sharing
1. **Start VirtualBox** and select your virtual machine.
2. Go to **Settings** → **General** → **Advanced**.
3. Set **Shared Clipboard** to:
   - **Bidirectional** (For both host-to-guest and guest-to-host copy-paste).
   - **Host to Guest** (For one-way copy from host to VM).
4. Click **OK** to save changes.

---

## ✅ 2️⃣ Install VirtualBox Guest Additions
For copy-paste to work, **Guest Additions** must be installed inside the VM.

### 📥 **For Ubuntu/Debian (Guest OS)**
1. Start your VM and open a **Terminal**.
2. Run the following command:
   ```bash
   sudo apt update
   sudo apt install virtualbox-guest-utils virtualbox-guest-x11
### Reboot 
- reboot the ubuntu
  ```bash
   sudo reboot
---
### ✅ You may also do the following steps if nothing works
1. Required before installing Guest Additions software.   
   ```bash
   sudo apt install gcc make perl bzip2
2. In VirtualBox, go to Devices → Insert Guest Additions CD.
3. Click on the CD icon on the Ubuntu sidebar.
4. Click on Run Software to start the installation.
5. Once the installation is complete, reboot the system:
