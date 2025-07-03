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

1. Install via LuCI.
2. Configure traffic splitting using `.txt` files before downloading.
3. Set up CN DNS servers: `223.5.5.5` / `114.114.114.114`.
4. Set up GFW DNS servers: `8.8.8.8` / `1.1.1.1`.

## Xray

1. Install via LuCI.
2. Configure using `config.json`.
3. Place the `.dat` files, create log files, set up the environment, and enable autostart on boot.

## Tproxy

Place the script in `/etc/init.d/tproxy`.

### Enable Autostart on Boot

To enable the script to run automatically on boot in OpenWrt:

```shell
chmod +x /etc/init.d/tproxy  # Ensure the script is executable
/etc/init.d/tproxy enable    # Enable autostart on boot
/etc/init.d/tproxy start     # Start the script immediately
```

Verify if the script has been added to system services:

```shell
ls -l /etc/rc.d/ | grep tproxy
```

If you see `S99tproxy`, the script has been successfully added to autostart.

