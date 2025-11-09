# Cloudflare Workers/Pages Proxy Script [Current Version: 25.5.4]

> **English Translation by Erfan (Rainman69)** | [View Original Chinese Version](https://github.com/yonggekkk/Cloudflare-vless-trojan)

------------------------------------------------

## 🌟 Project Overview

This project provides free VLESS and Trojan proxy node deployment solutions using Cloudflare Workers and Pages. It's designed for beginners with local configuration, no external subscription converters, and enhanced privacy protection.

### Key Features

1. **Beginner-Friendly**: Default nodes use CF official IPs, eliminating the need for frequent subscription updates
2. **Cost-Effective**: No custom domain required (though supported if desired)
3. **Simple Setup**: Deploy with one click, set a UUID/password, and you're ready to go
4. **Protocol Support**:
   - **Workers**: vless+ws+tls, trojan+ws+tls, vless+ws, trojan+ws
   - **Pages**: vless+ws+tls, trojan+ws+tls
5. **Multiple Export Formats**: Single node links, aggregated universal links, subscriptions for sing-box and clash
6. **NAT64 Version**: Automatic ProxyIP configuration for VLESS NAT64 variant (code by [badafans](https://github.com/badafans))

### Privacy & Security

- ✅ **Fully Local Configuration**: All settings are edited locally
- ✅ **No Third-Party Dependencies**: No subscription converters or external link references
- ✅ **Enhanced Privacy**: Your node subscription information remains private

------------------------------------------------

## 📚 Table of Contents

- [VLESS Node Configuration Variables](#1-vless-node-configuration-variables)
- [Trojan Node Configuration Variables](#2-trojan-node-configuration-variables)
- [Custom ProxyIP Configuration](#3-custom-proxyip-configuration)
- [Self-Hosted ProxyIP & Reverse Proxy IP](#4-self-hosted-proxyip--reverse-proxy-ip)
- [Viewing Configuration & Share Links](#5-viewing-configuration--share-links)
- [Optimal IP Selection](#6-optimal-ip-selection)
- [Recommended Clients](#7-recommended-clients)
- [Video Tutorials](#video-tutorials)
- [Mobile Optimization Scripts](#mobile-optimization-scripts)

------------------------------------------------

## 1. VLESS Node Configuration Variables

**Note**: NAT64 variant does NOT support ProxyIP configuration as it's automatically filled.

| Variable Function | Variable Name | Value Requirements | Default Value | Required |
|:---|:---|:---|:---|:---|
| **UUID** (Required) | `uuid` (lowercase) | Valid UUID format | Public UUID: `86c50e3a-5b87-49dd-bd20-03c7f2735e40` | Recommended |
| **Global CF Website Access** | `proxyip` (lowercase) | Port 443: IPv4 address, [IPv6 address], domain<br>Non-443: IPv4:port, [IPv6]:port, domain:port | Empty (default) | Optional |
| **Subscription Nodes: Optimal IPs** | `ip1` to `ip13` (13 variables) | CF official IP, CF reverse proxy IP, CF optimal domain | CF official visa domains from different regions | Optional |
| **Subscription Nodes: Port Mapping** | `pt1` to `pt13` (13 variables) | CF's 13 standard ports, or custom ports for reverse proxy | CF's 13 standard ports | Optional |

### Understanding IP Variables (For Advanced Users)

**IMPORTANT**: Only set `ip1` to `ip13` and `pt1` to `pt13` if you:
- Use subscription-based clients
- Want to customize optimal IPs

**Port & TLS Mapping**:
- `ip1` to `ip7`, `pt1` to `pt7`: Port 80 series (TLS OFF) nodes only
- `ip8` to `ip13`, `pt8` to `pt13`: Port 443 series (TLS ON) nodes only

**Configuration Rules**:
- Official IPs: No need to set ports (defaults to 13 CF standard ports)
- Reverse Proxy IPs: Must configure ports according to TLS status

------------------------------------------------

## 2. Trojan Node Configuration Variables

| Variable Function | Variable Name | Value Requirements | Default Value | Required |
|:---|:---|:---|:---|:---|
| **Password** (Required) | `pswd` (lowercase) | Letters and numbers recommended | Public password: `trojan` | Recommended |
| **Global CF Website Access** | `proxyip` (lowercase) | Port 443: IPv4 address, [IPv6 address], domain<br>Non-443: IPv4:port, [IPv6]:port, domain:port | Empty (default) | Optional |
| **Subscription Nodes: Optimal IPs** | `ip1` to `ip13` (13 variables) | CF official IP, CF reverse proxy IP, CF optimal domain | CF official visa domains from different regions | Optional |
| **Subscription Nodes: Port Mapping** | `pt1` to `pt13` (13 variables) | CF's 13 standard ports, or custom ports for reverse proxy | CF's 13 standard ports | Optional |

------------------------------------------------

## 3. Custom ProxyIP Configuration

While the script includes default ProxyIPs, you can customize them using IPv4, IPv6, or domain names.

### Method 1: Global Node Variable (Affects All Nodes)

| ProxyIP Port | IPv4 Format | IPv6 Format | Domain Format |
|:---|:---|:---|:---|
| **Port 443** | `IPv4_address` | `[IPv6_address]` | `domain.com` |
| **Non-443 Port** | `IPv4_address:port` | `[IPv6_address]:port` | `domain.com:port` |

### Method 2: Single Node Path (Affects Only Current Node)

| ProxyIP Port | IPv4 Format | IPv6 Format | Domain Format |
|:---|:---|:---|:---|
| **Port 443** | `/pyip=IPv4_address` | `/pyip=[IPv6_address]` | `/pyip=domain.com` |
| **Non-443 Port** | `/pyip=IPv4_address:port` | `/pyip=[IPv6_address]:port` | `/pyip=domain.com:port` |

### Priority Rules

1. **Path-based ProxyIP**: Takes precedence over global settings for that specific node
2. **Global ProxyIP**: Applies to all nodes without path-based ProxyIP configuration
3. **Keyword Trigger**: When path contains `/pyip=`, only path-based ProxyIP is used

------------------------------------------------

## 4. Self-Hosted ProxyIP & Reverse Proxy IP

### No SOCKS5 Needed! Use Reality Protocol to Build Your Own ProxyIP

#### For Serv00 (Free Hosting)

**Project**: [sing-box-yg for Serv00](https://github.com/yonggekkk/sing-box-yg#%E4%BA%8Cserv00%E4%B8%80%E9%94%AE%E4%B8%89%E5%8D%8F%E8%AE%AE%E5%85%B1%E5%AD%98%E8%84%9A%E6%9C%ACserv00%E4%B8%93%E7%94%A8)

Modified from Serv00 Old Wang's sing-box script. Supports three protocols:
- vless-reality
- vmess-ws (with Argo)
- hysteria2

**Key Feature**: Reality protocol defaults to support CF vless/trojan nodes as ProxyIP and non-standard port reverse proxy IPs.

**One-Click Installation Script** (includes auto-keepalive):
```bash
bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/sing-box-yg/main/serv00.sh)
```

#### For VPS (Virtual Private Server)

**Recommendation**: Use IPv6-only VPS that are:
- Close to China
- Affordable
- High bandwidth

**Why IPv6?**: IPv4 addresses are often scanned and added to public/commercial reverse proxy databases. If using IPv4, monitor your VPS traffic regularly.

**Recommended Scripts**:
- [x-ui-yg script](https://github.com/yonggekkk/x-ui-yg)
- [sing-box-yg script](https://github.com/yonggekkk/sing-box-yg)

### Four Usage Scenarios (Recommended for TLS Nodes)

#### Scenario 1: Client Optimal IP Only
- **Non-CF websites**: Traffic exits via VPS region
- **CF websites**: Traffic exits via ProxyIP region

#### Scenario 2: ProxyIP Only
- **CF websites**: Traffic exits via VPS region
- **Non-CF websites**: Traffic exits via client optimal IP region

#### Scenario 3: Both Client Optimal IP & ProxyIP
- **All websites**: Traffic exits via VPS region

#### Scenario 4: WARP Integration
- Install WARP dual-stack (IPv4+IPv6) on VPS
- **Result**: Fixed outbound IP (104.28.../2a09:...) or WARP unlock functionality

------------------------------------------------

## 5. Viewing Configuration & Share Links

### Access Your Configuration

**For VLESS**:
```
https://workers-domain.workers.dev/your-custom-uuid
https://pages-domain.pages.dev/your-custom-uuid
https://your-custom-domain.com/your-custom-uuid
```

**For Trojan**:
```
https://workers-domain.workers.dev/your-custom-password
https://pages-domain.pages.dev/your-custom-password
https://your-custom-domain.com/your-custom-password
```

### Important Notes

1. **Domain Blocking**: If workers/pages domains are blocked, you must use a proxy to access them
2. **Custom Domain Compatibility**: Original workers/pages domain configurations remain functional even after adding custom domains

------------------------------------------------

## 6. Optimal IP Selection

### Cloudflare Official Standard Ports

**Port 80 Series** (Non-TLS):
- 80, 8080, 8880, 2052, 2082, 2086, 2095

**Port 443 Series** (TLS):
- 443, 2053, 2083, 2087, 2096, 8443

### Recommended CF Official IPs (Lazy User Friendly)

These IPs support all 13 standard ports and are called "The Immortal Front-Line IPs":

```
104.16.0.0    104.17.0.0    104.18.0.0    104.19.0.0
104.20.0.0    104.21.0.0    104.22.0.0    104.24.0.0
104.25.0.0    104.26.0.0    104.27.0.0
172.66.0.0    172.67.0.0    162.159.0.0
2606:4700::0  (Requires IPv6 environment)
```

### CDN Optimal Domains

**Maintained Domains**: `yg1.ygkkk.dpdns.org` to `yg11.ygkkk.dpdns.org`
(Replace "1" with any number from 1-11)

### Local PC Optimization Tools

Available in the code section above:

1. **CDN Optimal Domain V23.8.18** (Windows x64)
2. **CF Optimal Reverse Proxy IP** (PC version with speed test)
3. **CF Optimal Official IP** (PC version, select specific countries)
4. **CF Optimal Official IP** (USA/Asia/Europe three-region non-interactive - **Highly Recommended!**)
5. **CF Optimal Official IP** (PC version with speed test)

### Load Balancing Tip

⚠️ When using load balancing or auto-selection with multiple CF nodes, ensure all nodes are from the same country/region to avoid IP jumping issues.

------------------------------------------------

## 7. Recommended Clients

### Fragment Function Benefits

Enables **TLS nodes** to bypass domain blocking and TLS interruption, allowing blocked workers domains to work with TLS.

**Note**: Unblocked custom domains or pages domains can use TLS nodes without enabling fragment.

### Supported Platforms & Clients

#### Android
- [v2rayNG](https://github.com/2dust/v2rayNG/tags) ⭐
- [Nekobox](https://github.com/starifly/NekoBoxForAndroid/releases)
- [Karing](https://github.com/KaringX/karing/tags)
- v2box

#### Windows
- [v2rayN](https://github.com/2dust/v2rayN/tags) ⭐
- [Hiddify](https://github.com/hiddify/hiddify-next/tags)
- [Karing](https://github.com/KaringX/karing/tags)

#### iOS
- Karing
- Hiddify Proxy & VPN
- Shadowrocket (小火箭)
- Streisand
- v2box

#### Software Router
- passwall
- ssr-plus
- homeproxy

### Important Client Notes

⚠️ **Without fragment enabled**: Workers domain's 6 TLS nodes (port 443 series) will NOT work

⚠️ **Trojan+WS Issue**: Shadowrocket, v2box, v2rayN, v2rayNG force TLS on trojan+ws, causing connection failures. Clash subscriptions don't include trojan+ws nodes.

------------------------------------------------

## 📖 Video Tutorials (Chinese)

### Essential Tutorials for Beginners

1. **[2025.9.8 Update]**: Semi-obfuscation usage, optimal IP confusion resolution, error 1101 warnings
   - 🎥 [Watch on YouTube](https://youtu.be/rUpCuXTQqmQ)

2. **CF VLESS Workers Native Domain**: No custom domain, no optimal IP subscription, no control panel
   - 🎥 [Watch on YouTube](https://youtu.be/PpPKzOYLZQg)

3. **CF VLESS Pages Native Domain**: NAT64 ProxyIP generation explained
   - 🎥 [Watch on YouTube](https://youtu.be/yR-JpVV6SHs)

4. **Code Obfuscation Era**: Workers/pages code obfuscation detailed setup, error 1101 summary
   - 🎥 [Watch on YouTube](https://youtu.be/QSFaP5EVI04)

### Complete Tutorial Series

1. **[Tutorial 1]**: IP jumping phenomenon, two node usage techniques, optimal IP/domain pros and cons
   - 🎥 [Watch on YouTube](https://youtu.be/9V9CQxmfwoA)

2. **[Tutorial 2]**: Optimal reverse proxy IP script, pages deployment, multi-platform client setup
   - 🎥 [Watch on YouTube](https://youtu.be/McdRoLZeTqg)

3. **[Tutorial 3]**: CF Trojan deployment without custom domain, Trojan vs VLESS comparison
   - 🎥 [Watch on YouTube](https://youtu.be/lmhhL8M1k0I)

4. **[Tutorial 4]** ⭐ **Highly Recommended**: Understanding optimal official IP, reverse proxy IP, and optimal domains
   - 🎥 [Watch on YouTube](https://youtu.be/NaLd-orwFUE)

5. **[Tutorial 5]** ⭐ **Highly Recommended**: No custom domain? No frequent IP optimization? Node & domain structure explained
   - 🎥 [Watch on YouTube](https://youtu.be/8s-ELRuFaeE)

6. **[Tutorial 6]** ⭐ **Highly Recommended**: Troubleshooting node issues, multi-platform client setup guide
   - 🎥 [Watch on YouTube](https://youtu.be/8E0l0nQWLxs)

7. **[Tutorial 7]** 🔥 **Advanced**: True "fixed IP" demonstration, solving Twitch/ChatGPT errors
   - 🎥 [Watch on YouTube](https://youtu.be/QOnMVULADko)

8. **[Tutorial 8]** 🔥 **Advanced**: Self-hosted universal port ProxyIP and reverse proxy IP
   - 🎥 [Watch on YouTube](https://youtu.be/CVZStM0t8BA)

### Additional Resources

- **Live Stream Recap**: CF workers vless free node features, connection issues
  - 🎥 [Watch on YouTube](https://youtu.be/9OHGpWlfdJ0)

- **Free Domain Tutorial**: ClouDNS permanent free domain with CF pages deployment
  - 🎥 [Watch on YouTube](https://youtu.be/PN0BLANXh4I)

- **Optimal IP for Beginners**: Auto-generate USA/Asia/Europe optimal IPs for Windows/Android/iOS
  - 🎥 [Watch on YouTube](https://youtu.be/6kKIzObEZ2c)

------------------------------------------------

## 📱 Mobile Optimization Scripts

### Optimal Domain & Official IP One-Click Scripts

Run these scripts on your mobile device using Termux (Android) or iSH (iOS) in your local network environment.

### Android - Termux Setup

1. **Download Termux** (MUST use official version from GitHub, NOT Google Play):
   - 📥 [Download Termux v0.118.1](https://github.com/termux/termux-app/releases/tag/v0.118.1)

2. **Install Dependencies** (first time only):
   ```bash
   pkg upgrade
   ```

3. **Run Your Chosen Script** (see below)

### iOS - iSH Setup

1. **Download iSH v1.2.2** (IMPORTANT: Latest version has bugs, use v1.2.2):
   - Install via TrollStore then downgrade, or find IPA installation tutorials online
   - 📥 [Download iSH 1.2.2](./ISH_1.2.2) (included in this repo)

2. **Install Dependencies** (first time only):
   ```bash
   apk add curl bash
   ```

3. **Run Your Chosen Script** (see below)

### Available Scripts

#### Script 1: CF Optimal Official IP (USA/Asia/Europe) ⭐ HIGHLY RECOMMENDED

**For Android & iOS tablets/phones**:
```bash
curl -sSL https://raw.githubusercontent.com/yonggekkk/Cloudflare_vless_trojan/main/cf/cf.sh -o cf.sh && chmod +x cf.sh && bash cf.sh
```

**Features**:
- Automatic region selection (America, Asia, Europe)
- No interaction required
- Best for beginners

#### Script 2: CF CDN Optimal Public Domains

**For Android & iOS tablets/phones**:
```bash
curl -sSL https://gitlab.com/rwkgyg/CFwarp/raw/main/point/CFcdnym.sh -o CFcdnym.sh && chmod +x CFcdnym.sh && bash CFcdnym.sh
```

**Features**:
- Tests popular CDN provider domains
- Finds best performing domains for your network

#### Script 3: CF Optimal Official IP (With Speed Test)

**For Android & iOS tablets/phones**:
```bash
curl -sSL https://gitlab.com/rwkgyg/CFwarp/raw/main/point/cfip.sh -o cfip.sh && chmod +x cfip.sh && bash cfip.sh
```

**Features**:
- Comprehensive speed testing
- More detailed results
- Slightly longer execution time

------------------------------------------------

## 🙏 Credits & Acknowledgments

### Code Sources

- [ca110us](https://github.com/ca110us/epeius) - Core epeius implementation
- [emn178](https://github.com/emn178/js-sha256/blob/master/src/sha256.js) - SHA256 implementation
- [3Kmfi6HP](https://github.com/3Kmfi6HP/EDtunnel) - EDtunnel base
- [badafans](https://github.com/badafans/Cloudflare-IP-SpeedTest) - NAT64 code & speed test tools
- [XIU2](https://github.com/XIU2/CloudflareSpeedTest) - CloudflareSpeedTest

### Original Author Community

- 📝 **Blog**: [Yongge's Blog](https://ygkkk.blogspot.com)
- 🎥 **YouTube**: [Yongge's Channel](https://www.youtube.com/@ygkkk)
- 💬 **Telegram Group**: [Join Discussion](https://t.me/+jZHc6-A-1QQ5ZGVl)
- 📢 **Telegram Channel**: [Follow Updates](https://t.me/+DkC9ZZUgEFQzMTZl)

### Disclaimer

All code is sourced from the GitHub community and integrated with assistance from ChatGPT. This project is for educational purposes only.

------------------------------------------------

## ⭐ Star History

[![Stargazers over time](https://starchart.cc/yonggekkk/Cloudflare-workers-pages-vless.svg)](https://starchart.cc/yonggekkk/Cloudflare-workers-pages-vless)

------------------------------------------------

## 📄 License

This project follows the original repository's licensing terms. Please refer to individual component licenses as credited above.

------------------------------------------------

### Thank you for your support! ⭐ Please star this repository if you find it useful!

**English Translation & Enhancement by**: [Erfan (Rainman69)](https://github.com/Rainman69) | **Original Author**: [Yongge (yonggekkk)](https://github.com/yonggekkk)