## What are we building?
We are building a network, with some degree of complexity.

Feel free to pick and choose the sections of this tutorial which apply to your use case.

## Who is this for?
For tinkerers who aren't afraid to build cool stuff so they can brag about it to their mates.  
Also, for anyone looking to build/enhance their home/home lab/home office/small office network.

## By the end of this guide, you will be able to achieve the following:
* Have a separate Guest WiFi (or wired) Network - _your Guests will not be able to browse your router page, or to communicate with other devices on your network_
* Have a separate IoT WiFi (or wired) Network - _for smart appliances which do not require access to the Internet (such as CCTV / some smart plugs/lights, etc)_
* Have a separate IoT 
* gdasdgsa


# Hardware
Hardware used:
| Component        |  Model   | Use case      |
| ---------------- |:--------:| ------------- |
| Router           | [TP-Link Archer C7](https://www.amazon.com/TP-Link-AC1750-Smart-WiFi-Router/dp/B079JD7F7G) | Define VLANs, Firewall rules, WiFi networks, etc. |
| Managed Switch   | [TP-Link TL-SG108E](https://www.amazon.com/Ethernet-Unmanaged-Shielded-Replacement-TL-SG108E/dp/B00K4DS5KU) | Pass VLANs down over more ethernet ports |
| Raspberry Pi     | 4B 8GB RAM | AdGuard, DNS & WireGuard Server |
| _*Unmanaged Switch_ | _[TP-Link TL-SG1005D](https://www.amazon.com/TP-Link-Ethernet-Optimization-Unmanaged-TL-SG1005D/dp/B000N99BBC)_ | _Adds more ethernet ports_ |
| _*Proxmox Server_ | _Any_ | _An old PC/laptop/server_ |

_* optional_

Please note that this setup can be achieved with other hardware as well, however some of the instructions may vary depending on the hardware used. For the purpose of this tutorial, we will be using all of the above components.

# Other Requirements:
* A domain name for the private VPN server

You could also get a free domain from somewhere like [duckdns.org](https://www.duckdns.org/) or [noip.com](https://www.noip.com/). Not sure about duckdns, but noip requires you to sign in to their website every month and keep reactivating your domain. So for the sake of simplicity, let's use a .cyou domain _(you can purchase any other TLD, however .cyou is amongst the cheaper options)_ from [namecheap.com](https://www.namecheap.com/) _(or wherever else you decide to buy the domain from)_ for 10 years (~ $45).

For the remaining of this tutorial we will be referring to our domain name as `myprivatenetwork.cyou`

# Installation
## Step 1. Setting up your domain name
_This process requires Namecheap to communicate with Cloudflare which usually takes a few minutes, but it can take up to 24 hours. Cloudflare will notify you once the configuration is completed, and hopefully that notification will arrive while we're busy setting up the other elements of this network configuration._

[Create a free Cloudflare account](https://dash.cloudflare.com/sign-up) if you don't already have one.

If you just purchased a domain using namecheap.com, then use [this link](https://www.namecheap.com/support/knowledgebase/article.aspx/9607/2210/how-to-set-up-dns-records-for-your-domain-in-cloudflare-account/) to setup Cloudflare so that it can manage the DNS records for our `myprivatenetwork.cyou` domain _(the entire process is completely free)_.

After `myprivatenetwork.cyou` is added to your Cloudflare account, let's head back to Cloudflare's dashboard, select our `myprivatenetwork.cyou` domain and click on the 'DNS' option in the menu (on the left):
![image](https://user-images.githubusercontent.com/106243598/170295495-4590a37e-9af8-4dc6-a585-df73acc1c3f7.png)
_(We are essentially configuring a public address on the Internet to help us find our Raspberry Pi which runs our WireGuard VPN server. In this case, the address which will eventually point to the Raspberry Pi, is `local.myprivatenetwork.cyou`)_

Click 'Add record' to create a new DNS record for our `myprivatenetwork.cyou` domain - we will use this later to link to our WireGuard server on the Raspberry Pi.

Select Type `A`, choose a name (any name you like, for example `local`), enter the IPv4 address as `0.0.0.0` (it's important that you use 0.0.0.0 for this step), select Proxy status to be `DNS only` and leave TTL to `Auto`.  

Click Save.

## Step 2. OpenWRT
Check the hardware version of your router and install the latest [OpenWRT](https://openwrt.org/toh/tp-link/archer_c7) according to the instructions on the OpenWRT website.

Once OpenWRT is installed, go to http://192.168.1.1 and update the login password to something secure.

## Step 3. Raspberry Pi
  i) Follow [@trinib's tutorial](https://github.com/trinib/AdGuard-WireGuard-Unbound-Cloudflare) to setup the Raspberry Pi
  ii) Follow pivpn instructions to setup WireGuard
  iii) Follow these instructions to setup dynamic DNS for Cloudflare https://www.youtube.com/watch?v=rI-XxnyWFnM&t=600s
  
## Step 4. Back to OpenWRT
  i) Setup the various VLANs and interfaces on the Router

## Step 5. Managed Switch

# Credits:
* **OneMarcFifty** - OpenWRT, Raspberry Pis, Proxmox and more - [YouTube](https://www.youtube.com/c/OneMarcFifty) / [Discord](https://discord.com/invite/DXnfBUG)
* [@trinib](https://github.com/trinib) - configuring RPI with AdGuard, WireGuard, Unbound, Cloudflare
* [@pivpn](https://github.com/pivpn) - the simplest way to get a private VPN server up and running
* [K0p1-Git](https://github.com/K0p1-Git) - Cloudflare DNS auto-renewal script
* 
