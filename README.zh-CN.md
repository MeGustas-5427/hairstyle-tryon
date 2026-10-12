# Hairstyle Try-on · 发型试戴

[English](README.md) | 简体中文 | [Español](README.es.md) | [Français](README.fr.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [한국어](README.ko.md) | [日本語](README.ja.md)

一个用于现实换发参考的 Codex skill，根据自拍推荐发型并生成试戴参考照。

提供一张自拍，可附目标发型图。Codex 根据头发条件和打理习惯推荐 4–6 款完整方案，用户多选后，通过内置 imagegen 逐款生成试戴参考照，并附对比页面和给理发师看的发型需求卡。

## 效果展示

来自 4 组网络素材测试的 12 张实际 AI 试戴图，仅供视觉参考，不是真实剪发前后照，也不代表照片人物为本项目背书。W02 包含向下扩图，新增颈肩、衣物和背景为 AI 推测补全。

[查看全部 12 张效果图、原照对比与图片来源](examples/README.md)

| 原照 | AI 试戴效果 |
| --- | --- |
| **P02**<br><a href="examples/p02/original.webp"><img src="examples/p02/original.webp" alt="P02 原照" width="320"></a> | **H02 · 蓬松卷刘海**<br><a href="examples/p02/h02.webp"><img src="examples/p02/h02.webp" alt="P02 AI 试戴效果: 蓬松卷刘海" width="320"></a> |
| **W02**<br><a href="examples/w02/original.webp"><img src="examples/w02/original.webp" alt="W02 原照" width="320"></a> | **H01 · 暖栗棕法式波波**<br><a href="examples/w02/h01.webp"><img src="examples/w02/h01.webp" alt="W02 AI 试戴效果: 暖栗棕法式波波" width="320"></a> |
| **W03**<br><a href="examples/w03/original.webp"><img src="examples/w03/original.webp" alt="W03 原照" width="320"></a> | **H04 · 保留眼镜的顺直波波**<br><a href="examples/w03/h04.webp"><img src="examples/w03/h04.webp" alt="W03 AI 试戴效果: 保留眼镜的顺直波波" width="320"></a> |

## 工作流程

1. 提供清晰正面自拍；侧面、背面与目标发型图可选。
2. 用选项填写头发条件、烫染接受度、打理时间和禁忌；允许“不清楚”与自由表达。
3. 浏览带参考图、推荐理由、实现条件和来源链接的候选。
4. 默认选 1–3 款，每款生成一张；明确要求更多时可扩展。
5. 查看独立图片和并排对比，再按编号微调。

发型按长度和特征组织，不限男女。有目标图时优先适配本人条件；每款生成均以原始自拍为本人外貌依据。

## 运行条件

本仓库是技能指令，不包含图像模型、API 服务或插件实现。需要可运行本地 skill、查看图片，并能调用内置 imagegen 的 Codex 环境。

| 能力 | 用途 | 不可用时 |
| --- | --- | --- |
| Codex 内置 imagegen | 生成与修改试戴照 | 保留方案并说明情况；不会自动改用付费 API |
| Exa（可选） | 优先搜索和读取发型来源 | 回退普通网页搜索 |
| TypeSafe（可选） | 候选文本筛选、排序 | 由 Codex 完成筛选 |
| Interactive Form Save（可选） | 条件填写、多选与提交读回 | 使用编号选项和自由回复 |

内置 imagegen 路径不要求配置 `OPENAI_API_KEY`。外部工具的可用性、额度和使用条款由各自服务决定；本仓库不附带这些服务的访问权限。

## 安装

将本仓库克隆或解压为 `hairstyle-tryon` 文件夹，放入你的 Codex 已配置的 skills 目录，使路径为：

```text
你的 skills 目录/
└── hairstyle-tryon/
    ├── SKILL.md
    ├── README.md
    ├── README.zh-CN.md
    ├── README.es.md
    ├── README.fr.md
    ├── README.pt.md
    ├── README.ru.md
    ├── README.ko.md
    ├── README.ja.md
    ├── examples/
    └── LICENSE
```

已设置 `CODEX_HOME` 的环境可使用其 `skills` 子目录。安装前检查同名文件夹，保留已有修改；不要将文件套在两层 `hairstyle-tryon` 目录中。

## 使用

在 Codex 中调用技能并附上照片，例如：

```text
使用 $hairstyle-tryon，帮我找适合日常通勤的发型。
保留原发色，不烫发，每天愿意花约 5 分钟打理。
我会上传正面自拍，先让我多选方案，再生成试戴照。
```

有目标发型时可一起上传，并说明哪些特征最想保留。后续可以直接说：“把 H02 的刘海稍微缩短，其余保持不变。”

## 交付

默认保存到运行任务工作区的 `output/hairstyle-tryon/本次唯一标识/`，也可指定其他目录：

- 每款独立试戴照，按方案编号和版本命名。
- `comparison.html`：引用原照与成图的并排对比页面。
- `notes.md`：来源、生成提示、检查结果，以及每款发型需求卡。

“发型需求卡”是一段可以直接给理发师看的要求：想保留哪些特征、接受哪些改变、平时如何打理，以及需要现场确认的条件。它不是保证效果的剪发处方。

## 验证与图片使用

当前 skill 版本为 `v0.1.0`。2026-09-28 与 2026-10-12 已使用内置 imagegen 完成 4 组网络素材试戴、共 12 张成图，目视与文件检查见[完整案例](examples/README.md)。用户本人自拍流程与真实剪染效果尚未验证。外貌保持依靠提示约束和目视检查，不承诺像素级不变。

仓库包含技能、文档及 `examples/` 中明确选入的网络素材演示，图片适用各自的[来源与许可](examples/CREDITS.md)；不包含用户自拍或私人表单记录。运行时照片仅用于当次请求。发布改动前，请检查暂存内容，避免提交私人照片、无关生成结果或凭据。运行输出目录及常见本地输入目录仍由 `.gitignore` 忽略。

## 联系方式

QQ群：`1094787834`。

## 许可证

本仓库的技能指令与文档采用 [MIT License](LICENSE)，标准文本来源见 [Open Source Initiative](https://opensource.org/license/mit)。用户照片、网络参考图片与外部服务不因本仓库使用 MIT 而获得新的授权。
