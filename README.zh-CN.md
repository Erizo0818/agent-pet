# Agent Pet

[English](README.md) · **简体中文**

两只可以直接安装到兼容 Codex 宠物系统的桌面应用中的宠物：**Indigo · 靛蓝猫**与 **G.E.M.**。每只包含 9 组日常动画与 16 个注视方向。

**[安装与使用指南](docs/HOW_TO.zh-CN.md)** · **[下载安装包](https://github.com/Erizo0818/agent-pet/releases/latest)**

| Indigo · 靛蓝猫 | G.E.M. |
| :---: | :---: |
| ![Indigo 待机动画](previews/indigo-cat/idle.gif) | ![G.E.M. 待机动画](previews/gem-tang/idle.gif) |
| 蓝紫色像素猫，青色 `>_` 表情。 | 受邓紫棋舞台造型启发的漫画风 Q 版歌手。 |
| [下载 ZIP](https://github.com/Erizo0818/agent-pet/releases/latest/download/indigo-cat.zip) · [全部动作](previews/indigo-cat/actions.gif) | [下载 ZIP](https://github.com/Erizo0818/agent-pet/releases/latest/download/gem-tang.zip) · [全部动作](previews/gem-tang/actions.gif) |

## 快速安装

从 [Releases](https://github.com/Erizo0818/agent-pet/releases/latest) 下载宠物 ZIP，解压后把宠物文件夹复制到本地安装目录：

```text
~/.codex/pets/
├── indigo-cat/
│   ├── pet.json
│   └── spritesheet.webp
└── gem-tang/
    ├── pet.json
    └── spritesheet.webp
```

安装包还附带许可证和素材来源说明。如果桌面应用配置了自定义 `CODEX_HOME`，请使用该目录下的 `pets` 子目录。

打开 **设置 → Pets → Refresh**，选择宠物，输入 `/pet` 唤出。安装不需要 API Key、重新生图或构建步骤。当前应用的操作方式见[官方 Pets 文档](https://learn.chatgpt.com/docs/pets)。

详细安装步骤、Windows 路径、更新和卸载方法见[安装与使用指南](docs/HOW_TO.zh-CN.md)。

## 已包含的动画

待机、向右移动、向左移动、挥手、跳跃、失败、等待输入、工作、审阅，以及 16 个注视方向。具体播放状态由宿主应用控制。

两只宠物均使用 `spriteVersionNumber: 2`：透明背景 **1536 × 2288** WebP 图集，**8 列 × 11 行**，每格 **192 × 208** 像素。GIF 用于预览；安装时需要 WebP 及对应的清单文件。

## 仓库结构

```text
pets/       可安装的宠物清单与精灵图集
previews/   待机与九宫格动作 GIF 预览
docs/       中英文安装与使用指南
LICENSE     MIT 许可证
CREDITS.md  创作来源与第三方权利说明
```

## 许可与来源

项目贡献在贡献者拥有的权利范围内沿用 [MIT 许可证](LICENSE)。本项目不另行授予第三方参考素材，以及姓名、肖像和商标方面的权利。详情见 [CREDITS.md](CREDITS.md)。

这是一个社区项目，与 OpenAI、邓紫棋及其团队不存在隶属关系，也不表示获得了其背书。
