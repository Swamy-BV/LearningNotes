# VirtualBox Ubuntu Setup Guide For Development

## Prerequisites
- Download and install [VirtualBox](https://www.virtualbox.org/)
- Install [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- Ensure your system has **VT-x/AMD-V** enabled in BIOS

## Download latest Ubuntu
- Download latest Ubuntu ISO from [Ubuntu](https://ubuntu.com/download/desktop)

## Creating a New Virtual Machine
1. Open **VirtualBox** and click **New**.
2. Enter a **name**.
3. Select **ISO Image** of Ubuntu. The **type, subtype, and version** should populate automatically.
4. Click **Unattended Install** and enter **username** and **password**.
5. Allocate **RAM** (recommended: **4-8GB+** for Linux).
6. Allocate **Processors** (recommended: **Half of the total number of cores, up to the pink line**).
7. Select **Create a virtual hard disk now** → Choose **VDI** (VirtualBox Disk Image).
8. If you don't select **Pre-allocated**, you have effectively selected **Dynamically allocated** disk.
9. Set the disk size (e.g., **100GB** for Linux) and click **Finish**.

## Configuring VM Settings
1. Select the VM and click **Settings**.
2. **Display** → Increase **Video Memory** to **128MB+**.
3. **Network** → Choose **NAT** or **Bridged Adapter** (for internet access).

## Installing the Guest OS
1. Start the VM
2. Let it bootup, if you see black screen shutdown the VM and start again.
3. Follow the OS installation steps.

## Install VirtualBox Extension Pack
[VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads).
