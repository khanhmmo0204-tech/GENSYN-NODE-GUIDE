=========================================
GENSYN AI RL SWARM NODE GUIDE
=========================================

RL Swarm is an open-source peer-to-peer reinforcement learning system.
Running a swarm node lets you train your model with swarm intelligence.
Connect to Gensyn Testnet to get an on-chain identity tracking your progress.

System Requirements:
- CPU: arm64 or amd64
- RAM: 16 GB minimum
- Python: 3.10 or higher
- GPU (optional): RTX 3090, 4090, A100, H100 supported

Install Dependencies:
1. Update and install core tools:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y python3 python3-venv python3-pip curl screen git lsof nano

2. Install Node.js 20.x and npm:
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

3. Add Yarn and install:
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install -y yarn

4. Verify installs (optional):
python3 --version
node -v
npm -v
yarn -v

Clone and Setup RL-Swarm:
1. git clone https://github.com/gensyn-ai/rl-swarm.git
2. screen -S gensyn
3. cd rl-swarm
4. python3 -m venv .venv
5. source .venv/bin/activate
6. cd modal-login
7. yarn install
8. yarn upgrade
9. yarn add next@latest viem@latest
10. cd ..
11. git switch main
12. git reset --hard
13. git clean -fd
14. git pull origin main

Run the node:
cd ..
./run_rl_swarm.sh

Answer prompts:
- Connect to Testnet? Y
- Join swarm (Math (A) or Math Hard (B))? A
- Parameters (billions)? 0.5 (or your choice)

Important: Building server takes long, keep terminal open!

Additional steps:
- If nano missing: sudo apt install nano
- Edit config: nano hivemind_exp/configs/mac/grpo-qwen-2.5-0.5b-deepseek-r1.yaml
Change:
torch_dtype: float32
bf16: false
tf32: false
gradient_checkpointing: false
per_device_train_batch_size: 1
Save and exit (Ctrl+X, Y, Enter)

Bypass slow web login:
- Open new terminal tab
- npm install -g localtunnel
- lt --port 3000
- Copy URL, open in browser, login
- Close tab, return to main terminal

Final prompts:
- Push models to Hugging Face? N
- W&B integration? 3 (Don't visualize results)

Save Node Name & Peer ID!

Manage node:
- Detach screen: Ctrl+A then D
- Reattach: screen -r gensyn
- Save swarm.pem:
sudo cp /root/rl-swarm/swarm.pem /home/$(logname)/
sudo chown $(logname):$(logname) /home/$(logname)/swarm.pem

Check status:
Use Telegram bot @gensynImpek_bot

FAQ:
- swarm.pem = your node key file, keep safe
- Mac not supported, Linux/WSL only
- Check logs: screen -r gensyn

More info: https://github.com/gensyn-ai/rl-swarm

Happy swarming!
