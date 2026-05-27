# Building with Managed Agents in the Gemini API

A hands-on tutorial covering Google's new [Managed Agents](https://blog.google/innovation-and-ai/technology/developers-tools/managed-agents-gemini-api/) — from your first call to a custom agent defined in `AGENTS.md` and `SKILL.md`.

📖 **Read the companion post on Medium:** [[Agents Are Now Files](https://medium.com/@roya90/agents-are-now-files-4ecc3c352a29)]

## What's here

- **`managed_agents_tutorial.ipynb`** — the notebook. Walks through hello-world → multi-turn → streaming → safely pulling files out of the sandbox → registering a custom agent → an end-to-end news-digest agent.
- **`.env.example`** — template for your Gemini API key. Copy to `.env` and fill in the value.
- **`.gitignore`** — keeps `.env` and extraction temp directories out of version control.

## Quick start

1. Get a Gemini API key at [aistudio.google.com/apikey](https://aistudio.google.com/apikey).
2. Copy `.env.example` to `.env` and paste your key after `GEMINI_API_KEY=`.
3. Install dependencies and launch:
   ```bash
   pip install --upgrade google-genai requests python-dotenv
   jupyter notebook managed_agents_tutorial.ipynb
   ```
4. Run cells top to bottom.

## A few things worth knowing before you run it

- **If your key gets flagged as "leaked" right after creation**, the flag is on the *project*, not the key. Create a fresh Google Cloud project in [console.cloud.google.com](https://console.cloud.google.com) and generate the key under it.
- **Never paste the key into a notebook cell.** Cell outputs get saved to the `.ipynb` JSON. Use the `.env` flow above. Before committing, `Restart Kernel and Clear All Outputs` and grep the raw file for `AIza` to confirm it's clean.
- **The sandbox is sandboxed; your laptop is not.** The notebook downloads files an agent produced (potentially from untrusted web content) and extracts them. It uses a temp directory + an `EXPECTED` allowlist + member-type checks + `filter="data"` to defend against tar slip, symlink tricks, and unexpected files. Read the comments in those cells before changing them.
- **Network access defaults to open.** Managed Agent environments have unrestricted outbound network by default. The notebook's "Locking down the network" section shows the patterns for `network.allowlist` and `network="disabled"`.

## Why this exists

The Medium post is the argument: "agents are now files." This repo is the evidence — every claim about the API in the post has runnable code here. If you only want the prose, read the post; if you want to verify or extend any of it, start with the notebook.

## Feedback / issues

Hit a bug in the tutorial? Open an issue in this repo. Hit a bug in the Gemini API docs? The official feedback channel is the "Send feedback" button on each page at [ai.google.dev](https://ai.google.dev/gemini-api/docs/agents).
