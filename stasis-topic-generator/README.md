# stasis-topic-generator

用**争点理论（Stasis）**给公众号找选题的 Claude Skill。

> English: A Claude Skill that applies stasis theory (fact / definition / quality / procedure) to turn a topic or a piece of AI news into discussion-worthy, fact-checked article angles for WeChat Official Accounts.

## 它做什么

给它一个话题，或一条 AI 资讯，它会：

1. 拆开事实、观点和待核实信息，涉及当前事实时先联网核实
2. 找到真正的矛盾，压成一个读者能站队的问题
3. 按**事实、定义、性质、程序**四层逐层找争点，淘汰换皮和空话选题
4. 评估这个选题和哪几类读者真实相关，只保留真实的关联
5. 推荐 3 个选题，每个都带标题、争点、开头和读者原本的想法

选出方向后可以继续**深挖**：检验概念与反例、构造最强反方、换一种解释、找前人解法、规划系列文章，最后给出"立即写 / 修改后写 / 暂缓 / 放弃"的决策。

## 设计原则

- **找真争点，不凑数量。** 找不到就直说没有，不硬造矛盾。
- **事实优先。** 区分已验证事实、厂商宣称和单方指控，涉及当前事实先搜索核实，不编造数据和案例。
- **关联必须真实。** 靠夸大的"和你有关"换来的点击，会消耗账号的信任。
- **他人内容只当素材。** 拆成事实、问题、观点，再形成自己的判断，不洗稿。
- **默认面向对 AI 好奇的普通读者**，可以在对话里改成其他读者。

## 使用示例

直接在对话里说，不需要提到"争点"：

- `OpenAI 刚发布了一个新模型，号称很强，帮我想想怎么写`（快速模式）
- `帮我深挖第二个选题`（深挖模式）
- `只要定义争点，给我 5 个选题，话题是 AI 写作`（单层模式）

## 安装

### Claude Code

把本仓库里的 `stasis-topic-generator/` 文件夹复制到：

- 个人（所有项目可用）：`~/.claude/skills/stasis-topic-generator/`
- 或某个项目内：`<项目>/.claude/skills/stasis-topic-generator/`

最终应当存在 `.../skills/stasis-topic-generator/SKILL.md`。

```bash
git clone https://github.com/<你的用户名>/stasis-topic-generator.git
mkdir -p ~/.claude/skills
cp -r stasis-topic-generator/stasis-topic-generator ~/.claude/skills/
```

### Claude 网页版 / 桌面版

1. 把 skill 文件夹打成 zip，**zip 的根目录应是 `stasis-topic-generator` 文件夹本身**，不要多套一层：

   ```bash
   cd stasis-topic-generator          # 进入仓库根目录
   zip -r stasis-topic-generator.zip stasis-topic-generator
   ```

2. 在 Claude 的设置里找到 Skills，上传这个 zip 并开启。自定义 skill 通常需要开启"代码执行与文件创建"，具体入口和套餐要求以 Claude 官方界面和文档为准。

## 目录结构

```
stasis-topic-generator/              # 仓库根目录
├── README.md
├── LICENSE
└── stasis-topic-generator/          # skill 本体
    ├── SKILL.md                     # 流程、三种模式、输出模板、底线
    └── references/
        ├── four-stases.md           # 四层争点定义、边界测试、示例
        ├── relevance.md             # 关联度评估与"扩大关联"
        ├── stress-test.md           # 深挖工具箱：反例、反方、换解释、找前人解法等
        └── gongzhonghao.md          # 公众号标题、摘要、开头、文章骨架
```

`SKILL.md` 保持精简，引用文件只在需要时才读取，这样日常使用不会占用过多上下文。

## 关于方法

争点理论源自古希腊罗马的修辞学传统，通常认为由赫尔马戈拉斯（Hermagoras）系统化，后来经西塞罗等人发展，经典的四个争点是推测（事实）、定义、性质、转移（程序）。这里的版本是面向内容创作的改编，不是学术复原。具体流程和测试为原创整理。

## 注意事项

- 涉及时效内容时，skill 会要求联网核实。没有搜索能力的环境里，相关信息会被标为【待核实】。
- 输出是选题和写作建议，发布前请自行核对事实和来源。

## 许可

[MIT](./LICENSE)
