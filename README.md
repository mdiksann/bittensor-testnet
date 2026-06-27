# Bittensor Testnet Mining Guide

This folder contains the complete, standalone codebase and necessary scripts to easily start your Bittensor miner on the test network (NetUID 1).

## Prerequisites

Before running the miner, ensure that you have:
1. **WSL (Windows Subsystem for Linux)** installed and configured.
2. Your Bittensor Python virtual environment set up (e.g., at `~/bittensor-env/`).
3. A Bittensor wallet and hotkey created.
4. Your hotkey must be successfully registered on **NetUID 1** on the **test network**.

## How to Run the Miner

We have provided a convenient bash script (`run_miner.sh`) that will automatically activate your environment and start the miner with all the correct flags (including `--logging.debug` so you can see the startup logs).

### Step 1: Open WSL Terminal
Open your WSL terminal (Ubuntu).

### Step 2: Navigate to this directory
Use the `cd` command to enter this specific folder:
```bash
cd path/to/bittensor-testnet
```

### Step 3: Install Editable Package
If this is your first time using this new standalone directory, you might need to register this folder as the template package:
```bash
source ~/bittensor-env/bin/activate  # Update with the path to your actual venv if different
pip install -e . --no-deps
```

### Step 4: Register your wallet on the subnet
Before mining, you must register your hotkey to the subnet on the test network:
```bash
btcli subnets register --netuid 1 --wallet.name mywallet --wallet.hotkey miner1 --subtensor.network test
```

### Step 5: Execute the script
Run the bash script to start mining, passing your wallet and hotkey names as arguments:
```bash
bash run_miner.sh mywallet miner1
```

### What happens next?
The script will output the initial Bittensor configuration, connect to the test network (`wss://test.finney.opentensor.ai:443`), verify your wallet registration, and then begin listening for requests as an active miner. To stop the miner at any time, press `Ctrl + C` in your terminal.

## Troubleshooting

- **"Wallet is not registered on netuid 1"**: This means your hotkey was deregistered or you haven't registered it yet. You can re-register using:
  `btcli subnets register --netuid 1 --wallet.name <your_wallet_name> --wallet.hotkey <your_hotkey_name> --subtensor.network test`
- **ModuleNotFoundError**: Ensure your virtual environment is properly activated and you have run `pip install -e . --no-deps` inside this directory.
