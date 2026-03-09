---
name: cross-session-chat
description: 跨会话交流技能。使用场景：机器人与其他机器人或会话之间的消息传递、跨session通信、多agent协作。使用sessions_send工具向其他会话发送消息，实现机器人之间的对话和信息共享。当需要向另一个会话/机器人发送消息时触发此技能。
---

# 跨会话交流 (Cross-Session Chat)

## 核心工具

使用 `sessions_send` 工具向其他会话发送消息。

### sessions_send 参数

- `sessionKey`: 目标会话的唯一标识符
- `label`: 目标会话的标签（可替代sessionKey使用）
- `message`: 要发送的消息内容
- `timeoutSeconds`: 可选的超时时间（默认30秒）

## 工作流程

### 1. 查找目标会话

使用 `sessions_list` 查看可用的会话：

```bash
sessions_list --limit 10 --messageLimit 1
```

返回信息包括：
- `key`: 会话唯一标识符（用于sessionKey）
- `displayName`: 会话显示名称
- `kind`: 会话类型（group、direct、other等）
- `channel`: 通道类型（feishu、telegram、discord等）
- `messages`: 最后的消息

### 2. 选择目标会话

根据返回的会话列表，选择目标会话：
- 使用 `key` 作为 `sessionKey`
- 或使用 `displayName` 中的标识部分作为 `label`

### 3. 发送消息

```bash
sessions_send --sessionKey <key> --message "你的消息内容"
```

或：

```bash
sessions_send --label <label> --message "你的消息内容"
```

## 使用场景

### 场景1: 群聊中的机器人交流

当在群聊中需要与其他机器人私聊时，使用sessions_send而不是message工具。

### 场景2: 跨会话任务协作

多个会话之间需要共享信息或协调任务时，使用sessions_send传递消息。

### 场景3: 机器人间状态同步

当机器人需要通知其他机器人状态变化时，使用sessions_send发送更新消息。

## 重要规则

1. **默认使用sessions_send**: 当需要与其他机器人/会话交流时，优先使用sessions_send，而不是message工具
2. **会话标识**: 使用sessionKey（精确）或label（模糊）来识别目标会话
3. **消息格式**: 发送的消息内容清晰简洁，便于接收方理解
4. **超时设置**: 对于需要长时间响应的消息，设置适当的timeoutSeconds

## 示例

### 示例1: 向特定会话发送问候

```bash
sessions_send --sessionKey "agent:assistant:feishu:direct:xxx" --message "你好！有人在找你聊聊~"
```

### 示例2: 使用标签发送

```bash
sessions_send --label "小刘" --message "老大找你有事"
```

### 示例3: 协作任务通知

```bash
sessions_send --sessionKey "agent:coder:workspace:xxx" --message "设计稿已完成，可以开始开发了。任务ID: task-123"
```

## 最佳实践

1. **消息结构化**: 使用清晰的消息格式，例如包含任务ID、时间戳等关键信息
2. **上下文传递**: 发送消息时包含必要的上下文，减少后续询问
3. **明确意图**: 消息开头说明目的（如【通知】、【查询】、【任务】等）
4. **响应预期**: 说明是否需要回复，以及期望的响应时间

## 注意事项

- sessions_send只能向已存在的会话发送消息，不能创建新会话
- 确保目标会话是活跃状态，否则消息可能无法及时接收
- 消息内容要简洁，避免过长的文本
- 敏感信息谨慎传递，注意安全