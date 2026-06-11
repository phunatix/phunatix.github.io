+++
date = '2024-10-31T06:22:38+02:00'
draft = false
title = 'Getting Started with a home lab'
+++

My motivation on starting a homelab is primarily driven by a strong interest in technology and the desire to experiment with hardware and software in a safe and controlled environment. Also, for simple deployments of software I thought it might be a good idea to have my own environment for testing, instead of creating random tenants in cloud providers. However, the later reason is less important as I started to utilize their free tiers more and more. The first step was getting the right hardware.

## Hardware

I opted for a small, energy efficient box that would fit in my IT-rack in the basement. I did not want to have the noise of a traditional server in my living space. I am particularly interested in using the homelab for running self-hosted open-source services, like Bitwarden, Nextcloud, Home Assistant and others. Currently, AI workloads are out of scope, but I am also looking into running AI models on premise in the future. The box is a mini PC from Intel with an 8th gen i5 processor. I'd recommend using x86 architecture over ARM, as most container images (still) have better support for it. Beefed up to 32GB of RAM, this is enough for running lihtweight VMs but if needed, the QEMU/KVM virtualization allows running desktop OSes for testing old software, too.
For storage, I have one NVMe SSD for the OS and the other for data, in total 2TB (when storage was still cheap). For some persistent data I am using an older Synology NAS that is connected via NFA and 2.5 GbE (using an to Ethernet adapter as the NAS only has 1GbE ports)
I installed Proxmox on the machine and mainly use VMs with Docker on it.

## Scripts

A very useful hint I got from a colleague was to look into the [community scripts](https://github.com/tteck/Proxmox) for the installation of packages software itself. This helps to install popular software with just a few clicks. The scripts include updating of software versions. If you don't require massive modification of the installed software besides config settings, I can highly recommend this approach for anyone looking to get started with Proxmox.

I am using the following services (most liked in descending order):

- Immich: Photo and video backup and management
- Vaultwarden: Password manager based on Bitwarden
- Linkding: Bookmark manager
- Gitea: Git repository hosting
- Pinchflat: Video downloader for local library (youtube-dl replacement)
- Pinepods: Podcast management for a local podcast library
- Home Assistant: Home automation
- Paperless-ngx: Document management
- Nginx Proxy Manager: Reverse proxy for external access
- Pi-Hole: DNS based ad blocker
- Nextcloud: File sync and share

## Access

To access the services running in the homelab, I use a Cloudflare Zero Trust Tunnel. It is a simple and secure way to access my services from anywhere in the world, without having to open any ports on my router. I am using a separate LXC box to run the tunnel, which is very easy to set up. I can also configure it to use a custom domain name, which makes it even more convenient.
