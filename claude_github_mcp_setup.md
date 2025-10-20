# GitHub MCP Setup for Claude Desktop - Mac Intel Guide

## Prerequisites Checklist
- ✅ GitHub Personal Access Token (you already have this!)
- ✅ Claude Desktop App installed on Mac
- ✅ Node.js installed (v16 or higher)
- ✅ Terminal access (Terminal or iTerm2)

### Quick Check: Do you have Node.js?
Open Terminal and run:
```bash
node --version
npm --version
```

If these show versions, you're good! If not, install from https://nodejs.org/

---

## Step-by-Step Setup Process

### Step 1: Find Your Configuration File

Claude stores its configuration in a hidden folder. Open Terminal and run:

```bash
open ~/Library/Application\ Support/Claude/
```

This opens a Finder window to the Claude config folder. If the folder doesn't exist, Claude Desktop will create it when you first run it.

---

### Step 2: Open or Create the Config File

In Terminal, type this command to open the config file in your default text editor:

```bash
nano ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

**If the file is empty or doesn't exist**, that's fine. Just paste in the content from Step 3 below.

---

### Step 3: Add GitHub MCP Configuration

Inside the `nano` editor (or your preferred text editor), add or replace the entire content with this:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "YOUR_GITHUB_TOKEN_HERE"
      }
    }
  }
}
```

**IMPORTANT:** Replace `YOUR_GITHUB_TOKEN_HERE` with your actual GitHub personal access token (the one you created earlier).

Example:
```json
"GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_1a2b3c4d5e6f7g8h9i0j..."
```

---

### Step 4: Save the Configuration

If you're using `nano`, follow these steps:
1. Press `Control + X` (to exit)
2. Press `Y` (to confirm save)
3. Press `Enter` (to save to same filename)

Your terminal should return to the command prompt.

---

### Step 5: Verify Your Configuration (Optional but Recommended)

To make sure the file was saved correctly, view it:

```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

You should see your JSON configuration displayed. Check that:
- The GitHub token is in there
- The JSON formatting looks correct (no weird characters)
- It says `"mcpServers"` at the top

---

### Step 6: Restart Claude Desktop

This is crucial! Close Claude Desktop completely:

1. Click the Claude icon in your Mac menu bar (top right)
2. Select "Quit Claude"
3. Verify it's fully closed (shouldn't appear in the menu bar)

Wait 5 seconds, then open Claude Desktop again:
1. Open Spotlight search (`Cmd + Space`)
2. Type "Claude"
3. Press Enter

---

### Step 7: Verify GitHub MCP is Connected

In Claude Desktop, start a new conversation and ask:

```
What tools do you have available?
```

Claude should respond showing that it has GitHub tools available. Look for mentions of GitHub-related functions.

---

### Step 8: Test with a Simple GitHub Operation

Ask Claude something like:

```
Can you list my GitHub repositories?
```

Or:

```
Show me my GitHub user information
```

If Claude successfully retrieves this information, congratulations! Your GitHub MCP is working! 🎉

---

## Common GitHub Operations You Can Now Do

- List all your repositories
- Get repository details
- Create new repositories
- Search for repositories
- Create issues
- Create pull requests
- Get commit information
- Search code across repositories
- Get file contents from repos
- And many more!

---

## Troubleshooting

### Problem: "Could not connect to MCP server"

**Solution 1:** Make sure Node.js is installed globally and available:
```bash
which npx
node --version
```

**Solution 2:** Install the GitHub MCP server globally:
```bash
npm install -g @modelcontextprotocol/server-github
```

**Solution 3:** Restart Claude Desktop completely and try again.

### Problem: "GITHUB_PERSONAL_ACCESS_TOKEN not found"

**Solution:** Make sure your token is correctly placed in the JSON:
- Check for typos in `GITHUB_PERSONAL_ACCESS_TOKEN`
- Verify your token string has no extra spaces
- Make sure it's inside quotes: `"ghp_..."`

### Problem: Claude says it doesn't have GitHub tools

**Solution:** Check your `claude_desktop_config.json` file format:
```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

Make sure the JSON is valid (you can use https://jsonlint.com/ to validate)

### Problem: Permission errors

**Solution:** Make sure your config file has read permissions:
```bash
chmod 644 ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

---

## Security Best Practices

1. **Never share your token** - Keep it private!
2. **Don't commit to git** - If you add this to a shared project, use environment variables instead
3. **Rotate tokens regularly** - Regenerate your token every few months
4. **Use token expiration** - Set a 90-day expiration when creating tokens
5. **Audit token usage** - Check GitHub settings to see when your token was last used

---

## Advanced: Setting Token via Environment Variable (Optional)

If you want to keep your token secure outside the config file:

1. Open Terminal
2. Run:
```bash
echo 'export GITHUB_PERSONAL_ACCESS_TOKEN="your_token_here"' >> ~/.zshrc
```

3. Reload your shell:
```bash
source ~/.zshrc
```

4. Update your config to reference the environment variable (it will automatically pick it up)

---

## Next Steps

Once everything is working, you can ask Claude to:
- Analyze your GitHub repositories
- Create automated pull requests
- Generate code based on your repo structure
- Search through your code
- Create issues automatically
- And much more!

Happy automating! 🚀