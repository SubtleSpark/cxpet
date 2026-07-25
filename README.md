# cxpet

Codex custom pets collection.

这个仓库用来收集、整理和分享有意思的 Codex 自定义 pet。每个 pet 应该尽量保持可直接安装、可预览、可追溯来源，方便后续继续补充、修复或重新打包。

## Codex Pet 是什么

Codex pet 是 Codex app 里的小型动画伴侣。自定义 pet 通常是一个本地包：

```text
~/.codex/pets/<pet-id>/
├── pet.json
└── spritesheet.webp
```

`pet.json` 描述 pet 的基本信息，`spritesheet.webp` 提供所有动画帧。Codex 会从 `~/.codex/pets/` 下按文件夹加载这些自定义 pet。

## Pet 包格式

建议每个 pet 放在 `pets/<pet-id>/` 下：

```text
pets/<pet-id>/
├── pet.json
├── spritesheet.webp
├── preview.png
└── README.md
```

最小可用的 `pet.json`：

```json
{
  "id": "pet-id",
  "displayName": "Pet Name",
  "description": "One short sentence.",
  "spriteVersionNumber": 2,
  "spritesheetPath": "spritesheet.webp"
}
```

spritesheet 约定：

- 格式：WebP，透明背景。
- v1 尺寸：`1536x1872`，8 列 x 9 行；可省略 `spriteVersionNumber`。
- v2 尺寸：`1536x2288`，8 列 x 11 行；必须设置 `"spriteVersionNumber": 2`。
- 单格：`192x208`。
- 未使用的单元格必须完全透明。

动画行约定：

| Row | State | Used columns |
| --- | --- | ---: |
| 0 | `idle` | 0-5 |
| 1 | `running-right` | 0-7 |
| 2 | `running-left` | 0-7 |
| 3 | `waving` | 0-3 |
| 4 | `jumping` | 0-4 |
| 5 | `failed` | 0-7 |
| 6 | `waiting` | 0-5 |
| 7 | `running` | 0-5 |
| 8 | `review` | 0-5 |
| 9 | `look directions A` | 0-7 |
| 10 | `look directions B` | 0-7 |

v2 的方向行固定按顺时针排列：

- Row 9：`000`, `022.5`, `045`, `067.5`, `090`, `112.5`, `135`, `157.5`
- Row 10：`180`, `202.5`, `225`, `247.5`, `270`, `292.5`, `315`, `337.5`

其中 `000` 表示向上看，静止/正面状态仍由普通 `idle` 动画提供。

## 安装

把某个 pet 文件夹复制到 Codex 的 pets 目录：

```bash
mkdir -p ~/.codex/pets
cp -R pets/<pet-id> ~/.codex/pets/<pet-id>
```

然后在 Codex app 的外观或 pet 设置里选择它。

## 收录标准

提交 pet 时请尽量满足：

- `pet.json` 能被解析，`id` 与文件夹名一致。
- `spritesheet.webp` 存在，并符合固定图集尺寸。
- 背景透明，没有边框、格线、文字标签或多余画布元素。
- 每个动画状态的角色身份一致，轮廓、配色和主要特征不跳变。
- 附带 `preview.png` 或本 pet 的 `README.md`，说明来源、作者和生成方式。
- 不提交临时生成目录、模型缓存、原始大文件或本机私有配置。

## 建议工作流

1. 生成或收集一个 pet 包。
2. 检查 `pet.json` 和 spritesheet 尺寸。
3. 添加预览图和简短说明。
4. 放入 `pets/<pet-id>/`。
5. 在本地 Codex app 中安装并确认可用。

## 目录规划

```text
.
├── pets/          # 已收录的 pet 包
└── README.md
```

当前仓库先保留轻量结构，等 pet 数量和校验需求变多后再补工具脚本或其他目录。
