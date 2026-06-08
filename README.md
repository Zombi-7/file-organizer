# 📁 File Organizer

A simple but powerful Python script that automatically organizes files in any folder by sorting them into subfolders based on their type.

## ✨ Features

- Organizes files into **9 categories**: Images, Videos, Audio, Documents, Sheets, Slides, Code, Archives, Executables
- **Dry run mode** — preview what will happen before moving anything
- Handles **duplicate file names** automatically (adds timestamp)
- Works on Windows, macOS, and Linux
- No external libraries needed — pure Python

## 📂 Categories

| Folder | Extensions |
|---|---|
| Images | .jpg .jpeg .png .gif .webp .svg .bmp |
| Videos | .mp4 .mov .avi .mkv .wmv .flv |
| Audio | .mp3 .wav .ogg .flac .aac |
| Documents | .pdf .doc .docx .txt .odt |
| Sheets | .xls .xlsx .csv |
| Slides | .ppt .pptx |
| Code | .py .js .html .css .json .sql ... |
| Archives | .zip .rar .tar .gz .7z |
| Others | everything else |

## 🚀 How to use

**1. Run and type the folder path:**
```bash
python file_organizer.py
```

**2. Or pass the path directly:**
```bash
python file_organizer.py /path/to/your/folder
```

**3. Preview before moving (dry run):**
```
Preview only (no files moved)? [y/N]: y
```

## 📋 Example output

```
============================================
        FILE ORGANIZER by Henrique
============================================

Organizing: /Users/you/Downloads
Files found: 12

  [MOVING] photo.jpg         →  Images/
  [MOVING] report.pdf        →  Documents/
  [MOVING] script.py         →  Code/
  [MOVING] archive.zip       →  Archives/

── Summary ──────────────────────────────────
  Archives        1 file(s)
  Code            1 file(s)
  Documents       1 file(s)
  Images          1 file(s)
  Total           4 file(s)
──────────────────────────────────────────────
```

## 🛠 Requirements

- Python 3.6+
- No external libraries needed

## 👤 Author

**Henrique** — Python Developer & Automation Specialist  
[Fiverr](https://fiverr.com/henrique1ia) · [GitHub](https://github.com/zumbi7)
