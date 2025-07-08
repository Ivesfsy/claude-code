# Claude Code 快速入门指南

欢迎使用Claude Code！这个强大的AI编程助手能够帮助您提高编程效率，自动化开发任务。


# 1. 安装与配置

## 1.1 系统要求
- **操作系统**: macOS 10.15+, Ubuntu 20.04+/Debian 10+, 或 Windows via WSL
- **硬件**: 4GB+ RAM
- **软件**: Node.js 18+
- **网络**: 需要互联网连接进行身份验证和AI处理

## 1.2 安装步骤

使用npm进行全局安装：

```bash
npm install -g @anthropic-ai/claude-code
```

**重要**: 不要使用 `sudo npm install -g`，这可能导致权限问题和安全风险。

安装完成后，导航到您的项目目录并启动Claude Code：

```bash
cd your-awesome-project
claude
```


# 2. API密钥获取与配置

## 2.1 注册账户

1. 访问 https://coultra.blueshirtmap.com/
2. 点击注册按钮创建新账户
3. 填写必要的注册信息

![注册](https://github.com/user-attachments/assets/8f5636c5-a17e-4fd9-9bb2-b2de1b73899d)

## 2.2 创建API密钥

1. 登录成功后，进入API密钥管理页面
2. 创建一个新的API密钥分组
3. 选择"ClaudeCode"作为分组名称
4. 生成并复制您的API密钥

![创建令牌](https://github.com/user-attachments/assets/5b775385-12f9-414d-8d82-c60d263b8f24)

## 2.3 认证选项

Claude Code提供以下认证选项：

1. **Anthropic Console**: 默认选项，通过Anthropic Console连接并完成OAuth流程
2. **Claude App (Pro或Max计划)**: 订阅Claude的Pro或Max计划，获得统一的订阅体验
3. **企业平台**: 配置Claude Code使用Amazon Bedrock或Google Vertex AI


# 3. 配置文件设置

## 3.1 API密钥配置

### 配置文件设置方法
创建或编辑配置文件：
```bash
# 用户设置 (全局)
~/.claude/settings.json

# 项目设置 (项目级)
.claude/settings.json
```

配置文件示例：
```json
{
    "env": {
      "ANTHROPIC_API_KEY": "您的APIkey",
      "ANTHROPIC_BASE_URL": "https://coultra.blueshirtmap.com",
      "CLAUDE_CODE_MAX_OUTPUT_TOKENS":64000,
      "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC":1,
      "CLAUDE_MODEL": "Claude模型名称"
    },
    "permissions": {
      "allow": [],
      "deny": []
    }
  }
```

## 3.2 权限设置（可选）

Claude Code采用保守的权限策略，默认需要用户确认可能修改系统的操作。您可以自定义允许的工具列表：

- 使用 `/permissions` 命令添加或移除工具
- 编辑 `settings.json` 文件进行批量配置
- 使用 `--allowedTools` CLI标志设置会话特定权限

## 3.3 工作目录配置（可选）

配置Claude可以访问的附加工作目录：

```json
{
  "permissions": {
    "additionalDirectories": ["../docs/", "../shared/"]
  }
}
```


# 4. 基础使用

## 4.1 启动方式

### 交互式模式
```bash
claude
```
![claude进入](https://github.com/user-attachments/assets/9673575e-2f7a-4711-a421-2f28d7629f6a)

### 带初始提示启动
```bash
claude "explain this project"
```

### 非交互式模式
```bash
claude -p "explain this function"
```

### 处理管道输入
```bash
cat logs.txt | claude -p "explain"
```

## 4.2 常用命令

- `claude update` - 更新到最新版本
- `claude -c` - 继续最近的对话
- `claude -r <session-id>` - 恢复特定会话
- `claude mcp` - 配置MCP服务器

## 4.3 快捷键

### 通用控制
- `Ctrl+C`: 取消当前输入或生成
- `Ctrl+D`: 退出Claude Code会话
- `Ctrl+L`: 清除终端屏幕
- `Up/Down`: 浏览命令历史
- `Esc + Esc`: 编辑上一条消息

### 多行输入
- `\ + Enter`: 适用于所有终端
- `Option+Enter`: macOS默认
- `Shift+Enter`: 执行`/terminal-setup`后可用


# 5. 高级功能

## 5.1 CLI参考

Claude Code提供丰富的命令行选项来自定义其行为：

### 基础CLI命令

| 命令 | 描述 | 示例 |
|------|------|------|
| `claude` | 启动交互式REPL | `claude` |
| `claude "query"` | 带初始提示启动REPL | `claude "explain this project"` |
| `claude -p "query"` | 通过SDK查询后退出 | `claude -p "explain this function"` |
| `claude -c` | 继续最近的对话 | `claude -c` |
| `claude update` | 更新到最新版本 | `claude update` |

### 重要CLI标志

| 标志 | 描述 | 示例 |
|------|------|------|
| `--allowedTools` | 允许的工具列表 | `--allowedTools "Bash(git log:*)" "Read"` |
| `--verbose` | 启用详细日志 | `claude --verbose` |
| `--model` | 设置使用的模型 | `claude --model claude-sonnet-4` |
| `--permission-mode` | 指定权限模式 | `claude --permission-mode plan` |
| `--dangerously-skip-permissions` | 跳过权限提示（谨慎使用） | `claude --dangerously-skip-permissions` |

## 5.2 交互式模式

### Vim模式
启用vim风格编辑：
```bash
/vim
```

#### 模式切换
- `Esc`: 进入NORMAL模式
- `i`: 在光标前插入
- `a`: 在光标后插入
- `o`: 在下方新建行

#### 导航（NORMAL模式）
- `h/j/k/l`: 左/下/上/右移动
- `w`: 下一个单词
- `0`: 行首
- `$`: 行尾
- `gg`: 文本开头
- `G`: 文本结尾

## 5.3 斜杠命令

Claude Code提供多种斜杠命令来增强交互体验：

### 基础命令

| 命令 | 描述 | 示例 |
|------|------|------|
| `/help` | 显示帮助信息 | `/help` |
| `/clear` | 清除对话历史 | `/clear` |
| `/config` | 管理配置 | `/config` |
| `/permissions` | 管理权限 | `/permissions` |
| `/vim` | 启用vim模式 | `/vim` |

### 高级命令

| 命令 | 描述 | 功能 |
|------|------|------|
| `/init` | 初始化项目 | 自动生成CLAUDE.md文件 |
| `/terminal-setup` | 设置终端 | 配置键盘快捷键 |
| `/project:<command>` | 项目特定命令 | 运行项目自定义命令 |

### 自定义斜杠命令

您可以创建自定义斜杠命令：

1. 在 `.claude/commands/` 目录创建Markdown文件
2. 文件名即为命令名
3. 内容为命令模板，可使用 `$ARGUMENTS` 占位符

示例：`.claude/commands/fix-github-issue.md`
```markdown
请分析并修复GitHub issue: $ARGUMENTS。

请按以下步骤操作：
1. 使用 `gh issue view` 获取issue详情
2. 理解问题描述
3. 搜索相关代码文件
4. 实现必要的修复
5. 编写并运行测试
6. 确保代码通过lint检查
7. 创建描述性的提交信息
8. 推送并创建PR
```


# 6. 实战教程

## 6.1 理解新代码库

### 快速了解代码库概况

如果你刚加入一个新项目，想要快速了解其结构，你可以按照以下步骤进行：

1. 进入项目根目录：`cd /path/to/project`
2. 启动 Claude Code：`claude`
3. 请求代码库的概况：`> 给我一个代码库概览`
4. 深入了解特定组件：
   - `> 解释这里使用的主要架构模式`
   - `> 关键的数据模型有哪些？`
   - `> 认证是如何处理的？`

**小技巧：**
- 从广泛的问题入手，然后逐步聚焦到具体领域
- 询问项目中使用的编码约定和模式
- 请求项目特定术语的词汇表

### 查找相关代码

当你需要定位与某个功能相关的代码时，可以按如下方式操作：

1. 请求 Claude 查找相关文件：`> 查找处理用户认证的文件`
2. 获取组件交互的上下文：`> 这些认证文件是如何协同工作的？`
3. 了解执行流程：`> 从前端到数据库，跟踪登录过程`

**小技巧：**
- 明确你想要查找的内容
- 使用项目中领域特有的语言

## 6.2 高效修复Bug

### 诊断错误消息

遇到错误时，你可以通过以下方法找出并修复问题：

1. 与 Claude 分享错误消息：`> 我在运行 npm test 时看到错误`
2. 请求修复建议：`> 提供一些修复 user.ts 中 @ts-ignore 的方法`
3. 应用修复：`> 更新 user.ts，添加你建议的 null 检查`

**小技巧：**
- 告诉 Claude 用于重现问题的命令，并提供堆栈跟踪
- 提及任何重现错误的步骤
- 说明错误是间歇性的还是一致性的

## 6.3 代码重构

### 现代化旧代码

当需要更新旧代码，采用现代的编程模式时，可以按照以下步骤进行：

1. 识别要重构的旧代码：`> 查找我们代码库中弃用的 API`
2. 请求重构建议：`> 建议如何重构 utils.js，使用现代 JavaScript 特性`
3. 安全地应用更改：`> 重构 utils.js，使用 ES2024 特性，同时保持原有行为`
4. 验证重构：`> 对重构后的代码运行测试`

**小技巧：**
- 向 Claude 询问现代方法的好处
- 要求在需要时保持向后兼容性
- 进行小步、可测试的增量式重构

## 6.4 处理测试

### 添加测试覆盖率

若需要为未覆盖的代码添加测试，可以按如下步骤进行：

1. 识别未经测试的代码：`> 查找 NotificationsService.swift 中未覆盖的函数`
2. 生成测试框架：`> 为通知服务添加测试`
3. 添加有意义的测试用例：`> 为通知服务中的边缘情况添加测试用例`
4. 运行并验证测试：`> 运行新测试，修复任何失败`

**小技巧：**
- 要求覆盖边缘情况和错误条件的测试
- 根据需要请求单元测试和集成测试
- 请 Claude 解释测试策略

## 6.5 创建Pull Request

### 生成全面的PR

当你需要为你的更改创建一个文档清晰的 pull request 时，按以下步骤操作：

1. 总结你的更改：`> 总结我对认证模块所做的更改`
2. 使用 Claude 生成 PR：`> 创建一个 PR`
3. 审查并完善描述：`> 增强 PR 描述，补充有关安全性改进的更多信息`
4. 添加测试信息：`> 添加关于如何测试这些更改的信息`

**小技巧：**
- 直接要求 Claude 为你创建一个 PR
- 提交前审查 Claude 生成的 PR
- 要求 Claude 突出潜在的风险或注意事项

## 6.6 处理文档

### 生成代码文档

如果你需要添加或更新代码文档，可以按照以下步骤操作：

1. 识别没有适当 JSDoc 注释的代码：`> 查找 auth 模块中没有适当 JSDoc 注释的函数`
2. 生成文档：`> 为 auth.js 中未注释的函数添加 JSDoc 注释`
3. 审查和增强文档：`> 改进生成的文档，增加更多上下文和示例`
4. 验证文档：`> 检查文档是否符合我们项目的标准`

**小技巧：**
- 指定你所需的文档风格（如 JSDoc、docstrings 等）
- 在文档中要求提供示例
- 为公共 API、接口和复杂逻辑请求文档

## 6.7 使用图像

### 分析图像和屏幕截图

如果你需要在代码库中使用图像或让 Claude 分析图像内容，按照以下步骤进行：

1. 将图像添加到对话中：
   - 将图像拖入 Claude Code 窗口
   - 复制并粘贴图像至 CLI (ctrl+v)
   - 提供图像路径：`> 分析此图像：/path/to/your/image.png`

2. 请求 Claude 分析图像：
   - `> 这张图显示了什么？`
   - `> 描述一下这张截图中的 UI 元素`
   - `> 这个图表中有什么问题吗？`

3. 使用图像获取上下文：
   - `> 这是错误的截图，是什么导致了它？`
   - `> 这是当前的数据库架构，我们需要如何修改以支持新特性？`

4. 从图像中获取代码建议：
   - `> 生成与这个设计草图匹配的 CSS`
   - `> 用什么 HTML 结构可以重建这个组件？`

**小技巧：**
- 当文本描述不清晰或繁琐时，可以使用图像
- 提供错误、UI 设计或图表的截图，以便获得更好的上下文
- 可以在对话中使用多个图像

## 6.8 设置项目记忆

### 创建有效的CLAUDE.md文件

为了存储重要的项目信息、约定和常用命令，你可以设置一个 CLAUDE.md 文件：

为你的代码库初始化 CLAUDE.md 文件：`> /init`

**小技巧：**
- 包括常用命令（如构建、测试、检查）以避免重复搜索
- 记录代码风格偏好和命名约定
- 添加特定于项目的重要架构模式

你可以将 CLAUDE.md 文件添加到你运行 Claude 的文件夹、父目录（Claude 会自动读取这些文件）或子目录（Claude 会按需拉取这些文件）。

## 6.9 Unix风格实用程序

### 添加到验证过程

将 Claude 添加到你的构建脚本：

```json
// package.json
{
  ...
  "scripts": {
    ...
    "lint:claude": "claude -p '你是一个代码检查工具，请查看与主分支的差异，并报告任何与拼写错误相关的问题。每个问题的文件名和行号要在一行上，描述在第二行。不要返回任何其他文字。'"
  }
}
```

### 管道输入输出

通过 Claude 管道传输数据：
```bash
cat build-error.txt | claude -p '简明扼要地解释这个构建错误的根本原因' > output.txt
```

## 6.10 MCP服务器配置

### 配置MCP服务器

如果你想通过将 Claude 连接到专用工具和外部服务器来增强其功能，请按以下步骤操作：

1. 添加 MCP Stdio 服务器：
   - 基本语法：`claude mcp add <name> <command> [args...]`
   - 示例：添加本地服务器：`claude mcp add my-server -e API_KEY=123 -- /path/to/server arg1 arg2`

2. 管理 MCP 服务器：
   - 列出所有配置的服务器：`claude mcp list`
   - 获取特定服务器的详细信息：`claude mcp get my-server`
   - 删除服务器：`claude mcp remove my-server`

**小技巧：**
- 使用 `-s` 或 `--scope` 标志与 `project`（默认）或 `global` 一起指定配置的存储位置
- 使用 `-e` 或 `--env` 标志设置环境变量（例如，`-e KEY=value`）
- MCP 遵循客户端-服务器架构，Claude Code（客户端）可以连接到多个专用服务器

### 连接到Postgres MCP服务器

如果你希望 Claude 具有只读权限来查询 PostgreSQL 数据库和检查架构，按照以下步骤操作：

1. 添加 Postgres MCP 服务器：
```bash
   claude mcp add postgres-server /path/to/postgres-mcp-server --connection-string "postgresql://user:pass@localhost:5432/mydb"
   ```

2. 使用 Claude 查询数据库：
   - `> 描述一下我们用户表的架构`
   - `> 系统中最新的订单有哪些？`
   - `> 展示客户和发票之间的关系`

**小技巧：**
- Postgres MCP 服务器提供只读访问，确保安全
- Claude 可以帮助你探索数据库结构并运行分析查询
- 使用它可以快速了解不熟悉项目中的数据库架构
- 确保你的连接字符串使用具有所需最低权限的凭据


# 7. 进阶特性

## 7.1 IDE集成

Claude Code 支持连接到主流IDE：
- 您可以直接在IDE中看到Claude Code的改动，在IDE中与其交互
- Claude Code 现在支持 VSCode 与 JetBrains
- 如果您使用Linux / MacOS，您可以直接使用该插件
  - 如果您使用VSCode，在VSCode的内置终端唤起Claude Code，插件将被自动安装
  - 如果您使用JetBrains，您需要通过此链接下载：Claude Code [Beta] - IntelliJ IDEs Plugin
- 您可能需要手动指定IDE或检查IDE连接，通过以下命令测试：`> /ide`
- 如果您使用 VSCode+WSL，请您提前在VSCode 插件商店安装 WSL 插件
- 对于更多的用法，您可以参考Claude Code的官方文档

## 7.2 模型切换和配置

Claude Code 支持 Claude 4 Opus 与 Claude 4 Sonnet 灵活切换：
- 我们强烈推荐您使用Claude 4 Sonnet，其使用体验与Claude 4 Opus没有明显差别，但计费倍率仅为1/5
- 我们为您默认选择了Claude 4 Sonnet，您可以在登录后在配置中修改这一选项
- 如果您没有在站点中关闭"强制使用 Sonnet"，您在/model中切换的模型不会被切换
- 在 Claude Code 中使用此命令切换模型：`> /model`

## 7.3 上下文管理

Claude Code 支持压缩上下文以节省点数：
- Claude Code 通常会有长上下文，我们建议您使用以下斜杠命令来压缩以节省点数，较长的上下文往往需要更多点数
- `/compact [您的描述]`

## 7.4 对话恢复

Claude Code 能够恢复以前的对话：
- 使用以下命令可以恢复您上次的对话：`claude --continue`
- 这会立即恢复您最近的对话，无需任何提示
- 您如果需要显示时间，可以输入此命令：`claude --resume`
- 这会显示一个交互式对话选择器，显示：
  - 对话开始时间
  - 初始提示或对话摘要
  - 消息数量
- 使用箭头键导航并按Enter选择对话，您可以使用这个方法选择上下文

## 7.5 图像处理

Claude Code 可以处理图像信息：
- 您可以使用以下任何方法：
  - 将图像拖放到Claude Code窗口中（在MacOS上）
  - 复制图像并使用Ctrl+v粘贴到CLI中（在MacOS上）
  - 提供图像路径：`> 分析这个图像：/path/to/your/image.png`
- 您可以完全使用自然语言要求他进行工作，如：
  - `> 这是错误的截图。是什么导致了它？`
  - `> 这个图像显示了什么？`
  - `> 描述这个截图中的UI元素`
  - `> 生成CSS以匹配这个设计模型`
  - `> 什么HTML结构可以重新创建这个组件？`

## 7.6 深入思考

Claude Code 支持深入思考：
- 您需要通过自然语言要求其进行深入思考
- `> 我需要使用OAuth2为我们的API实现一个新的身份验证系统。深入思考在我们的代码库中实现这一点的最佳方法。`
- `> 思考这种方法中潜在的安全漏洞`
- `> 更深入地思考我们应该处理的边缘情况`
- 推荐您在使用复杂问题的时候使用这一功能，这也会消耗大量的额度点数

## 7.7 Git高级操作

Claude Code 支持使用自然语言操作Git，如：
- `> 提交我的更改`
- `> 创建一个 pr`
- `> 哪个提交在去年十二月添加了 markdown 测试？`
- `> 在 main 分支上变基并解决任何合并冲突`

### 使用Git工作树

您可以使用工作树创建隔离的编码环境：
- 如果您需要同时处理多个任务，并在Claude Code实例之间完全隔离代码，您可以使用此功能
- Git工作树允许您从同一存储库中检出多个分支到单独的目录。每个工作树都有自己的工作目录，文件是隔离的，同时共享相同的Git历史
- 创建新工作树：
```bash
  # 创建带有新分支的工作树
  git worktree add ../project-feature-a -b feature-a
  
  # 或使用现有分支创建工作树
  git worktree add ../project-bugfix bugfix-123
  ```
- 在每个工作树中运行Claude Code：
```bash
  # 导航到您的工作树
  cd ../project-feature-a
  
  # 在这个隔离环境中运行Claude Code
  claude
  ```

## 7.8 其他高级功能

Claude Code 支持多种高级功能：
- Claude Code可以被用作类Unix工具
- Claude Code支持自定义斜杠指令
- Claude Code支持使用$ARGUMENTS添加命令参数
- Claude Code支持高级设置配置
- Claude Code支持GitHub Actions集成
- Claude Code支持SDK开发
- Claude Code支持模型上下文协议（MCP）


# 8. 常见问题解决

## 8.1 存储记忆问题

### Claude Code如何存储记忆？
Claude Code 将记忆存储在`~/.claude`中，如果没有特殊要求，请不要删除此目录。

## 8.2 模型名称问题

### 为什么偶尔回复错误的模型名称？
TryAllAI 向您承诺不会替换您请求的模型，绝不掺杂其他模型。这是由于Claude Code在使用简单任务时，不会使用Claude 4 系列模型。

## 8.3 命令行错误

### 命令行参数执行错误怎么办？
此类问题在WSL上常见，是Agent自身的错误。我们推荐您使用MacOS/Ubuntu，这类环境往往问题较少。

## 8.4 清理Claude Code

### 如何彻底清理Claude Code？
您可以执行以下命令清理Claude Code的登录信息：
```bash
rm ~/.claude* -rf
```

## 8.5 API错误

### 遇到API Error、Tools Error怎么办？
这通常是网络问题，请您退出后使用`claude -c`重新执行。如果问题依然存在，请联系售后支持。

## 8.6 OAuth验证错误

### OAuth验证错误的解决方案
- 请您确保环境变量中没有配置任何代理再进行登录验证
- 如果问题仍然存在，请您无视弹出的浏览器并复制终端中的链接并打开，通过验证码方式验证

## 8.7 响应超时问题

### 长时间没有响应怎么办？
- 我们建议您按下ctrl+c并重启Claude Code，这往往是网络问题
- 如果命令行仍然无响应，我们建议您杀死进程并重新进行会话，这将不会影响您的工作进度
- 您可以通过以下命令恢复上次的会话：`claude -c`


# 9. 结语

Claude Code是一个强大的AI编程助手，通过合理的配置和使用，可以显著提高您的开发效率。建议您：

1. 从基础功能开始，逐步探索高级特性
2. 根据项目需求定制配置
3. 利用CLAUDE.md文件记录项目特定信息
4. 合理使用权限管理确保安全
5. 探索MCP和自定义命令扩展功能

祝您使用愉快！如有问题，请参考官方文档或社区支持。
