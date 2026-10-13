# Hairstyle Try-on

English | [简体中文](README.zh-CN.md) | [Español](README.es.md) | [Français](README.fr.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [한국어](README.ko.md) | [日本語](README.ja.md)

A Codex skill for realistic hairstyle recommendations and selfie-based try-on references.

Provide a selfie and, optionally, a target hairstyle image. Codex recommends 4–6 complete styles based on your hair and daily styling routine. After you select your favorites, built-in imagegen creates a separate try-on photo for each style, along with a comparison page and a plain-language brief to share with your hairdresser.

## Examples

8 portrait test cases, 24 AI try-on results, all in WebP. Latest update: 2026-10-13. These are visual simulations, not real haircut before/after photos or endorsements. The gallery explains source-image provenance, canvas extensions and reconstructed regions.

[View all 24 results, comparisons and image credits](examples/README.md)

| Original | AI try-on |
| --- | --- |
| **CNM01**<br><a href="examples/cnm01/original.webp"><img src="examples/cnm01/original.webp" alt="CNM01 Original source" width="320"></a> | **H04 · Soft chestnut curly wolf cut**<br><a href="examples/cnm01/h04.webp"><img src="examples/cnm01/h04.webp" alt="CNM01 AI try-on: Soft chestnut curly wolf cut" width="320"></a> |
| **JPM01**<br><a href="examples/jpm01/original.webp"><img src="examples/jpm01/original.webp" alt="JPM01 Original source" width="320"></a> | **H03 · Cool dark brown spiral curls**<br><a href="examples/jpm01/h03.webp"><img src="examples/jpm01/h03.webp" alt="JPM01 AI try-on: Cool dark brown spiral curls" width="320"></a> |
| **KR01**<br><a href="examples/kr01/original.webp"><img src="examples/kr01/original.webp" alt="KR01 Original source" width="320"></a> | **H02 · Milk-tea beige brown blunt bob**<br><a href="examples/kr01/h02.webp"><img src="examples/kr01/h02.webp" alt="KR01 AI try-on: Milk-tea beige brown blunt bob" width="320"></a> |
| **JP01**<br><a href="examples/jp01/original.webp"><img src="examples/jp01/original.webp" alt="JP01 Original source" width="320"></a> | **H03 · Rose brown collarbone layers · v2**<br><a href="examples/jp01/h03.webp"><img src="examples/jp01/h03.webp" alt="JP01 AI try-on: Rose brown collarbone layers · v2" width="320"></a> |
| **P02**<br><a href="examples/p02/original.webp"><img src="examples/p02/original.webp" alt="P02 Original" width="320"></a> | **H02 · Curly fringe**<br><a href="examples/p02/h02.webp"><img src="examples/p02/h02.webp" alt="P02 AI try-on: Curly fringe" width="320"></a> |
| **W02**<br><a href="examples/w02/original.webp"><img src="examples/w02/original.webp" alt="W02 Original" width="320"></a> | **H01 · Warm chestnut French bob**<br><a href="examples/w02/h01.webp"><img src="examples/w02/h01.webp" alt="W02 AI try-on: Warm chestnut French bob" width="320"></a> |
| **W03**<br><a href="examples/w03/original.webp"><img src="examples/w03/original.webp" alt="W03 Original" width="320"></a> | **H04 · Sleek bob with glasses**<br><a href="examples/w03/h04.webp"><img src="examples/w03/h04.webp" alt="W03 AI try-on: Sleek bob with glasses" width="320"></a> |

## Workflow

1. Provide a clear front-facing selfie. Side, back, and target hairstyle photos are optional.
2. Choose options describing your hair, willingness to perm or color it, daily styling time, and things to avoid. “Not sure” and free-text answers are welcome.
3. Browse candidates with reference images, recommendation reasons, practical requirements, and source links.
4. Select 1–3 styles by default, with one generated photo per style. You can explicitly request more.
5. Review the individual photos and side-by-side comparison, then request refinements by style ID.

Styles are organized by length and features, for all genders. A target hairstyle is adapted to your own hair conditions. Every generation uses your original selfie as the reference for your appearance.

## Requirements

This repository contains skill instructions, not an image model, API service, or plugin implementation. It requires a Codex environment that supports local skills, image viewing, and built-in imagegen.

| Capability | Purpose | When unavailable |
| --- | --- | --- |
| Codex built-in imagegen | Generate and edit try-on photos | Keep the proposed styles and explain the limitation; never automatically switch to a paid API |
| Exa (optional) | Preferred search and retrieval of hairstyle sources | Fall back to ordinary web search |
| TypeSafe (optional) | Filter and rank candidate descriptions | Codex handles the selection |
| Interactive Form Save (optional) | Collect preferences, multiple selections, and read back submitted answers | Use numbered choices and free-text replies |

The built-in imagegen workflow does not require an `OPENAI_API_KEY`. Availability, quotas, and terms for external tools depend on their respective services; this repository does not grant access to them.

## Installation

Clone or extract this repository into a `hairstyle-tryon` folder inside your configured Codex skills directory:

```text
your-skills-directory/
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

If `CODEX_HOME` is configured, you can use its `skills` subdirectory. Check for an existing folder and preserve any local changes before installing. Avoid nesting the files inside two `hairstyle-tryon` folders.

## Usage

Invoke the skill in Codex and attach your photo. For example:

```text
Use $hairstyle-tryon to help me find a hairstyle for everyday work.
Keep my current hair color, no perm, and about 5 minutes of styling per day.
I'll upload a front-facing selfie. Let me choose multiple styles before generating try-on photos.
```

If you have a target hairstyle image, attach it too and describe the features you most want to keep. You can then request changes such as: “Make the bangs in H02 a little shorter and keep everything else the same.”

## Deliverables

By default, outputs are saved under `output/hairstyle-tryon/<unique-run-id>/` in the task workspace. You can specify another directory.

- A separate try-on photo for each style, named by style ID and version.
- `comparison.html`: a side-by-side comparison page referencing the original and generated photos.
- `notes.md`: sources, generation prompts, review results, and a brief for each hairstyle.

The hairstyle brief is a plain-language note you can show your hairdresser: which features to keep, which changes you accept, your daily styling routine, and what needs an in-person assessment. It is not a cutting prescription or a guarantee of the result.

## Validation and image use

Skill version: `v0.1.0`. Eight portrait workflows produced 24 final images with built-in imagegen on 2026-09-28, 2026-10-12 and 2026-10-13; visual and file checks are recorded in the [example gallery](examples/README.md). A user-selfie workflow and real haircut results remain unverified. Appearance preservation relies on prompt constraints and visual review, with no guarantee of pixel-level consistency.

The repository contains the skill, documentation and selected portrait demonstrations in `examples/`, subject to their [photo credits and image terms](examples/CREDITS.md). It contains no user selfies or private form submissions. Runtime photos are used for that request. Before publishing changes, check staged files for private photos, unrelated outputs or credentials. Runtime output folders and common local input folders remain excluded by `.gitignore`.

## Contact

QQ group: `1094787834`.

## License

The skill instructions and documentation are licensed under the [MIT License](LICENSE). See the [Open Source Initiative](https://opensource.org/license/mit) for the standard license text. This license does not grant additional rights to user photos, online reference images, or external services.
