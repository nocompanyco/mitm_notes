Notes of session save and load

## TODO
- [ ] try node-capture for windows
- [ ] 

## Notes
test code: [mitm_tests/3_pcaps_replay/](https://github.com/nocompanyco/mitm_tests/tree/master/3_pcaps_replay)

* node_pcap (posix) supports this already and one simply changes the device interface string to a file name. 
* cap (posix, windows) does not work. gives [error](https://github.com/mscdex/cap/blob/master/src/binding.cc#L314): `Warning: SIOCGIFADDR: ./http_2packets.pcap: No such device - This may not actually work`