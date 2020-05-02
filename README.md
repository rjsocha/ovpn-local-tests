# ovpn-local-tests
Local OpenVPN bw tests

Tested only on Ubuntu 18/20 LTS

Usage:
```
# Required apps
apt-get update && apt-get install -qq openvpn iperf3 

# Setup
git clone https://github.com/rjsocha/ovpn-local-tests.git
cd ovpn-local-tests
./ovpn-local-tests setup

# For RAW test
./ovpn-local-tests test-raw

# For OpenVPN
./ovpn-local-tests test

# Tune OpenVPN
./ovpn-local-tests test --tun-mtu 9000 --fragment 0 --mssfix 0 --cipher aes-256-cbc --engine aesni
./ovpn-local-tests test --tun-mtu 9000 --fragment 0 --mssfix 0 --cipher none --auth none

# Cleanup when done
./ovpn-local-tests clean
```

Example output
```
./ovpn-local-tests test-raw
Starting IPerf3 server
Starting IPers3 client
Connecting to host 10.0.0.1, port 5201
[  5] local 10.0.0.2 port 46313 connected to 10.0.0.1 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  3.54 GBytes  30.4 Gbits/sec    0   3.03 MBytes
[  5]   1.00-2.00   sec  3.87 GBytes  33.2 Gbits/sec    0   3.03 MBytes
[  5]   2.00-3.00   sec  3.75 GBytes  32.2 Gbits/sec    0   3.03 MBytes
[  5]   3.00-4.00   sec  3.78 GBytes  32.5 Gbits/sec    0   3.03 MBytes
[  5]   4.00-5.00   sec  3.75 GBytes  32.2 Gbits/sec    0   3.03 MBytes
[  5]   5.00-6.00   sec  3.70 GBytes  31.8 Gbits/sec    0   3.03 MBytes
[  5]   6.00-7.00   sec  3.81 GBytes  32.8 Gbits/sec    0   3.03 MBytes
[  5]   7.00-8.00   sec  3.80 GBytes  32.6 Gbits/sec    0   3.03 MBytes
[  5]   8.00-9.00   sec  3.81 GBytes  32.7 Gbits/sec    0   3.03 MBytes
[  5]   9.00-10.00  sec  3.79 GBytes  32.6 Gbits/sec    0   3.03 MBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  37.6 GBytes  32.3 Gbits/sec    0             sender
[  5]   0.00-10.05  sec  37.6 GBytes  32.2 Gbits/sec                  receiver

iperf Done.
```

```
./ovpn-local-tests test
Generating common secret key
Starting OpenVPN server on ns1 namespace at 10.0.0.1
Starting OpenVPN client on ns2 namespace at 10.0.0.2
Testing VPN connection: .. OK
Starting IPerf3 server
Starting IPers3 client
Connecting to host 1.1.1.1, port 5201
[  5] local 2.2.2.2 port 52521 connected to 1.1.1.1 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  16.1 MBytes   135 Mbits/sec    7    111 KBytes
[  5]   1.00-2.00   sec  17.1 MBytes   144 Mbits/sec    8   85.9 KBytes
[  5]   2.00-3.00   sec  17.1 MBytes   143 Mbits/sec    6   96.5 KBytes
[  5]   3.00-4.00   sec  17.1 MBytes   144 Mbits/sec    5    108 KBytes
[  5]   4.00-5.00   sec  17.1 MBytes   144 Mbits/sec    6    116 KBytes
[  5]   5.00-6.00   sec  16.5 MBytes   139 Mbits/sec    6   89.9 KBytes
[  5]   6.00-7.00   sec  16.7 MBytes   140 Mbits/sec    4   96.5 KBytes
[  5]   7.00-8.00   sec  16.9 MBytes   142 Mbits/sec    4    108 KBytes
[  5]   8.00-9.00   sec  17.1 MBytes   143 Mbits/sec    7   80.7 KBytes
[  5]   9.00-10.00  sec  16.9 MBytes   142 Mbits/sec    4   92.6 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   169 MBytes   142 Mbits/sec   57             sender
[  5]   0.00-10.05  sec   168 MBytes   141 Mbits/sec                  receiver

iperf Done.
Stopping OpenVPN...
```

```
./ovpn-local-tests test --tun-mtu 9000 --fragment 0 --mssfix 0 --cipher none --auth none
Generating common secret key
Starting OpenVPN server on ns1 namespace at 10.0.0.1
Starting OpenVPN client on ns2 namespace at 10.0.0.2
Testing VPN connection: .. OK
Starting IPerf3 server
Starting IPers3 client
Connecting to host 1.1.1.1, port 5201
[  5] local 2.2.2.2 port 58107 connected to 1.1.1.1 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   171 MBytes  1.43 Gbits/sec   13    603 KBytes
[  5]   1.00-2.00   sec   179 MBytes  1.50 Gbits/sec   13    699 KBytes
[  5]   2.00-3.00   sec   180 MBytes  1.51 Gbits/sec   16    533 KBytes
[  5]   3.00-4.00   sec   181 MBytes  1.52 Gbits/sec   14    629 KBytes
[  5]   4.00-5.00   sec   183 MBytes  1.53 Gbits/sec   17    751 KBytes
[  5]   5.00-6.00   sec   183 MBytes  1.53 Gbits/sec   17    620 KBytes
[  5]   6.00-7.00   sec   181 MBytes  1.52 Gbits/sec   13    638 KBytes
[  5]   7.00-8.00   sec   178 MBytes  1.49 Gbits/sec   18    551 KBytes
[  5]   8.00-9.00   sec   175 MBytes  1.47 Gbits/sec   12    612 KBytes
[  5]   9.00-10.00  sec   175 MBytes  1.47 Gbits/sec   14    690 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  1.74 GBytes  1.50 Gbits/sec  147             sender
[  5]   0.00-10.05  sec  1.74 GBytes  1.49 Gbits/sec                  receiver

iperf Done.
Stopping OpenVPN...
```
