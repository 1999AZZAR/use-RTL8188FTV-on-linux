# Realtek RTL8188FTV WiFi Adapter on Linux

This step-by-step guide is designed for beginners who want to use the Realtek RTL8188FTV WiFi adapter on Linux. The instructions were tested on Ubuntu 22.04.1 LTS x86_64 with Linux 5.15.0-58-generic. If you're using a different distro or version, some steps may vary. Feel free to ask any questions if needed.

### Prerequisites:

- Plug in the Realtek RTL8188FTV WiFi adapter into one of the USB ports of your Linux PC.
- Boot up your Linux PC.

## Step 1: Open Terminal

1. Click the Grid button (9 dots) to open the Application drawer.
2. Find and click "Terminal" to open it.
3. A Terminal window with a black background and white text will appear, similar to the Windows Command Prompt.

## Step 2: Check WiFi Adapter

### Check if the Realtek RTL8188FTV WiFi adapter is detected by the OS:

1. In Terminal, enter `ip a` and press Enter.
2. Look for a network interface with a prefix "wlx".
3. Alternatively, enter `lsusb` in Terminal and press Enter.
4. Look for "Realtek Semiconductor Corp. RTL8188FTV 802.11b/g/n 1T1R 2.4G WLAN Adapter".

## Step 3: Update Linux Packages

### Update your Ubuntu to the latest packages:

1. Enter `sudo apt update` in Terminal and press Enter.
2. Enter `sudo apt upgrade` in Terminal and press Enter.
3. Enter `sudo apt install net-tools` in Terminal and press Enter.

## Step 4: Add Kelebek Repository

### Kelebek is the contributor who wrote the driver for the adapter. You can find more details [here](https://launchpad.net/~kelebek333/+archive/ubuntu/kablosuz):

1. Enter `sudo add-apt-repository ppa:kelebek333/kablosuz` in Terminal and press Enter.
2. Enter `sudo apt-get update` in Terminal and press Enter.

## Step 5: Install WiFi Adapter

### Install the driver for the adapter:

1. Enter `sudo apt-get install rtl8188fu-dkms` in Terminal and press Enter.
2. (Optional) To remove the driver, enter `sudo apt purge rtl8188fu-dkms` in Terminal and press Enter.

Refer to the [GitHub repository](https://github.com/kelebek333/rtl8188fu) for more information.

## Step 6: Change Driver Config

1. Enter `echo "options rtl8188fu rtw_ips_mode=0" | sudo tee /etc/modprobe.d/rtl8188fu.conf` in Terminal and press Enter.
2. Enter `sudo modprobe -rv rtl8188fu && sudo modprobe -v rtl8188fu` in Terminal and press Enter.

## Step 7: Reboot PC

### Restart your Linux PC to complete the setup:

1. Click the Power menu (top right of the screen).
2. Choose Restart.

## Step 8: Connect to Wi-Fi

### Connect to a Wi-Fi network:

1. Click Grid button > Settings > Wi-Fi.
2. Turn ON Wi-Fi if it's off.
3. Select the network and enter the password.

That's it! You should now be able to use the Realtek RTL8188FTV WiFi adapter on your Linux PC.

### How to Remove the Driver and PPA

If you want to remove the driver and the PPA, follow these steps:

1. Open Terminal.
2. Enter `sudo apt purge rtl8188fu-dkms` in Terminal and press Enter.
3. Enter `sudo add-apt-repository --remove ppa:kelebek333/kablosuz` in Terminal and press Enter.
4. Reboot your PC to complete the removal.

That's it! You should now be able to use the Realtek RTL8188FTV WiFi adapter on your Linux PC.
