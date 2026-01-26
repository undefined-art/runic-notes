# Runic Notes

Your notes live in the URL. No account. No cloud. Just type and share you thoughts.

<p align="center">
  <img src=".github/preview.webp" alt="Rune notes UI preview" width="100%">
</p>

## What is this?

Runic Notes is a tiny text editor that stores everything in the browser URL. Write something, copy the URL, send it to anyone — they'll see exactly what you wrote. No signup, no database, no tracking.

**Perfect for:**
- Quick notes you want to share instantly
- Code snippets that need to survive Slack's formatting
- Sensitive text that shouldn't touch someone else's server
- Bookmarkable scratchpads

## How to use

1. Open page in your browser
2. Type something (starting with `#` set tab title)
3. Your text auto-saves to the URL
4. Copy the URL → share it anywhere

That's it. The URL *is* your document.

## Keyboard shortcuts

| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| Save now | `⌘ + S` | `Ctrl + S` |
| Copy URL | `⌘ + Shift + C` | `Ctrl + Shift + C` |
| Close popup | `Esc` | `Esc` |

## Tips

**Encrypt sensitive notes** — Click the 🔒 button, enter a password. The URL becomes encrypted. Anyone with the URL still needs the password to read it.

**Large documents work too** — Notes under ~2KB go directly in the URL. Bigger notes get stored locally with a short reference code. Hit "Copy URL" to get a full shareable link regardless of size.

## Privacy & Security

- Everything happens in your browser
- Nothing is sent anywhere
- Encryption uses AES-256-GCM with PBKDF2 key derivation (100k iterations)
- Works offline once loaded
- No cookies, no analytics, no external requests

## Run it yourself

```bash
# Just open the file
open index.html

# Or start a local server (or use something like Live Server extention)
python -m http.server 8000
```

Works on any static hosting: GitHub Pages, Netlify, Vercel, S3, or just a folder on your computer.

## Useful commands

```bash
# Check file sizes after minification
ls -lh index.html index.min.html

# Check gzipped size
gzip -c index.min.html | wc -c

# Minify and check size
npx html-minifier --collapse-whitespace --remove-comments --minify-css true --minify-js true index.html -o index.min.html && ls -lh index.min.html
```

## Technical details

- Single HTML file (~23KB, ~21KB minified, ~7KB gzipped)
- Zero dependencies, zero build step required
- Web Worker for non-blocking compression
- LZ-String compression (URL-safe base64)
- IndexedDB for large content storage
- requestIdleCallback for smooth saves
- Falls back gracefully when Web Crypto isn't available

---

Built because sometimes you just want to share text without creating an account.
