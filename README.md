# openwrt_tproxy

OpenWrt Transparent Proxy Toolchains

Includes:

- DNS
- Xray
- Tproxy

## Prerequisites

Download the required files from [v2ray_rules](https://github.com/Loyalsoldier/v2ray-rules-dat.git), including:

- `geoip.dat`
- `geosite.dat`
- `direct-list.txt`
- `proxy-list.txt`
- `reject-list.txt`

## DNS

Using **SmartDNS**:

1. Install via official website (may be 'lite' in source).
2. Configure traffic splitting using `.txt` files before downloading.
3. Set up CN DNS servers: `223.5.5.5` / `114.114.114.114`.
4. Set up GFW DNS servers: `8.8.8.8` / `1.1.1.1`.

## Xray

1. Install via LuCI. 
2. Update from GitHub release (optional) and move to `/usr/bin/xray`:
   ```shell
   mv xray /usr/bin/xray
   ```
3. Configure using `config.json` to `/etc/xray/config.json`.
4. Place the `.dat` files in `/usr/share/xray`, and enable autostart on boot:
   ```shell
   mkdir /usr/share/xray
   ```

## Tproxy

The Tproxy script supports both `iptables` and `nftables`. Choose the appropriate script based on your system's configuration.

### Differences Between iptables and nftables

- **iptables**:
  - Uses `ipset` to manage reserved IP ranges.
  - Relies on `iptables` rules for packet marking and forwarding.
  - Suitable for systems where `iptables` is already in use or preferred.

- **nftables**:
  - Uses a single configuration file for all rules.
  - Provides better performance and flexibility compared to `iptables`.
  - Recommended for newer systems or those already using `nftables`.

### Setup Instructions

1. Place the appropriate script (`iptables` or `nftables`) in `/etc/init.d/tproxy`.
2. Enable autostart on boot:
   ```shell
   chmod +x /etc/init.d/tproxy  # Ensure the script is executable
   /etc/init.d/tproxy enable    # Enable autostart on boot
   /etc/init.d/tproxy start     # Start the script immediately
   ```
3. Verify if the script has been added to system services:
   ```shell
   ls -l /etc/rc.d/ | grep tproxy
   ```
   If you see `S99tproxy`, the script has been successfully added to autostart.

