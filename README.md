# Invisible Unicode Tools

Small browser-based experiments for invisible Unicode text effects and hidden-message encoding.

## Project Overview

This project contains two standalone HTML tools:

- `index.html`: a "Zalgo" generator that uses only `U+2800` (Braille Pattern Blank)
- `invisible-message.html`: an encoder/decoder that hides a message inside zero-width Unicode characters

Both files are plain HTML/CSS/JS and run directly in a browser with no build step.

## Files

- `index.html`
  - Generates text with large amounts of invisible `U+2800` inserted around characters
  - Includes an escaped preview so inserted characters are visible as `\u2800`
  - Includes intensity control and copy-to-clipboard
- `invisible-message.html`
  - Encodes a secret message into invisible Unicode
  - Optionally appends the invisible payload to visible cover text
  - Decodes hidden payloads back to the original message
  - Shows visible text with invisible characters stripped out
- `README.md`
  - Project documentation

## Tool 1: U+2800 Zalgo Generator (`index.html`)

### What it does

- Adds random amounts of `U+2800` around characters to create a hidden/invisible "glitch" effect
- Preserves readability better than normal Zalgo because the inserted codepoint is invisible
- Shows metrics like output length and inserted `U+2800` count

### Important note

`U+2800` is invisible in most fonts, so the output may look almost identical to the input even though it contains many extra characters.

## Tool 2: Invisible Message Hider (`invisible-message.html`)

### What it does

- Encodes a secret message into zero-width Unicode characters
- Appends that invisible payload to optional visible cover text
- Decodes a pasted encoded string and restores the hidden message
- Displays the visible text without hidden characters

### Unicode characters used

- `U+200B` (zero-width space) = bit `0`
- `U+200C` (zero-width non-joiner) = bit `1`
- `U+200D` (zero-width joiner) = byte separator
- `U+2060` (word joiner) = payload start/end marker

### Payload format (high level)

The hidden payload stores:

1. A short signature (`INV1`)
2. Message byte length (4 bytes)
3. UTF-8 encoded secret message bytes

This makes decoding more reliable and helps detect invalid or corrupted payloads.

## How to Run

1. Open `index.html` in any modern browser.
2. Open `invisible-message.html` in any modern browser.

No installation, package manager, or local server is required.

## Usage Examples

### U+2800 Zalgo Generator

1. Enter normal text in the input box
2. Adjust the intensity slider
3. Click `Generate`
4. Copy the output (invisible characters included)
5. Use the escaped preview to verify where `\u2800` was inserted

### Invisible Message Hider

1. Enter optional cover text (for example `normal sentence here`)
2. Enter a secret message (for example `meet at midnight`)
3. Click `Encode Hidden Message`
4. Copy the encoded output
5. Paste it into the decode area
6. Click `Decode Hidden Message`

## Limitations / Warnings

- Some websites, chat apps, editors, and social platforms strip or normalize invisible Unicode
- Copy/paste may remove some zero-width characters depending on the app
- These tools are not encryption and should not be used for security/privacy-sensitive data
- Invisible characters can behave differently across fonts, browsers, and platforms

## Browser Compatibility

Designed for modern browsers with support for:

- `TextEncoder` / `TextDecoder`
- Clipboard API (`navigator.clipboard`) for copy buttons

If clipboard copy fails, you can still manually copy from the textareas.

## Why this exists

This is a text/unicode experiment project for:

- weird text effects
- invisible payload demos
- Unicode behavior testing
- browser copy/paste experimentation
