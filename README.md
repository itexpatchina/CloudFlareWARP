# WARP VPN Usage Guide in Mainland China

This document provides a practical overview of how to use Cloudflare’s free VPN services — WARP and 1.1.1.1 — while operating within mainland China.

<img src="https://one.one.one.one/media/warp-plus.png"/>

## Current Status of the WARP App in China

As of 2025, Cloudflare’s WARP and 1.1.1.1 apps generally do **not** function reliably behind China’s Great Firewall (GFW). In contrast, throughout much of 2023, the apps operated smoothly across iPhones, Android devices, and PCs.

While it’s still possible to download and install the apps — assuming access to a non-China Apple ID or Google Play Store — successfully establishing a WARP connection has become increasingly rare, if not impossible.

Many Chinese tech YouTubers suspect that Cloudflare’s ingress IPs have been blacklisted by the GFW, and this theory holds weight. Cloudflare openly publishes its WARP ingress IP list here:  🔗 [Cloudflare WARP Ingress IPs](https://developers.cloudflare.com/cloudflare-one/connections/connect-devices/warp/deployment/firewall/#warp-ingress-ip)

### WireGuard Protocol IP Ranges (Quoted from Cloudflare on 2025-07-13)

- **IPv4 Range**: `162.159.193.0/24`  
- **IPv6 Range**: `2606:4700:100::/48`  
- **Default Port**: `UDP 2408`  
- **Fallback Ports**:  
  - `UDP 500`  
  - `UDP 1701`  
  - `UDP 4500`

## WireGuard Configuration via Telegram Bot

Since Cloudflare's WARP is fundamentally a WireGuard-based solution, it’s possible to either extract an existing configuration or create a new one — provided it adheres to Cloudflare’s standard settings.

One of the most convenient tools I use personally is the following Telegram bot:

<img width="335" height="442" alt="Telegram Bot Interface" src="https://github.com/user-attachments/assets/789096c1-7ee5-48c2-8995-a9962e4c7e71" />

Simply send the `/generate` command to this bot, and you’ll receive a `wg-config.conf` file — a valid WireGuard configuration that can be imported into the standard WireGuard app (iOS, Android, or Windows).

<img width="450" height="188" alt="Generated WireGuard Config File" src="https://github.com/user-attachments/assets/9be0fe66-215d-4da5-b661-e60c1c4f84ad" />


## Limitations of WireGuard Config Inside China

Below is a sample `wg-config.conf` file generated via the Telegram bot (sensitive keys truncated for privacy):

<img width="412" height="175" alt="Sample WireGuard Configuration" src="https://github.com/user-attachments/assets/85de15ed-373f-4fa6-a220-8a40833430e5" />

While this configuration may appear valid, it typically **will not work inside mainland China** due to how DNS resolution interacts with the Great Firewall (GFW). Specifically:

- The endpoint `engage.cloudflareclient.com:2408` often resolves to a Cloudflare ingress IP close to the user’s geographic location.
- These localized IPs are highly likely to be blacklisted by GFW, resulting in failed connections.
- This same behavior occurs when using the WARP app directly — tapping the "Connect" button simply attempts to resolve and connect to one of those inaccessible ingress IPs.

Therefore, while the bot-generated config file might work in less restricted regions, additional measures are needed for stable connectivity within China.

## Searching for Viable Endpoints

While the default endpoint `engage.cloudflareclient.com:2408` often fails inside mainland China, several Cloudflare ingress IPs (previously listed) may still be accessible.

Chinese tech YouTuber **yonggekkk** shares a helpful set of scripts on GitHub that can scan and identify working endpoint IP–port pairs.  
🔗 GitHub Project: [warp-yg](https://github.com/yonggekkk/warp-yg)  
📦 Windows-only Script Bundle: [Download ZIP](https://github.com/yonggekkk/warp-yg/blob/main/WIN%E7%AB%AFwarp%E8%87%AA%E9%80%89IP-v23.11.15.zip)

> ⚠️ **Security Warning**:  
> Windows Defender may flag parts of this script as suspicious. Use a **dedicated virtual machine (VM)** on the same network as your main workstation to run tests safely.

> 🈶 **Language Note**:  
> The script’s interactive menu is in Chinese, so basic understanding of the language will help navigate it more efficiently.

<img width="260" height="55" alt="Script Running Screenshot" src="https://github.com/user-attachments/assets/9ef05c97-6b29-4f6b-a2a5-705a2fc3fd2b" />




