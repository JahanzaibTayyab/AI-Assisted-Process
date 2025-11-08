The **Gemini Command Line Interface (CLI)** is an open-source AI agent that brings the power of the Gemini model directly into your terminal. It's designed to be a developer-first tool, excelling at coding tasks but versatile enough for general content generation and problem-solving.

---

## 💎 Gemini CLI Key Features

| Feature Category                | Key Capabilities                    | Usage/Benefit                                                                                                                                                                                                                           |
| :------------------------------ | :---------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Core AI & Context**           | **Powerful Model Access**           | Access to **Gemini 2.5 Pro** model with a massive **1 million token context window**, enabling analysis of very large codebases and complex projects.                                                                                   |
|                                 | **Conversation Checkpointing**      | Save and resume complex, multi-step sessions without losing context.                                                                                                                                                                    |
|                                 | **Context Files (`GEMINI.md`)**     | Define project-specific instructions, code styles, and rules in a Markdown file to tailor the agent's behavior for a repository.                                                                                                        |
| **Built-in Tools**              | **File System Operations**          | Tools like `read-file`, `write-file`, `ls` (ReadFolder), `glob` (FindFiles), and `grep` (SearchText) allow the AI to interact with your local files and code.                                                                           |
|                                 | **Shell Commands**                  | Run shell commands directly within the CLI using the `!` prefix (e.g., `! npm test`). Recent updates include **pseudo-terminal (PTY) support** for running interactive commands like `vim` or `git rebase -i` within the CLI's context. |
|                                 | **Web Integration**                 | **Google Search grounding** provides real-time information to answer queries with up-to-date and reliable context. **Web Fetch** tool can retrieve and analyze content from specific URLs.                                              |
| **Extensibility & Integration** | **Model Context Protocol (MCP)**    | Open standard support to integrate **custom tools** or external services (e.g., GitHub, image/media generation models like Imagen) by configuring MCP servers.                                                                          |
|                                 | **IDE Integration (VS Code)**       | Connect the CLI to your IDE for a context-aware experience, including access to selected code and native diff viewing for approving code changes.                                                                                       |
|                                 | **Custom Commands**                 | Create your own reusable commands to automate repetitive tasks.                                                                                                                                                                         |
| **Developer Workflows**         | **Code Understanding & Generation** | Query, explain, and edit large codebases. Generate new code, functions, or entire apps from natural language prompts, even using multimodal inputs like PDFs or sketches.                                                               |
|                                 | **Debugging & Troubleshooting**     | Explain errors, detect bugs, and troubleshoot issues using natural language instructions.                                                                                                                                               |
|                                 | **Automation**                      | Automate operational tasks, such as generating documentation, creating changelogs, or handling complex Git operations.                                                                                                                  |
| **Access & Security**           | **Free Tier**                       | Generous free access (e.g., 60 requests/min, 1,000 requests/day) with a personal Google account, accessing Gemini 2.5 Pro.                                                                                                              |
|                                 | **Open Source**                     | The project is open-source (Apache 2.0 licensed), encouraging community contributions.                                                                                                                                                  |

---

## 🛠️ How to Use Gemini CLI

### 1\. Installation

The Gemini CLI requires **Node.js (v18 or later)**.

The recommended way to install it globally is using npm:

```bash
npm install -g @google/gemini-cli
```

Alternatively, you can run it instantly without a global install using `npx`:

```bash
npx @google/gemini-cli
```

### 2\. Launch and Authentication

1.  Launch the CLI by typing:
    ```bash
    gemini
    ```
2.  The CLI will guide you through selecting a theme and choosing an **Authentication method**.
    - **Login with Google (Recommended Free Tier):** This uses OAuth to grant free access with set quotas.
    - **API Key:** You can use a custom API key (set as an environment variable `GEMINI_API_KEY`) for higher usage limits or specific models.

### 3\. Basic Interaction

The CLI operates in an interactive **REPL (Read-Eval-Print Loop)** mode.

- **Ask a Question/Task:** Simply type your prompt in natural language:
  ```
  > Write a Python script to fetch the latest news from an RSS feed.
  ```
- **Reference Local Files:** Use the `@` symbol to bring a file or directory into context for analysis or modification:
  ```
  > @src/index.js Add error handling to this file.
  ```
- **Run Shell Commands:** Use the `!` prefix to execute a command directly in your system's shell:
  ```
  > ! npm test
  ```
- **Access Help:** Type `/help` to see a list of all commands, shortcuts, and usage tips.

### 4\. Important Commands and Shortcuts

| Command  | Description                                                                            |
| :------- | :------------------------------------------------------------------------------------- |
| `/help`  | Displays help information, including all available commands.                           |
| `/chat`  | Toggles the conversational chat mode (usually the default).                            |
| `/tools` | Shows a list of all built-in and custom tools the agent can use.                       |
| `/mcp`   | Displays the list of configured Model Context Protocol servers.                        |
| `/quit`  | Exits the Gemini CLI.                                                                  |
| `Ctrl+Y` | Toggles **YOLO mode**, which automatically approves all tool calls (use with caution). |

This video provides an introductory overview of the Gemini CLI and its key features for developers. [Introducing Gemini CLI - YouTube](https://www.youtube.com/watch?v=KUCZe1xBKFM)
http://googleusercontent.com/youtube_content/0
