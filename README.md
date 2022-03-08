# mansible - provision a fun webserver with Ansible

In the support of LGBT I would say that the `man` from `mansible` is not the `man` you're thinking of. It's a stupid word combination from marvin (the eternally depressed robot from "Hitchhiker's guide to the galaxy" (depressed, because I administrate it, get it, get it?)) and [Ansible](https://www.ansible.com/). Since we discussed the gender of this repo let's continue to the fun part.

# What's the purpose of this repo

The sole purpose is to automate my dear `marvin` to a much cleaner state as it is now. Ansible can help me do things cleaner and, once automated, a lot quicker to upgrade.

# Don't you like the ISPConfig?

No.

# What will be run on mansible

A lot. Starting from the usual nginx/PHP/mySQL/WordPress, then trough the ELK stack (probably in Docker containers) and 

# What about the IaC

IaC provisioning is one of the mandatory steps of this repo, but the terraform wouldn't fit the `mansible` - `mantsible`? Nah.

# Where you'll host the `marvin`

As now it leaves on DigitalOcean and I'm still not 100% sure should I move it to my bare metal (named `vortex`) or some hybrid solution as LB on DigitalOcean behind with one VPS and the bare metal instance, but we all know that this is an absolute overkill (which means I'll probably do it :D)
