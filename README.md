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
  - vra_host
  - vra_user
  - vra_pass
```

### Injector Config
```
env:
  VRA_HOST: '{{ vra_host }}'
  VRA_PASS: '{{ vra_pass }}'
  VRA_USER: '{{ vra_user }}'
```


## References
### How to add an image to vSphere Aria
https://docs.vmware.com/en/VMware-Aria-Automation/SaaS/Using-Automation-Assembler/GUID-9CBAA91A-FAAD-4409-AFFC-ACC1810E4FA5.html#add-an-image-from-a-vcenter-content-library-7
### Getting Started with vSphere Aria
https://docs.vmware.com/en/VMware-Aria-Automation/SaaS/Getting-Started-VMware-Aria-Automation.pdf
### Blog Post About Using REST to interact with vSphere Aria
https://vra4u.com/2022/01/13/vra-8-request-vm-via-rest-api/
### Aria Programming Guide
https://vdc-download.vmware.com/vmwb-repository/dcr-public/4e3fc812-7817-4ad3-92af-766007499000/57daec73-115a-4e1b-ae43-9b2ced09dc9f/Programming-Guide.pdf
### Ansible URI Module
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/uri_module.html
### Swagger Endpoint on a VRA deployed instance for REST API
https://vra.connected.dragonslair.dev/automation-ui/api-docs/
### Containerized AAP Install
https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.4/html/containerized_ansible_automation_platform_installation_guide/aap-containerized-installation#preparing-the-rhel-host-for-containerized-installation_aap-containerized-installation

### Lab URLs
#### Red Hat IDM
https://idm01.connected.dragonslair.dev/
#### vSphere
https://vsphere.connected.dragonslair.dev/
#### AAP
https://aap.connected.dragonslair.dev:8443/
