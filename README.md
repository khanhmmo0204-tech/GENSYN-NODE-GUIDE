=========================================
GENSYN AI RL SWARM NODE GUIDE
=========================================

RL Swarm is an open-source system for peer-to-peer reinforcement learning over the internet.
Running a swarm node allows you to train your personal model against the swarm intelligence.
Each swarm performs RL reasoning as a group, with a gossiping system (Hivemind) for collaborative
improvement between models. You can also connect your node to the Gensyn Testnet to receive
an on-chain identity that tracks your progress over time.

RL Swarm is fully open and permissionless, meaning you can run it on a basic consumer laptop at
home or on a powerful GPU in the cloud. You can also experiment with different models to see which
ones perform best.

-----------------------------------------
System Requirements
-----------------------------------------
CPU: arm64 or amd64 architecture
RAM: At least 16 GB
Python Version: 3.10 or higher
GPU (Optional): Supported models include RTX 3090, RTX 4090, A100, H100

-----------------------------------------
Install Dependencies & Setup
-----------------------------------------

1. Update system packages and install core tools:

sudo apt update && sudo apt upgrade -y
sudo apt install -y python3 python3-venv python3-pip curl screen git lsof nano

2. Install Node.js 20.x and npm:

curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

3. Add Yarn repository and install Yarn:

curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install -y yarn

4. Verify installations (optional):

python3 --version
node -v
npm -v
yarn -v

-----------------------------------------
Clone and Setup RL-Swarm
-----------------------------------------

1. Clone RL-Swarm repository:

git clone https://github.com/gensyn-ai/rl-swarm.git

2. Start a screen session:

screen -S gensyn

3. Go to project directory:

cd rl-swarm

4. Create and activate Python virtual environment:

python3 -m venv .venv
source .venv/bin/activate

5. Install frontend dependencies:

cd modal-login
yarn install
yarn upgrade
yarn add next@latest viem@latest
cd ..

6. Update repository:

git switch main
git reset --hard
git clean -fd
git pull origin main

-----------------------------------------
Run the Node
-----------------------------------------

cd ..
./run_rl_swarm.sh

Answer the prompts exactly as below:
- Would you like to connect to the Testnet? → Y
- Which swarm would you like to join (Math (A) or Math Hard (B))? → A
- How many parameters (in billions)? → 0.5 (or your choice)

⚠️ Important: After this, the server build will start and takes a long time. Do NOT close this terminal!

-----------------------------------------
Additional Setup Steps & Bug Fixes
-----------------------------------------

1. If nano is missing, install it:

sudo apt install nano

2. Edit config file to improve performance:

nano hivemind_exp/configs/mac/grpo-qwen-2.5-0.5b-deepseek-r1.yaml

Change the following values:
torch_dtype: float32
bf16: false
tf32: false
gradient_checkpointing: false
per_device_train_batch_size: 1

Save file: Ctrl + X → Y → Enter

-----------------------------------------
Bypass Slow Web Login
-----------------------------------------

1. Open a new terminal tab on your VPS and install LocalTunnel:

npm install -g localtunnel

2. Start LocalTunnel:

lt --port 3000

3. Copy the generated localhost URL, open it in your browser, and complete login.

4. After login, close this tab and return to the main terminal.

-----------------------------------------
Final Prompts in Main Terminal
-----------------------------------------

- Push models you train to Hugging Face Hub? → N
- W&B Account integration → 3 (Don't visualize my results)

⚠️ Save your Node Name and Peer ID somewhere safe for future status checks.

-----------------------------------------
Manage Node & Screen Session
-----------------------------------------

- Detach screen session (keep node running): Ctrl + A, then D
- Re-attach screen session:

screen -r gensyn

- Save swarm.pem for future logins:

sudo cp /root/rl-swarm/swarm.pem /home/$(logname)/
sudo chown $(logname):$(logname) /home/$(logname)/swarm.pem

-----------------------------------------
Check Node Status
-----------------------------------------

Use official Telegram bot:

@gensynImpek_bot
https://t.me/gensynImpek_bot

-----------------------------------------
FAQ
-----------------------------------------

Q: What is swarm.pem?  
A: It’s your key file for authenticating and managing your node. Keep it safe!

Q: Can I run this on Mac?  
A: No, this guide is for Linux/WSL only.

Q: How do I check my node’s logs?  
A: Re-attach to screen session with `screen -r gensyn`.

-----------------------------------------
More Information
-----------------------------------------

For more details, visit the official Gensyn GitHub page:  
https://github.com/gensyn-ai/rl-swarm

-----------------------------------------
Happy Swarming! 🚀
-----------------------------------------
