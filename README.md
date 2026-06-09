# Wallpaper Scraper Skill

Claude Code 高清电脑壁纸爬虫 Skill — 从 WallpapersWide 等站点批量下载高清壁纸。

## 功能

- 🖼️ 每次下载 ~60 张高清壁纸
- 📐 默认 16:10 宽高比（MacBook 全系适配），可切换 16:9
- 🏷️ 12 个分类：风景 / 美女 / 城市 / 抽象 / 游戏 / 动漫 / 卡通 / 动物 / 汽车 / 太空 / 极简 / 科技
- 🔍 自动 SHA-256 去重，增量下载不重复
- 📏 最低分辨率 1920×1080，PIL 实际校验

## 安装

```bash
# 安装 Skill
cp wallpaper-scraper.skill ~/Downloads/
# 在 Claude Code 中导入 .skill 文件

# 或直接放到 skills 目录
cp -r ./* ~/.claude/skills/wallpaper-scraper/
```

## 使用

```
/claude-code 下载 60 张风景壁纸
/claude-code 帮我找 30 张 4K 动漫壁纸
/claude-code 下载美女壁纸
```

## 依赖

```bash
pip3 install requests beautifulsoup4 lxml Pillow
```

## 结构

```
├── SKILL.md              # Skill 定义
├── scripts/
│   └── scrape_wallpapers.py   # 核心爬虫
├── references/
│   └── wallpaper_sites.md     # 站点参考
└── wallpaper-scraper.skill    # 打包文件
```

## License

MIT
