# ovpn-local-tests
Local OpenVPN bw tests

Usage:
```
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
