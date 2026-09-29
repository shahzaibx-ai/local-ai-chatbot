# 🤖 Local AI Chatbot

A private, local AI chatbot built with **Python, Ollama, and Streamlit**.

This project allows you to run open-source language models directly on your own computer through Ollama. It provides an interactive chat interface with local model selection, customizable system prompts, temperature and context controls, chat reset, streaming responses, model information, and conversation export.

The application is designed for users who want to experiment with local AI without sending their conversations to a remote AI API.

---

## ✨ Features

* 🏠 **Run AI locally** using Ollama
* 🤖 **Automatically detect installed Ollama models**
* 🔄 **Refresh available local models**
* 🎯 **Select the model from the Streamlit sidebar**
* 🧠 **Custom system prompt**
* 🌡️ **Adjust temperature**
* 📚 **Adjust context length**
* 💬 **Interactive chat interface**
* ⚡ **Streaming AI responses**
* 🔄 **Regenerate the latest response**
* 🗑️ **Clear chat history**
* 📊 **Display generation statistics**
* 📄 **Export conversations as TXT**
* 📦 **Export conversations as JSON**
* 🟢 **Ollama connection status**
* 🌙 **Custom dark interface**
* 🔒 **Local/private model execution**

---

## 🛠️ Technologies Used

| Technology            | Purpose                                  |
| --------------------- | ---------------------------------------- |
| **Python 3.14+**      | Main programming language                |
| **Ollama**            | Runs open-source AI models locally       |
| **Ollama Python SDK** | Connects Python application to Ollama    |
| **Streamlit**         | Creates the web-based chatbot interface  |
| **uv**                | Python project and dependency management |
| **JSON**              | Conversation export                      |
| **datetime**          | Export timestamps and metadata           |

The project declares Python `>=3.14` in `pyproject.toml` and uses Streamlit and the Ollama Python package as its main external dependencies.

---

# 📋 Requirements

Before running the project, make sure your computer has the following:

### 1. Python

Python **3.14 or newer** is required by this project.

Check your installed version:

```powershell
python --version
```

Example:

```text
Python 3.14.x
```

You can download Python from:

https://www.python.org/downloads/

---

### 2. Ollama

This application requires the **Ollama application/runtime** in addition to the Python `ollama` package.

The Python package allows this project to communicate with Ollama, while the Ollama application actually runs the AI model locally.

Download Ollama:

https://ollama.com/download

For Windows, Ollama supports Windows 10 and later. After installation, Ollama provides a local service that applications can connect to.

Verify Ollama:

```powershell
ollama --version
```

Also check installed models:

```powershell
ollama list
```

---

### 3. A Local Ollama Model

The application does not contain an AI model inside the GitHub repository.

You must download at least one model through Ollama.

For example:

```powershell
ollama pull gemma3:4b
```

Another example:

```powershell
ollama pull qwen2.5:3b
```

Check the installed models:

```powershell
ollama list
```

The application automatically reads the models installed on your local Ollama server and shows them in the sidebar.

For example, `gemma3:4b` is available through Ollama and is listed as a multimodal model with a current package size of about 3.3 GB.

> **Important:** Model storage size and hardware requirements depend on the model you choose. Larger models generally require more RAM/VRAM and storage.

---

# 📥 Installation

There are two easy ways to install this project.

## Option 1 — Recommended: Using uv

This project is configured with `pyproject.toml` and is suitable for `uv`.

### Step 1 — Install uv

Install uv from:

https://docs.astral.sh/uv/

Check the installation:

```powershell
uv --version
```

---

### Step 2 — Clone the repository

Open PowerShell or Command Prompt and run:

```powershell
git clone https://github.com/shahzaibx-ai/local-ai-chatbot.git
```

Move into the project folder:

```powershell
cd local-ai-chatbot
```

---

### Step 3 — Install project dependencies

Run:

```powershell
uv sync
```

`uv` reads the project's `pyproject.toml`, creates/manages the project environment, and installs the declared dependencies.

The main Python dependencies are:

```text
ollama>=0.6.3
streamlit>=1.64.0
```

---

### Step 4 — Run the application

Run:

```powershell
uv run streamlit run app.py
```

This starts the Streamlit application using the project's managed environment.

---

# ▶️ Option 2 — Using Python + pip

You can also run the project without uv.

### Step 1 — Clone the repository

```powershell
git clone https://github.com/shahzaibx-ai/local-ai-chatbot.git
```

Then:

```powershell
cd local-ai-chatbot
```

---

### Step 2 — Create a virtual environment

```powershell
python -m venv .venv
```

---

### Step 3 — Activate the virtual environment

For Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

For Windows Command Prompt:

```cmd
.venv\Scripts\activate.bat
```

After activation, your terminal should show something similar to:

```text
(.venv)
```

Using a virtual environment keeps the project's Python packages isolated from other projects. Streamlit's official installation guide also recommends using a virtual environment.

---

### Step 4 — Install dependencies

You can install the dependencies directly:

```powershell
pip install "ollama>=0.6.3" "streamlit>=1.64.0"
```

Or install the project from its `pyproject.toml`:

```powershell
pip install -e .
```

---

### Step 5 — Run the application

```powershell
streamlit run app.py
```

If the `streamlit` command is not recognized, use:

```powershell
python -m streamlit run app.py
```

The official Streamlit documentation supports both forms.

---

# 🚀 Quick Start

Once Python, Ollama, and the dependencies are installed, the normal workflow is:

```powershell
git clone https://github.com/shahzaibx-ai/local-ai-chatbot.git
cd local-ai-chatbot
uv sync
ollama pull gemma3:4b
uv run streamlit run app.py
```

Then open the local Streamlit URL shown in your terminal, normally:

```text
http://localhost:8501
```

---

# 🧠 How the Application Works

The application uses the following flow:

```text
User
  │
  ▼
Streamlit Interface
  │
  ▼
Select Local Ollama Model
  │
  ▼
Build Chat Messages
  │
  ├── System Prompt
  ├── Previous Messages
  └── New User Message
  │
  ▼
Ollama Local API
  │
  ▼
Selected Local LLM
  │
  ▼
Streaming Response
  │
  ▼
Streamlit Chat Interface
```

The application connects to Ollama using:

```text
http://127.0.0.1:11434
```

This address is configured in `app.py`:

```python
OLLAMA_HOST = "http://127.0.0.1:11434"
```

The chatbot therefore expects Ollama to be available locally on the default Ollama service address.

---

# 🎛️ Application Configuration

The sidebar contains several configuration options.

## Ollama Connection

The application checks whether Ollama is reachable.

### Online

When Ollama is available, the interface displays:

```text
● ONLINE
```

### Offline

When the application cannot connect to Ollama, it displays:

```text
● OFFLINE
```

and shows the connection error.

---

## 🤖 Local Model Selection

The application uses:

```python
client.list()
```

to retrieve models installed on the local Ollama server.

Only models actually installed on the computer are displayed.

For example:

```text
gemma3:4b
qwen2.5:3b
```

The application prefers:

```text
gemma3:4b
```

when it is installed.

If that model is not available, the application automatically selects another installed model.

---

## 🌡️ Temperature

Temperature controls how the model generates responses.

The application allows values from:

```text
0.0 → 2.0
```

Generally:

* Lower temperature = more focused/predictable responses
* Higher temperature = more variation/creativity

The default value is:

```text
0.7
```

---

## 📚 Context Length

The application provides these context-length options:

```text
1024
2048
4096
8192
16384
32768
```

The default is:

```text
4096
```

Higher context settings can require more system resources depending on the model and hardware.

---

## 🧠 System Prompt

The application includes a customizable system prompt.

Default:

```text
You are a helpful local AI assistant.
Answer clearly and accurately.
Use simple explanations when possible.
```

You can change this from the sidebar.

For example:

```text
You are a Python programming tutor.
Explain programming concepts in simple English
and provide practical examples.
```

The system prompt is sent separately from the visible conversation history.

---

# 💬 Chat Features

## Streaming Responses

The application streams the model response as it is generated instead of waiting for the complete response before displaying it.

This provides a more interactive chatbot experience.

---

## Regenerate Response

After the assistant generates a response, the interface provides a:

```text
🔄 Regenerate
```

button.

Clicking this removes the last assistant response so the request can be generated again.

---

## Clear Chat

The sidebar includes:

```text
🗑️ Clear Chat
```

This removes the current conversation from the application's session state.

---

# 📤 Conversation Export

The chatbot supports two export formats.

## TXT

The conversation can be downloaded as:

```text
ollama_chat.txt
```

---

## JSON

The conversation can also be downloaded as:

```text
ollama_chat.json
```

The JSON export contains information such as:

* Export timestamp
* Selected model
* System prompt
* Temperature
* Context length
* Conversation messages

Example structure:

```json
{
  "exported_at": "2026-09-29T23:00:00",
  "model": "gemma3:4b",
  "temperature": 0.7,
  "context_length": 4096,
  "messages": []
}
```

---

# 📊 Dashboard

The main interface displays four pieces of information:

| Dashboard Item       | Description                                    |
| -------------------- | ---------------------------------------------- |
| **Connection**       | Shows whether Ollama is reachable              |
| **Installed Models** | Number of locally available models             |
| **Messages**         | Number of messages in the current conversation |
| **Current Model**    | Currently selected Ollama model                |

---

# 📁 Project Structure

```text
local-ai-chatbot/
│
├── README.md
├── app.py
├── pyproject.toml
├── .python-version
│
└── src/
    └── local_ai_chatbot/
        └── __init__.py
```

### `README.md`

Project documentation, installation instructions, usage information, and troubleshooting.

### `app.py`

Main Streamlit application.

This file contains:

* Streamlit UI
* Ollama connection
* Model detection
* Chat functionality
* System prompt handling
* Generation settings
* Chat history
* Response streaming
* Regeneration
* Export functions
* Error handling
* Custom CSS

### `pyproject.toml`

Project configuration and Python dependency definitions.

It contains:

```toml
requires-python = ">=3.14"
```

and:

```toml
dependencies = [
    "ollama>=0.6.3",
    "streamlit>=1.64.0",
]
```

### `.python-version`

Specifies the project's Python version:

```text
3.14
```

This is particularly useful with uv.

### `src/local_ai_chatbot/__init__.py`

Package initialization file for the Python project structure.

---

# 🔧 Troubleshooting

## Problem 1 — Ollama is Offline

You may see:

```text
Could not connect to local Ollama.
```

First check:

```powershell
ollama --version
```

Then:

```powershell
ollama list
```

If Ollama is installed but its service is not running, start Ollama. Depending on your installation, you may also start the Ollama server manually:

```powershell
ollama serve
```

Then return to the application and click:

```text
🔄 Refresh Models
```

---

## Problem 2 — No Models Found

The application may display:

```text
No locally installed models found.
```

Install a model:

```powershell
ollama pull gemma3:4b
```

Then verify:

```powershell
ollama list
```

After that, click:

```text
🔄 Refresh Models
```

---

## Problem 3 — `streamlit` Command Not Found

Instead of:

```powershell
streamlit run app.py
```

use:

```powershell
python -m streamlit run app.py
```

---

## Problem 4 — Python Version Error

The project requires:

```text
Python >= 3.14
```

Check your version:

```powershell
python --version
```

With uv, you can also check:

```powershell
uv python list
```

Make sure the environment uses a compatible Python version.

---

## Problem 5 — PowerShell Does Not Allow Virtual Environment Activation

You may receive an execution-policy error when running:

```powershell
.venv\Scripts\Activate.ps1
```

You can instead use Command Prompt:

```cmd
.venv\Scripts\activate.bat
```

or use the uv workflow:

```powershell
uv sync
uv run streamlit run app.py
```

This avoids manually activating the environment.

---

## Problem 6 — Model Takes a Long Time to Respond

Local AI performance depends on:

* Model size
* Available RAM
* CPU performance
* GPU availability
* Context length
* Quantization
* Other applications running on the computer

Try a smaller model if your computer has limited resources.

For example:

```powershell
ollama pull qwen2.5:3b
```

---

# 🔐 Privacy

One of the main goals of this project is local AI execution.

The chatbot communicates with the local Ollama server configured at:

```text
http://127.0.0.1:11434
```

The application does not require an OpenAI API key or another cloud AI API key to generate responses.

However, privacy still depends on the Ollama models, software, operating system, and other applications installed on your computer.

---

# 🌐 Why Local AI?

Running AI models locally can be useful for:

* Learning about Large Language Models
* AI experimentation
* Offline/limited-internet environments
* Local development
* Privacy-sensitive experimentation
* Understanding model configuration
* Learning how applications communicate with local LLM servers

---

# 🧪 Example Usage

After starting the application, you can ask questions such as:

```text
Explain Python OOP in simple English.
```

```text
Write a Python function to reverse a string.
```

```text
Explain the difference between supervised and unsupervised learning.
```

```text
Help me debug this Python code.
```

You can also change the system prompt to make the chatbot behave as a tutor, coding assistant, researcher, or general-purpose assistant.

---

# 📌 Important Notes

### Ollama and the Python package are different

Installing this Python dependency:

```text
ollama
```

does **not** install the Ollama application itself.

You need both:

```text
Ollama Runtime
        +
Python Ollama Package
```

The application uses the Python package to communicate with the locally running Ollama service.

---

### The application entry point is `app.py`

This project is a Streamlit application, so start it with:

```powershell
streamlit run app.py
```

or, when using uv:

```powershell
uv run streamlit run app.py
```

The Streamlit documentation uses `streamlit run <file>` as the standard way to launch a Streamlit application.

---

# 🚀 Development

To modify the project:

1. Clone the repository.
2. Install the dependencies.
3. Start the Streamlit application.
4. Edit `app.py`.
5. Save the changes.
6. Streamlit automatically reloads the application during development.

With uv:

```powershell
uv sync
uv run streamlit run app.py
```

---

# 📦 Main Dependencies

The project currently uses:

```text
Python >= 3.14
Ollama Python >= 0.6.3
Streamlit >= 1.64.0
```

The Python standard library modules used by the application include:

```text
json
datetime
```

No separate database is required.

---

# 📄 License

No license has currently been specified in this repository.

If you plan to distribute or reuse the project publicly, consider adding an appropriate open-source license.

---

# 👨‍💻 Author

**Muhammad Shahzaib**

IT / Computer Science Graduate
AI & Technology Enthusiast

### GitHub

[![GitHub](https://img.shields.io/badge/GitHub-shahzaibx--ai-black?style=for-the-badge\&logo=github)](https://github.com/shahzaibx-ai)

Project repository:

[shahzaibx-ai/local-ai-chatbot](https://github.com/shahzaibx-ai/local-ai-chatbot)

### LinkedIn

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Muhammad%20Shahzaib-blue?style=for-the-badge\&logo=linkedin)](https://www.linkedin.com/in/muhammad-shahzaib-arshed/)

### Email

📧 **[mszaibi007@gmail.com](mailto:mszaibi007@gmail.com)**

---

# 🔗 Useful Links

* **GitHub Repository:** https://github.com/shahzaibx-ai/local-ai-chatbot
* **Ollama:** https://ollama.com/
* **Ollama Models:** https://ollama.com/library
* **Streamlit:** https://streamlit.io/
* **Python:** https://www.python.org/
* **uv:** https://docs.astral.sh/uv/

---

## ⭐ Project

If this project is useful for you, consider giving the repository a ⭐ on GitHub.

Built with **Python + Ollama + Streamlit**.
