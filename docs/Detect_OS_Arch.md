# System OS and Architecture Detection

This document provides commands to check the operating system and CPU architecture on **Linux**

## Linux Commands
Open a terminal and run the following commands:

### **Check OS Name and Version**
```sh
uname -s   # Shows the OS name (e.g., Linux)
uname -r   # Displays the kernel version
cat /etc/os-release  # Provides detailed OS information
```
**Example Output:**
```cmd
Linux
5.15.0-84-generic
PRETTY_NAME="Ubuntu 22.04 LTS"
```

### **Check CPU Architecture**
```sh
uname -m    # Shows the machine hardware name (e.g., x86_64, aarch64)
lscpu | grep "Architecture"  # More detailed CPU info
```
**Example Output:**
```
Architecture: x86_64
```

## Common Architecture Outputs

| Architecture | Description |
|-------------|------------|
| `x86_64` / `amd64` | 64-bit Intel/AMD CPU (most desktops, servers) |
| `aarch64` / `arm64` | 64-bit ARM CPU (Raspberry Pi, Apple M1/M2, some servers) |
| `armv7l` / `armhf` / `arm` | 32-bit ARM CPU (older Raspberry Pi, embedded devices) |

Use these commands to determine your system's OS and architecture type. 🚀

