# PureClaude

[中文文档](README_CN.md)

PureClaude is an optimized version of Claude Code that provides a more flexible interactive experience through dynamic system prompt modification.

## Features

- Automatic result caching to avoid redundant generation
- Fast text processing using Node.js
- Smart file update detection, regenerates only when necessary
- Removes certain restrictive prompts from the original version

## Installation & Usage

1. **Prerequisites**
   - Claude Code installed (`npm install -g @anthropic-ai/claude-code`)
   - Node.js installed

2. **Install PureClaude**
   ```bash
   # Copy script to executable path
   cp pureclaude /usr/local/bin/pureclaude
   chmod +x /usr/local/bin/pureclaude
   ```

3. **Usage**
   ```bash
   # Direct usage, syntax identical to claude-code
   pureclaude "help me write a function"
   
   # Enter interactive mode
   pureclaude
   ```

## How It Works

PureClaude will:
1. Check Claude Code installation path
2. Verify if `pure.js` exists and is up to date
3. Generate optimized `pure.js` from `cli.js` if needed
4. Execute the optimized version

## Notes

- First run requires generating `pure.js` file
- Automatically regenerates when Claude Code updates
- Maintains full compatibility with official Claude Code