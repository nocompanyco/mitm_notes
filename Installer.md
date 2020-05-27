Status: able to build windows installer on linux, linux installer on linux. have no tested root perms nor osx. for some reason installed windows app opens twice upon attempting to open once.

Installer
- [x] Linux/OSX Test electron installer 
- [ ] Linux/OSX Test electron installer root permissions
- [ ] OSX test pcap permissions 
- [ ] Linux test pcap permissions 
- [x] Windows Test electron installer 
- [ ] Windows Test electron installer root permissions
- [ ] Windows test pcap permissions 
- [ ] Software Updates method (automatic, documented?)

Contents:
- [Notes](#notes)
- [Official Attempt](#official-attempt)
  - [Electron.build Attempt](#electronbuild-attempt)
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



## Electron.build Attempt
`5_install_electron.build/`

notes using [electron.build](https://www.electron.build/configuration/win)  
- instructions have you install the builder and then try a boiler plate. 
  - e.g. [electron-boilerplate](https://github.com/szwacz/electron-boilerplate) A minimalistic yet comprehensive boilerplate application.  Is setup in `5_install_electron.build/example`. Works well but does appear to require some structural change in coding architecture so instead I went back to the simplest example or building up from scratch

go through:
- https://github.com/electron-userland/electron-builder#buildwin
- get certificate https://www.electron.build/code-signing#where-to-buy-code-signing-certificate
^ Lets address that some time later if it becomes relevant ^  
- `yar add electron --save-dev` adds version `"electron": "^9.0.0"` to devDependencies
- Create hello world electron app
  - https://www.electronjs.org/docs/tutorial/first-app
  - create boiler plat hello world example as ^^
  - `echo "hello" > index.html`E
- now try: `yarn run pack`
- then exec: `./dist/linux-unpacked/5_install_electron.build`
- now try: `yarn run dist`
- creates linux images
  
setup to build for multiple platforms:
- https://www.electron.build/multi-platform-build
- Build app for windows on linux via local dependencies wine (+mono if want to use Squirrel installer)
- `./node_modules/.bin/electron-builder --mac --win --linux .` or just try one platform at a time
  
build for windows on linux
- `./node_modules/.bin/electron-builder --win --x64 --ia32 --publish=never .` 
- this builds a mitm.exe but would need to test on windows machine
- build installer version setup package.json win section https://www.electron.build/configuration/win
  added to build section of package.json: `"win": { "target": ["nsis", "zip"] }`
- run again `./node_modules/.bin/electron-builder --win --x64 --ia32 --publish=never .` 
  - error: `wine /home/user/.cache/electron-builder/winCodeSign/winCodeSign-2.6.0/rcedit-ia32.exe ...workingDir= Above command failed, retrying 0 more times`
    - https://github.com/electron/electron-packager/issues/654
      try without `--x64` did not help
    - https://github.com/jiahaog/nativefier/issues/375  
      try with `mkdir ~/.wine32; WINEPREFIX=~/.wine32; winecfg && WINEPREFIX=~/.wine32 WINEARCH=win32 ./node_modules/.bin/electron-builder --win --ia32 --publish=never .`   
      ^^^^^^^^^^^^^ THIS WORKED ^^^^^^^^^^^^^^
- pull up vm (see [Windows.md](./Windows.md)) and copy over 
- nsis option https://www.electron.build/configuration/nsis  
add to build section in package.json: `"nsis": { "allowElevation": true, "oneClick": false }`

## Electron.build_rootperms Attempt
`6_install_electron.build_rootperm/`

Test with root permissions
- see https://github.com/electron-userland/electron-builder/issues/2227 which includes example that installs additional msi and for root its recommended to add perMachine = true

PS. look into how other desktop apps handle install such as https://github.com/mattermost/desktop
 - https://github.com/mattermost/desktop/blob/master/package.json
   - https://github.com/mattermost/desktop/blob/master/electron-builder.json