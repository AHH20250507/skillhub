# Skill Hub

一个**纯前端单页**的 Skill 管理平台，零后端、零构建，一键部署到 GitHub Pages。

所有 Skill 元数据（中文名称、简介、标签、版本历史、备注）存储在仓库根目录的 `skills/metadata.json` 中；每个版本的 ZIP 包存储在 `skills/{skill-id}/` 下。

![preview](https://img.shields.io/badge/stack-Tailwind%20+%20Lucide%20+%20Fetch-818cf8?style=flat-square)

## ✨ 核心特性

- **中文友好**：技能名、简介、标签、备注全部支持中文
- **GitHub 托管**：通过 Contents API 读写 `metadata.json` 与 ZIP 文件，无需任何后端
- **版本管理**：同日多版本自动递增（`YYYYMMDD.N`），版本说明、上传日期、文件大小一目了然
- **一键安装**：每个版本生成跨平台安装指令，复制粘贴给任意 Agent 即可自动下载并解压
- **搜索 & 筛选**：模糊搜索（名称 / 简介 / 标签 / 备注）+ 标签分类筛选
- **自定义备注**：每个 Skill 可记录仅自己可见的笔记
- **标签增删**：详情中一键管理标签
- **离线缓存**：未配置 GitHub 时降级到 `localStorage`，支持 JSON 导入 / 导出 / 一键推送到 GitHub
- **暗色主题**：基于 Tailwind + Lucide 的现代 UI，响应式布局

## 🚀 快速开始

### 1. Fork / 新建仓库
创建一个新的公开仓库（例如 `my-skill-hub`），把本目录全部文件推送上去。

### 2. 开启 GitHub Pages
在仓库 `Settings → Pages → Build and deployment` 中选择 `Deploy from a branch`，分支选 `main / root`，保存。

### 3. 生成 Personal Access Token
到 https://github.com/settings/tokens → `Generate new token (classic)`，勾选 `repo` 权限，复制 token。

### 4. 打开页面并配置
访问 `https://<username>.github.io/<repo>/`，点击右上角 ⚙ 设置按钮，填入：

| 字段 | 示例 |
|------|------|
| 仓库 | `username/my-skill-hub` |
| 分支 | `main` |
| Token | `ghp_xxxxxxxx` |
| Skill 根目录 | `skills` |

保存后页面自动从 `skills/metadata.json` 拉取数据。

## 📦 目录约定

```
repo/
├── index.html               # 单页应用
├── README.md                # 本文件
└── skills/                  # 默认 Skill 根目录（可自定义）
    ├── metadata.json        # 所有 Skill 元数据（自动生成）
    ├── daily-report/        # 一个 Skill
    │   ├── daily-report-20260702.1.zip
    │   └── daily-report-20260703.1.zip
    └── excel-analyst/
        └── excel-analyst-20260702.1.zip
```

`metadata.json` 结构：

```json
{
  "skills": {
    "daily-report": {
      "id": "daily-report",
      "name": "日报生成器",
      "description": "汇总当日 Git 提交、飞书消息、日程，自动生成结构化日报",
      "author": "AHH",
      "tags": ["效率", "日报"],
      "notes": "每周五下午自动触发",
      "versions": [
        {
          "version": "20260702.1",
          "file": "daily-report-20260702.1.zip",
          "date": "2026-07-02T14:30:00.000Z",
          "changelog": "初始版本",
          "size": 12345
        }
      ],
      "createdAt": "2026-07-01T00:00:00.000Z",
      "updatedAt": "2026-07-02T14:30:00.000Z"
    }
  },
  "updatedAt": "2026-07-02T14:30:00.000Z"
}
```

## 🧩 Skill ZIP 格式约定

ZIP 解压后应得到一个**与 Skill ID 同名**的目录，目录内至少包含 `SKILL.md`：

```
daily-report.zip
└── daily-report/
    ├── SKILL.md
    ├── reference.md (可选)
    └── scripts/ (可选)
```

Agent 拿到安装指令后会把解压出的目录放到用户的 `~/.qoderworkcn/skills/` 下。

## 🛠 常用操作

- **新建 Skill**：点右上角 `+ 新建 Skill`，填写名称、简介、标签，上传 ZIP
- **新增版本**：打开 Skill 详情 → 版本历史 → `+ 新增版本`
- **编辑 / 删除**：详情页右上角按钮
- **标签管理**：详情页标签区点击 `+ 添加` 或 `×` 删除
- **复制安装指令**：展开版本详情 → 一键复制
- **数据迁移**：`数据` 按钮 → 导出 / 导入 JSON / 推送到 GitHub

## 🔐 安全与隐私

- Token 仅保存在浏览器 `localStorage`，不会上传到任何服务器
- 建议使用**仅授予 repo 权限**的细粒度 Token
- 若仓库私有，访问 GitHub Pages 需要额外授权，建议用公开仓库 + 单独私有仓库存敏感 Skill

## 📝 License

MIT — 自由使用、修改、分发。
