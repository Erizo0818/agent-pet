# 如何安装和使用 Agent Pet

[English](HOW_TO.en.md) · [返回项目首页](../README.md)

本文介绍如何在支持 Codex v2 自定义宠物的桌面应用中，安装 **Indigo · 靛蓝猫**（`indigo-cat`）、**G.E.M.**（`gem-tang`），或同时安装两只。安装包已经包含成品图片，不需要 API Key、重新生图或构建工具。

## 1. 下载安装包

打开 [Releases 下载页](https://github.com/Erizo0818/agent-pet/releases/latest)，选择：

| 文件 | 内容 |
| --- | --- |
| `indigo-cat.zip` | Indigo 靛蓝猫 |
| `gem-tang.zip` | G.E.M. |

解压 ZIP，保持 `pet.json` 与 `spritesheet.webp` 在同一个宠物文件夹中。附带的 `LICENSE` 和 `CREDITS.md` 说明了使用许可与素材来源。

## 2. 放入安装目录

### 使用下载的 ZIP：无需终端

把解压后的 `indigo-cat` 或 `gem-tang` 文件夹复制到下方目录。如果没有 `pets` 文件夹，先创建它。

| 系统 | 默认目录 | 打开方法 |
| --- | --- | --- |
| macOS | `~/.codex/pets/` | Finder → 前往 → 前往文件夹（`⌘⇧G`） |
| Windows | `%USERPROFILE%\.codex\pets\` | 在文件资源管理器地址栏粘贴路径 |

如果桌面应用配置了 `CODEX_HOME`，则使用 `<CODEX_HOME>/pets/`。文件需要放在运行桌面应用的电脑上；复制到 WSL 或远程开发机器里，不会安装到 Windows/macOS 桌面应用中。

同时安装两只时，目录结构应为：

```text
<CODEX_HOME 或用户目录下的 .codex>/pets/
├── indigo-cat/
│   ├── pet.json
│   ├── spritesheet.webp
│   ├── LICENSE
│   └── CREDITS.md
└── gem-tang/
    ├── pet.json
    ├── spritesheet.webp
    ├── LICENSE
    └── CREDITS.md
```

不要多套一层目录，例如 `pets/agent-pet-main/pets/indigo-cat/` 或 `pets/indigo-cat/indigo-cat/`。

### 另一种方法：从 Git 仓库安装

克隆公开仓库：

```sh
git clone https://github.com/Erizo0818/agent-pet.git
cd agent-pet
```

macOS：在仓库目录中执行：

```sh
pet_dir="${CODEX_HOME:-$HOME/.codex}/pets"
mkdir -p "$pet_dir"
cp -R pets/indigo-cat pets/gem-tang "$pet_dir/"
```

Windows：在仓库目录中打开 PowerShell 执行：

```powershell
$petRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE '.codex' }
$petDir = Join-Path $petRoot 'pets'
New-Item -ItemType Directory -Force -Path $petDir | Out-Null
Copy-Item -Path 'pets\indigo-cat', 'pets\gem-tang' -Destination $petDir -Recurse -Force
```

只安装一只时，在复制命令中仅保留对应宠物的源路径。已安装同名宠物时，这些命令会替换其文件；如果做过个人修改，请先备份。

## 3. 选择并唤出宠物

1. 打开桌面应用的 **设置 → Pets**。
2. 点击 **Refresh**，选择 **Indigo · 靛蓝猫**或 **G.E.M.**。
3. 在应用中输入 `/pet`，或在命令菜单中选择 **Wake Pet**。

再次输入 `/pet` 可以收起悬浮宠物。具体动画由应用根据工作状态播放；GIF 用于展示已有动作，不是额外的动作控制界面。以上操作参考 [官方 Pets 文档](https://learn.chatgpt.com/docs/pets)。

## 4. 更新与卸载

**更新：**下载新版 ZIP，或在仓库里执行 `git pull --ff-only`。把已安装的宠物文件夹备份到 `pets` 目录之外，再用新版文件夹替换。返回设置 → Pets，刷新并重新选择。

**卸载：**先切换到其他宠物或收起当前宠物，再从安装目录中仅移除对应的 `indigo-cat` 或 `gem-tang` 文件夹，随后刷新。其他宠物可以继续保留。

## 5. 常见问题

| 问题 | 检查方法 |
| --- | --- |
| 列表里没有宠物 | 检查目录是否多套了一层、应用实际使用的 `CODEX_HOME`、两个必需文件是否齐全。点击 Refresh，必要时重新打开应用。 |
| 提示图片尺寸或版本错误 | 使用支持 v2 宠物的应用版本，保留 `spriteVersionNumber: 2`，不要缩放原始 1536 × 2288 WebP。 |
| 宠物一直不动 | 检查系统是否开启了“减少动态效果”。待机动作本身比较轻微。 |
| 只有 GIF，没有安装文件 | 下载宠物 ZIP。预览 GIF 不能代替安装用的 spritesheet。 |
| 网页或另一台电脑里没有它 | 桌面自定义宠物保存在本机，不会自动同步；其他电脑需要分别安装。 |

本仓库提供桌面 v2 安装包。当前[官方文档](https://learn.chatgpt.com/docs/pets)中的网页上传入口要求 1536 × 1872 布局，与这里的文件不同；这些 ZIP 不是网页上传包。安装步骤已在 macOS 检查，Windows 复制步骤尚未在 Windows 桌面环境实测。

## 6. 理解和修改安装包

每只宠物通过清单关联图片：

```json
{
  "id": "indigo-cat",
  "displayName": "Indigo · 靛蓝猫",
  "description": "蓝紫色像素猫，青色终端表情。",
  "spriteVersionNumber": 2,
  "spritesheetPath": "spritesheet.webp"
}
```

图集为 8 列 × 11 行，每格 192 × 208 像素。第 0–8 行依次是待机、向右移动、向左移动、挥手、跳跃、失败、等待、工作、审阅；第 9–10 行是从向上开始、每隔 22.5° 顺时针排列的 16 个注视方向。修改图片时需要保留这个布局。想让自己的变体与原版共存，请更换文件夹名及对应的 `id`。

分发变体前，请阅读 [LICENSE](../LICENSE) 与 [CREDITS.md](../CREDITS.md)，保留相关声明，并说明自己的修改与新增参考素材。
