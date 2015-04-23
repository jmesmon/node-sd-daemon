# Bindings for libsystemd-daemon #

## Dependencies ##
* pkg-config
* libsystemd-daemon-dev

## Install ##
```
npm install sd-daemon
```

### On Debian ###
```
sudo apt-get install devscripts
sudo mk-build-deps -ir
debuild
sudo dpkg -i ../node-sd-daemon_*.deb
```

## Test ##

### Watchdog ###
```
systemctl --user link "$PWD/test/test.service"
systemctl --user start test.service

curl localhost:8089
systemctl --user status test.service
curl localhost:8089/block
....
systemctl --user status test.service

systemctl --user stop test.service
systemctl --user disable test.service
```

### Socket Activation ###

test.service:
```
...
[Service]
ExecStart=...
NonBlocking=yes
```

```
systemctl --user link "$PWD/test/test-socket.socket" "$PWD/test/test-socket.service"
systemctl --user start test-socket.socket

curl localhost:8088
systemctl --user status test-socket.service
....

systemctl --user stop test-socket.socket test-socket.service
systemctl --user disable test-socket.socket
```
