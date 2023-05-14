# WORMHOLES
Guide wormholes official
https://www.wormholes.com/docs/install/run/docker/docker_3/index.html
# Automatic:
```
wget -O wormholes.sh https://raw.githubusercontent.com/quynhgianggithub/Wormholes/main/wormholes.sh && chmod +x wormholes.sh && ./wormholes.sh
```
# Manual: 
# update package
```
sudo apt update && sudo apt list --upgradable && sudo apt upgrade -y
```
# Install library
```
sudo apt install curl tar wget clang pkg-config libssl-dev jq build-essential git make ncdu net-tools -y
```
# Install go
```
ver="1.20.2" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```
# Install binary
```
mkdir -p .wormholes/wormholes
cd $HOME
git clone https://github.com/wormholes-org/wormholes
cd wormholes
git checkout v0.13.1
```
# Build binary
```
cd wormholes
go build -o wormholes cmd/wormholes/main.go
mv wormholes /usr/local/bin
```
# Create service
```
tee /etc/systemd/system/wormholesd.service > /dev/null <<EOF
[Unit]
Description=wormholes
After=online.target
[Service]
Type=simple
User=$USER
WorkingDirectory=$HOME
ExecStart= /usr/local/bin/wormholes \
  --datadir $HOME/.wormholes \
  --devnet \
  --identity dwentz \
  --mine \
  --miner.threads 1 \
  --rpc \
  --rpccorsdomain "*" \
  --rpcvhosts "*" \
  --http \
  --rpcaddr 127.0.0.1 \
  --rpcport 8545 \
  --port 30303 \
  --maxpeers 50 \
  --syncmode full
Restart=on-failure
RestartSec=5
LimitNOFILE=4096
[Install]
WantedBy=multi-user.target
EOF
```
# Start service
```
sudo systemctl daemon-reload
sudo systemctl enable wormholesd
sudo systemctl restart wormholesd
```
# Commands
#check log
```
journalctl -fu wormholesd -o cat
```
#check version
```
wormholes version
```
#Remove node
```
systemctl stop wormholesd
systemctl disable wormholesd
rm -rf root/usr/local/bin/wormholes
rm -rf wormholes
rm -rf wormholes.sh
rm -rf .wormholes
```
# Snapshot
```
curl -o - -L https://wm.explorer.co.id/wmsnapshot.tar.lz4 | lz4 -c -d - | tar -x -C /wm/.wormholes/wormholes/
```
remove snaphot after restart your node
```
rm -rf wmsnapshot.tar.lz4
```
