# Initia-Node
Initia node demands significant server resources and is primarily necessary for specific tasks, such as developing dApps or functioning as validators.

![image](https://github.com/user-attachments/assets/d98ad042-9cba-4036-95c6-3c498b4e99b4)

# Overview
Initia is a blockchain platform designed to integrate Layer 1 and Layer 2 architectures into a unified ecosystem called Omnitia The key components include:

Initia Orchestration Layer (Layer 1): Coordinates network security, consensus, governance, interoperability, liquidity, and inter-chain messaging

Initia Rollups (Layer 2s): Known as "Minitias", these are Layer 2 solutions built on top of the Initia Base Chain to enhance scalability and transaction throughput

Initia Optimistic Rollup Framework (OPinit Stack): Built in the CosmosSDK, used to secure Initia Rollups with fraud proofs and rollbacks

Interoperability/Bridging Middleware: Includes IBC protocol and TBA Bridge Provider for seamless asset transfer across chains
# Prerequisites
## Hardware
The minimum hardware requirements for running an Initia node are:


CPU: 16 cores


Memory: 32GB RAM


Disk: 2 TB NVMe/SSD Storage with Write Throughput > 1000 MiBps


Bandwidth: 100 Mbps

For hosting a Initia node, opt for a VPS 3 server. I chose Contabo for its reliability and performance, ideal to meet the technical requirements of Initia.
To order your Contabo VPS server, you can click on link:
https://contabo.com/en/

## Install Initia
# Update Your System
Start by updating your system packages:

```bash
sudo apt update && sudo apt upgrade -y  
```
# Install Dependencies
Install essential build tools and other dependencies:
```bash
sudo apt install -y build-essential jq git curl  
```
# Install Go
Download and install Go (version 1.18 or later):
```bash
wget https://golang.org/dl/go1.18.4.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.18.4.linux-amd64.tar.gz  
```
Add Go to your system’s PATH:
```bash
echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.profile
source ~/.profile  
```
# Verify the installation:
```bash
go version  
```
# Clone Initia Repository
Clone the Initia GitHub repository:
```bash
git clone https://github.com/Initia-Labs/initia.git
cd initia  
```
# Build Initia
Build the Initia binaries:
```bash
make build  
```
Move the binary to the Go bin directory:
```bash
sudo mv build/initiad /usr/local/bin/  
```
Verify the installation by checking the version:
```bash
initiad version
```
# Initialize the Node
Initialize your node with a unique name (replace <your_node_name>):
```bash
initiad init <your_node_name> --chain-id initiation-1  
```
# Download the Genesis File
Download the genesis file to synchronize with the network:
```bash
curl -Ls https://initia.s3.ap-southeast-1.amazonaws.com/initiation-1/genesis.json > $HOME/.initia/config/genesis.json  
```
# Configure Node
Edit the config.toml file to include persistent peers and seeds:
```bash
nano $HOME/.initia/config/config.toml  
```
Add the following lines under the relevant sections:
```bash
persistent_peers = "093e1b89a498b6a8760ad2188fbda30a05e4f300@35.240.207.217:26656,2c729d33d22d8cdae6658bed97b3097241ca586c@195.14.6.129:26019"
seeds = "2eaa272622d1ba6796100ab39f58c75d458b9dbc@34.142.181.82:26656,c28827cb96c14c905b127b92065a3fb4cd77d7f6@testnet-seeds.whispernode.com:25756"  
```
# Start the Node
Start your Initia node:
```bash
 initiad start 
```
#  Monitor Logs
Monitor your node logs to ensure proper synchronization:
```bash
tail -f $HOME/.initia/config/config.toml  
```
# Registering Initia as a Service
To make managing the Initia node easier, you can register it as a service:
Create a service file:
```bash
sudo nano /etc/systemd/system/initiad.service  
```
Add the following configuration to the service file:
```bash
[Unit]
Description=initiad

[Service]
Type=simple
User=<your_username>
ExecStart=/usr/local/bin/initiad start
Restart=on-abort
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=initiad
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target  
```
Replace <your_username> with your actual username.

Enable and start the service:
```bash
sudo systemctl enable initiad
sudo systemctl start initiad  
```
# To view logs:
```bash
journalctl -t initiad -f  
```
For further details and updates

https://docs.initia.xyz/run-initia-node/running-initia-node

https://x.com/initia

