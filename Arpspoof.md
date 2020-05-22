Notes on using arpspoof to take control of routing, as apposed to installing a wifi router everyone uses. For details see [Initial_Notes.md](./Initial_Notes.md) / Challenges Details / "4. config A".

TOC
- [TODO](#todo)
- [Windows](#windows)
  - [Npcap, winpcap nodejs libs](#npcap-winpcap-nodejs-libs)
- [Comparability of pcap libs](#comparability-of-pcap-libs)
  - [aprspoof non-javascript windows](#aprspoof-non-javascript-windows)


## TODO
* [-] check comparability of decoders (node_pcap, cap)
* [ ] test the windows libs on windows (node-capture, cap)
* [ ] test arpspoof libs

## Windows
no existing nodejs+arpspoof npcap or wincap for node found
Could build up from pcap lib on windows.

###  Npcap, winpcap nodejs libs
Options for building our own arpspoof in node.
* https://github.com/pauldorn/node-capture
  - npcap bindings for nodejs
  - very basic however
* https://github.com/mscdex/cap
  - For Windows: Npcap with WinPcap compatibility
  - For *nix: libpcap and libpcap-dev/libpcap-devel packages
  - Has parsers
  * https://github.com/mscdex/cap/issues/95
    [ _"If I'm not mistaken, this module could starve the loop, because it enters an infinite loop until there's no packets: {code} So if packets arrive very fast (or the processing of each one takes a long time), this could block for an arbitrary amount of time."_
    - from alba's email private: _"I have never used cap, though. That issue was just because I noticed it applied to that project too."_
    * https://www.winpcap.org/docs/docs_412/html/group__wpcap__tut3.html
      - from winpcap docs: _"to_ms specifies the read timeout, in milliseconds. A read on the adapter (for example, with pcap_dispatch() or pcap_next_ex()) will always return after to_ms milliseconds, even if no packets are available from the network. "_
      - Suggestion from review... use a thread as used in: 
      https://github.com/pauldorn/node-capture/blob/f4e49244d864bfc69d94d295b3d02684d7211479/src/binding.cc#L573

* https://github.com/pauldorn/node-capture
  - windows only npcap bindings
  - seems small enough. appears to have resolve the cap issue by putting it in a thread
  - does not have the tcpsession, dns and other parsers. just simple packet info

## Comparability of pcap libs
Compare the output nodejs pcap lib packet decoders. see `2_pcaps_compare/index.js` for test case

### aprspoof non-javascript windows
have yet to find a nodejs implementation working on windows so we may have to write one from scratch. these other examples may be helpful.
* https://github.com/alandau/arpspoof
  C++, arpspoofer for windows

