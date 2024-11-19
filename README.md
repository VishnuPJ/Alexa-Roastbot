# Alexa-Roastbot-GPT

# Step 1 : Creating a Roastbot using Ollama
## RoastBot: A Roasting Bot Using Ollama

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

![Check Ollama Installation]("https://github.com/user-attachments/assets/c1d23688-11fb-4be9-a629-3c1d5c7ea093)
<img width="534" alt="ollama_check" src="https://github.com/user-attachments/assets/c1d23688-11fb-4be9-a629-3c1d5c7ea093">

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

![Building RoastBot](path_to_your_image)

---

### Step 6: Verify the Model
- Check if the model is successfully built:
  ```bash
  ollama list
  ```
- You should see `roastbot` listed as an available model.

![Verify RoastBot](path_to_your_image)

---

### Step 7: Run the RoastBot
- Start the RoastBot by running:
  ```bash
  ollama run roastbot
  ```
- The bot will initialize and wait for your prompts.

![Run RoastBot](path_to_your_image)

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
