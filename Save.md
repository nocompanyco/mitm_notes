Notes of session save and load/replay. Would be best if user can save from cached data rather than pre-configuring. For debug reasons ability to load raw pcap (from wireshark) also good.

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