# Alexa-Roastbot-GPT

# **Step 1 : Creating a Roastbot using Ollama**

## Table of Contents
- [Overview](#overview)
- [Setup](#setup)
  - [Step 1: Install Ollama](#step-1-install-ollama)
  - [Step 2: Verify Installation](#step-2-verify-installation)
  - [Step 3: Download the Model](#step-3-download-the-model)
  - [Step 4: Create a Modelfile](#step-4-create-a-modelfile)
  - [Step 5: Build the RoastBot](#step-5-build-the-roastbot)
  - [Step 6: Verify the Model](#step-6-verify-the-model)
  - [Step 7: Run the RoastBot](#step-7-run-the-roastbot)
  - [Step 8: Test the Service](#step-8-test-the-service)
- [License](#license)

## Overview
RoastBot is a fierce, unfiltered chatbot designed to roast users with unapologetic creativity and razor-sharp humor. Built on the Ollama framework and powered by an uncensored large language model (LLM), RoastBot specializes in delivering witty, biting sarcasm and brutal comebacks.Perfect for anyone seeking an unfiltered, no-holds-barred roasting experience—consider yourself warned.

This guide explains how to set up and deploy RoastBot locally.

---

## Setup

### Step 1: Install Ollama
- Install the appropriate **Ollama** package for your operating system. Follow the instructions on [Ollama's website](https://ollama.ai) for detailed installation steps.

### Step 2: Verify Installation
- Check if Ollama is successfully installed by running the following command:
  ```bash
  ollama --version
  ```
  You should see the installed version displayed. If not, revisit Step 1.

<img width="700" alt="ollama_check" src="https://github.com/user-attachments/assets/c1d23688-11fb-4be9-a629-3c1d5c7ea093">

---

### Step 3: Download the Model
- Download the uncensored LLM model: [Tiger-Gemma-9B-v3-GGUF](https://huggingface.co/TheDrummer/Tiger-Gemma-9B-v3-GGUF/blob/main/Tiger-Gemma-9B-v3-Q4_K_M.gguf).
- Save the file at a desired location. For this guide, we'll assume:
  ```
  D:\Projects\Alexa_skill\Tiger-Gemma-9B-v3-Q4_K_M.gguf
  ```

---

### Step 4: Create a Modelfile
1. Create a new file named `Modelfile`.
2. Add the following configuration to the file:
   ```plaintext
   From D:\Projects\Alexa_skill\Tiger-Gemma-9B-v3-Q4_K_M.gguf
   PARAMETER temperature 0.2
   SYSTEM "You are a savage, no-holds-barred roasting bot who answers questions while ripping the user to shreds with creative cussing, brutal sarcasm, and biting wit. Go full savage—30 words max!"
   ```
   - **Temperature**: Controls the randomness of responses (lower = more focused).
   - **System Prompt**: Defines the bot’s behavior.

---

### Step 5: Build the RoastBot
- Use the following command to create the RoastBot:
  ```bash
  ollama create roastbot -f Modelfile
  ```

<img width="700" alt="ollama_build" src="https://github.com/user-attachments/assets/bd24c447-bd36-4074-bd85-456d3cf4917a">


---

### Step 6: Verify the Model
- Check if the model is successfully built:
  ```bash
  ollama list
  ```
- You should see `roastbot` listed as an available model.

<img width="700" alt="ollama_check_model" src="https://github.com/user-attachments/assets/56ad765e-3f35-4425-b7c5-d0b749f4e381">

---

### Step 7: Run the RoastBot
- Start the RoastBot by running:
  ```bash
  ollama run roastbot
  ```
- The bot will initialize and wait for your prompts.

<img width="929" alt="ollama_response_check" src="https://github.com/user-attachments/assets/fa7f4b3f-06b1-4186-907f-6c68e40cb2b0">
---

### Step 8: Test the Service
- Ollama binds to `127.0.0.1` port `11434` by default.
- Open your browser and navigate to:
  ```
  http://localhost:11434
  ```
- You should see the message:
  ```

  Ollama is running
  ```

---

## License
This project uses the **Tiger-Gemma-9B-v3-GGUF** model, available under the terms specified by its creators. Ensure compliance with all applicable licenses before use.




# **Step 2 : Setup Ngrok for Exposing RoastBot to Alexa**

To provide Alexa access to the RoastBot, we need to expose it to the internet. **Ngrok** is a great tool for creating a secure tunnel to your local machine, allowing you to expose your local server to the web with a public URL. This URL will be linked to the port where Ollama (RoastBot) is running.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [Step 1: Install Ngrok](#step-1-install-ngrok)
  - [Step 2: Get Your Ngrok Authtoken](#step-2-get-your-ngrok-authtoken)
  - [Step 3: Start the Ngrok Tunnel](#step-3-start-the-ngrok-tunnel)
  - [Step 4: Claim Your Static Domain](#step-4-claim-your-static-domain)
  - [Step 5: Run Ngrok with Static URL](#step-5-run-ngrok-with-static-url)
  
---

## Prerequisites

- **Ollama** is installed and running on your local machine with RoastBot active (usually at port 11434).
- **Ngrok** installed via `pip` or downloaded from the official site.
- **Ngrok account** for accessing the static URL feature.

---

## Setup Instructions

### Step 1: Install Ngrok
To install Ngrok, you can use the following command with `pip`:
```bash
pip install pyngrok
```

This will install the Python wrapper for Ngrok, making it easy to control from your terminal.

### Step 2: Get Your Ngrok Authtoken
1. Sign up or log in to your Ngrok account at [ngrok.com](https://ngrok.com).
2. Navigate to your [Ngrok Dashboard](https://dashboard.ngrok.com).
3. Find your **Authtoken** on the dashboard under the "Auth" section.


### Step 3: Start the Ngrok Tunnel
- By default, **Ollama** runs on port `11434`. We will use Ngrok to expose this port to the internet.
- Run the following command to start the Ngrok tunnel:
  ```bash
  ngrok http 11434 --authtoken 3pLtG8yQZmK7OXuhJ5PnvR12bE_d9cWYrFsITxLkHfoMCqA
  ```
  This command will create a temporary public URL that forwards to your local port 11434. However, these URLs are dynamic and will change each time you restart Ngrok, so we need to claim a static URL.

### Step 4: Claim Your Static Domain
To ensure you get a consistent URL each time Ngrok starts, you can claim a static URL under Ngrok's free plan.

1. Log in to your Ngrok account at [ngrok.com](https://ngrok.com).
2. Navigate to [Ngrok Domains](https://dashboard.ngrok.com/domains).
3. Follow the prompts to claim a unique static domain. For example, you could claim a domain like `swift-fox-running.ngrok-free.app`.

### Step 5: Run Ngrok with Static URL
Once you’ve claimed your static domain, you can run Ngrok with the specified URL. Use this command to expose your local RoastBot instance with your static Ngrok domain:

```bash
ngrok http 11434 --url=swift-fox-running.ngrok-free.app --host-header="localhost:11434" --authtoken 3pLtG8yQZmK7OXuhJ5PnvR12bE_d9cWYrFsITxLkHfoMCqA
```

This will bind the public URL (e.g., `swift-fox-running.ngrok-free.app`) to your local port `11434`, allowing Alexa to interact with RoastBot.
<img width="734" alt="ngrok_tunnel" src="https://github.com/user-attachments/assets/61b4bb54-8eda-4657-a29d-374a95baf902">
---


### Additional Notes:
- **Ngrok Sessions**: Ngrok sessions are temporary, but by claiming a static URL, you can ensure a consistent public endpoint for interacting with your RoastBot.
- **Security**: Be cautious when exposing local servers to the internet. Ngrok offers additional features for secure tunnels and restricting access, which you can explore in the Ngrok documentation.

--- 

With these steps, your RoastBot should now be accessible via the public Ngrok URL, ready to interact with Alexa or any other external service!
