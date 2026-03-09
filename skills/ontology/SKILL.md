---
name: ontology
description: "本体构建技能。用于构建、管理、查询知识本体，建立概念之间的层次关系、属性定义、语义关联。适用于：知识管理、数据建模、智能推理、语义搜索。"
metadata: { "openclaw": { "emoji": "🕸️", "requires": {} } }
---

# 🕸️ 本体构建技能

## 📍 使用场景

✅ **使用此技能：**
- "构建一个知识体系"
- "定义概念之间的关系"
- "建立分类结构"
- "语义搜索"
- "智能推理"
- "数据建模"

---

## 🧠 核心概念

### 1. 本体 (Ontology)
对概念及其关系的形式化描述，包括：
- **类 (Class)**：概念的抽象（如：人、动物、食物）
- **属性 (Property)**：类的特性（如：年龄、颜色、产地）
- **关系 (Relation)**：概念之间的连接（如：属于、包含、相关）
- **实例 (Instance)**：类的具体对象（如：张三、猫、苹果）

### 2. 关系类型

| 关系 | 说明 | 示例 |
|------|------|------|
| **is-a** | 继承关系 | 猫 is-a 动物 |
| **has-a** | 拥有关系 | 车 has-a 轮子 |
| **part-of** | 组成关系 | 引擎 part-of 车 |
| **related-to** | 关联关系 | 学习 related-to 成长 |
| **located-at** | 位置关系 | 学校 located-at 城市 |

---

## 🏗️ 本体结构

### 层次结构

```
根节点
├─ 实体 (Entity)
│  ├─ 人 (Person)
│  │  ├─ 学生 (Student)
│  │  └─ 教师 (Teacher)
│  ├─ 组织 (Organization)
│  │  ├─ 公司 (Company)
│  │  └─ 学校 (School)
│  └─ 物体 (Object)
│     ├─ 设备 (Device)
│     └─ 工具 (Tool)
├─ 概念 (Concept)
│  ├─ 知识 (Knowledge)
│  ├─ 技能 (Skill)
│  └─ 价值观 (Value)
└─ 事件 (Event)
   ├─ 活动 (Activity)
   └─ 里程碑 (Milestone)
```

---

## 📝 本体定义格式

### JSON 格式

```json
{
  "classes": {
    "Person": {
      "properties": {
        "name": "string",
        "age": "number",
        "gender": "enum:Male|Female|Other"
      },
      "subclasses": ["Student", "Teacher"]
    },
    "Student": {
      "properties": {
        "school": "string",
        "grade": "number",
        "major": "string"
      },
      "superclass": "Person"
    }
  },
  "relations": {
    "studies_at": {
      "domain": "Student",
      "range": "School",
      "type": "functional"
    },
    "teaches": {
      "domain": "Teacher",
      "range": "Course",
      "type": "non-functional"
    }
  },
  "instances": {
    "student_001": {
      "class": "Student",
      "properties": {
        "name": "张三",
        "age": 20,
        "school": "武汉大学",
        "major": "计算机科学"
      }
    }
  }
}
```

---

## 🔍 查询方式

### 属性查询
- "张三的年龄是多少？" → 返回：20
- "计算机科学专业的学生有哪些？" → 返回：[学生列表]

### 关系查询
- "张三在哪个学校读书？" → 返回：武汉大学
- "谁教人工智能课程？" → 返回：[教师列表]

### 推理查询
- "张三是学生吗？" → 是（Student 的实例）
- "张三是人吗？" → 是（通过 is-a 继承）

---

## 🎯 应用场景

### 1. 知识管理
- 构建个人知识体系
- 整理工作相关概念
- 建立技能图谱
- 追踪学习进度

### 2. 数据建模
- 设计数据库架构
- 定义数据实体关系
- 优化数据结构
- 支持复杂查询

### 3. 智能推理
- 基于规则推理
- 关联知识发现
- 缺失信息补全
- 逻辑验证

### 4. 语义搜索
- 理解查询意图
- 返回相关概念
- 提供上下文
- 推荐关联内容

---

## 🔄 本体维护

### 更新流程
1. **发现新概念** → 添加到本体
2. **定义属性** → 描述概念特性
3. **建立关系** → 连接相关概念
4. **验证逻辑** → 确保一致性
5. **更新实例** → 添加具体对象

### 优化原则
- 保持层次清晰
- 避免过度嵌套
- 确保关系明确
- 定期清理冗余

---

## 💡 最佳实践

### 类命名
- 使用单数形式：`Person` 而非 `People`
- 使用大驼峰：`ComputerScience`
- 描述性强：`GraduateStudent` 而非 `Grad`

### 属性命名
- 使用小驼峰：`firstName`
- 描述性强：`dateOfBirth` 而非 `dob`
- 避免缩写：`phoneNumber` 而非 `phoneNo`

### 关系命名
- 使用动词短语：`studiesAt`、`worksFor`
- 明确方向：`hasParent` vs `isChildOf`
- 保持一致性

---

## 🌐 高级特性

### 多继承
一个类可以继承多个父类：
```
TeachingAssistant is-a Student
TeachingAssistant is-a Teacher
```

### 属性约束
- 必填属性：`required: true`
- 唯一属性：`unique: true`
- 值域限制：`range: [1, 100]`

### 推理规则
```
如果 X is-a Student 且 Y teaches Z 且 X studies Z
那么 Y 是 X 的老师
```

---

构建知识网络，连接智慧节点！🕸️✨