# 🖼️ Wallpaper Scraper Skill

[![EN](https://img.shields.io/badge/README-English-blue)](README_EN.md)

Claude Code 高清电脑壁纸爬虫 Skill — 从 WallpapersWide 等站点批量下载 16:10 MacBook 高清壁纸。

## 功能

- 🖼️ 每次下载 ~60 张高清壁纸
- 📐 默认 16:10 宽高比（MacBook 全系适配），可切换 16:9
- 🏷️ 12 个分类：风景 / 美女 / 城市 / 抽象 / 游戏 / 动漫 / 卡通 / 动物 / 汽车 / 太空 / 极简 / 科技
- 🔍 自动 SHA-256 去重，增量下载不重复
- 📏 最低分辨率 1920×1080，PIL 实际校验
- 🌐 支持自定义 URL 或自动多关键词搜索
- ⚡ WallpapersWide 专用爬虫 + 通用爬虫双模式

## 安装

```bash
# 方式一：导入 .skill 打包文件
# 在 Claude Code 中直接导入 wallpaper-scraper.skill

# 方式二：放到 skills 目录
cp -r SKILL.md scripts/ references/ ~/.claude/skills/wallpaper-scraper/
```

## 使用

在 Claude Code 中直接对话即可：

```
下载 60 张风景壁纸
帮我找 30 张 4K 动漫壁纸
下载美女壁纸
https://wallhaven.cc/search?q=nature 从这个链接爬壁纸
```

脚本命令行：

```bash
# 自动模式（混合风格）
python3 scripts/scrape_wallpapers.py

# 指定分类
python3 scripts/scrape_wallpapers.py -c 风景
python3 scripts/scrape_wallpapers.py -c 美女 -n 30

# 切换宽高比
python3 scripts/scrape_wallpapers.py -r 16:9

# 查看所有参数
python3 scripts/scrape_wallpapers.py --help
```

## 依赖

```bash
pip3 install requests beautifulsoup4 lxml Pillow
```

## 项目结构

```
├── SKILL.md                    # Skill 定义文件
├── scripts/
│   └── scrape_wallpapers.py    # 核心爬虫脚本（~800 行 Python）
├── references/
│   └── wallpaper_sites.md      # 壁纸站点参考
├── wallpaper-scraper.skill     # 打包文件（可直接导入 Claude Code）
├── README.md                   # 中文说明
└── README_EN.md                # English README
```

## 工作原理

1. 扫描已有壁纸 → SHA-256 哈希索引去重
2. 中文分类名映射为英文搜索关键词列表
3. 多关键词轮询 WallpapersWide 搜索页
4. 详情页解析 → 宽高比过滤 → 取最大分辨率
5. 下载 + PIL 校验分辨率 + 宽高比
6. 哈希去重写入

## 支持的站点

| 站点 | 类型 | 状态 |
|------|------|------|
| WallpapersWide | 专用爬虫 | ✅ 默认源 |
| Wallhaven | 专用爬虫 | ⚠️ 需翻墙 |
| 任意 URL | 通用爬虫 | ✅ |

## License

MIT
