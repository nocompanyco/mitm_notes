## Monster In the Middle - Status 1 - Alpha
Prepared 2020.06.05

The delivery of the Alpha version with installation instructions originally planned for 2020.06.05 will be delayed by one week to 2020.06.13.

The intended features for the Alpha as originally planned are: Windows support (libpcap, electron if time), first UI changes, simpler install, simpler network, session save/restart. Each of these features have been partially explored through feature specific tests that can be found in the [mitm_tests](https://github.com/nocompanyco/mitm_tests) repository. This approach has been useful in clarifying some design choices but has also moved slower that desired. From this point effort will switch to coding the deliverable with integrated features.

Issues that have arrisen are:
- Npcap, a library required on windows, has a [license](https://github.com/nmap/npcap/blob/master/LICENSE) with some restrictions. In the best case, upon further investigating, we may find it is no issue to integrate the installation of NPcap into MiTM. In the worst case we may have to ask the user to install it independently or install wireshark which has it integrated. 
- Windows laptop purchased for testing and development, a Lenovo IdeaPad Slim for <$300, is incredibly slow. Also windows laptop development environment initially worked but later became corrupted somehow. Development will continue within a Windows VM instead and laptop will be used for final installation and use testing.

Timeline for this phase:
* `C` are days spent on this phase
* `D` is new Alpha delivery deadline

|-         |  m  |  t  |  w  |  t  |  f  |  s  |  s  |
|----------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|05.18 cw21|     |     |     |     |C    |C    |     | 
|05.25 cw22|     |C    |C    |C    |C    |     |     | 
|06.01 cw23|     |     |C    |C    |C    |     |     | 
|06.08 cw24|     |     |     |     |D    |     |     | 
