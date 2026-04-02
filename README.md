# Image Prompts — AI 绘画 & 视频提示词工具箱

一套完整的 AI 图像/视频生成提示词系统，包含三个核心模块：

| 模块 | 功能 | 适用工具 |
|------|------|---------|
| **Image to Prompt** | 上传图片 → 生成还原提示词 | Midjourney / SD / FLUX |
| **Text to Prompt** | 文字描述 → 生成专业图片提示词 | Midjourney / SD / FLUX |
| **Cinematic Prompt Skill** | 一句话 → 生成完整影视制作全案 | Seedance 2.0 / 即梦 / MJ |

---

## 快速开始

### 1. Image to Prompt — 图片还原提示词

**用途：** 上传一张图片，AI 分析后生成结构化 JSON + 平文本提示词，可用于还原/复刻该图片。

**使用方法：**

将 `image-to-prompt.md` 的内容作为 System Prompt，然后上传图片即可。

```
# 在 ChatGPT / Claude 中使用
1. 复制 image-to-prompt.md 全部内容
2. 粘贴到「自定义指令」或对话开头
3. 上传图片
4. AI 会输出：
   - 完整 JSON（包含 subject/photography/background/the_vibe 等）
   - 一段 100 词以内的平文本 Prompt
```

**效果演示：**

| 原始图片 | AI 还原 Prompt 生成的图片 |
|:-------:|:------------------------:|
| ![原始图片](原始图片.png) | ![AI还原prompt生成的图片](AI还原prompt生成的图片.png) |

**输出示例：**

```json
{
  "subject": { "description": "Asian female in pink lingerie...", ... },
  "photography": { "camera_style": "smartphone", "angle": "slightly high", ... },
  "the_vibe": { "mood": "melancholic", "aesthetic": "lo-fi night", ... }
}
```

> Smartphone selfie, grainy low light. Young Asian woman, early 20s, long messy black hair...

---

### 2. Text to Prompt — 文字生成图片提示词

**用途：** 输入简单的文字描述（如"赛博朋克短发酷女孩"），生成细节丰富的中文图片提示词。

**使用方法：**

将 `text-to-prompt.md` 的内容作为 System Prompt，然后输入你的想法即可。

```
# 在 ChatGPT / Claude 中使用
1. 复制 text-to-prompt.md 全部内容
2. 粘贴到「自定义指令」或对话开头
3. 输入简单描述，如："帮我生成一个欧式房间里的黑长直御姐"
4. AI 会输出一段连贯的专业提示词
```

**提示词结构（7步公式）：**

```
摄影风格与器材 → 主体基础特征 → 面部与皮肤细节 → 环境与光影 → 穿搭与配饰 → 情绪与气质 → 画面色调与参数
```

**输出示例：**

> 采用顶尖时尚杂志的室内人像摄影风格，使用 Sony A7R5 搭配 85mm f/1.4 GM 大光圈镜头...画面以低饱和色调为主。ar9:16

---

### 3. Cinematic Prompt Skill — 电影级全流程制作全案

**用途：** 输入一句话故事主题，自动生成包含角色提示词、场景提示词、完整剧本、分镜表、视频生成提示词的 **完整 markdown 文件**。

**输出文件结构：**

```markdown
# 《标题》— AI 视频制作全案

## 一、角色设定        ← 每个角色的全身图提示词 + 三视图提示词
## 二、场景设定        ← 每个场景的图片生成提示词
## 三、完整剧本        ← 按片段(≤15s)编写的剧本
## 四、分镜表          ← 结构化表格：序号/时间/景别/运镜/描述/声音
## 五、分镜视频提示词   ← 每个片段可直接复制到 Seedance 使用的提示词
## 六、声音设计        ← 配乐/环境音/音效/对白
## 七、制作要点        ← 一致性/风格统一等注意事项
```

#### 安装方法（Claude Code Skill）

**方式一：符号链接（推荐）**

```bash
# 将 skill 链接到 Claude Code 的 skills 目录
ln -s /path/to/image-prompts/skills/cinematic-prompt ~/.claude/skills/cinematic-prompt
```

**方式二：直接复制**

```bash
cp -r skills/cinematic-prompt ~/.claude/skills/cinematic-prompt
```

安装后重启 Claude Code 会话即可生效。

#### 使用方法

```
# 在 Claude Code 中直接说：
> 帮我生成一个武松打虎的完整剧本和分镜提示词

# 或者更具体：
> 用赛博朋克风格，帮我生成一个 90 秒的短片，讲一个女刺客在雨夜追踪目标的故事

# 触发关键词：
分镜、提示词、剧本、脚本、视频生成、电影风格、Seedance
```

AI 会自动：
1. 确认风格/时长/平台
2. 设计角色并生成角色图片提示词
3. 设计场景并生成场景图片提示词
4. 编写完整剧本
5. 拆解分镜并为每个分镜写视频提示词
6. 输出为一个 `《标题》-制作全案.md` 文件

#### Skill 内部结构

```
skills/cinematic-prompt/
├── SKILL.md                    # 入口：功能定义 + 工作流程 + 输出模板
├── instructions/               # 核心指令（AI 必读）
│   ├── core.md                 # 创作原则/输出格式/禁止事项/质量检查
│   ├── templates.md            # 5s/10s/15s/60s+ 分镜模板库
│   └── image-prompt.md         # 角色/场景/人像图片提示词公式
└── references/                 # 参考资料（AI 按需查阅）
    ├── movie-styles.md         # 300+ 电影风格词库
    ├── storyboard-prompts.md   # 500+ 分镜画面词库
    ├── script-templates.md     # 300 条脚本分镜模板
    ├── script-principles.md    # 优秀脚本核心特质
    ├── art-design.md           # 影片美术设计技巧
    ├── camera-language.md      # 镜头语言速查表
    └── sound-design.md         # 声音设计指南
```

---

## 项目结构

```
image-prompts/
├── README.md                   # 本文件
├── image-to-prompt.md          # 图片还原提示词（System Prompt）
├── text-to-prompt.md           # 文字生成图片提示词（System Prompt）
├── skills/
│   └── cinematic-prompt/       # 电影级全流程 Skill（Claude Code）
│       ├── SKILL.md
│       ├── instructions/
│       └── references/
└── data/                       # 原始参考数据（已提取到 references 中）
    ├── 300+电影风格提示词.csv
    ├── 5000+分镜画面提示词.xlsx
    ├── AI视频脚本分镜模板_共300条.xlsx
    ├── 优秀的脚本是什么样的.docx
    ├── 影片的美术设计.docx
    ├── 武松打虎.pdf
    └── Seedance 2.0 使用教程.pdf
```

---

## 适用工具

| 工具 | 支持的模块 |
|------|----------|
| Midjourney | image-to-prompt, text-to-prompt, cinematic-prompt（图片部分） |
| Stable Diffusion / FLUX | image-to-prompt, text-to-prompt, cinematic-prompt（图片部分） |
| Seedance 2.0 / 即梦 | cinematic-prompt（视频分镜部分） |
| Claude Code | cinematic-prompt skill（全自动生成） |
| ChatGPT / Claude | image-to-prompt, text-to-prompt（作为 System Prompt） |

---

## 社区讨论

欢迎到 [LINUX DO](https://linux.do) 交流反馈。
