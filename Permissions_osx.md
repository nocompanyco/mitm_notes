Discussion of possible ways to resolve permissions for OSX

- include apple script that executes app with admin privs: 
  - `do shell script "/Applications/Wireshark.app/Contents/MacOS/Wireshark" ¬`  
    `  with administrator privileges user name "username" password "password"`
    Or:
  - `/usr/bin/osascript -e \'do shell script "bash -c \\\"' + cmd + '\\\"" with administrator privileges\''` see example complete startup code using exec:
  https://github.com/miguelmota/global-keypress/blob/master/index.js
- use sudo-prompt or electron-sudo for specific moment to access pcap part
  https://www.npmjs.com/package/sudo-prompt
  https://github.com/automation-stack/electron-sudo
- Instruct user to setup access via Wireshark like ChmodBPF startup service which chmods /dev/bpf* to admin group and require admin group on user. OR, add user to the access_bpf group?