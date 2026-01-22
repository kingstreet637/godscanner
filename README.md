# GodScanner

<p align="center">
  <img src="https://img.shields.io/badge/python-3.7+-blue.svg" alt="Python 3.7+">
  <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="MIT License">
  <img src="https://img.shields.io/badge/platform-linux%20%7C%20windows%20%7C%20macos-lightgrey.svg" alt="Platform">
</p>

<p align="center">
  <b>CloudFlare Proxy Scanner</b><br>
  Find non-official IPs that relay traffic through CloudFlare CDN
</p>

---

## 🚀 What is GodScanner?

GodScanner finds IP addresses that proxy traffic through CloudFlare CDN but are **NOT official CloudFlare IPs**. These IPs can be used as relay nodes for VLESS/VMess WebSocket TLS connections.

### How it works

```
Your Client → Found IP:443 → CloudFlare CDN → Your Origin Server
```

When someone sets up a VLESS Reality server with SNI pointing to a CloudFlare-backed domain, their server essentially becomes a relay. GodScanner finds these servers.

## ✨ Features

- 🔍 **Interactive TUI Menu** - Easy to use interface
- ⚡ **Multi-threaded Scanning** - Up to 1000 concurrent threads
- 🌐 **Built-in VPS Providers** - Contabo, Hetzner, OVH, DigitalOcean, Vultr, Linode, and more
- 🏢 **ASN Scanning** - Scan any ASN by number (fetches ranges automatically)
- 📊 **Real-time Progress** - See results as they come
- 💾 **Export Results** - JSON, CSV, or plain text
- 📋 **VLESS Config Generator** - Generate ready-to-use configs with 0-RTT and Fragment support

## 📦 Installation

```bash
# Clone the repository
git clone https://github.com/useruserdev/godscanner.git
cd godscanner

# No dependencies required! Uses only Python standard library
python3 godscanner.py
```

### Requirements

- Python 3.7+
- No external dependencies

## 🎮 Usage

### Interactive Mode (Recommended)

```bash
python3 godscanner.py
```

This opens the interactive menu:

```
   ██████╗  ██████╗ ██████╗ ███████╗ ██████╗ █████╗ ███╗   ██╗███╗   ██╗███████╗██████╗ 
  ██╔════╝ ██╔═══██╗██╔══██╗██╔════╝██╔════╝██╔══██╗████╗  ██║████╗  ██║██╔════╝██╔══██╗
  ██║  ███╗██║   ██║██║  ██║███████╗██║     ███████║██╔██╗ ██║██╔██╗ ██║█████╗  ██████╔╝
  ╚██████╔╝╚██████╔╝██████╔╝███████║╚██████╗██║  ██║██║ ╚████║██║ ╚████║███████╗██║  ██║
   ╚═════╝  ╚═════╝ ╚═════╝ ╚══════╝ ╚═════╝╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝  ╚═══╝╚══════╝╚═╝  ╚═╝

╔════════════════════════════════════════════════════════════════════╗
║                         MAIN MENU                                  ║
╠════════════════════════════════════════════════════════════════════╣
║                                                                    ║
║  [1]  🔍  Scan by Provider                                         ║
║  [2]  🎯  Scan Custom CIDR Range                                   ║
║  [3]  📝  Check Single IP                                          ║
║  [4]  📁  Scan from File                                           ║
║  [5]  🌐  Scan ALL Providers                                       ║
║  [6]  🏢  Scan by ASN                                              ║
║                                                                    ║
║  [7]  ⚙️   Settings                                                 ║
║  [8]  📊  View Results                                             ║
║  [9]  💾  Save Results                                             ║
║  [10] 📋  Generate VLESS Configs                                   ║
║                                                                    ║
║  [0]  ❌  Exit                                                      ║
╚════════════════════════════════════════════════════════════════════╝
```

## 📖 Menu Options

| Option | Description |
|--------|-------------|
| **[1] Scan by Provider** | Select a VPS provider, then choose specific subnets |
| **[2] Custom CIDR** | Enter your own IP range (e.g., `144.91.64.0/24`) |
| **[3] Check Single IP** | Test one specific IP address |
| **[4] Scan from File** | Load IPs from a text file (one per line) |
| **[5] Scan ALL** | Scan all known VPS provider ranges (takes long!) |
| **[6] Scan by ASN** | Enter ASN number, auto-fetches IP ranges |
| **[7] Settings** | Configure threads, timeout, port |
| **[8] View Results** | Display found CF proxies |
| **[9] Save Results** | Export to JSON/CSV/TXT |
| **[10] VLESS Configs** | Generate VLESS connection strings |

## 🏢 ASN Scanning

Scan any Autonomous System by number. GodScanner automatically fetches IP ranges from BGPView/RIPE.

```
═══ Scan by ASN ═══

Popular ASNs:
  AS51167    - Contabo
  AS24940    - Hetzner
  AS16276    - OVH
  AS14061    - DigitalOcean
  AS20473    - Vultr
  AS63949    - Linode
  AS12876    - Scaleway
  AS31898    - Oracle Cloud
  AS15169    - Google Cloud
  AS8075     - Microsoft Azure
  AS16509    - Amazon AWS

Enter ASN (e.g., AS51167 or 51167): 51167

[*] Fetching IP ranges for AS51167...
[✓] Found 47 IPv4 ranges from BGPView

Scan Options:
  [A]  Scan ALL ranges
  [S]  Select specific ranges
  [L]  Scan only /24 and smaller (faster)
```

## 🏢 Supported Providers

| Provider | IP Ranges |
|----------|-----------|
| Contabo | 144.91.x.x, 167.86.x.x, 62.171.x.x |
| Hetzner | 95.216.x.x, 135.181.x.x, 65.108.x.x |
| OVH | 51.68.x.x, 51.75.x.x, 54.36.x.x |
| DigitalOcean | 134.209.x.x, 157.245.x.x, 159.65.x.x |
| Vultr | 45.32.x.x, 45.63.x.x, 108.61.x.x |
| Linode | 45.79.x.x, 139.162.x.x, 172.104.x.x |
| Scaleway | 51.15.x.x, 163.172.x.x |
| Oracle Cloud | 129.146.x.x, 140.238.x.x, 152.67.x.x |
| Google Cloud | 34.64.x.x, 35.184.x.x |
| Azure | 13.64.x.x, 20.x.x.x, 40.64.x.x |
| AWS Lightsail | 3.8.x.x, 18.130.x.x, 52.x.x.x |

## 📋 VLESS Config Generator

Generate ready-to-use VLESS configs with advanced options:

```
═══ Generate VLESS Configs ═══

[1/6] UUID
  UUID: your-uuid-here

[2/6] Host Header
  Host: your-domain.com

[3/6] SNI (Server Name Indication)
  SNI: your-domain.com

[4/6] WebSocket Path
  Path: /vless

[5/6] 0-RTT Early Data
  Add 0-RTT (?ed=2048)? [Y/n]: y
  Path with 0-RTT: /vless?ed=2048

[6/6] TLS Fragment
  Add fragment? [y/N]: y
  Fragment value: 1-3,1-1,tlshello
```

### Generated Config Example

```
vless://uuid@144.91.121.101:443?encryption=none&type=ws&host=domain.com&path=%2Fvless%3Fed%3D2048&security=tls&fp=chrome&sni=domain.com&allowInsecure=false&fragment=1-3,1-1,tlshello#GodScanner-1-45ms
```

### Config Options

| Option | Description |
|--------|-------------|
| **UUID** | Your VLESS server UUID |
| **Host** | Domain for Host header |
| **SNI** | TLS Server Name Indication |
| **Path** | WebSocket path on your server |
| **0-RTT** | Early data for lower latency (`?ed=2048`) |
| **Fragment** | TLS fragmentation to bypass DPI |

## ⚙️ Settings

| Setting | Default | Range | Description |
|---------|---------|-------|-------------|
| Threads | 200 | 1-1000 | Concurrent connections |
| Timeout | 5.0s | 1-30s | Connection timeout |
| Port | 443 | 1-65535 | Target port |

## 📤 Output Formats

### JSON (Full Details)
```json
[
  {
    "ip": "144.91.121.101",
    "port": 443,
    "is_cf_proxy": true,
    "cf_ray": "9c1390647c985d97-FRA",
    "server": "cloudflare",
    "cert_cn": "www.cloudflare.com",
    "response_time_ms": 45
  }
]
```

### Text (IP List)
```
144.91.121.101
167.86.85.42
95.216.45.123
```

### CSV
```csv
ip,port,cf_ray,server,latency_ms,cert_cn
144.91.121.101,443,9c1390647c985d97-FRA,cloudflare,45,www.cloudflare.com
```

## 🔒 Official CloudFlare IPs (Excluded)

GodScanner automatically excludes official CloudFlare IP ranges:

- 173.245.48.0/20
- 103.21.244.0/22
- 103.22.200.0/22
- 103.31.4.0/22
- 141.101.64.0/18
- 108.162.192.0/18
- 190.93.240.0/20
- 188.114.96.0/20
- 197.234.240.0/22
- 198.41.128.0/17
- 162.158.0.0/15
- 104.16.0.0/13
- 104.24.0.0/14
- 172.64.0.0/13
- 131.0.72.0/22

## 🤔 How to Use Found IPs

1. **Run GodScanner** and find CF proxy IPs
2. **Generate VLESS config** with your domain and settings
3. **Import** into your client (v2rayN, Shadowrocket, v2rayNG, Nekobox, etc.)

### Example VLESS Config
```
Address: 144.91.121.101 (found IP)
Port: 443
UUID: your-uuid
Network: ws
Path: /your-path?ed=2048
TLS: enabled
SNI: your-domain.com
Host: your-domain.com
Fragment: 1-3,1-1,tlshello (optional)
```

## 📝 Tips

- **Start small**: Test with `/24` ranges before scanning larger ranges
- **Use ASN scan**: Faster than scanning all provider ranges
- **Increase threads** for faster scanning (if your connection allows)
- **Lower timeout** (2-3s) for faster but less reliable scans
- **Check single IP** first to verify your setup works
- **Use 0-RTT**: Reduces latency on connections
- **Use Fragment**: Helps bypass DPI in restricted networks

## ⚠️ Disclaimer

This tool is for **educational and research purposes only**. Users are responsible for complying with all applicable laws and regulations. The authors are not responsible for any misuse of this tool.

## 📄 License

MIT License - see [LICENSE](LICENSE) file

## 🤝 Contributing

Contributions are welcome! Feel free to:

- Report bugs
- Suggest new features
- Add new VPS provider ranges
- Add new ASN references
- Submit pull requests

## ⭐ Star History

If you find this tool useful, please give it a star! ⭐

---

<p align="center">
  Made with ❤️ for the community
</p>
