# DeepSeek Installation Guide on Ubuntu 24.04 Using Ollama LLM

## Overview
Running large language models like DeepSeek locally on your machine is a powerful way to explore AI capabilities without relying on cloud services. This guide provides a step-by-step walkthrough to install DeepSeek using Ollama on Ubuntu 24.04 and set up a Web UI for a more interactive and user-friendly experience.

## What is DeepSeek and Ollama?
- **DeepSeek:** An advanced AI model designed for natural language processing tasks such as answering questions, generating text, and more.
- **Ollama:** A platform that simplifies running large language models locally by providing tools to manage and interact with models like DeepSeek.
- **Web UI:** A graphical interface that allows you to interact with DeepSeek through your browser, making it more accessible and user-friendly.

## Prerequisites
Ensure you have the following:
- **Ubuntu 24.04** installed on your machine.
- **Stable internet connection.**
- **At least 8GB of RAM** (16GB or more is recommended).
- **Basic familiarity with the terminal.**

---
## Step 1: Install Python and Git
First, update your system to ensure all existing packages are up to date.
```bash
sudo apt update && sudo apt upgrade -y
```

### Install Python 3
Ensure that Python 3.8 or higher is installed.
```bash
sudo apt install python3
python3 --version
```

### Install pip
pip is required to install dependencies.
```bash
sudo apt install python3-pip
pip3 --version
```

### Install Git
Git is essential for cloning repositories from GitHub.
```bash
sudo apt install git
git --version
```

---
## Step 2: Install Ollama for DeepSeek
Install Ollama to manage DeepSeek.
```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama --version
```

Start and enable Ollama to launch automatically on system boot.
```bash
sudo systemctl start ollama
sudo systemctl enable ollama
```

---
## Step 3: Download and Run DeepSeek Model
Download the DeepSeek model using Ollama.
```bash
ollama run deepseek-r1:7b
```
This may take a few minutes depending on your internet speed.

Verify that the model is available:
```bash
ollama list
```
You should see `deepseek` listed as an available model.

---
## Step 4: Run DeepSeek in a Web UI
To interact with DeepSeek via a web interface, install and set up Open WebUI.

### Create a Virtual Environment
Isolate Python dependencies from the system-wide installation.
```bash
sudo apt install python3-venv
python3 -m venv ~/open-webui-venv
source ~/open-webui-venv/bin/activate
```

### Install Open WebUI
```bash
pip install open-webui
```

### Start the Web UI Server
```bash
open-webui serve
```
Open your web browser and navigate to [http://localhost:8080](http://localhost:8080).

In the Web UI, select the `deepseek` model from the dropdown menu to start interacting with it.

---
## Step 5: Enable Open-WebUI on System Boot
To make Open-WebUI start on boot, create a systemd service.
```bash
sudo nano /etc/systemd/system/open-webui.service
```
Add the following content to the file:
```ini
[Unit]
Description=Open WebUI Service
After=network.target

[Service]
User=your_username
WorkingDirectory=/home/your_username/open-webui-venv
ExecStart=/home/your_username/open-webui-venv/bin/open-webui serve
Restart=always
Environment="PATH=/home/your_username/open-webui-venv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

[Install]
WantedBy=multi-user.target
```
Replace `your_username` with your actual username.

### Reload systemd and Enable the Service
```bash
sudo systemctl daemon-reload
sudo systemctl enable open-webui.service
sudo systemctl start open-webui.service
```

### Check the Service Status
```bash
sudo systemctl status open-webui.service
```

If everything is set up correctly, you should see that the service is active and running.

---
## Conclusion
You have successfully installed and configured DeepSeek on Ubuntu 24.04 using Ollama and set up a Web UI for interaction. Happy exploring!

