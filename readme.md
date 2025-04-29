
# 🌐 Network Lesson Summary

## 📌 NetworkManager Overview

- Introduced in Red Hat Enterprise Linux 7.
- Manages dynamic network configuration.
- Supports: Ethernet, Bridge, Bond, Teams, Wifi, Mobile.
- Uses `ifcfg` configuration files.

## 🧰 Tools

| Tool                 | Description                                                             |
|----------------------|-------------------------------------------------------------------------|
| `nmtui`              | Text-based user interface for NetworkManager                            |
| `nmcli`              | Command-line interface for managing network interfaces                  |
| `nm-connection-editor` | GUI tool to manage network connections                                |

## 📂 Configuration Files

- Network configs stored in: `/etc/sysconfig/network-scripts/`
- Example:
  ```bash
  TYPE=Ethernet
  NAME=eno123654
  UUID=567fa98b00-cf642324-ad456456
  DEVICE=eno123654
  ONBOOT=YES
  BOOTPROTO=dhcp
  ```

## 🖥️ `nmcli` Command Usage

- General Status:
  ```bash
  nmcli general status
  ```
- Show connections:
  ```bash
  nmcli connection show
  ```
- Device status:
  ```bash
  nmcli device status
  ```
- Connect/disconnect a device:
  ```bash
  nmcli device connect eno33554968
  nmcli device disconnect eno33554968
  ```
- Configure IP and DNS:
  ```bash
  nmcli connection add type ethernet con-name eno33554968 ifname eno33554968 ip4 192.168.1.100 gw4 192.168.1.1
  nmcli connection modify eno33554968 ipv4.dns "8.8.8.8 8.8.4.4"
  nmcli -p connection show eno33554968
  ```

## 🔧 `ip` Command Usage

- Show interfaces:
  ```bash
  ip link show
  ```
- Bring interface up/down:
  ```bash
  ip link set eno33554968 down
  ip link set eno33554968 up
  ```
- IP address configuration:
  ```bash
  ip addr show
  ip addr add 192.168.1.100/24 dev eno16777736
  ip addr del 192.168.1.43/24 dev eno16777736
  ```
- Routing:
  ```bash
  ip route
  ip route add default via 192.168.2.1 dev eno16777736
  ip route del 192.168.2.1 dev eno16777736
  ```

## 🔐 OpenSSH

- Provides secure remote sessions, file transfers, and TCP tunneling.
- Uses encryption (symmetric/asymmetric).
- Install:
  ```bash
  yum -y install openssh-server openssh-clients
  ```
- Components:
  - `ssh`, `scp`, `sftp`, `ssh-add`, `ssh-agent`, `ssh-copy-id`, `ssh-keyscan`

## 🧳 SSH Usage Examples

- Connect to server:
  ```bash
  ssh ludo@192.168.0.10
  ssh -X ludo@192.168.0.10
  ```
- Remote command execution:
  ```bash
  ssh root@192.168.1.20 tar xvfz file.tar.gz
  ```
- Copy files with SCP:
  ```bash
  scp -r /home/ludo ludo@192.168.0.10:/home/
  scp -r root@192.168.0.10:/home/ /home/
  ```
- Manage files with SFTP:
  ```bash
  sftp root@192.168.0.10
  ```

## 🔑 SSH Key Management

- Asymmetric key pair: **Private** (keep secret), **Public** (shared).
- Generate key pair:
  ```bash
  ssh-keygen -t dsa -C "clé de ludo"
  ```
- Copy public key to server:
  ```bash
  ssh-copy-id 192.168.1.20
  ```
- Authorized keys location:
  ```bash
  cat ~/.ssh/authorized_keys
  ```
