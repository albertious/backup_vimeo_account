# backup_vimeo_account

How to back up your Vimeo account using **yt-dlp**.
So I used this method with the cookies, because if you have unlisted/private videos you will 

Essentially this mode downloads all videos from a Vimeo user page using `yt-dlp` and an authenticated `cookies.txt`.

## Requirements

- A Vimeo account
- `yt-dlp` installed and available in your `PATH` (see the verify stage below!!)
- A `cookies.txt` exported from a browser session where you are logged into Vimeo
- macOS or Linux terminal

## 1) Install yt-dlp

### Windows
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
incommmand line or terminal run:
```bash
yt-dlp --version
```
if successfully installed, it will give you a version number for the yt-dlp installation.

## 2) Export Vimeo cookies

You must export your logged-in Vimeo session cookies to a file named `cookies.txt`.
Unfortunately you need the cookies.txt to provide credentials to `yt-dlp` so it can access private, unlisted, or account-owned videos.

### Steps

1. Log into Vimeo in your web browser.
2. Install a browser extension that can export cookies in **Netscape cookies.txt format**.
   - Search your browser’s extension store for tools like “Get cookies.txt”.
   - There are multiple extensions that do this; results may vary.
3. Use the extension to export cookies for `vimeo.com`.
4. Save the exported file as `cookies.txt`.

### Browser notes

- Chromium-based browsers (Chrome, Brave, Edge) tend to work more reliably for Vimeo cookie export - i dont know why, maybe I used the wrong extensions for firefox.
- If downloads fail later, try:
  - Re-exporting cookies
  - Using a different cookies exporter extension
  - Switching browsers and exporting again?

Place `cookies.txt` in the destination folder where you want your videos saved (you /PATH/TO/SAVE/ where you will run the terminal commandline stuff later)

**Keep `cookies.txt` private.**  
Anyone with this file may be able to access your account. Don't share it or screengrabs of it online, you dingus!

## 3) Download your videos

Open a terminal/commandline and change into your destination folder:

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
Or instead, you can try downloading the original upload format like this:
```bash
yt-dlp "https://vimeo.com/YOURUSERNAME/videos" \
  --cookies "cookies.txt" \
  --format "source/original" \
  --merge-output-format mp4 \
  -o "%(upload_date)s_%(title)s.%(ext)s"
```
I had varying results.

## Output

- Downloads the highest available quality (`bestvideo+bestaudio` when available)
- Merges into `.mp4`
- Filenames should save as: YYYYMMDD_Title.mp4

## Notes / Troubleshooting

- If private or unlisted videos fail to download, re-export `cookies.txt` and try again.
- Vimeo may invalidate cookies over time; re-export if errors appear.
- Some titles may contain characters that your filesystem modifies automatically.

## Disclaimer

Use this to back up **your own** content only.  
Respect Vimeo’s Terms of Service and applicable copyright laws.
