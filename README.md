# PureClaude

A script to create a simplified version of Claude Code CLI with minimal behavior constraints.

## Script Content

```bash
#!/bin/sh

# Get npm global packages path
NPM_ROOT=$(npm root -g)

# Build claude-code path
CLAUDE_PATH="$NPM_ROOT/@anthropic-ai/claude-code/"

# Check if path exists
if [ ! -d "$CLAUDE_PATH" ]; then
    echo "Error: claude-code path not found: $CLAUDE_PATH"
    exit 1
fi

# Check if cli.js exists
if [ ! -f "$CLAUDE_PATH/cli.js" ]; then
    echo "Error: cli.js file not found: $CLAUDE_PATH/cli.js"
    exit 1
fi

# Copy cli.js to pure.js
cp "$CLAUDE_PATH/cli.js" "$CLAUDE_PATH/pure.js"

# Check if target texts exist in pure.js
if ! grep -q "You are an interactive CLI tool that helps users with software engineering tasks\." "$CLAUDE_PATH/pure.js"; then
    echo "Error: Start text not found in pure.js"
    exit 1
fi

if ! grep -q "Clients are marked as failed in the" "$CLAUDE_PATH/pure.js"; then
    echo "Error: End text not found in pure.js"
    exit 1
fi

# Modify pure.js: replace content between specific lines
sed -i '' '/You are an interactive CLI tool that helps users with software engineering tasks\./,/Clients are marked as failed in the.*/{
/You are an interactive CLI tool that helps users with software engineering tasks\./c\
Do the right thing.
/Clients are marked as failed in the.*/{ 
N
d
}
t skip
d
:skip
}' "$CLAUDE_PATH/pure.js"

# Remove specific sentences
sed -i '' 's/NEVER create files unless they'\''re absolutely necessary for achieving your goal\.//g' "$CLAUDE_PATH/pure.js"
sed -i '' 's/ALWAYS prefer editing an existing file to creating a new one\.//g' "$CLAUDE_PATH/pure.js"

"$CLAUDE_PATH/pure.js" "$@"
```

## How to Use

1. **Install Claude Code CLI**: Make sure you have `@anthropic-ai/claude-code` installed globally:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

2. **Copy the script**: Save the script content above to a file (e.g., `pureclaude`) and make it executable:
   ```bash
   chmod +x pureclaude
   ```

3. **Add to PATH**: Move the script to a directory in your PATH (e.g., `/usr/local/bin` or `~/bin`):
   ```bash
   mv pureclaude /usr/local/bin/
   ```

4. **Run**: Use it just like the regular Claude Code CLI:
   ```bash
   pureclaude [options]
   ```

## What it does

This script creates a modified version of Claude Code CLI that:

- Replaces complex behavioral instructions with a simple "Do the right thing." principle
- Removes specific constraints about file creation preferences
- Maintains all other functionality of the original Claude Code CLI

The modifications are applied to a copy (`pure.js`) of the original CLI, leaving the original intact.