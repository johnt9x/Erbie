# Guide update
```
sudo systemctl stop erbied
cd && rm -rf erbie
git clone https://github.com/erbieio/erbie
cd erbie
git checkout v0.14.5
go build -o erbie cmd/erbie/main.go
mv erbie /usr/local/bin
sudo systemctl restart erbied
journalctl -fu erbied -o cat
```
