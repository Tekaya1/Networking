

# 📡 Network Lesson Summary

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
    - Modify IP address:
    ```bash
    nmcli connection modify eno33554968 ipv4.addresses 192.168.1.200/24
    ```
- Modify DNS servers:
    ```bash
    nmcli connection modify eno33554968 ipv4.dns "8.8.8.8 1.1.1.1"
    ```
- Set connection to start on boot:
    ```bash
    nmcli connection modify eno33554968 connection.autoconnect yes
    ```
- Activate a connection:
    ```bash
    nmcli connection up eno33554968
    ```
- Deactivate a connection:
    ```bash
    nmcli connection down eno33554968
    ```
- Delete a connection:
    ```bash
    nmcli connection delete eno33554968
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

### 👤 Create a New System User
1. Create a new user on both machines:
         ```bash
         adduser secureadmin
         ```
2. Grant sudo privileges to the user:
         ```bash
         usermod -aG wheel secureadmin
         ```

### 📂 SCP File Copying
1. On the client side, create a file:
         ```bash
         touch hello
         ```
2. Copy the file to the server:
         ```bash
         scp -r hello secureadmin@IPServer:/home/secureadmin/
         ```
         - Enter the password when prompted.
3. On the server side, verify the file:
         ```bash
         ls /home/secureadmin/
         ```

### 📁 Manage Files with SFTP
1. On the client side, start an SFTP session:
         ```bash
         sftp secureadmin@192.168.150.129
         ```
2. Inside the SFTP session:
         ```bash
         mkdir from_sftp
         ls
         ```
3. On the server side, check if the folder was created:
         ```bash
         ls /home/secureadmin/
         ```

### 🔑 SSH Key Management
1. **Generate SSH Keys** (on the client machine as `secureadmin`):
         ```bash
         ssh-keygen -t dsa -C "client"
         ```
         - Press `Enter` for all prompts.
2. **Copy the Public Key to the Server**:
         ```bash
         ssh-copy-id secureadmin@IPServer
         ```
         - Enter the user password when prompted.
3. **Test the Connection** (from the client):
         ```bash
         ssh secureadmin@IPServer
         ```
4. **Verify the Authorized Key** (on the server side):
         ```bash
         cat /home/secureadmin/.ssh/authorized_keys
         ```

