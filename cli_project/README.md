# MCP Chat

MCP Chat is a command-line interface application that enables interactive chat capabilities with AI models through the Anthropic API. The application supports document retrieval, command-based prompts, and extensible tool integrations via the MCP (Model Control Protocol) architecture.

## Prerequisites

- Python 3.10+
- Anthropic API Key

## Setup

### Step 1: Configure the environment variables

1. Create or edit the `.env` file in the project root and verify that the following variables are set correctly:

```
ANTHROPIC_API_KEY=""  # Enter your Anthropic API secret key
```

### Step 2: Install dependencies

#### Option 1: Setup with uv (Recommended)

[uv](https://github.com/astral-sh/uv) is a fast Python package installer and resolver. This project is uv-managed (it has a `uv.lock`), so you don't need to create a virtual environment, activate it, or `pip install` anything manually — uv handles all of that.

1. Install uv, if not already installed:

```bash
pip install uv
```

2. From the project directory (the folder containing `pyproject.toml`), sync the environment. This creates `.venv` and installs the locked dependencies:

```bash
cd cli_project   # if you aren't already inside it
uv sync
```

3. Run the project. `uv run` automatically uses the project's environment — no activation step needed:

```bash
uv run main.py
```

> **Notes**
> - Run `uv sync` / `uv run` from inside the project folder. Running elsewhere gives `error: No pyproject.toml found in current directory or any parent directory`.
> - If you see `VIRTUAL_ENV ... does not match the project environment path`, you have another venv activated. It's only a warning — uv correctly ignores it and uses the project's `.venv`. Run `deactivate` to silence it.
> - Re-run `uv sync` whenever dependencies change; otherwise `uv run main.py` is all you need day to day.

#### Option 2: Setup without uv

1. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

2. Install dependencies:

```bash
pip install anthropic python-dotenv prompt-toolkit "mcp[cli]==1.8.0"
```

3. Run the project

```bash
python main.py
```

## Usage

### Basic Interaction

Simply type your message and press Enter to chat with the model.

### Document Retrieval

Use the @ symbol followed by a document ID to include document content in your query:

```
> Tell me about @deposition.md
```

### Commands

Use the / prefix to execute commands defined in the MCP server:

```
> /summarize deposition.md
```

Commands will auto-complete when you press Tab.

## Development

### Adding New Documents

Edit the `mcp_server.py` file to add new documents to the `docs` dictionary.

### Implementing MCP Features

To fully implement the MCP features:

1. Complete the TODOs in `mcp_server.py`
2. Implement the missing functionality in `mcp_client.py`

### Linting and Typing Check

There are no lint or type checks implemented.
