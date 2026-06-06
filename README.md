# 🚀 Ultimate MCP Setup Guide for Claude Code

> A complete, step-by-step guide to supercharge Claude Code with the best MCP (Model Context Protocol) servers — covering Azure, GitHub, browser automation, web search, and more.

---

## 📋 Table of Contents

- [What is MCP?](#what-is-mcp)
- [Prerequisites](#prerequisites)
- [MCP Servers Covered](#mcp-servers-covered)
- [Installation](#installation)
  - [1. Azure MCP Server](#1-azure-mcp-server)
  - [2. Azure DevOps MCP](#2-azure-devops-mcp)
  - [3. Playwright MCP](#3-playwright-mcp)
  - [4. Chrome DevTools MCP](#4-chrome-devtools-mcp)
  - [5. Fetch MCP](#5-fetch-mcp)
  - [6. DuckDuckGo Search MCP](#6-duckduckgo-search-mcp)
  - [7. Context7 MCP](#7-context7-mcp)
  - [8. YouTube Transcript MCP](#8-youtube-transcript-mcp)
  - [9. Markitdown MCP](#9-markitdown-mcp)
  - [10. Memory MCP](#10-memory-mcp)
  - [11. GitHub MCP](#11-github-mcp)
- [One-Command Setup](#one-command-setup)
- [Verify Installation](#verify-installation)
- [Usage Examples](#usage-examples)
- [Troubleshooting](#troubleshooting)

---

## 🤔 What is MCP?

**Model Context Protocol (MCP)** is an open standard by Anthropic that lets Claude connect to external tools, APIs, and services. Think of it as **plugins for Claude** — each MCP server adds new capabilities like browsing the web, reading files, querying databases, or managing cloud resources.

---

## ✅ Prerequisites

Before installing any MCP server, make sure you have the following:

### 1. Claude Code CLI
```bash
npm install -g @anthropic-ai/claude-code
```

### 2. Node.js (v20 or higher)
```bash
# Check version
node --version

# Install via Homebrew (macOS)
brew install node

# Install via nvm (recommended)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 20
nvm use 20
```

### 3. Python + uv/uvx
`uvx` is needed for Python-based MCP servers (Fetch, DuckDuckGo, Markitdown).
```bash
# Install uv (includes uvx)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Verify
uvx --version
```

### 4. Azure CLI (for Azure MCPs only)
```bash
# macOS
brew install azure-cli

# Windows
winget install -e --id Microsoft.AzureCLI

# Login after install
az login
```

### 5. GitHub Personal Access Token (for GitHub MCP only)
1. Go to **github.com → Settings → Developer Settings**
2. Click **Personal Access Tokens → Tokens (classic)**
3. Click **Generate new token (classic)**
4. Select scopes: `repo`, `read:org`, `read:user`, `workflow`
5. Set expiration: **No expiration** (recommended for dev tools)
6. Copy the generated token

---

## 📦 MCP Servers Covered

| # | MCP Server | Purpose | API Key | Cost |
|---|-----------|---------|---------|------|
| 1 | Azure MCP Server | Azure resources management | Azure login | Free |
| 2 | Azure DevOps MCP | ADO projects, pipelines, work items | Azure login | Free |
| 3 | Playwright MCP | Browser automation | None | Free |
| 4 | Chrome DevTools MCP | Browser debugging & performance | None | Free |
| 5 | Fetch MCP | URL → Markdown content | None | Free |
| 6 | DuckDuckGo MCP | Private web search | None | Free |
| 7 | Context7 MCP | Up-to-date code documentation | None | Free |
| 8 | YouTube Transcript MCP | YouTube video transcripts | None | Free |
| 9 | Markitdown MCP | PDF/Word/Excel → Markdown | None | Free |
| 10 | Memory MCP | Persistent cross-session memory | None | Free |
| 11 | GitHub MCP | GitHub repos, PRs, issues | GitHub Token | Free |

---

## 🔧 Installation

> All commands use `--scope user` to install **globally** — available in every Claude Code session on your machine.

---

### 1. Azure MCP Server

**What it does:** Connect Claude to your Azure resources — subscriptions, resource groups, storage accounts, databases, and more.

**Prerequisites:** Azure CLI installed + `az login` completed

```bash
claude mcp add --scope user azure-mcp-server -- npx -y @azure/mcp@latest server start
```

**Test it:**
```
"List my Azure subscriptions"
"Show all resource groups"
"List storage accounts in my subscription"
```

---

### 2. Azure DevOps MCP

**What it does:** Manage Azure DevOps projects, pipelines, work items, and repositories directly from Claude.

**Prerequisites:** Azure CLI installed + `az login` completed. Replace `YOUR-ORG` with your ADO organization name (e.g., from `https://dev.azure.com/YOUR-ORG`).

```bash
claude mcp add --scope user azure-devops-mcp -- npx -y @azure-devops/mcp YOUR-ORG --authentication azcli
```

**Test it:**
```
"List all projects in my Azure DevOps organization"
"Show failed pipelines this week"
"List open work items assigned to me"
```

---

### 3. Playwright MCP

**What it does:** Full browser automation — open pages, click buttons, fill forms, take screenshots, and scrape dynamic JavaScript-rendered websites.

**Prerequisites:** None

```bash
claude mcp add --scope user playwright -- npx @playwright/mcp@latest
```

**Test it:**
```
"Open https://example.com and take a screenshot"
"Go to this URL and extract all the links"
"Fill out this form on the website"
```

---

### 4. Chrome DevTools MCP

**What it does:** Deep browser debugging using Chrome's DevTools Protocol — performance profiling, console error analysis, source-mapped stack traces, and CrUX performance data.

**Prerequisites:** Google Chrome installed

```bash
claude mcp add --scope user chrome-devtools -- npx chrome-devtools-mcp@latest
```

**Test it:**
```
"Analyze performance of https://myapp.com"
"Show console errors on this page"
"Profile the load time of this URL"
```

> **Playwright vs Chrome DevTools:**
> - Use **Playwright** for automation (clicking, scraping, form filling)
> - Use **Chrome DevTools** for debugging (performance, errors, traces)

---

### 5. Fetch MCP

**What it does:** Fetch any URL and convert its content to clean Markdown — strips ads, navigation, and clutter. Fast and lightweight for static pages.

**Prerequisites:** `uvx` installed

```bash
claude mcp add --scope user fetch -- uvx mcp-server-fetch
```

**Test it:**
```
"Fetch https://docs.python.org/3/ and summarize it"
"Get the content of this documentation page"
```

> **Fetch vs Playwright:**
> - Use **Fetch** for fast, simple static pages
> - Use **Playwright** for JavaScript-heavy/dynamic pages

---

### 6. DuckDuckGo Search MCP

**What it does:** Private web search directly inside Claude — no API key, no tracking, completely free.

**Prerequisites:** `uvx` installed

```bash
claude mcp add --scope user duckduckgo -- uvx duckduckgo-mcp-server
```

**Test it:**
```
"Search for latest React 19 features"
"What are the top results for 'Azure DevOps best practices'?"
```

---

### 7. Context7 MCP

**What it does:** Injects up-to-date, version-specific documentation for thousands of libraries directly into Claude's context. Eliminates outdated code suggestions.

**Prerequisites:** None (API key optional for higher rate limits)

```bash
claude mcp add --scope user context7 -- npx -y @upstash/context7-mcp
```

**Test it — add `use context7` to any prompt:**
```
"How do I use useState in React 19? use context7"
"Show me how to setup Express.js middleware use context7"
"Latest Next.js 15 routing syntax use context7"
```

---

### 8. YouTube Transcript MCP

**What it does:** Extract full transcripts from any YouTube video — summarize lectures, tutorials, podcasts, and talks without watching them.

**Prerequisites:** None

```bash
claude mcp add --scope user youtube-transcript -- npx -y @kimtaeyoon83/mcp-server-youtube-transcript
```

**Test it:**
```
"Get transcript of https://youtube.com/watch?v=... and summarize it"
"Extract key points from this YouTube tutorial"
```

---

### 9. Markitdown MCP

**What it does:** Convert virtually any file format to Markdown so Claude can read it — PDF, Word (.docx), Excel (.xlsx), PowerPoint (.pptx), images, and audio files.

**Prerequisites:** `uvx` installed

```bash
claude mcp add --scope user markitdown -- uvx markitdown-mcp
```

**Test it:**
```
"Read this PDF and extract the key points: /path/to/file.pdf"
"Convert this Word document to markdown"
"Extract data from this Excel spreadsheet"
```

---

### 10. Memory MCP

**What it does:** Gives Claude a persistent knowledge graph that survives across sessions — Claude remembers project details, preferences, and decisions without you repeating yourself every time.

**Prerequisites:** None

```bash
claude mcp add --scope user memory -- npx -y @modelcontextprotocol/server-memory
```

**Test it:**
```
"Remember that our database is PostgreSQL on port 5433"
"Remember my name is Saurav and I work on Azure projects"
→ Next session: Claude will already know this!
```

---

### 11. GitHub MCP

**What it does:** Full GitHub integration — read/create issues, review PRs, search commits, manage repositories, and trigger workflows — all from Claude.

**Prerequisites:** GitHub Personal Access Token (see [Prerequisites](#5-github-personal-access-token-for-github-mcp-only))

```bash
claude mcp add --scope user github \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=YOUR_TOKEN_HERE \
  -- npx -y @modelcontextprotocol/server-github
```

> ⚠️ **Security tip:** Never share your token in chat or commit it to a repository. Use environment variables or a secrets manager.

**Test it:**
```
"List my GitHub repositories"
"Show open pull requests in repo X"
"Create an issue titled 'Bug: login fails on mobile'"
"Search commits mentioning 'fix auth'"
```

---

## ⚡ One-Command Setup

Run all commands at once (replace placeholders with your values):

```bash
# Azure MCPs (requires az login first)
brew install azure-cli && az login

# Install all MCP servers
claude mcp add --scope user azure-mcp-server -- npx -y @azure/mcp@latest server start
claude mcp add --scope user azure-devops-mcp -- npx -y @azure-devops/mcp YOUR-ORG --authentication azcli
claude mcp add --scope user playwright -- npx @playwright/mcp@latest
claude mcp add --scope user chrome-devtools -- npx chrome-devtools-mcp@latest
claude mcp add --scope user fetch -- uvx mcp-server-fetch
claude mcp add --scope user duckduckgo -- uvx duckduckgo-mcp-server
claude mcp add --scope user context7 -- npx -y @upstash/context7-mcp
claude mcp add --scope user youtube-transcript -- npx -y @kimtaeyoon83/mcp-server-youtube-transcript
claude mcp add --scope user markitdown -- uvx markitdown-mcp
claude mcp add --scope user memory -- npx -y @modelcontextprotocol/server-memory
claude mcp add --scope user github -e GITHUB_PERSONAL_ACCESS_TOKEN=YOUR_TOKEN -- npx -y @modelcontextprotocol/server-github
```

---

## ✔️ Verify Installation

After installing, restart Claude Code and run:

```bash
claude mcp list
```

You should see all servers with `✓ Connected` status.

Inside Claude Code, run `/mcp` to see the same list visually.

---

## 💡 Usage Examples

### Research Workflow
```
"Search DuckDuckGo for 'microservices best practices 2026',
 fetch the top 3 articles, and summarize them"
```

### Code Documentation
```
"How do I implement JWT auth in Express? use context7"
```

### Azure Management
```
"List all my Azure resource groups and their locations"
"Show me all failed pipeline runs in Azure DevOps this week"
```

### File Analysis
```
"Read this PDF report and create a bullet point summary"
"Extract all data from this Excel file into a table"
```

### YouTube Learning
```
"Get the transcript of this 1-hour tutorial and give me
 the 10 most important takeaways"
```

### GitHub Workflow
```
"Show all open PRs in my repo that need review"
"Create a GitHub issue for this bug I found"
```

---

## 🔧 Troubleshooting

### MCP shows "Failed to connect"
- Make sure Node.js v20+ is installed: `node --version`
- Make sure uvx is installed: `uvx --version`
- Restart Claude Code after adding servers

### Azure MCPs not working
```bash
# Check if logged in
az account show

# Re-login if needed
az login
```

### GitHub MCP not working
- Check if token has correct scopes: `repo`, `read:org`, `read:user`, `workflow`
- Generate a new token if expired
- Update with: `claude mcp remove github` then re-add with new token

### Remove a server
```bash
claude mcp remove <server-name>
# Example:
claude mcp remove memory
```

### List all servers and status
```bash
claude mcp list
```

---

## 📚 Resources

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [MCP Official Docs](https://modelcontextprotocol.io)
- [Azure MCP Server](https://github.com/microsoft/mcp)
- [Azure DevOps MCP](https://github.com/microsoft/azure-devops-mcp)
- [Playwright MCP](https://github.com/microsoft/playwright-mcp)
- [Chrome DevTools MCP](https://github.com/ChromeDevTools/chrome-devtools-mcp)
- [Context7 MCP](https://github.com/upstash/context7)

---

## 🤝 Contributing

Found a better MCP or have improvements? PRs welcome!

---

## ⭐ Star this repo if it helped you!

> Made with ❤️ to help the developer community get the most out of Claude Code.
