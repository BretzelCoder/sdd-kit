# Image sources

| Source | Rendered image | Size |
|---|---|---|
| `workflow.html` | `../workflow.png` | 1620 × 2025 px (4:5) |
| `evolution.html` | `../evolution.png` | 1620 × 2025 px (4:5) |
| `social-preview.html` | `../social-preview.png` | 1280 × 640 px (2:1) |
| `icon.html` | `../../../.claude-plugin/icon.png` | 512 × 512 px, the plugin's listing icon |

No upstream project name, spec number or action number in these images (see `MAINTAINING.md`, section 3).

`social-preview.png` is the repository's social preview (the card shown when the link is shared). GitHub has no API for it: after re-rendering, upload it by hand in **Settings → General → Social preview**.

## Edit and re-render

1. Edit the text in the `.html` source. Colours and spacing are at the top of the file, in `<style>`.
2. Render it with headless Chrome (or Edge: same flags). The fonts (Inter, JetBrains Mono) load from Google Fonts, so you need network access. Run from the repository root:

   ```bash
   NAME=workflow; SIZE=1620,2025          # or: NAME=evolution; SIZE=1620,2025
                                          # or: NAME=social-preview; SIZE=1280,640
                                          # or: NAME=icon; SIZE=512,512, and OUT=.claude-plugin/icon.png

   # Windows (Git Bash)
   CHROME="/c/Program Files/Google/Chrome/Application/chrome.exe"
   # macOS: CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
   # Linux: CHROME=google-chrome

   SRC="file://$(pwd)/docs/images/src/$NAME.html"   # Windows: "file:///$(cygpath -m "$PWD")/docs/images/src/$NAME.html"
   OUT="$(pwd)/docs/images/$NAME.png"                # Windows: "$(cygpath -m "$PWD")/docs/images/$NAME.png"

   # 1. Check that everything fits: expect data-fits="true", and data-height no larger than the canvas height
   "$CHROME" --headless=new --disable-gpu --window-size=$SIZE --virtual-time-budget=10000 \
     --dump-dom "$SRC" | grep -o '<body[^>]*>'

   # 2. Render
   "$CHROME" --headless=new --disable-gpu --hide-scrollbars --force-device-scale-factor=1 \
     --window-size=$SIZE --virtual-time-budget=10000 --screenshot="$OUT" "$SRC"
   ```

3. If step 1 prints `data-fits="false"`, or a height above the canvas height, the content overflows. Shorten a text or reduce the spacing until it fits again: `.card` padding, `.card-wrap` and `.gate` height in `workflow.html`; `.text` padding in `evolution.html`; `.step` font size and padding in `social-preview.html` (the cycle row must fit on one line). Don't change the canvas size: 4:5 is the format social networks display without cropping, and 1280 × 640 is the size GitHub asks for.
4. Open the PNG and check it, then update the image's alt text (`README.md`, `CHANGELOG.md`) if the content changed.
