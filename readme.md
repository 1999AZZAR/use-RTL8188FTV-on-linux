# Realtek RTL8188FTV WiFi Adapter on Linux

This step-by-step guide is designed to help you set up the Realtek RTL8188FTV WiFi adapter on Linux. The instructions were tested on **Ubuntu 22.04.1 LTS (x86_64)** with **Linux kernel 5.15.0-58-generic**. If you're using a different distribution or version, some steps may vary. Feel free to ask questions if you encounter any issues.

---

## Prerequisites

1. **Plug in the Realtek RTL8188FTV WiFi adapter** into a USB port on your Linux PC.
2. **Boot up your Linux PC**.

---

## Step 1: Open Terminal

1. Click the **Grid button** (9 dots) to open the Application drawer.
2. Search for and open the **Terminal** application.
   - The Terminal window will have a black background with white text, similar to the Windows Command Prompt.

---

## Step 2: Check if the WiFi Adapter is Detected

Verify that the Realtek RTL8188FTV WiFi adapter is recognized by your system.

### Option 1: Check Network Interfaces
1. Run the following command in the Terminal:
   ```bash
   ip a
   ```
2. Look for a network interface with a prefix like `wlx` (e.g., `wlx1234567890ab`).

### Option 2: Check USB Devices
1. Run the following command in the Terminal:
   ```bash
   lsusb
   ```
2. Look for an entry similar to:
   ```
   Realtek Semiconductor Corp. RTL8188FTV 802.11b/g/n 1T1R 2.4G WLAN Adapter
   ```

---

## Step 3: Update System Packages

Ensure your system is up to date before proceeding.

1. Update the package list:
   ```bash
   sudo apt update
   ```
2. Upgrade installed packages:
   ```bash
   sudo apt upgrade
   ```
3. Install the `net-tools` package (optional but useful for network troubleshooting):
   ```bash
   sudo apt install net-tools
   ```

---

## Step 4: Add the Kelebek Repository

The Kelebek repository contains the driver for the Realtek RTL8188FTV adapter. Add it to your system:

1. Add the repository:
   ```bash
   sudo add-apt-repository ppa:kelebek333/kablosuz
   ```
2. Update the package list again:
   ```bash
   sudo apt-get update
   ```

---

## Step 5: Install the WiFi Adapter Driver

Install the driver for the Realtek RTL8188FTV adapter:

1. Install the driver:
   ```bash
   sudo apt-get install rtl8188fu-dkms
   ```
2. (Optional) To remove the driver later, use:
   ```bash
   sudo apt purge rtl8188fu-dkms
   ```

For more details, visit the [GitHub repository](https://github.com/kelebek333/rtl8188fu).

---

# Step 6: Configure the Driver

Adjust the driver configuration to ensure proper functionality:

#### 1. Disable IPS Mode (Optional but Recommended)
IPS (Inactive Power Save) mode can sometimes cause connectivity issues. Disabling it is recommended for better performance:

1. Create or update the driver configuration file:
   ```bash
   echo "options rtl8188fu rtw_ips_mode=0" | sudo tee /etc/modprobe.d/rtl8188fu.conf
   ```
   - This command writes `options rtl8188fu rtw_ips_mode=0` to the file `/etc/modprobe.d/rtl8188fu.conf`.
   - If the file already exists, it will be overwritten. To append instead, use `tee -a`.

2. Reload the driver to apply the changes:
   ```bash
   sudo modprobe -rv rtl8188fu && sudo modprobe -v rtl8188fu
   ```
   - This unloads (`-r`) and reloads (`-v`) the `rtl8188fu` module with the new configuration.

#### 2. Fix MAC Address Changes (Optional)
If the MAC address of your adapter changes after every reboot, you can set a static MAC address:

1. Replace `xx:xx:xx:xx:xx:xx` with your desired MAC address and run:
   ```bash
   echo "options rtl8188fu rtw_ips_mode=0 rtw_initmac=xx:xx:xx:xx:xx:xx" | sudo tee /etc/modprobe.d/rtl8188fu.conf
   ```
   - This sets both `rtw_ips_mode=0` and a static MAC address (`rtw_initmac=xx:xx:xx:xx:xx:xx`).

2. Reload the driver to apply the changes:
   ```bash
   sudo modprobe -rv rtl8188fu && sudo modprobe -v rtl8188fu
   ```

---

## Step 7: Reboot Your PC

Restart your system to ensure all changes are applied:

1. Click the **Power menu** (top-right corner of the screen).
2. Select **Restart**.

---

## Step 8: Connect to Wi-Fi

Connect to your Wi-Fi network:

1. Open **Settings** from the Application drawer.
2. Go to **Wi-Fi** and turn it on if it’s off.
3. Select your network and enter the password.

---

## How to Remove the Driver and PPA

If you no longer need the driver or the Kelebek repository, follow these steps:

1. Remove the driver:
   ```bash
   sudo apt purge rtl8188fu-dkms
   ```
2. Remove the Kelebek repository:
   ```bash
   sudo add-apt-repository --remove ppa:kelebek333/kablosuz
   ```
3. Reboot your PC to complete the removal:
   ```bash
   sudo reboot
   ```

---

That’s it! Your Realtek RTL8188FTV WiFi adapter should now be fully functional on your Linux PC. If you encounter any issues, refer to the [GitHub repository](https://github.com/kelebek333/rtl8188fu) or seek help from the Linux community.
