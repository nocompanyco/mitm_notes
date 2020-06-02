Status: 
- built pcap windows installer on linux, and tested on windows,
- built pcap linux package on linux, and tested on linux
- built pcap osx version on osx, and test on osx

TODO:
- [x] Linux Test electron installer 
- [x] OSX Test electron installer 
- [x] Windows Test electron installer 
- [ ] Linux Test electron installer root permissions
- [ ] OSX Test electron installer root permissions
- [ ] Windows Test electron installer root permissions
- [-] OSX test pcap permissions setup from installer 
- [ ] Linux test pcap permissions setup from installer
- [ ] Windows test pcap permissions setup from installer
- [ ] Software Updates method (automatic, documented?)
- [ ] OSX test pcap permissions on second fresh computer
- [ ] Windows test pcap permissions on second fresh computer
- [ ] OSX signing certs - https://www.electron.build/code-signing#where-to-buy-code-signing-certificate
- [ ] Windows signing certs

Contents:
- [Notes](#notes)
- [Official Attempt](#official-attempt)
  - [5_install_electron](#5_install_electron)
    - [Build with pcap](#build-with-pcap)
  - [Electron.build_rootperms Attempt](#electronbuild_rootperms-attempt)


# Notes
- [electron-packager suggest](https://github.com/electron/electron-packager/issues/647)  
  using node-sudo to request root perm for pcap 
  - clearly linux/osx compatible. windows?
- [official guide](https://www.electronjs.org/docs/tutorial/application-distribution)  
  - electron-forge
  - electron-builder
  [electron.build](https://www.electron.build/configuration/win)  
  "use the requestedExecutionLevel value as "requireAdministrator""
  - electron-packager
- https://github.com/electron/windows-installer
NPM module that builds Windows installers for Electron apps using Squirrel.
https://github.com/Squirrel/Squirrel.Windows
An installation and update framework for Windows desktop apps



# Official Attempt
Installer attempt/test notes using the
[official guide](https://www.electronjs.org/docs/tutorial/application-distribution)  



## 5_install_electron
Test only basica hello world installer

notes using [electron.build](https://www.electron.build/configuration/win)  
- instructions have you install the builder and then try a boiler plate. 
  - e.g. [electron-boilerplate](https://github.com/szwacz/electron-boilerplate) A minimalistic yet comprehensive boilerplate application.  Is setup in `5_install_electron/example`. Works well but does appear to require some structural change in coding architecture so instead I went back to the simplest example or building up from scratch

go through:
- https://github.com/electron-userland/electron-builder#buildwin
- `yarn add electron --save-dev` adds version `"electron": "^9.0.0"` to devDependencies
- Create hello world electron app
  - https://www.electronjs.org/docs/tutorial/first-app
  - create boiler plat hello world example as ^^
  - `echo "hello" > index.html`
- now try: `yarn run pack`
- then exec: `./dist/linux-unpacked/5_install_electron`
- now try: `yarn run dist`
- creates linux images
  
setup to build for multiple platforms:
- https://www.electron.build/multi-platform-build
- Build app for windows on linux via local dependencies wine (+mono if want to use Squirrel installer)
- `./node_modules/.bin/electron-builder --mac --win --linux .` or just try one platform at a time
  
build for windows on linux
- `./node_modules/.bin/electron-builder --win --x64 --ia32 --publish=never .` 
- this builds a mitm.exe which tested works on windows
- build installer version setup package.json win section https://www.electron.build/configuration/win
  added to build section of package.json: `"win": { "target": ["nsis", "zip"] }`
- Requires wine with new wine dir running in 32 bit mode:
  `mkdir ~/.wine32; WINEPREFIX=~/.wine32; winecfg && WINEPREFIX=~/.wine32 WINEARCH=win32 ./node_modules/.bin/electron-builder --win --ia32 --publish=never .`   

- pull up vm (see [Windows.md](./Windows.md)) and copy over 
- nsis option https://www.electron.build/configuration/nsis  
add to build section in package.json: `"nsis": { "allowElevation": true, "oneClick": false }`

PS. helpfull config examples:
- https://github.com/mattermost/desktop/blob/master/package.json
- https://github.com/mattermost/desktop/blob/master/electron-builder.json

Build for OSX
- added mac section. according to https://github.com/electron-userland/electron-builder/issues/143 we need official signing cert to make dmg's but not zips. limiting targets to zips worked
- Tested zip on osx and works fine when user has admin privs
- TEsted zip on osx with fresh standard user and get permissions error

Automated builds for OSX electron on Travis CI
- https://studiolacosanostra.github.io/2019/03/26/Automate-electron-app-release-build-on-github-with-Travis-CI/

### Build with pcap
`5_install_electron_withpcap/`
- On osx we get incompatible compiled version issue 
  needed to add a dependency: `yard add electron-rebuild` and run `./node_modules/.bin/electron-rebuild` then `yarn run start` works. 
  - Our user has admin and access_bpf as their groups so was able to access packets. Else would need to resolve the permission issues. See [Permissions_osx.md](./Permissions_osx.md)  


## Electron.build_rootperms Attempt
`6_install_electron.build_rootperm/`


Test with root permissions
- see https://github.com/electron-userland/electron-builder/issues/2227 which includes example that installs additional msi and for root its recommended to add perMachine = true

- https://www.authentise.com/post/electron-and-uac-on-windows
uses priv esc for windows electron install