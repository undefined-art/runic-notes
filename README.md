# Runic Notes

Runic Notes is a simple text editor that stores your note directly in the URL. Your browser keeps the data locally, so the note stays only with you and the person who opens the link.

![Preview](.github/preview.webp)

## Features

### Core

- Your note can live directly in the URL, so you can share it with a single link.  
- Short notes are compressed and stored in the URL hash.  
- Large notes are saved locally in IndexedDB on your device.  
- You can protect a note with a password using AES-GCM encryption.  
- You can generate a QR code and share the note by scanning it.

### Sharing

- You can copy a shareable link with one shortcut: Ctrl or Cmd + Shift + C.  
- Mobile devices can use the native share menu of the browser.  
- You can download the note as a .txt file with Ctrl or Cmd + S.  
- You can drag and drop a .txt file into the editor to import it.

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `⌘/Ctrl + N` | Create a new note |
| `⌘/Ctrl + S` | Download the note as a .txt file |
| `⌘/Ctrl + Shift + C` | Copy the note URL |
| `Escape` | Close an open modal window |

## Privacy & Security

Runic Notes keeps everything inside your browser.

- No data leaves your device while you write or read a note.  
- Encrypted notes use AES-256-GCM with PBKDF2 for key derivation.  
- There are no trackers, analytics scripts, cookies, or telemetry.  
- The code is open source, so anyone can inspect how it works.

## How It Works

Small notes stay completely inside the link.

If the compressed text is smaller than about 2KB, the whole note is stored in the URL hash. The browser reads the hash and restores the text. If the note grows larger, the editor saves it to IndexedDB on your device.  
The link then contains a short reference ID that points to that local data.

Encrypted notes start with the `#!` prefix. When someone opens such a link, the editor asks for the password and decrypts the text locally.

## Tech Stack

- Vanilla JavaScript with no external dependencies  
- LZW compression to fit notes inside the URL  
- Web Crypto API for encryption and decryption  
- IndexedDB for local storage of larger notes

## Browser Support

Runic Notes works in modern browsers.

- Chrome and Edge 79 and newer  
- Firefox 51 and newer  
- Safari 10 and newer  
- Opera works as well, except Opera Mini

## Installation

### Self-hosted

```bash
git clone https://github.com/undefined-art/runic-notes.git
cd runic-notes
python -m http.server 8000