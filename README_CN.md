# PureClaude

[English Documentation](README.md)

PureClaude 是 Claude Code 的优化版本，去掉了原版中冗长无用、偏执的提示词，修改之后更听话、更节省token。


## 安装使用

1. **前置要求**
   - 已安装 Claude Code (`npm install -g @anthropic-ai/claude-code`)
   - 已安装 Node.js

2. **安装 PureClaude**
   ```bash
   # 复制脚本到可执行路径
   cp pureclaude /usr/local/bin/pureclaude
   chmod +x /usr/local/bin/pureclaude
   ```

3. **使用方法**
   ```bash   
   # 进入交互模式
   pureclaude
   ```

## 工作原理

PureClaude 会：
1. 检查 Claude Code 的安装路径
2. 验证 `pure.js` 是否存在且为最新版本
3. 如果需要，则从 `cli.js` 生成优化版本的 `pure.js`
4. 执行优化后的版本

## 注意事项

- 首次运行时需要生成 `pure.js` 文件
- 当 Claude Code 更新时会自动重新生成
- 保持与官方 Claude Code 的完全兼容性