# backup_vimeo_account

How to back up your Vimeo account using **yt-dlp**.

## Overview

This guide downloads all videos from a Vimeo user page using `yt-dlp` and an authenticated `cookies.txt`.

## Requirements

- A Vimeo account
- `yt-dlp` installed and available in your `PATH`
- A `cookies.txt` exported from a browser session where you are logged into Vimeo
- macOS or Linux terminal

## 1) Install yt-dlp

Install `yt-dlp` so your system recognizes it as a command.

Official instructions: https://github.com/yt-dlp/yt-dlp

### macOS (Homebrew)

```bash
brew install yt-dlp
```

### Linux (pip)

```bash
python3 -m pip install -U yt-dlp
```

Verify:

```bash
yt-dlp --version
```

## 2) Export Vimeo cookies

1. Log into Vimeo in your browser.
2. Export your cookies to a file named `cookies.txt`.
3. Place `cookies.txt` in the destination folder where you want your videos saved.

> Keep `cookies.txt` private. It can grant access to your account.

## 3) Download your videos

Open a terminal and change into your destination folder:

```bash
cd "/PATH/TO/SAVE/"
```

Run (replace `YOURUSERNAME`):

```bash
yt-dlp "https://vimeo.com/YOURUSERNAME/videos" \
  --cookies "cookies.txt" \
  --format "bestvideo+bestaudio/best" \
  --merge-output-format mp4 \
  -o "%(upload_date)s_%(title)s.%(ext)s"
```

## Output

- Downloads the highest available quality (`bestvideo+bestaudio` when available)
- Merges into `.mp4`
- Filenames:

```
YYYYMMDD_Title.mp4
```

## Notes / Troubleshooting

- If private/unlisted videos fail to download, re-export `cookies.txt` and try again.
- Some titles may contain characters that your filesystem changes/strips automatically; this is expected.

## Disclaimer

Use this to back up **your own** content and follow Vimeo’s Terms of Service and applicable copyright laws.
