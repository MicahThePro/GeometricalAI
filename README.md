# 🧠 GeometricalAI (cmdgpt) v0.2

A Grok-powered command-line assistant for Windows. Describe what you want in plain English, review the suggested PowerShell or CMD command, and decide whether to run it.

## ✨ Features

- **Natural language to commands:** turns requests into PowerShell (default) or CMD commands.
- **Risk warnings:** commands are tagged 🚨 HIGH RISK, ⚠️ CAUTION, or ✅ Safe / Read-Only, with the reasons shown before you confirm.
- **Confirm, edit, or copy:** run it, edit it first, copy it to the clipboard, or cancel.
- **Live output with capture:** output streams to the terminal and is kept so Grok can fix errors.
- **Follow-up awareness:** recent commands, their output, and the working directory are passed to the model, so follow-ups like "put a readme inside that folder" work.
- **Chat mode with memory:** `grok your question` keeps a running conversation and can see recent command output.
- **Usage and cost tracking:** every turn shows tokens and cost; `stats` shows session totals.
- **History log:** every executed command is logged to `~/.cmdgpt/history.log`.

## 🛠️ Install

1. Extract `cmdgpt.zip`.
2. Open PowerShell or Command Prompt in the extracted folder.
3. Run:

```
python install_and_setup.py
```

This installs the tool and asks for your xAI (Grok) API key on first run. You can also install directly with:

```
pip install -e .
```

Requires Python 3.7 or newer and Windows.

## 🔑 API key

Provide your xAI key in either of these ways:

- Set the `XAI_API_KEY` environment variable (takes priority), or
- Enter it at first run. It's saved to `~/.cmdgpt/config.json`.

The tool uses the xAI API at `https://api.x.ai/v1` with the model `grok-4.7`.

## 🚀 Usage

Start the assistant from any terminal:

```
cmdgpt
```

`gai` works as a short alias.

| Input | What it does |
|---|---|
| `Create a folder called ideas` | Suggests a command, shows risk, and asks what to do |
| `grok <question>` | Chats with Grok, with conversation memory (`gpt <question>` also works) |
| `stats` (or `cost`, `usage`) | Shows session tokens, spend, and commands run |
| `reset` (or `clear`) | Clears chat history and recent command memory |
| `exit` (or `quit`) | Quits |

### Confirmation

- Normal commands: `Run command? [y]es / [e]dit / [c]opy / [n]o:`
- HIGH RISK commands: `⚠️ HIGH RISK — Type 'yes' to run, or [e]dit / [c]opy / [n]o:`

Edits are single-line. Copy places the command on your clipboard without running it.

## 🛡️ Safety

Risk checks are advisory: they flag likely dangerous operations but can't catch everything. Read the command before you confirm.

- **HIGH RISK:** deleting files or folders, formatting or partitioning disks, registry, service, firewall, or shutdown changes, and downloads piped into execution.
- **CAUTION:** writing or overwriting file contents, moving or renaming items, and uninstalling packages.
- Text inside quotes and URLs is ignored by the checks.

## 📁 Project layout

```
cmdgpt/
  cmdgpt/__init__.py   package marker and version
  cmdgpt/cli.py        all application logic
  setup.py             package metadata and console scripts (cmdgpt, gai)
  install_and_setup.py double-click installer
  cmdgpt.spec          PyInstaller config for building cmdgpt.exe
```

## 📝 Changelog

See `RELEASE_NOTES_v0.2.md` for the full list of changes.
