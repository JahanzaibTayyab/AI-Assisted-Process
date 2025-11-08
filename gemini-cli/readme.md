# Gemini Command Line Interface (CLI)

The **Gemini Command Line Interface (CLI)** is an open-source AI agent that brings the power of the Gemini 2.5 Pro model directly into your terminal. It's designed to be a developer-first tool, excelling at coding tasks but versatile enough for general content generation and problem-solving.

---

## 💎 Gemini CLI Key Features

| Feature Category                | Key Capabilities                    | Usage/Benefit                                                                                                                                                                                                                                                  |
| :------------------------------ | :---------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Core AI & Context**           | **Powerful Model Access**           | Access to **Gemini 2.5 Pro** model with a massive **1 million token context window**, enabling analysis of very large codebases and complex projects.                                                                                                          |
|                                 | **Conversation Checkpointing**      | Save and resume complex, multi-step sessions without losing context.                                                                                                                                                                                           |
|                                 | **Context Files (`GEMINI.md`)**     | Define project-specific instructions, code styles, and rules in a Markdown file to tailor the agent's behavior for a repository.                                                                                                                               |
| **Built-in Tools**              | **File System Operations**          | Tools like `read-file`, `write-file`, `ls` (ReadFolder), `glob` (FindFiles), and `grep` (SearchText) allow the AI to interact with your local files and code.                                                                                                  |
|                                 | **Shell Commands**                  | Run shell commands directly within the CLI using the `!` prefix (e.g., `! npm test`). Recent updates include **pseudo-terminal (PTY) support** for running interactive commands like `vim` or `git rebase -i` within the CLI's context.                        |
|                                 | **Web Integration**                 | **Google Search grounding** provides real-time information to answer queries with up-to-date and reliable context. **Web Fetch** tool can retrieve and analyze content from specific URLs.                                                                     |
| **Extensibility & Integration** | **Model Context Protocol (MCP)**    | Open standard support to integrate **custom tools** or external services (e.g., GitHub, image/media generation models like Imagen) by configuring MCP servers.                                                                                                 |
|                                 | **IDE Integration (VS Code)**       | Connect the CLI to your IDE for a context-aware experience, including access to selected code and native diff viewing for approving code changes.                                                                                                              |
|                                 | **Custom Commands**                 | Create your own reusable commands to automate repetitive tasks.                                                                                                                                                                                                |
| **Developer Workflows**         | **Code Understanding & Generation** | Query, explain, and edit large codebases. Generate new code, functions, or entire apps from natural language prompts, even using **multimodal inputs** like PDFs, images, or sketches. Supports vision capabilities for analyzing diagrams and visual content. |
|                                 | **Debugging & Troubleshooting**     | Explain errors, detect bugs, and troubleshoot issues using natural language instructions.                                                                                                                                                                      |
|                                 | **Automation**                      | Automate operational tasks, such as generating documentation, creating changelogs, or handling complex Git operations.                                                                                                                                         |
| **Access & Security**           | **Free Tier**                       | Generous free access with a personal Google account: **60 requests per minute**, **1,000 requests per day**, accessing Gemini 2.5 Pro. For higher limits, use API key authentication.                                                                          |
|                                 | **Open Source**                     | The project is open-source (Apache 2.0 licensed), encouraging community contributions.                                                                                                                                                                         |

---

## 🛠️ Installation & Setup

### 1. Install Gemini CLI

The Gemini CLI requires **Node.js (v18 or later)**.

**Global installation (recommended):**

```bash
npm install -g @google/gemini-cli
```

**Or run instantly without global install:**

```bash
npx @google/gemini-cli
```

### 2. Launch and Authentication

1. Launch the CLI by typing:

   ```bash
   gemini
   ```

2. The CLI will guide you through:
   - Selecting a theme
   - Choosing an authentication method:
     - **Login with Google (Recommended Free Tier)**: Uses OAuth to grant free access with set quotas (60 requests/min, 1,000 requests/day)
     - **API Key**: Use a custom API key (set as environment variable `GEMINI_API_KEY`) for higher usage limits or specific models

### 3. Verify Installation

```bash
gemini --version
```

### 4. System Requirements

- **Node.js**: Version 18 or later (required)
- **Operating System**: macOS, Linux, or Windows
- **Internet Connection**: Required for API access and authentication

---

## 📁 Project Configuration

### 1. Create `GEMINI.md` Context File

Create a `GEMINI.md` file in your project root to define project-specific instructions, code styles, and rules:

```markdown
# Project Context for Gemini CLI

## Project Overview

[Your project description]

## Code Style Guidelines

- Follow PEP 8 for Python code
- Use TypeScript strict mode
- Follow our design system guidelines

## Development Rules

- Always use UV for Python package management
- Follow our process files in `.cursor/process/`
- Write comprehensive tests for all new features

## Project Structure

- Source code: `src/`
- Tests: `tests/`
- Documentation: `docs/`
```

### 2. MCP Server Configuration

Configure Model Context Protocol (MCP) servers for extended functionality:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"]
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem"]
    }
  }
}
```

---

## 💻 Basic Usage & Commands

### 1. Interactive REPL Mode

The CLI operates in an interactive **REPL (Read-Eval-Print Loop)** mode, allowing you to have continuous conversations with the AI:

```bash
> Write a Python script to fetch the latest news from an RSS feed.
> @src/index.js Add error handling to this file.
> ! npm test
```

**REPL Features:**

- Maintains conversation context across multiple prompts
- Supports multi-line input (press Enter to continue, Ctrl+D to submit)
- History navigation with arrow keys
- Tab completion for commands and file paths

### 2. File References

Use the `@` symbol to bring files or directories into context:

```
> @src/components/Button.tsx Explain this component
> @.cursor/process/create-prd.md Follow this process to create a PRD
> @tasks/prd-feature-x.md Generate tasks from this PRD
```

### 3. Shell Commands

Use the `!` prefix to execute shell commands:

```
> ! uv run pytest
> ! git status
> ! npm run build
```

**Advanced Shell Features:**

- **Pseudo-terminal (PTY) Support**: Run interactive commands like `vim`, `git rebase -i`, or `nano` directly within the CLI
- **Command Chaining**: Combine multiple commands with `&&` or `||`
- **Output Capture**: Command outputs are captured and can be referenced in subsequent prompts
- **Working Directory**: Commands run in the current project directory

### 4. Important Commands and Shortcuts

| Command  | Description                                                                           |
| :------- | :------------------------------------------------------------------------------------ |
| `/help`  | Displays help information, including all available commands                           |
| `/chat`  | Toggles the conversational chat mode (usually the default)                            |
| `/tools` | Shows a list of all built-in and custom tools the agent can use                       |
| `/mcp`   | Displays the list of configured Model Context Protocol servers                        |
| `/quit`  | Exits the Gemini CLI                                                                  |
| `Ctrl+Y` | Toggles **YOLO mode**, which automatically approves all tool calls (use with caution) |

---

## 🔄 Process Files Integration

### 1. Adapt Process Files for Gemini CLI

Since Gemini CLI uses `GEMINI.md` for context, reference process files:

```markdown
# In GEMINI.md

## Development Process

When creating PRDs, follow: `.cursor/process/create-prd.md`
When generating tasks, follow: `.cursor/process/generate-tasks.md`
When implementing tasks, follow: `.cursor/process/process-task-list.md`
```

### 2. Workflow Integration

Use Gemini CLI in your development workflow:

```
> @.cursor/process/create-prd.md Create a PRD for [feature description]
> @tasks/prd-feature-x.md Generate a task list from this PRD
> @tasks/feature-x/tasks-prd-feature-x.md Start implementing these tasks
```

---

## 📝 Prompt Templates

### 1. Feature Implementation Prompt

```
Using the process in @.cursor/process/create-prd.md, help me create a PRD for [feature description].
Context: [relevant background information]
Requirements: [specific requirements from PMO/Jira]
Design Reference: [Figma link or description]
```

### 2. Task Generation Prompt

```
@tasks/prd-[feature-name].md Generate a detailed task list following @.cursor/process/generate-tasks.md
Include all parent tasks and sub-tasks with implementation notes.
```

### 3. Code Review Prompt

```
Review @src/components/Button.tsx for:
- Code quality and best practices
- Potential bugs or edge cases
- Performance optimizations
- Security considerations
- Test coverage recommendations
```

### 4. Python Agent Development Prompt

```
Help me create a Python agent with OpenAI SDK:
- [specific agent functionality]
- Uses UV for project management
- Implements proper error handling
- Includes comprehensive testing
- Follows async/await patterns

Follow our Python development rules and use UV for dependencies.
```

### 5. Debugging Prompt

```
I'm experiencing [specific issue] in @src/utils/api.ts
Error message: [paste error]
Expected behavior: [describe expected outcome]
Actual behavior: [describe what's happening]
```

---

## 🚀 Advanced Features

### 1. Conversation Checkpointing

Save and resume complex sessions:

```
> /save checkpoint-name
> /load checkpoint-name
```

### 2. MCP Integration

Use MCP servers for extended functionality:

```
> /mcp  # List available MCP servers
> Use GitHub MCP to create an issue
> Use filesystem MCP to analyze project structure
```

### 3. Web Integration

Leverage Google Search and Web Fetch:

```
> Search for latest best practices on [topic]
> Fetch and analyze https://example.com/api-docs
```

### 4. Custom Commands

Create reusable commands for repetitive tasks:

```
> /command create test-runner "! uv run pytest tests/"
> /command test-runner  # Execute the custom command
> /command list  # List all custom commands
> /command delete test-runner  # Remove a custom command
```

### 5. Multimodal Input Support

Gemini CLI supports multimodal inputs for enhanced code generation:

```
> Analyze this PDF: @docs/requirements.pdf and generate implementation plan
> Review this diagram: @images/architecture.png and explain the system design
> Based on this sketch: @designs/wireframe.jpg, generate the HTML structure
```

**Supported Formats:**

- PDF documents
- Images (PNG, JPG, WebP)
- Diagrams and sketches
- Code screenshots

---

## 🔌 VS Code Integration

### 1. Connect Gemini CLI to VS Code

- Install the Gemini CLI VS Code extension (if available)
- Configure IDE integration in Gemini CLI settings
- Access selected code and native diff viewing

### 2. Workflow with VS Code

```
# In VS Code, select code
# In Gemini CLI terminal:
> Explain the selected code
> Refactor this code following our style guide
> Generate tests for this function
```

---

## 💡 Productivity Tips

### 1. Context Management

- Use `GEMINI.md` for project-wide context
- Reference specific files with `@` for focused tasks
- Use conversation checkpointing for long sessions

### 2. Efficient Workflows

- Combine file references with shell commands
- Use MCP servers for external integrations
- Leverage web search for up-to-date information

### 3. Code Generation

- Reference existing code patterns with `@`
- Use process files to maintain consistency
- Generate tests alongside implementation

---

## 🔧 Troubleshooting

### 1. Common Issues

- **Authentication errors**: Re-authenticate with Google or check API key
- **Context window limits**: Use checkpointing for long sessions
- **Tool execution errors**: Check file permissions and paths
- **MCP server issues**: Verify MCP server configuration

### 2. Performance Optimization

- Use specific file references instead of entire directories
- Leverage checkpointing for complex multi-step tasks
- Configure MCP servers only for needed functionality
- Clear conversation history periodically

### 3. Getting Help

```bash
> /help  # View all commands and shortcuts
> /tools  # List available tools
> /mcp    # Check MCP server status
```

---

## 📚 Additional Resources

### Official Documentation

- [Gemini CLI GitHub Repository](https://github.com/google/gemini-cli)
- [Model Context Protocol (MCP) Documentation](https://modelcontextprotocol.io/)
- [Gemini API Documentation](https://ai.google.dev/docs)

### Video Tutorials

This video provides an introductory overview of the Gemini CLI and its key features for developers: [Introducing Gemini CLI - YouTube](https://www.youtube.com/watch?v=KUCZe1xBKFM)

---

## 📄 License

The Gemini CLI is open-source and licensed under the Apache 2.0 license, encouraging community contributions.

---

**Last Updated**: Based on latest Gemini CLI features and capabilities
