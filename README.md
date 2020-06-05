
# Roadmap / Methodology

This todo list mirrors original proposals primary milestones (found in [Initial_notes.md](./Initial_Notes.md)). These may change based on further conversations.

`x` = completed
`-` = partially completed

Alpha
- [ ] Create github repository
  * [x] for project management (this here)
  * [ ] for code
- [ ] Windows development system ready ([Windows.md](./Windows.md))
  * [x] Trying Windows VM for development
  * [x] tested packet capture
  * [X] tested electronjs framework (or others. see [AppFramework.md](./AppFramework.md) 
- [-] Installer (osx/linux/electron) [[Installer.md](./Installer.md)]
  * [ ] installer or simplified config
  * [ ] ability to install without root
- [ ] Network simplification
  * [-] aprspoof or standard router ([Arpspoof.md](./Arpspoof.md))
- [-] Session save/restart ([Save.md](./Save.md))

Issues:
- Npcap Windows lib [license](https://github.com/nmap/npcap/blob/master/LICENSE) for now resolve by require user install npcap
- Windows laptop is incredibly slow, also node stopped working, may have to reinstall

Alpha Testing
- [ ] Q/A tested most features and all platforms
- [ ] Test methodology instructions

Beta
- [ ] build test tools (e.g. name discovery, cpu/memory/nodejs resource monitor)
- [ ] sniffer code ported to windows running
- [ ] unify front-end and back-end into one code base
- [ ] electron win/linux/osx quick install
- [ ] sslstrip and mitm fake logins/gmail/facebook	
- [ ] plugin framework
- [ ] os detect plugin

Beta Testing
- [ ] Q/A tested most features and all platforms
- [ ] Test methodology instructions

RC1 
- [ ] testing
- [ ] stretch: wifi ssid extract
- [ ] 0knowledge threat sharing/discovery
- [ ] documentation
- [ ] code published

Website & Support
- [ ] Setup website with github pages
- [ ] Work with the ISC technical Director to bind domain name and give admin control
- [ ] Provide a few days of ongoing support for bugs


List is a mirror of the scheduling and milestones spreadsheet found at <https://pad.ano.la/sheet/#/2/sheet/view/KSEtCRPXDtKd+VZW+SqWSYpHEZ2QZv4x+cizKP5YYYQ/> (corrupted currently 2020.05.14)
