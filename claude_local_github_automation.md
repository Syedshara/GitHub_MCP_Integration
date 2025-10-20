# Claude Local Files + GitHub Automation Setup

## Overview: What We're Building

You'll now have TWO MCP servers connected to Claude:
1. **GitHub MCP** - To create repos and push code (already done ✅)
2. **Filesystem MCP** - To access your local VS Code project files (NEW)

This lets Claude:
- Read your project files from your Mac
- Make changes to files if needed
- Create a GitHub repository
- Commit and push everything to GitHub

---

## Step 1: Update Your Configuration File

Open Terminal and edit your Claude config:

```bash
nano ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

Replace the entire content with this (add the filesystem server while keeping GitHub):

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your token"
      }
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/mog/Documents", "/Users/mog/Desktop", "/Users/mog/Projects"]
    }
  }
}
```

### Important: Replace the Paths!

Replace these paths with where your VS Code projects actually are:
- `/Users/mog/Documents` - Example path, use your actual username and directory
- `/Users/mog/Desktop` - Where your project might be
- `/Users/mog/Projects` - Where you keep projects (create if needed)

**To find your projects path:**
```bash
pwd
```

This shows your current directory. If your project is in a folder called "my-project", use:
```
/Users/mog/my-project
```

---

## Step 2: Save the Configuration

In nano editor:
1. Press `Control + X`
2. Press `Y` (yes to save)
3. Press `Enter` (confirm filename)

Verify it saved:
```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

---

## Step 3: Restart Claude Desktop

1. Completely close Claude Desktop (⌘+Q)
2. Wait 5 seconds
3. Open Claude Desktop again (Cmd+Space, type "Claude")

---

## Step 4: Check Both MCP Servers are Connected

In Claude, ask:
```
What tools do you have available?
```

You should see:
- **GitHub tools** (list_repos, create_repository, create_pull_request, etc.)
- **Filesystem tools** (read_file, write_file, list_directory, etc.)

Look for a **hammer icon** in the bottom right of the input box. Click it to see all available tools.

---

## Step 5: Now Automate Your Workflow!

### Example 1: Push Existing Project to GitHub

Let's say you have a project at `/Users/mog/my-project`. Ask Claude:

```
I have a project at /Users/mog/my-project. 
Please:
1. Read all the files in this directory
2. Create a new GitHub repository called "my-project"
3. Initialize git in the project
4. Add all files
5. Make an initial commit
6. Push to GitHub

My GitHub username is: mog
```

### Example 2: Create and Push a New Project

```
Create a new folder called "my-app" in /Users/mog/Desktop
Then:
1. Create an initial README.md with project description
2. Create a .gitignore file
3. Create a GitHub repository called "my-app"
4. Initialize git and push everything to GitHub

My GitHub username is: mog
```

### Example 3: Update Existing Code and Push

```
1. Update the file at /Users/mog/my-project/index.js with [your changes]
2. Commit the changes with message "Update index.js"
3. Push to GitHub repository "my-project"

My GitHub username is: mog
```

---

## Complete Automation Example

Here's a detailed example you can copy and customize:

```
I want to create and push a project. Here's what I need:

1. Create a new folder: /Users/mog/my-automation-project
2. Create these files inside:
   - README.md (with title "My Automation Project")
   - main.py (with simple Python code)
   - .gitignore (ignore __pycache__ and .env)

3. Initialize a Git repository
4. Create a GitHub repository called "my-automation-project"
5. Add all files to git
6. Make initial commit with message "Initial commit"
7. Push to GitHub

My GitHub username is: mog
```

---

## How It Works: Complete Flow

```
You ask Claude in Claude Desktop
          ↓
Claude reads your local files (via Filesystem MCP)
          ↓
Claude understands your project structure
          ↓
Claude uses GitHub MCP to create repository
          ↓
Claude uses Filesystem MCP to initialize git repo
          ↓
Claude stages files and commits
          ↓
Claude pushes to GitHub using your token
          ↓
Files appear on GitHub.com 🎉
```

---

## Important Notes

### Security
- Your GitHub token is in the config file - **keep it private**
- Filesystem MCP can only access directories you listed
- Claude asks for permission before modifying files (usually)

### Common Issues

**Issue: "Permission denied" when creating directories**
```bash
# Make sure you have write permissions
ls -la /Users/mog/
```

**Issue: Filesystem tools not appearing**
- Restart Claude Desktop completely
- Check that paths are correct absolute paths (not relative)
- Verify JSON syntax

**Issue: Git is not found**
Claude might say "git not found". You need to:
```bash
git --version
```

If not installed, install from https://git-scm.com/

---

## Testing Step-by-Step

### Test 1: Filesystem Access
Ask Claude:
```
List all files and folders in /Users/mog/Desktop
```

Claude should show you the contents.

### Test 2: GitHub Access
Ask Claude:
```
List my GitHub repositories
```

Claude should show your repos.

### Test 3: Combined
Ask Claude:
```
Read the file at /Users/mog/Desktop/test.txt
Then create a GitHub repository called "test-repo"
```

If both work, you're ready! ✅

---

## Recommended Workflow for Your Projects

**For NEW projects:**
```
Ask Claude:
"Create a new project in /Users/mog/Projects called [project-name] with these files: [list files]
Then push to GitHub as [repo-name]"
```

**For EXISTING projects:**
```
Ask Claude:
"Push the project at /Users/mog/path/to/project to GitHub as [repo-name]"
```

**For UPDATES:**
```
Ask Claude:
"Update [filename] in /Users/mog/project with [changes]
Then commit and push with message: [commit message]"
```

---

## Next Steps

1. ✅ Update your config with both MCP servers
2. ✅ Restart Claude Desktop
3. ✅ Test with simple commands
4. ✅ Start automating your workflows!

Once this is working, Claude becomes your development assistant that can:
- Create projects
- Read and modify files
- Manage Git repositories
- Push to GitHub
- All from natural language! 🚀