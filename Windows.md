Status: cap works on windows. very different structure from node_pcap should be explored
Status: VM shuts down after hour due to license.

Windows setup
1. [x] VM
2. [x] SDK setup
3. [x] SDK test
4. [x] Nodejs
5. [x] Pcap test
6. [ ] electronjs test

* https://www.electronjs.org/docs/tutorial/development-environment
- use free windows VM's https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/

# VM
Need 16+33GB. 

## Virtualbox image to Qemu:vert-manager (status: works)
### Run
if already setup
- s systemctl start libvirtd
- s virt-manager
- check that 'default' network is started 
  `s virsh net-info default`
  `s virsh net-start default` or use GUI
### Setup
* Download WinDev2002Eval.VirtualBox (16GB) from free windows VM's 
  (https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/)
* convert from virtualbox to qemu (33GB): 
  (https://wiki.hackzine.org/sysadmin/kvm-import-ova.html)
    - tar xvf WinDev2002Eval.ova; cd WinDev2002Eval
    - qemu-img convert -O qcow2 WinDev2002Eval-disk001.vmdk WinDev2002Eval-disk001.qcow2
    - install virt-manager extra/dmidecode ebtables
        * s systemctl disable libvirtd
        * s systemctl start libvirtd
        * s virt-manager
    - add windows vm with defaults and use the cow2 as the external disk. done
      - error: `libvirt.libvirtError: Requested operation is not valid: network 'default' is not active` == check that vert manager has that network started in gui or `s virsh net-info default`
* **setup shared folder** (add hardware to vm, filesystem) virtio filesystem passthrough doesnt work
  instead just share folder in guest and then access from linux file manager:
  https://unix.stackexchange.com/a/332105
  - setup share
  - change user password in windows (some reason couldnt access anonymous)
  - in dolphin go to smbshare section: smb://192.168.122.13 and give user password when asked. will then be given a selection of shared paths

## Virtualbox image to gnome-box
If you need install disk:
    download windows 10 ISO 64bit (5GB) (so gnome-boxes can work): 
      https://www.microsoft.com/en-us/software-download/windows10ISO
      (downloaded to local folders)
    - gnome-boxes

# VM Test pcap
This setup provides Windows VM with interface on network (obtain own ip from main network)
using a bridge interface on host. Host can see traffic from guest VM. Guest VM cannot see traffic from host. I suppose if you setup network sharing in Windows VM and set all hosts to route through Windows VM IP that one would see all traffic. Or arpspoofing could be used.

- install wireshark in guest (not portable)
- Setup a br0 interface on host and attach eth0 to it:
  *  ip link add name br0 type bridge
  *  ip link set br0 up
  *  ip link set eth0 master br0
  *  bridge link
     # if adding wlan the ssid has to be associated first
     # wlan0: "Error: Device does not allow enslaving to a bridge."
  * Expose br0 to virt-manager: (systemctl restart libvirtd  -- didnt help)
     echo "<network><name>br0</name><forward mode="bridge"/><bridge name="br0" /></network>" > /tmp/br0.xml
     virsh net-define /tmp/br0.xml
     # in virt manager windows vm gui setup interface for br0 with "e1000" type
helpful links:
https://serverfault.com/questions/998890/kvm-qemu-bridged-network-not-working-guest-can-only-access-host https://www.techotopia.com/index.php/Creating_a_RHEL_KVM_Networked_Bridge_Interface#Virtual_Networks_and_Network_Bridges
    setup bridge on host and then setup virt-manager to attach to that for guest
    _This is achieved by configuring a network bridge interface on the host system to which the guests can connect._ https://wiki.archlinux.org/index.php/Network_bridge

For SMB share smb://user@192.168.178.43/Users/User/Downloads/
username: user  password: user
 (change assigned ip from network)

# VM setup node and test cap
- Node install is strait forward
- `npm install -g cap` fails with _"missing VC++ toolkit"_ currently installing
  requires installing VS Studio C++ core and VS toolkit. We did this under 2019 packages found in Studio installer
  - requires npcap install with wincap support. This can be set when installing wireshark
- Test: node c:\Users\User\AppData\Roaming\npm\node_modules\cap\test\test.js
- 
# VM electronjs
https://www.electronjs.org/docs/development/build-instructions-windows
requires: 
- windows 10 server  or higher? 
- Visual Studio 2017 (have in win 10 vm image)
- python 2.7.10+ with pywin32 extensions https://pypi.org/project/pywin32/#filesv 
  https://www.python.org/downloads/release/python-2718/
  extension installation doc: https://github.com/mhammond/pywin32
- nodejs
- git
- debug tools for windows

# VM sshd