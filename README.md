# mansible - provision a fun webserver with Ansible

In the support of LGBT I would say that the `man` from `mansible` is not the `man` you're thinking of. It's a stupid word combination from marvin (the eternally depressed robot from "Hitchhiker's guide to the galaxy" (depressed, because I administrate it, get it, get it?)) and [Ansible](https://www.ansible.com/). Since we discussed the gender of this repo, let's continue to the fun part.

# What's the purpose of this repo

The sole purpose is to automate my dear `marvin` to a much cleaner state as it is now. Ansible can help me do things cleaner and once automated, upgrade will be much quicker.

# Don't you like the ISPConfig?

No. Some time ago I decided to make my life easier with a web panel where I can control my shit, but I hate every second of it. It's time to go vanilla Debian and Ansible (and containers, but it's a topic for another conversation).

# What will be run on `mansible`

A lot. Starting from the usual nginx/PHP/mySQL/WordPress, then through the ELK stack (probably in Docker containers). More at the end of the README

# What about the IaC

IaC provisioning is one of the mandatory steps of this repo, but the terraform wouldn't fit the `mansible` - `mantsible`? Nah.

# Where you'll host the `marvin`

As now, it leaves on DigitalOcean, and I'm still not 100% sure if I should move it to my bare metal (named `vortex`) or some hybrid solution as LB on DigitalOcean behind with one VPS and the bare metal instance, but we all know that this is an absolute overkill (which means I'll probably do it :D)

# CI/CD implementation
Sure. Pushing to a tag version will trigger `molecule` tests and then an ansible deployment if there are any playbook changes. This will be handy when I add another website to `marvin`. Code linting and vulnerability scanning will be implemented too.


# Technical details
In order of importance for me here is the list of what the hell the ready ansible code should provision:

* Time machine backups
* Pi Hole to filter youtube mobile and TV videos
* VPN to use with [Automate](https://play.google.com/store/apps/details?id=com.llamalab.automate&hl=en&gl=US) to use home server connectivity to have access to storage and to take advantage of Pi Hole filtering
* Plex for video library
* *** for phone synchronization
* Grafana for monitoring:
    * Server stats
    * Network stats (to prove to my ISP that they are exceptionally inconsistent with the speeds they offer)
    * Dashboard for learning Grafana
* Next Cloud (or alternative) to host and organize terabytes of family photos (DSLR) in combination with [Nextcloud all-in-one](https://github.com/nextcloud/all-in-one) plugin and other
* Docker to host most of the services. As orchestrator, I'll use docker-compose
* Probably an instance of [VaultWadren](https://github.com/dani-garcia/vaultwarden) to test it and if it works good and eventually migrate from SaaS BitWarden
* K8s - I need to learn more about k8s, so there will be a ready-to-work k8s with some services running (isolated from docker-compose) to learn and not production ready.
* Basically everything that I need, and I'm interested in the [most detailed self-hosted list](https://github.com/mikeroyal/Self-Hosting-Guide) I've ever seen

# Availability
So many services, but ... how will they be kept secure? 90% of them will be behind VPN, but hardening will be done on OS and service level. No one wants to get hacked, right?

# Backups?
Keeping files on the same server that can be destroyed easily by a toddler and a baby, a cat, a wife, and mostly by me doesn't seems a good idea, so I have a second Microserver gen8 that will be running as a backup instance (and thanks to Ansible will be easy to configure).

# Hardware
Most services do not require a vast amount of CPU or RAM, but I have that covered... somehow. The setup will live in a double of [HP Microserver Gen8](https://support.hpe.com/hpesc/public/docDisplay?docId=emr_na-c03793258) with [Xeon E3-1220v2](https://www.intel.co.uk/content/www/uk/en/products/sku/65734/intel-xeon-processor-e31220-v2-8m-cache-3-10-ghz/specifications.html), 8GB HP ECC RAM, 1GB networking with 100mbps speed from the ISP.
I really like the HP Microserver gen8, because it's compact, well made, have iLO and it's silent. Unofficial CPU support is way up to Xeon E3-1270 V2, 16GB RAM, and [4x12TB](https://www.reddit.com/r/freenas/comments/agu22i/hp_microserver_gen8_largest_supported_drive/) (officially HP supports 4x4TB, but multiple Reddit users reported waaaay more), 1xSSD disk for OS and containers (replacing the CD-ROM).