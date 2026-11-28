---
name: wy-git-commit
description: 使用 wgc（wy-git-commit）执行格式化消息的 Git 提交。仅在 Woisol 的个人项目中使用，其它项目请遵循原仓库的提交规范。
---

# wgc

wgc 是对 git commit 的格式化消息 wraper，执行 wgc 等价于执行 git commit。

## 使用

```sh
wgc --type TYPE --title "TITLE" [选项] [Git 提交参数]
```

### 基本参数

| 参数 | 用法 |
| --- | --- |
| `--type TYPE` | 必填。传类型键。多个类型可用逗号分隔或重复传参，按传入顺序显示。 |
| `--title TITLE` | 必填。单行标题。 |
| `--scope SCOPE` | 单行作用域，不需括号。 |
| `--body BODY` | 正文。 |
| `--breaking TEXT` | 破坏性变更说明，不需 `BREAKING CHANGE:` 前缀。 |
| `--wy-dry-run` | 只输出格式化后的提交信息。 |

用 `--title` 和 `--body` 提供消息内容。其他 Git 提交参数可直接传入，例如 `--amend`。

### TYPE

| 类型 | 相关 |
| --- | --- |
| `feat` | 新功能 |
| `fix` | Bug 修复 |
| `change` | 不属于其他类型的项目专属变更，包括配置或非代码变更 |
| `refactor` | 重构 |
| `build` | 构建、打包或依赖 |
| `ci` | 持续集成与交付 |
| `chore` | 维护与仓库日常事务 |
| `docs` | 文档 |
| `test` | 测试 |
| `perf` | 性能优化 |
| `style` | 不改变行为的代码格式调整 |
| `revert` | 撤销提交 |
| `init` | 项目或环境初始化 |

change 不应是 refactor、fix 或 feat 的模糊替代。当存在更具体的类型时，优先使用后者。

### AI Meta

| 参数 | 含义 |
| --- | --- |
| `--harness NAME` | 执行提交的 Agent 运行环境，只要由你（AI）执行提交就应当添加。 |
| `--ai-generated true\|false` | 改动是否主要由 AI 生成，false 时建议省略。 |
| `--ai-review true\|false` | 改动是否未经过实质性人工审阅，true 时建议省略。 |


例如，使用 `wgc --type feat --title "Add new feature" --scope fe --body "This is a new feature." --harness DSH --ai-generated true --amend` 等价于

```sh
git commit -m "「 :sparkles: 新增 / feat 」(fe): Add new feature

This is a new feature.

「[AI] Agentic Coding 产物 / Agentic Coding Product」
本次提交由 DSH 执行 / This commit was made by DSH.
AI-Generated: true" --amend
```

## 建议规范

* 提交语言与文案风格参考仓库历史提交，不存在或不明确时默认使用中文。
* 默认使用一种类型，但当变更确实涉及多项关注点、且拆分提交并不现实时，允许且建议使用多类型。
* title 使用简洁的祈使句描述变更结果，不以句号结尾。