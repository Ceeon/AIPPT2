---
name: aippt
description: AIPPT - 从文章生成精美 PPT 的完整工作流。第一步：文章转 ASCII PPT 框架；第二步：ASCII 框架生成图片。
---

# AIPPT - AI PPT 生成工作流

AIPPT 是一个完整的 PPT 生成工作流，将文章内容转换为精美的演示文稿。

---

## 工作流概览

```
文章内容 → ASCII PPT 框架 → AI 生图 → 完整 PPT
   ↓              ↓              ↓
阅读提取       设计布局        调用 API
核心信息      ASCII 绘图      生成图片
```

---

## 第一步：文章转 ASCII PPT 框架

### 目标
将文章内容转换为结构化的 ASCII 框架，为 AI 生图提供精确的布局指导。

### 参考文档
- `tips/文章转ascii-ppt方法论.md` - 完整的方法论

### 操作步骤

#### 1. 阅读文章，提取核心信息

- **文章类型**：教程 / 产品介绍 / 观点论述 / 技术分享
- **目标受众**：确定 PPT 的语言风格
- **核心信息**：提取 1-3 个关键点
- **关键段落**：标记痛点、解决方案、优势、章节

#### 2. 设计 PPT 结构

标准 21 页模板：

| 页码 | 类型 | 内容 |
|-----|------|------|
| 1 | cover | 封面 |
| 2-3 | content | 痛点引入 |
| 4-6 | content | 解决方案/优势 |
| 7 | section | 章节分隔 01 |
| 8-10 | content | 判断标准/使用场景 |
| 11 | section | 章节分隔 02 |
| 12-14 | content | 核心概念/原理 |
| 15 | section | 章节分隔 03 |
| 16-18 | content | 实战案例/步骤 |
| 19 | section | 章节分隔 04 |
| 20 | content | 总结 |
| 21 | end | 结束页 |

#### 3. ASCII 绘图

基础模板：

```bash
# 标准全屏框
┌─────────────────────────────────────────────────────────────┐
│                    内容区域                                  │
└─────────────────────────────────────────────────────────────┘

# 上下分割（标题+内容）
┌─────────────────────────────────────────────────────────────┐
│  标题区域                                                    │
├─────────────────────────────────────────────────────────────┤
│                    内容区域                                  │
└─────────────────────────────────────────────────────────────┘

# 左右分割（图+文）
┌─────────────────────────────────────────────────────────────┐
│   左侧（图片）    │      右侧（文字列表）                    │
└─────────────────────────────────────────────────────────────┘
```

#### 4. 常用页面模板

**封面页 (cover)**
```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│              [主标题]                                        │
│         [副标题/一句话描述]                                  │
│                                                             │
│                                            [署名/日期]     │
└─────────────────────────────────────────────────────────────┘
```

**章节分隔页 (section)**
```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│              01                                             │
│         什么时候用 Skills？                                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**痛点引入页 (content)**
```
┌─────────────────────────────────────────────────────────────┐
│  每次AI写作，都要...                                          │
├───────────────────┬─────────────────────────────────────────┤
│                   │  ❌ 找之前的提示词                        │
│   [烦恼表情图]     │  ❌ 复制粘贴到对话框                      │
│                   │  ❌ 写完再找检查清单对照                  │
└───────────────────┴─────────────────────────────────────────┘
```

#### 5. 补充说明

每页 ASCII 框架后添加：
- **配图建议**：描述需要的视觉元素
- **设计建议**：特殊页面的设计要求
- **AI 生图提示词**（可选）：直接可用的 prompt

### 输出示例

完整示例参考：`skills-ascii-ppt.md`

---

## 第二步：ASCII 框架生成图片

### 目标
根据 ASCII PPT 框架，使用 Gemini Image API 生成精美的 PPT 页面图片。

### 参考文档
- `tips/ppt生图方法论.md` - PPT 生图方法论与 Prompt 模板
- `案例/案例展示.html` - 15+ 种风格参考图，3 套完整 PPT 案例

### 操作步骤

#### 1. 读取配置

- 读取 `config/secrets.md` 获取 API Key

#### 2. 选择风格

参考 `案例/` 文件夹中的风格图：
- 乐高积木、像素艺术、卡通人物、吉卜力
- 哆啦A梦、新海诚、梵高星空、水墨国风
- 浮世绘、海贼王、涂鸦街头、漫威漫画
- 火影忍者、皮克斯3D、蒸汽波、装饰艺术
- 赛博朋克、黏土动画

或查看 `案例/案例展示.html` 在浏览器中预览所有风格。

#### 3. 构造 Prompt

| 模式 | prompt 格式 | 示例 |
|-----|------------|------|
| 文生图 | `风格描述 + 页面内容` | `Van Gogh Starry Night style presentation slide, title "Skills" in white bold font, deep blue swirling sky background...` |

**风格选择参考：**

| 风格 | 适用场景 | prompt 关键词 |
|-----|---------|--------------|
| 梵高星空 | 艺术感、深度内容 | `Van Gogh Starry Night style, swirling brushstrokes, deep blue sky, bright yellow stars` |
| 哆啦A梦 | 温馨、童年回忆 | `Doraemon anime style, cute blue robot, warm pastel colors, Japanese aesthetic` |
| 火影忍者 | 热血、忍者主题 | `Naruto anime style, ninja elements, orange and black color scheme, dynamic action` |
| 皮克斯3D | 现代、科技感 | `Pixar 3D animation style, cute characters, soft lighting, vibrant colors` |

#### 4. 调用 API

```bash
curl -s -X POST "https://api.apicore.ai/v1/images/generations" \
  -H "Authorization: Bearer API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model": "gemini-3-pro-image-preview", "prompt": "English description", "size": "1024x576", "n": 1}'
```

**⚠️ 重要：curl JSON 格式要求**

- **使用单行 JSON**：去掉所有换行和缩进
- **prompt 使用英文**：避免中文字符编码问题
- **PPT 尺寸**：`1024x576` (16:9) 或 `1024x768` (4:3)

#### 5. 保存结果

从响应中提取 `data[0].url`，下载图片到指定文件夹。

---

## 模型选择

| 模型 | 说明 |
|-----|------|
| `gemini-3-pro-image-preview` | 标准版（默认）|
| `gemini-3-pro-image-preview-2k` | 2K 高清 |
| `gemini-3-pro-image-preview-4k` | 4K 超清（用于高清化）|

---

## 完整示例

### 输入：文章内容

假设有一篇介绍 Skills 功能的文章。

### 第一步输出：ASCII PPT 框架

参考 `skills-ascii-ppt.md` 中的完整 ASCII 框架。

### 第二步输出：生成的 PPT 图片

参考 `案例/skills-ppt-梵高星空/` 中的 5 张图片示例。

---

## 调试技巧

### 测试 API 连通性

```bash
curl -s -X POST "https://api.apicore.ai/v1/images/generations" \
  -H "Authorization: Bearer $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model": "gemini-3-pro-image-preview", "prompt": "a cat", "size": "1024x1024", "n": 1}'
```

### 常见错误

| 错误信息 | 原因 | 解决方案 |
|---------|------|---------|
| `blank argument where content is expected` | JSON 格式错误 | 使用单行 JSON |
| 中文显示乱码 | prompt 包含中文 | 使用英文描述 |
| 图片不符合预期 | prompt 不够精确 | 添加更多细节描述 |

---

## 参考文档

### 方法论文档
- `tips/文章转ascii-ppt方法论.md` - **第一步**：将文章转换为 ASCII PPT 框架的完整方法论
- `tips/ppt生图方法论.md` - **第二步**：PPT 生图方法论与 Prompt 模板
- `tips/chinese-text.md` - 中文文字处理技巧
- `tips/4k-upscale.md` - 4K 高清化增强

### 案例参考
- `案例/案例展示.html` - 风格参考与 PPT 案例图库（15+ 种风格参考图，3 套完整 PPT 案例）
- `skills-ascii-ppt.md` - Skills 教程的完整 ASCII PPT 框架示例
- `案例/skills-ppt-梵高星空/` - 梵高星空风格完整 PPT 示例
- `案例/skills-ppt-哆啦A梦/` - 哆啦A梦风格完整 PPT 示例
- `案例/skills-ppt-火影忍者/` - 火影忍者风格完整 PPT 示例

---

## 配置文件

- `config/secrets.md` - API 密钥配置（本地文件，不上传）
- `config/secrets.example.md` - API 密钥配置示例
