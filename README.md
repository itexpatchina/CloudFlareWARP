# CloudFlareWARP
WARP VPN Related Knowledge Share for users behind China's GFW. This article is mainly about how to use CloudFlare's free VPN solution when you are in mainland China.

# Current Status of WARP app in China
WARP or the 1.1.1.1 app is, generally speaking, not working behind China's GFW since somewhere in 2024. During some good old days in 2023, this app was in full fledge on my Iphone, Android devices as well as on my PC's.
Of course, you can still download and install it on your Iphone and Android, provided you have an outside-of-China Apple ID or somehow have access to Google Play Store. However, a sucessful established connection is mostly rare if not impossible.
Most Chinese tech youtubers suspect that Cloudflare's ingress IPs are all on the blacklist of China's GFW and it is definitely a valid suspicion. As CloudFlare does honestly pulish their WARP ingress IP list on this page: https://developers.cloudflare.com/cloudflare-one/connections/connect-devices/warp/deployment/firewall/#warp-ingress-ip

Hence, as quoted on 2025-07-13 for Wireguard protocol:

WireGuard
IPv4 address	162.159.193.0/24
IPv6 address	2606:4700:100::/48
Default port	UDP 2408
Fallback ports	UDP 500
UDP 1701
UDP 4500

# Wireguard Configuration File 
Because WARP supports Wireguard protocol and essentially just a Wireguard implemention done by CloudFlare, there must be ways to extract these Wireguard configuration files or simply build new configuration files as long as they fit CloudFlare's standard settings. 
And one of the most frequently used ways by myself is through the below Telegram bot:

<img width="335" height="442 " alt="image" src="https://github.com/user-attachments/assets/789096c1-7ee5-48c2-8995-a9962e4c7e71" />
