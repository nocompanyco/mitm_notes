Conclusion: 
- user can load pcap from wireshark, node-pcap can replay
- user will be allowed to save json of cached data in ui and reload this
- save and load operations do not require root so install should also not require root


TOC

- [TODO](#todo)
- [Replay raw packets](#replay-raw-packets)

## TODO
- [ ] try node-capture save on windows
- [ ] save decoded packets to file
- [ ] replay decoded packets from file
- [x] replay raw packets from pcap file
- [ ] save raw packets to pcap file


## Replay raw packets
test code: 
[mitm_tests/3_pcaps_replay/](https://github.com/nocompanyco/mitm_tests/tree/master/3_pcaps_replay)

* node_pcap (posix) supports this already has replay support and one simply changes the device interface string to a file name. 
* cap (posix, windows) does not work. gives [error](https://github.com/mscdex/cap/blob/master/src/binding.cc#L314): `Warning: SIOCGIFADDR: ./http_2packets.pcap: No such device - This may not actually work`