# Memory System Skill - 记忆系统技能

## 概述
本文件定义了一个通用的记忆系统技能，可用于任何项目。当用户在新项目中提到此文件时，Claude应自动按照以下要求建立记忆系统。

## 使用方法
用户在新项目中说：
```
读取 /data/ypxia/github/GeomDrug/skill.md，按照要求建立记忆系统
```

---

## 记忆系统建立要求

### 1. 创建目录结构
在当前项目根目录下创建 `memory/` 文件夹：
```
memory/
├── INDEX.md              # 索引（每次必读）
├── README.md             # 使用说明
├── WORKFLOW.md           # 工作流程
├── experiments/          # 实验记录
├── configs/              # 配置信息
├── scripts/              # 常用脚本
└── notes/                # 笔记
```

### 2. 创建 CLAUDE.md 文件
在项目根目录创建 `CLAUDE.md`，添加以下规则：

```markdown
# CLAUDE.md - Project Rules

## 工作流程规则

### 1. 记忆系统（必须执行）
**用户消息以 `/m` 开头时，必须先读取记忆索引：**
\`\`\`bash
cat memory/INDEX.md
\`\`\`
然后根据任务关键词读取相关记忆文件。

**约定：用户在消息开头加 `/m` 表示需要记忆上下文。**

### 2. 关键词映射
根据项目内容定义关键词和记忆文件的映射关系。

### 3. 实验记录规则
**以下情况必须更新记忆文件：**
- 实验状态变化（开始、完成、失败）
- 发现重要结果或错误
- 配置或路径变更
- 用户要求记录

### 4. 工作习惯
- **中文对话**：使用中文交流
- **简洁直接**：回答简洁，直接解决问题
- **主动记录**：重要信息主动保存到memory
- **检查记忆**：用户使用 /m 时先检查相关记忆
```

### 3. 创建 INDEX.md 文件
在 `memory/INDEX.md` 中：
- 列出所有记忆文件
- 建立关键词映射表
- 说明使用方法

### 4. 创建快捷脚本
创建 `memory/scripts/workflow_check.sh`：
```bash
#!/bin/bash
# 工作流程检查脚本

echo "=========================================="
echo "  Memory System Check - 记忆系统检查"
echo "=========================================="

echo ""
echo "📁 Memory Directory Structure:"
ls -la memory/

echo ""
echo "📋 Memory Index:"
cat memory/INDEX.md

echo ""
echo "=========================================="
echo "  Check Complete - 检查完成"
echo "=========================================="
```

创建 `memory/scripts/quick_memory.sh`：
```bash
#!/bin/bash
# 快速记忆访问脚本

MEMORY_DIR="memory"

show_help() {
    echo "Usage: $0 [option]"
    echo ""
    echo "Options:"
    echo "  index     - 显示记忆索引"
    echo "  search    - 搜索记忆内容"
    echo "  list      - 列出所有记忆文件"
    echo "  help      - 显示此帮助"
}

case "$1" in
    index)
        cat "$MEMORY_DIR/INDEX.md"
        ;;
    search)
        grep -r "$2" "$MEMORY_DIR" --include="*.md" -l
        ;;
    list)
        find "$MEMORY_DIR" -name "*.md" -type f | sort
        ;;
    *)
        show_help
        ;;
esac
```

### 5. 记录项目信息
根据项目内容，创建相应的记忆文件：
- `experiments/` - 实验记录
- `configs/` - 配置信息（路径、环境等）
- `scripts/` - 常用命令
- `notes/` - 笔记（数据集、模型等）

---

## 用户约定

### 使用方法
用户在消息开头加 `/m` 表示需要记忆上下文：
```
/m 你的问题
```

### 示例
```
/m 检查训练状态
/m 之前的配置是什么
/m 继续上次的任务
```

### 工作流程
1. 用户发送以 `/m` 开头的消息
2. Claude读取 `memory/INDEX.md`
3. 根据关键词读取相关记忆文件
4. 结合记忆信息回答问题

---

## 注意事项
1. **通用性**：此skill适用于任何项目，不限于特定领域
2. **可扩展**：可根据项目需求添加更多记忆文件
3. **简洁性**：记忆文件应简洁，避免冗长
4. **及时更新**：重要信息及时保存到memory

---

## 版本信息
- **版本**: 1.0
- **创建日期**: 2026-05-28
- **作者**: Claude Code Assistant
