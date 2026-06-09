# 🖼️ Wallpaper Scraper Skill

[![中文](https://img.shields.io/badge/README-中文-red)](README.md)

Claude Code skill for batch downloading HD desktop wallpapers from WallpapersWide and other sources. Optimized for MacBook displays (16:10 aspect ratio).

## Features

- 🖼️ Downloads ~60 HD wallpapers per run
- 📐 Default 16:10 aspect ratio (MacBook native), switchable to 16:9
- 🏷️ 12 categories: landscape / girl / city / abstract / game / anime / cartoon / animal / car / space / minimalist / tech
- 🔍 SHA-256 deduplication — incremental downloads
- 📏 Minimum 1920×1080 resolution, PIL-verified
- 🌐 Custom URL support or auto multi-keyword search
- ⚡ WallpapersWide dedicated scraper + generic fallback

## Installation

```bash
# Option 1: Import the .skill package
# Import wallpaper-scraper.skill directly in Claude Code

# Option 2: Copy to skills directory
cp -r SKILL.md scripts/ references/ ~/.claude/skills/wallpaper-scraper/
```

## Usage

Chat naturally in Claude Code:

```
Download 60 landscape wallpapers
Get me 30 4K anime wallpapers
Download girl wallpapers
Scrape wallpapers from https://wallhaven.cc/search?q=nature
```

Or use the CLI directly:

```bash
# Auto mode (mixed styles)
python3 scripts/scrape_wallpapers.py

# By category
python3 scripts/scrape_wallpapers.py -c landscape
python3 scripts/scrape_wallpapers.py -c girl -n 30

# Switch aspect ratio
python3 scripts/scrape_wallpapers.py -r 16:9

# Show all options
python3 scripts/scrape_wallpapers.py --help
```

## Categories

| Category | Aliases |
|----------|---------|
| landscape | 风景, nature, 自然 |
| girl | 美女, 女孩, 人物 |
| city | 城市, 建筑 |
| abstract | 抽象, 艺术 |
| game | 游戏, games |
| anime | 动漫 |
| cartoon | 卡通 |
| animal | 动物, animals |
| car | 汽车, cars |
| space | 太空 |
| minimalist | 极简 |
| tech | 科技, technology |

## Dependencies

```bash
pip3 install requests beautifulsoup4 lxml Pillow
```

## Project Structure

```
├── SKILL.md                    # Skill definition
├── scripts/
│   └── scrape_wallpapers.py    # Core scraper (~800 lines Python)
├── references/
│   └── wallpaper_sites.md      # Wallpaper site reference
├── wallpaper-scraper.skill     # Packaged skill file
├── README.md                   # 中文说明
└── README_EN.md                # English README
```

## How It Works

1. Scan existing files → SHA-256 hash index for dedup
2. Map category names to English search keywords
3. Multi-keyword polling on WallpapersWide
4. Detail page parsing → aspect ratio filtering → pick highest resolution
5. Download + PIL validation (resolution & aspect ratio)
6. Hash-based dedup write

## Supported Sites

| Site | Type | Status |
|------|------|--------|
| WallpapersWide | Dedicated scraper | ✅ Default |
| Wallhaven | Dedicated scraper | ⚠️ VPN required |
| Any URL | Generic scraper | ✅ |

## License

MIT
