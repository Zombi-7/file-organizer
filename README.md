# file-organizer

"""
File Organizer — Automatic folder organizer by file type
Author: Henrique (github.com/zumbi7)
"""

import os
import shutil
from datetime import datetime

# ── CATEGORIES ──────────────────────────────────────────────────────────────
CATEGORIES = {
    "Images":     [".jpg", ".jpeg", ".png", ".gif", ".webp", ".svg", ".bmp", ".ico"],
    "Videos":     [".mp4", ".mov", ".avi", ".mkv", ".wmv", ".flv", ".webm"],
    "Audio":      [".mp3", ".wav", ".ogg", ".flac", ".aac", ".m4a"],
    "Documents":  [".pdf", ".doc", ".docx", ".txt", ".odt", ".rtf"],
    "Sheets":     [".xls", ".xlsx", ".csv", ".ods"],
    "Slides":     [".ppt", ".pptx", ".odp"],
    "Code":       [".py", ".js", ".ts", ".html", ".css", ".java", ".c", ".cpp", ".json", ".xml", ".sql"],
    "Archives":   [".zip", ".rar", ".tar", ".gz", ".7z"],
    "Executables":[".exe", ".msi", ".dmg", ".sh", ".bat"],
}

def get_category(extension: str) -> str:
    """Return the category name for a given file extension."""
    ext = extension.lower()
    for category, extensions in CATEGORIES.items():
        if ext in extensions:
            return category
    return "Others"

def organize_folder(folder_path: str, dry_run: bool = False) -> dict:
    """
    Organize all files in folder_path into subfolders by category.

    Parameters:
        folder_path : path to the folder you want to organize
        dry_run     : if True, only shows what would happen (no files moved)

    Returns:
        summary dict with count of files moved per category
    """
    folder = os.path.abspath(folder_path)

    if not os.path.isdir(folder):
        print(f"[ERROR] Folder not found: {folder}")
        return {}

    summary = {}
    files = [f for f in os.listdir(folder) if os.path.isfile(os.path.join(folder, f))]

    if not files:
        print("[INFO] No files found in the folder.")
        return {}

    print(f"\n{'[DRY RUN] ' if dry_run else ''}Organizing: {folder}")
    print(f"Files found: {len(files)}\n")

    for filename in files:
        # Skip hidden files and this script itself
        if filename.startswith(".") or filename == os.path.basename(__file__):
            continue

        _, ext = os.path.splitext(filename)
        category = get_category(ext)

        dest_folder = os.path.join(folder, category)
        src  = os.path.join(folder, filename)
        dest = os.path.join(dest_folder, filename)

        # Handle duplicate file names
        if os.path.exists(dest):
            timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
            name, extension = os.path.splitext(filename)
            dest = os.path.join(dest_folder, f"{name}_{timestamp}{extension}")

        print(f"  {'[WOULD MOVE]' if dry_run else '[MOVING]'} {filename}  →  {category}/")

        if not dry_run:
            os.makedirs(dest_folder, exist_ok=True)
            shutil.move(src, dest)

        summary[category] = summary.get(category, 0) + 1

    # Print summary
    print("\n── Summary ─────────────────────────────────")
    for category, count in sorted(summary.items()):
        print(f"  {category:<15} {count} file(s)")
    print(f"  {'Total':<15} {sum(summary.values())} file(s)")
    print("────────────────────────────────────────────\n")

    return summary


# ── MAIN ────────────────────────────────────────────────────────────────────
if __name__ == "__main__":
    import sys

    print("=" * 44)
    print("        FILE ORGANIZER by Henrique")
    print("=" * 44)

    # Accept folder path as argument or ask the user
    if len(sys.argv) > 1:
        path = sys.argv[1]
    else:
        path = input("Enter the folder path to organize: ").strip()

    # Ask for dry run
    preview = input("Preview only (no files moved)? [y/N]: ").strip().lower()
    dry_run = preview == "y"

    organize_folder(path, dry_run=dry_run)
