# Alexa-Roastbot

## Introduction
Welcome to Alexa-Roastbot, a project that transforms Amazon’s polite assistant into a chatbot with attitude! Built purely for fun, Roastbot is designed to deliver sharp, witty comebacks and next-level roasts, all powered by an uncensored large language model (LLM).Unlike typical AI models that play it safe with neutral or polite responses, Roastbot pushes the boundaries of conventional chatbots. It runs on the Ollama framework and utilizes an uncensored LLM to embrace humor, sarcasm, and creativity—no filters, no restrictions.

I have given all the steps to build Roastbot or any other bot in this repo.


<img width="400" alt="response" src="https://github.com/user-attachments/assets/e15d52db-4096-4f71-be5c-6bd15a50a0f6">

## Demo
Here’s a quick demo of the RoastBot:
<video src='https://github.com/user-attachments/assets/140e5ce5-d33d-40b3-9173-30066e9859c4' width=250/>
  
# 🛠️ **Step 1 : Creating a Roastbot using Ollama** 

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




# 🖥️ **Step 2 : Setup Ngrok for Exposing RoastBot to Alexa** 

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


# 🤖 **Step 3 : RoastBot Alexa Skill Setup Guide**

## Table of Contents
1. [Overview](#overview)  
2. [Setup Instructions](#setup-instructions)  
   - [Step 1: Log in to Amazon Developer Console](#step-1-log-in-to-amazon-developer-console)  
   - [Step 2: Create a New Skill](#step-2-create-a-new-skill)  
   - [Step 3: Name the Skill](#step-3-name-the-skill)  
   - [Step 4: Choose the Skill Model](#step-4-choose-the-skill-model)  
   - [Step 5: Choose Backend Resource](#step-5-choose-backend-resource)  
   - [Step 6: Start from Scratch](#step-6-start-from-scratch)  
   - [Step 7: Review and Create](#step-7-review-and-create)  
   - [Step 8: Update Interaction Model](#step-8-update-interaction-model)  
   - [Step 9: Build the Model](#step-9-build-the-model)  
   - [Step 10: Add Required Dependencies](#step-10-add-required-dependencies)  
   - [Step 11: Replace Lambda Function Code](#step-11-replace-lambda-function-code)  
   - [Step 12: Save and Deploy](#step-12-save-and-deploy)  
   - [Step 13: Enable Skill Testing](#step-13-enable-skill-testing)  
   - [Step 14: Test RoastBot Mode](#step-14-test-roastbot-mode)  
3. [Conclusion](#conclusion)
   
## Overview
This guide will walk you through the steps to create an Alexa skill called **"roasting skill"**, which will be integrated with the **RoastBot** functionality. After completing these steps, your Alexa will be able to roast users with sharp wit and creativity.

---

## Setup Instructions

### Step 1: Log in to Amazon Developer Console
- Log in to your **Amazon Developer** account at [developer.amazon.com](https://developer.amazon.com/).
- Navigate to the **Alexa Developer Console**.

### Step 2: Create a New Skill
- Click on **"Create Skill"** to begin.


<img width="837" alt="create_skill" src="https://github.com/user-attachments/assets/3800e375-3963-4756-9a58-2499c8e2e9a6">

### Step 3: Name the Skill
- Name the skill **"roasting skill"**.
- Choose the primary locale based on your language preference.
- Click **Next** to proceed.

<img width="769" alt="name_skill" src="https://github.com/user-attachments/assets/fe579169-97b9-499a-bc39-8d67cccbdea3">


### Step 4: Choose the Skill Model
- Select **"Other"** for the skill type.
- Choose **"Custom"** for the interaction model.
  
<img width="928" alt="choose_model" src="https://github.com/user-attachments/assets/38d452db-c45e-4106-bb25-bfd3f4d6f68f">


### Step 5: Choose Backend Resource
- Select **"Alexa-hosted (Python)"** for the backend resource.
- Click **Next**.

<img width="708" alt="hosting_service" src="https://github.com/user-attachments/assets/3b6ad2e7-c653-4947-897f-7532ce7d0b27">


### Step 6: Start from Scratch
- Choose **"Start from Scratch"** to begin with a blank skill template.
- Click **Next**.

<img width="713" alt="templates" src="https://github.com/user-attachments/assets/eaf3d3e5-f0bb-4039-8c6e-5755b3a5eae3">


### Step 7: Review and Create
- Review your selections, then click on **"Create Skill"**.
<img width="713" alt="templates" src="https://github.com/user-attachments/assets/48456af3-225d-4e98-bf1c-85559a0690a0">

### Step 8: Update Interaction Model
- In the **Build** section, navigate to the **"JSON Editor"** tab under **Interaction Model**.
- Replace the existing JSON content with the [provided JSON content](https://github.com/VishnuPJ/Alexa-Roastbot-GPT/blob/main/json_editor.json) :

<img width="900" alt="json" src="https://github.com/user-attachments/assets/fe81f093-fcca-4497-863c-662f707faddb">


### Step 9: Build the Model
- Click **Save** to save the model.

- After saving, click on **"Build Model"** to compile your interaction model.

### Step 10: Add Required Dependencies
- Go to the **"Code"** section.
- Add **"requests"** to the `requirements.txt` file.
- Your `requirements.txt` should look like this:

```text
ask-sdk-core==1.11.0
boto3==1.9.216
requests>=2.20.0
```

### Step 11: Replace Lambda Function Code
- In the **"Code"** section, replace the contents of the `lambda_function.py` file with the [provided Python code](https://github.com/VishnuPJ/Alexa-Roastbot-GPT/blob/main/lambda_function.py):


### Step 12: Save and Deploy
- Save your changes and click **Deploy** to update the skill on Alexa’s backend.

### Step 13: Enable Skill Testing
- Go to the **"Test"** section and enable **"Skill testing"** under **Development**.

<img width="692" alt="skill_testing" src="https://github.com/user-attachments/assets/050582d4-636f-4fda-84aa-93e40221b46e">


### Step 14: Test RoastBot Mode
- Once testing is enabled, you can begin interacting with your **RoastBot** skill.
- You should now receive responses like this from Alexa:

<img width="300" alt="resonse" src="https://github.com/user-attachments/assets/e15d52db-4096-4f71-be5c-6bd15a50a0f6">

---


## Conclusion
Your **RoastBot** Alexa skill is now up and running. Enjoy testing it out and roasting your friends with unfiltered, creative comebacks!





