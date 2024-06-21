# Ollama LLM Setup Guide

Welcome to the Ollama LLM Setup Guide! This repository will help you set up and interact with large language models (LLMs) on your local Windows system using Ollama. Specifically, we will guide you through the setup and use of the Llama3 and Phi-3 models.

## Table of Contents

1. [Introduction](#introduction)
2. [Windows Preview](#windows-preview)
3. [Prerequisites](#prerequisites)
4. [Setting Up Llama3](#setting-up-llama3)
   - [Download and Install Ollama](#download-and-install-ollama)
   - [Running the Llama3 Model](#running-the-llama3-model)
5. [Setting Up Phi-3](#setting-up-phi-3)
   - [Download and Install the Phi-3 Model](#download-and-install-the-phi-3-model)
   - [Running the Phi-3 Model](#running-the-phi-3-model)
6. [Scripts and Configuration Files](#scripts-and-configuration-files)
7. [Troubleshooting](#troubleshooting)
8. [Example Screenshots](#example-screenshots)

## Introduction

This guide demonstrates how to set up and run LLMs on Windows using Ollama. We will start with the Llama3 model and then move on to the Phi-3 model, showcasing how to download, install, and interact with these models using curl commands.

## Windows Preview

Ollama is now available on Windows in preview, making it possible to pull, run, and create large language models in a new native Windows experience. Ollama on Windows includes built-in GPU acceleration, access to the full model library, and the Ollama API including OpenAI compatibility.

### Hardware Acceleration

Ollama accelerates running models using NVIDIA GPUs as well as modern CPU instruction sets such as AVX and AVX2 if available. No configuration or virtualization required!

### Full Access to the Model Library

The full Ollama model library is available to run on Windows, including vision models. When running vision models such as LLaVA 1.6, images can be dragged and dropped into `ollama run` to add them to a message.

### Always-On Ollama API

Ollama’s API automatically runs in the background, serving on [http://localhost:11434](http://localhost:11434). Tools and applications can connect to it without any additional setup.

For example, here’s how to invoke Ollama’s API using **PowerShell** (Running in Local):
```powershell
(Invoke-WebRequest -method POST -Body '{"model":"llama2", "prompt":"Why is the sky blue?", "stream": false}' -uri http://localhost:11434/api/generate ).Content | ConvertFrom-json
```

## Prerequisites

Before starting, ensure you have the following:
- A Windows PC with an NVIDIA GPU (for hardware acceleration) or a modern CPU with AVX/AVX2 support.
- Administrative privileges to install software.
- Internet connection for downloading models and dependencies.

## Setting Up Llama3

### Download and Install Ollama

1. Visit [Ollama](https://ollama.com/) and download the Windows installer.
2. Run the installer (`OllamaSetup.exe`) and follow the on-screen instructions.

### Running the Llama3 Model

1. Open your favorite terminal (PowerShell, Command Prompt, etc.).
2. Check available list of Ollama models in Local:
   ```shell
   ollama list
   ```
3. In a separate terminal, run the Llama3 model:
   ```shell
   ollama run llama3
   
   ## Ask your queries
   >> ## Your Message ##
   ```

5. Test the setup by interacting with the model using a curl command:
   ```shell
   curl http://localhost:11434/api/generate -d '{
     "model": "llama3",
     "prompt": "Why is the sky blue?"
   }'
   ```

   You should receive a streamed JSON response from the model.

## Setting Up Phi-3

### Download and Install the Phi-3 Model

1. Ensure the Ollama service is running (if not, follow the previous steps to start it).
2. In a terminal, download the Phi-3 model:
   ```shell
   ollama pull phi-3
   ```

### Running the Phi-3 Model

1. In a terminal, run the Phi-3 model:
   ```shell
   ollama run phi-3
   ```

2. Test the setup by interacting with the model using a curl command:
   ```shell
   curl http://localhost:11434/api/generate -d '{
     "model": "phi-3",
     "prompt": "What is the capital of France?"
   }'
   ```

   You should receive a streamed JSON response from the model.

## Scripts and Configuration Files

### PowerShell Script to Start Ollama and Run Models

Create a script (`start_ollama_models.ps1`) to automate starting the Ollama service and running models:
```powershell
# Start Ollama service
Start-Process -NoNewWindow -FilePath "ollama.exe" -ArgumentList "serve"

# Wait for the service to start
Start-Sleep -Seconds 5

# Run Llama3 model
Start-Process -NoNewWindow -FilePath "ollama.exe" -ArgumentList "run llama3"
```

### Example Configuration for API Requests

Create a JSON configuration file (`api_request.json`) for API requests:
```json
{
  "model": "llama3",
  "prompt": "Why is the sky blue?",
  "stream": false
}
```

Use this configuration with curl:
```shell
curl http://localhost:11434/api/generate -d @api_request.json
```

## Troubleshooting

- Ensure the Ollama service is running by checking for the process in Task Manager.
- Verify the correct port (default: 11434) is used in API requests.
- Check for any error messages in the terminal where Ollama is running.
- Ensure your NVIDIA GPU drivers are up to date for hardware acceleration.

## Example Screenshots

1. Check the available ollama models in our local

![img.png](images/img.png)

2. Initiate and Run the **Llama3** model

![img_1.png](images/img_1.png)
3. Here is the sample query response

![img_1.png](images/img_2.png)

---

Thank you for using the Ollama LLM Setup Guide! I hope this documentation helps you get started with running LLMs locally on your Windows system.