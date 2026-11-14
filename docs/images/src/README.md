# Image sources

| Source | Rendered image | Size |
|---|---|---|
| `workflow.html` | `../workflow.png` | 1620 × 2025 px (4:5) |
| `evolution.html` | `../evolution.png` | 1620 × 2025 px (4:5) |

No upstream project name, spec number or action number in these images (see `MAINTAINING.md`, section 3).

## Edit and re-render

1. Edit the text in the `.html` source. Colours and spacing are at the top of the file, in `<style>`.
2. Render it with headless Chrome (or Edge: same flags). The fonts (Inter, JetBrains Mono) load from Google Fonts, so you need network access. Run from the repository root:

   ```bash
   NAME=workflow   # or evolution

   # Windows (Git Bash)
   CHROME="/c/Program Files/Google/Chrome/Application/chrome.exe"
   # macOS: CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
   # Linux: CHROME=google-chrome

   SRC="file://$(pwd)/docs/images/src/$NAME.html"   # Windows: "file:///$(cygpath -m "$PWD")/docs/images/src/$NAME.html"
   OUT="$(pwd)/docs/images/$NAME.png"                # Windows: "$(cygpath -m "$PWD")/docs/images/$NAME.png"

   # 1. Check that everything fits: expect data-fits="true" data-height="2025"
   "$CHROME" --headless=new --disable-gpu --window-size=1620,2025 --virtual-time-budget=10000 \
     --dump-dom "$SRC" | grep -o '<body[^>]*>'

   # 2. Render
   "$CHROME" --headless=new --disable-gpu --hide-scrollbars --force-device-scale-factor=1 \
     --window-size=1620,2025 --virtual-time-budget=10000 --screenshot="$OUT" "$SRC"
   ```

3. If step 1 prints `data-fits="false"`, or a height above 2025, the content overflows the canvas. Shorten a text or reduce the spacing until it fits again: `.card` padding, `.card-wrap` and `.gate` height in `workflow.html`; `.text` padding in `evolution.html`. Don't make the canvas taller: 4:5 is the format social networks display without cropping.
4. Open the PNG and check it, then update the image's alt text (`README.md`, `CHANGELOG.md`) if the content changed.
