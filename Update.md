Guide update
```
sudo systemctl stop wormholesd
cd && rm -rf wormholes
git clone https://github.com/wormholes-org/wormholes
cd wormholes
git checkout v0.13.1
go build -o wormholes cmd/wormholes/main.go
mv wormholes /usr/local/bin
sudo systemctl restart wormholesd
journalctl -fu wormholesd -o cat
```
