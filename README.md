# Instagram Archive Viewer

A single-file, offline browser app for browsing saved Instagram videos and images from your local disk. No server, no uploads — everything stays on your machine.

![Requires Chrome or Edge](https://img.shields.io/badge/browser-Chrome%20%7C%20Edge-blue)

## Features

- **Grid library** — Thumbnail grid with lazy loading and video frame previews
- **Reels mode** — Full-screen vertical scroll feed with autoplay, shuffle, and mute toggle
- **Account filtering** — Groups media by username parsed from filenames
- **Search & sort** — Filter by name, account, or path; sort by date, name, size, account, or random
- **Favorites** — Mark items locally (stored in your browser, not in the files)
- **Delete from disk** — Remove files directly from the selected folder (with confirmation)
- **Dark / light theme** — Toggle from the header
- **Keyboard shortcuts** — Navigate quickly without touching the mouse
- **Remembers your folder** — Re-opens the last selected directory on return (with permission)

## Requirements

- **Google Chrome** or **Microsoft Edge** (desktop)
- Uses the [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API) — not supported in Firefox or Safari at this time
- A folder on your computer containing saved Instagram media (videos and/or images)

## Quick start

1. Clone or download this repository.
2. Open `instagram-viewer.html` in Chrome or Edge (double-click, or drag the file into a browser window).
3. Click **Select Folder** and choose the folder where your saved media lives.
4. Grant read/write permission when prompted (write access is only used if you delete files from the viewer).

That's it — no install, no build step, no dependencies.

## Supported file types

| Type   | Extensions                                      |
|--------|-------------------------------------------------|
| Video  | `.mp4`, `.webm`, `.mov`, `.m4v`                |
| Image  | `.jpg`, `.jpeg`, `.png`, `.webp`, `.gif`, `.heic` |

All subfolders inside your selected directory are scanned recursively.

## Filename conventions

Usernames are inferred from filenames so you can filter by account in the sidebar:

| Pattern | Example | Parsed account |
|---------|---------|----------------|
| `username_timestamp_…` | `somecreator_1704067200_clip.mp4` | `somecreator` |
| `username_shortcode_date` | `somecreator_ABC123_2026-01-15.mp4` | `somecreator` |
| Fallback | `somecreator_anything.mp4` | First segment before `_` |

If your files are flat in one folder, you can optionally organize them into per-account subfolders with the included helper script:

```bash
python organize_by_username.py /path/to/your/media/folder
python organize_by_username.py --dry-run   # preview moves only
```

## Keyboard shortcuts

| Key | Action |
|-----|--------|
| `/` | Focus search |
| `j` / `↓` | Next item (opens player) |
| `k` / `↑` | Previous item (opens player) |
| `f` | Toggle favorite |
| `r` | Open Reels mode |
| `Delete` | Delete current file (with confirmation) |
| `Esc` | Close player or Reels overlay |

In **Reels mode**, use scroll or swipe to move between items. Press `Space` to play/pause the current video.

## Privacy

- Media files are read directly from your disk via the browser's File System Access API.
- Nothing is uploaded to any server.
- Favorites, theme, sort preferences, and the folder handle are stored locally in your browser (`localStorage` and IndexedDB).
- Thumbnail previews for videos are cached in IndexedDB to speed up repeat visits.

## Tips

- Click **↻** in the header to re-scan the folder after adding new files.
- Use **Random** sort or **🔀 Shuffle** for a mixed feed.
- **Reels** mode shuffles the current filtered set — filter by account first for a single-creator feed.
- On mobile-width viewports, tap **☰** to open filters and the account list.

## License

Use and modify freely. Instagram is a trademark of Meta Platforms, Inc.; this project is not affiliated with or endorsed by Instagram/Meta.
