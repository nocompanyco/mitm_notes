Windows setup
1. VM
2. SDK setup
3. SDK test
4. Nodejs
5. Pcap test

* https://www.electronjs.org/docs/tutorial/development-environment
    - use free windows VM's https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/

# VM
Need 16+33GB. 
* pcap inside of vm: http://blog.vmsplice.net/2011/04/how-to-capture-vm-network-traffic-using.html

## Virtualbox image to Qemu:vert-manager (status: works))
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
* setup shared folder (add hardware to vm, filesystem) virtio filesystem passthrough doesnt work
  instead just share folder in guest and then access from linux file manager:
  https://unix.stackexchange.com/a/332105
  - setup share
  - change user password in windows (some reason couldnt access anonymous)
  - in dolphin go to smbshare section: smb://192.168.122.13 and give user password when asked. will then be given a selection of shared paths

For pcap may need to setup bridge rather than nat interface


## Virtualbox image to gnome-box
If you need install disk:
    download windows 10 ISO 64bit (5GB) (so gnome-boxes can work): 
      https://www.microsoft.com/en-us/software-download/windows10ISO
      (downloaded to local folders)
    - gnome-boxes

# VM Test pcap
wireshare currently does not show the virtual interfaces

# VM electronjs
https://www.electronjs.org/docs/development/build-instructions-windows
requires: 
- windows 10 server  or higher? 
- Visual Studio 2017 (have in win 10 vm image)
- python 2.7.10+ with pywin32 extensions https://pypi.org/project/pywin32/#filesv 
  https://www.python.org/downloads/release/python-2718/
- nodejs
- git
- debug tools for windows