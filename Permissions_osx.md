Discussion of possible ways to resolve permissions for OSX

Also see [snifferjs Permissions wiki](https://github.com/cyphunk/snifferjs/wiki/User-Permissions)

- include apple script that executes app with admin privs: 
  - `do shell script "/Applications/Wireshark.app/Contents/MacOS/Wireshark" ¬`  
    `  with administrator privileges user name "username" password "password"`
    Or:
  - `/usr/bin/osascript -e \'do shell script "bash -c \\\"' + cmd + '\\\"" with administrator privileges\''` see example complete startup code using exec:
  https://github.com/miguelmota/global-keypress/blob/master/index.js
- Instruct user to setup access via Wireshark like ChmodBPF startup service which chmods /dev/bpf* to admin group and require admin group on user. OR, add user to the access_bpf group?
- use sudo-prompt or electron-sudo for specific moment to access pcap part
  https://www.npmjs.com/package/sudo-prompt
  https://github.com/automation-stack/electron-sudo
  - see specific attempt to use sudo-promp with cap: 
    https://github.com/jorangreef/sudo-prompt/issues/47
    conclusion: this will only work with processes. But could open process and release permissions once started, as is currently done in snifferjs
  - suggestion here that polkit be used instead https://github.com/Microsoft/vscode/issues/50964