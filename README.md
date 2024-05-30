## Configuring VRA
You'll need a copy of the VCSA and VMWare Automation Lifecycle Installer isos.  These will be used in eval modes.

## Prerequisites
I deployed this system in a remote lab and used Zerotier to access it.

I had the following systems:
1.) Bastion RHEL 9 deployed with a desktop and dualhome both on public and private network
2.) Headless RHEL 9 host configured to serve as a NAT router for the private network to the internet as well as a zerotier network node to bridge remote clients and the private network.
3.) Windows 10 host for deploying VCSA and vRA.  VCSA deploys from RHEL fine, but vRA just spins upon launching a deployment.
4.) RHEL IDM host to provide DNS (especially reverse DNS)
5.) Lifecycle host for managing VMWare IDM and VRA
6.) VMWare IDM host (necessary to provide auth for vRA) 
7.) VRA host to run automation from

### Injector Config
```
fields:
  - id: vra_host
    type: string
    label: VRA Hostname
  - id: vra_user
    type: string
    label: VRA Username
  - id: vra_pass
    type: string
    label: VRA Password
    secret: true
required:
  - instance
  - username
  - password
```

### Injector Config
```
env:
  VRA_HOST: '{{ vra_host }}'
  VRA_PASS: '{{ vra_pass }}'
  VRA_USER: '{{ vra_user }}'
```
