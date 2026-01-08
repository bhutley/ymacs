# Ymacs

An Emacs-like editor for the Web. [Ymacs homepage](https://lisperator.net/ymacs/).

## Features

- **Emacs keybindings** - Familiar key sequences like `C-x C-s`, `C-x b`, `M-x`, etc.
- **Buffer management** - Multiple buffers with `C-x b` to switch, `C-x k` to kill
- **Frame splitting** - Split horizontally (`C-x 3`) or vertically (`C-x 2`)
- **Syntax highlighting** - Built-in modes for JavaScript, Lisp, CSS, XML, and Markdown
- **Incremental search** - `C-s` / `C-r` with regex support
- **Kill ring** - Full kill/yank functionality with `M-y` to cycle
- **Undo** - Unlimited undo with `C-/` or `C-x u`
- **Keyboard macros** - Record with `C-x (`, end with `C-x )`, replay with `C-x e`
- **Minibuffer** - Command input with tab completion
- **Themes** - Multiple color themes included
- **Rectangle editing** - `C-x r k`, `C-x r y`, etc.

## Installation

```bash
git clone https://github.com/mishoo/ymacs.git
cd ymacs
npm install
npx parcel build
```

## Usage

```javascript
import { Ymacs } from "ymacs";

// Create editor instance
const ymacs = new Ymacs();

// Style and mount
Object.assign(ymacs.getElement().style, {
    position: "absolute",
    left: 0,
    top: 0,
    width: "100%",
    height: "100%"
});

document.body.appendChild(ymacs.getElement());
ymacs.focus();

// Optional: set a color theme
ymacs.setColorTheme("standard-dark");

// Optional: enable line numbers
ymacs.addClass("Ymacs-line-numbers");

// Optional: highlight current line
ymacs.addClass("Ymacs-hl-line");
```

### Working with Buffers

```javascript
// Get the active buffer
const buffer = ymacs.getActiveBuffer();

// Set buffer content
buffer.setCode("Hello, world!");

// Execute commands programmatically
buffer.cmd("end_of_buffer");
buffer.cmd("insert", "\nNew line");

// Switch to a different buffer
ymacs.switchToBuffer("*scratch*");

// Create a new buffer
const newBuf = ymacs.createBuffer({ name: "myfile.js" });
newBuf.cmd("javascript_mode");
```

### Available Modes

- `javascript_mode` - JavaScript/TypeScript
- `lisp_mode` - Common Lisp / Scheme
- `css_mode` - CSS
- `xml_mode` - HTML/XML
- `markdown_mode` - Markdown

## Development

```bash
# Install dependencies
npm install

# Start development server
npx parcel serve test/test.html

# Build for production
npx parcel build
```

Output files:
- `dist/ymacs.mjs` - ES module
- `dist/ymacs.css` - Main stylesheet
- `dist/themes/*.css` - Color themes

## Key Bindings

### Movement
| Key | Command |
|-----|---------|
| `C-f` / `C-b` | Forward/backward character |
| `M-f` / `M-b` | Forward/backward word |
| `C-n` / `C-p` | Next/previous line |
| `C-a` / `C-e` | Beginning/end of line |
| `M-<` / `M->` | Beginning/end of buffer |

### Editing
| Key | Command |
|-----|---------|
| `C-d` | Delete character |
| `M-d` | Kill word |
| `C-k` | Kill line |
| `C-w` | Kill region |
| `M-w` | Copy region |
| `C-y` | Yank |
| `M-y` | Yank pop (cycle kill ring) |
| `C-/` | Undo |

### Buffers & Frames
| Key | Command |
|-----|---------|
| `C-x b` | Switch buffer |
| `C-x k` | Kill buffer |
| `C-x 2` | Split vertically |
| `C-x 3` | Split horizontally |
| `C-x 1` | Delete other frames |
| `C-x o` | Other frame |

### Search
| Key | Command |
|-----|---------|
| `C-s` | Incremental search forward |
| `C-r` | Incremental search backward |
| `M-%` | Query replace |

### Other
| Key | Command |
|-----|---------|
| `M-x` | Execute command |
| `C-g` | Keyboard quit |
| `C-x C-c` | (Not bound by default - web apps can't close tabs) |

## License

MIT License - Copyright (c) 2009-2024 Mihai Bazon

See [LICENSE](LICENSE) for details.
