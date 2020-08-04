## Monster In the Middle - Status 2 - Beta
Prepared 2020.08.04

Line item #4 of proposal: "A MiTM and Phishing beta version for Windows and MacOS mentioned in the technology section & updated source code available in a recognized forge". The delivery was planned for August 10, 2020. Instead this likely delayed by 1+ week to August 17th.

2020.08.04: In previous week investigated the Pineapple platform. Discovered which tools may help with OS detection. Still exploring. Feel time pressure to stop playing with pineapple and start building our own tool to modify HTTP requests.

Important for this delivery:

- Modify client HTTP requests in transit to present fake login credential requests.

Deliveries carried over from Alpha that should be completed:

- session save/load

Desired deliverables:

- Modiffy client HTTPS requests in transit (sslstrip)
- OS detection 

Additional deliverables:

- Plugin framework
- Test tolls (name discovery test, cpu/memory/nodejs resources monitor)


Current (2020.08.04) planned timeline of 11.5 days for this phase:
* `C` are days spent or intended for this phase
* `D` is new Beta delivery deadline

|-         |  m  |  t  |  w  |  t  |  f  |  s  |  s  |
|----------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|07.27 cw31|     |     |C    |C    |     |     |     |
|08.03 cw32|     |C    |C    |C    |C    |     |     |
|08.10 cw33|C    |C    |C    |C    |C    |C    |C    |
|08.17 cw33|D    |     |     |     |     |     |     |

