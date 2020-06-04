Discussion of resolving permission issues on windows

* Use root installer option to somehow gain permissions
  - according to [wireshark](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Windows) the installation of winpcap (npcap too?) is enough to give all users permissions.
  - set `perMachine = false` and `allowElevation = true` to run installer as admin https://www.electron.build/configuration/nsis
  - [discussion](https://github.com/electron-userland/electron-builder/issues/2227) that includes how to install sub msi)
* request to run app as admin. example:
 https://www.authentise.com/post/electron-and-uac-on-windows
uses priv esc for windows electron install
  - or could try the runas `runas /user:<administrator username here> "<COMMAND>"`
    see example of nodejs wrapper for linux/mac and adapt