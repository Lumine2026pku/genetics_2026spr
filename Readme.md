🧬 Genetics Knowledge Distillation & Review System
A zero-cost, fully automated tool that converts your genetics lecture PDFs into a structured, bilingual (EN/CN) review website with progress tracking — powered by DeepSeek API.

✨ Features
📄 PDF → Structured Knowledge — Extracts text from lecture slides and distills it into concepts, formulas, and key points using LLM

🌐 Interactive Review Website — Single HTML file with chapter navigation, collapsible content, and dark mode

🔢 LaTeX Rendering — All formulas beautifully rendered with MathJax

✅ Learning Progress — localStorage-based tracking with visual progress bar

🌗 Dark Mode — Toggle between light and dark themes

💾 Resumable Processing — Cached results prevent re-processing completed chapters

🔧 JSON Auto-Repair — Robust error recovery for LLM outputs

🚀 Quick Start
1. Install dependencies
bash
pip install -r requirements.txt
2. Set up API key
Create a .env file:

text
DEEPSEEK_API_KEY=sk-your-key-here
3. Organize your files
text
course_review/
├── data/                    # Put your lecture PDFs here
│   ├── ch_01_a.pdf
│   ├── ch_01_b.pdf
│   └── ...
├── config.json              # Edit chapter titles and file mappings
├── build.py
└── template.html
4. Run
bash
python build.py
5. Open
text
output/review.html
📁 Project Structure
File	Purpose
config.json	Chapter metadata & file mapping
build.py	Main pipeline: extract → distill → generate
distill.py	LLM interaction, JSON repair, caching
extract.py	PDF text extraction
template.html	Jinja2 template for the review website
retry.py	Manually retry failed chapters
output/data.json	Intermediate distilled data
output/review.html	Final deployable website
🔑 Key Commands
bash
# Full build (uses cache when available)
python build.py

# Check which chapters have cache
python -c "from distill import show_cache_status; show_cache_status()"

# Retry a failed chapter
python retry.py 3

# Regenerate HTML from existing data.json
python -c "
import json; from jinja2 import Environment, FileSystemLoader
with open('output/data.json') as f: data = json.load(f)
html = Environment(loader=FileSystemLoader('.')).get_template('template.html').render(data=data)
open('output/review.html','w').write(html); print('Done')
"
📦 Dependencies
pdfplumber — PDF text extraction

openai — DeepSeek API client

jinja2 — HTML templating

python-dotenv — Environment variable management

🎯 Use Case
Built for genetics course review, but works with any subject — just update the chapter titles in config.json and provide your own lecture PDFs.

📄 License
MIT — feel free to use, modify, and share.