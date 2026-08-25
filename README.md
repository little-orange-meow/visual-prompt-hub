# Image Generation Workspace

这是一个按人物和生成批次整理参考图、提示词及生成图片的工作目录。

## 配置环境

复制环境变量模板：

```bash
cp .env.example .env
```

编辑 `.env`，填写实际的 API Key 和接口地址：

```dotenv
OPENAI_API_KEY=your_api_key_here
OPENAI_BASE_URL=https://api.openai.com/v1
```

如果使用其他 OpenAI 兼容服务，请将 `OPENAI_BASE_URL` 替换为该服务提供的地址。

`.env` 包含敏感凭据，已被 Git 忽略。不要提交、分享或在聊天中粘贴它的内容。

## 目录结构

每个人物使用一个独立目录：

```text
人物名/
├── 1-原图参考/
│   └── person-reference.png
└── YYYYMMDD-HHMMSS/
    ├── 提示词.md
    ├── 01-generated-image.png
    └── 02-generated-image.png
```

- 将人物原始参考图放入 `人物名/1-原图参考/`。
- 每次生图创建一个上海时区的 `YYYYMMDD-HHMMSS` 批次目录。
- 每个批次同时保存用户原始提示词、实际调用提示词、生成参数和全部最终图片。
- 图片文件使用 `01-`、`02-` 等序号前缀，确保按生成顺序排列。

详细归档规则见 [`AGENTS.md`](AGENTS.md)。

## 使用

完成 `.env` 配置并放入参考图后，在当前工作目录中向 Codex 提供生图要求，例如：

```text
以 Ally/1-原图参考/person-reference.png 作为人物面部参照，
根据以下提示词生成两张图片：<你的提示词>
```

生成完成后，图片与完整提示词记录会归档到对应人物目录下的新时间批次中。
