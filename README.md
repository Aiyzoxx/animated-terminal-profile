# 🖥️ Animated Terminal GitHub Profile README

[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-Automated_Heatmap-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)](https://github.com/Aiyzoxx/animated-terminal-profile/actions)
[![Python 3.11+](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](./LICENSE)

Build an animated, terminal-styled GitHub profile README featuring:
- **🖨️ Monochrome ASCII portrait** that "types" itself into the terminal using SMIL clip-path wipe animation.
- **📋 Neofetch-style info card** with customizable key-values, experience, stack, and staggered line entrance.
- **🟩 Live 53-week contribution calendar** scraped directly from GitHub's public endpoint (no auth tokens needed!) with animated diagonal box reveal.
- **🤖 Zero-maintenance GitHub Action** updating the heatmap daily on a scheduled cron.

---

## 👁️ Preview

<div align="center">

<h3><code>demo@github ~ $ whoami</code></h3>

<table>
  <tr>
    <td valign="top"><img src="./ascii-portrait.svg" width="370" alt="ASCII Portrait Demo" /></td>
    <td valign="top"><img src="./info-card.svg" width="490" alt="Neofetch Card Demo" /></td>
  </tr>
</table>

<br>

<h3><code>demo@github ~ $ ./contributions.sh</code></h3>

<img src="./contrib-heatmap.svg" width="860" alt="Contribution Heatmap Demo" />

</div>

---

## 💡 How It Works

GitHub profile READMEs strip `<script>` tags and sanitize external CSS. However, GitHub **does render SVG images embedded via `<img>`** and preserves both SMIL animations and CSS `@keyframes` contained inside the SVG.

This project packages all motion and rendering directly into self-contained SVG files:
1. `ascii-portrait.svg` uses SMIL `<clipPath>` wipes with cursor animation.
2. `info-card.svg` uses staggered `<animateTransform>` and opacity transitions.
3. `contrib-heatmap.svg` uses CSS `@keyframes` with staggered execution delays.

---

## 🚀 Quickstart

### 1. Fork or Clone this Repo
```bash
git clone https://github.com/Aiyzoxx/animated-terminal-profile.git
cd animated-terminal-profile
```

### 2. Install Dependencies
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r scripts/requirements.txt
# Optional for photo background removal:
pip install rembg "onnxruntime>=1.16.0" opencv-python
```

### 3. Generate Your Heatmap
Fetch public GitHub contribution data and render the SVG:
```bash
# Sets your GitHub username
export GH_PROFILE_USER="your-github-username"
# On Windows PowerShell: $env:GH_PROFILE_USER="your-github-username"

python scripts/fetch_contributions.py
python scripts/render_heatmap_svg.py
```

### 4. Personalize Your Neofetch Card
Edit `data/profile_info.json` with your role, tech stack, and highlights:
```json
{
  "username": "YourName",
  "rows": [
    ["host"],
    ["kv", "Role", "Vibe Coder & Fullstack Dev"],
    ["kv", "Focus", "Web Applications & AI Tools"],
    ["gap"],
    ["sec", "Stack"],
    ["kv", "Languages", "Python, TypeScript, Go"],
    ["kv", "Frontend", "React, Next.js, Tailwind"],
    ["kv", "Backend", "FastAPI, Node.js, PostgreSQL"]
  ]
}
```
Then generate the card:
```bash
python scripts/make_info_card.py
```

### 5. Generate Your ASCII Portrait
1. Place your headshot in the root directory as `source-photo.png`.
2. Prep the photo (removes background + enhances local contrast via CLAHE):
   ```bash
   python scripts/prep_photo.py source-photo.png source-prepped.png
   ```
3. Convert to typing ASCII SVG:
   ```bash
   python scripts/make_ascii_svg.py
   ```

### 6. Publish to Your Profile
1. Copy the generated files (`ascii-portrait.svg`, `info-card.svg`, `contrib-heatmap.svg`, `data/`, `scripts/`, `.github/`) into your special `<username>/<username>` repository.
2. Use the Markdown layout template from [PROFILE_SNIPPET.md](./PROFILE_SNIPPET.md).
3. Push to `main`. The included GitHub Action will automatically keep your contribution heatmap refreshed daily!

---

## 📂 Project Structure

```
├── .github/workflows/
│   └── update-profile-art.yml   # Daily cron to refresh contributions graph
├── data/
│   ├── contributions.json       # Parsed GitHub calendar data & streak stats
│   └── profile_info.json        # Configuration file for the info card
├── scripts/
│   ├── fetch_contributions.py   # Public HTML scraper (zero token needed)
│   ├── render_heatmap_svg.py    # 53-week animated SVG heatmap renderer
│   ├── make_info_card.py        # Neofetch-style terminal info card generator
│   ├── prep_photo.py            # AI background removal & CLAHE contrast
│   ├── make_ascii_svg.py        # Monochrome typewriter ASCII SVG converter
│   └── requirements.txt         # Python dependencies
├── ascii-portrait.svg           # Rendered ASCII portrait
├── info-card.svg                # Rendered Neofetch card
├── contrib-heatmap.svg          # Rendered Contribution Heatmap
├── PROFILE_SNIPPET.md           # Markdown template for profile README
└── LICENSE                      # MIT License
```

---

## 🙏 Credits & Acknowledgments

This project is built directly upon the concept, architecture, and code created by **Avi Vashishta**:

- **Original Author**: [Avi Vashishta](https://github.com/AVIVASHISHTA29) ([avivashishta.com](https://www.avivashishta.com))
- **Original Blog Post**: [How I Built an Animated GitHub Profile README (ASCII Portrait + Neofetch Card + Live Contribution Graph)](https://www.avivashishta.com/blog/build-animated-github-profile-readme)
- **Reference Repository**: [AVIVASHISHTA29/AVIVASHISHTA29](https://github.com/AVIVASHISHTA29/AVIVASHISHTA29)
- **Visual Design Style**: Inspired by Andrew6rant's monochrome terminal aesthetics.

---

## 📄 License

Distributed under the [MIT License](./LICENSE). Feel free to use, modify, and share!
