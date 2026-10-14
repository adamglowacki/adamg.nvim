# Neovim Manual

Quick reference for this configuration. Leader key is **Space**.

## What you'll see on screen

| Where | What | Provided by |
|---|---|---|
| Top | Buffer/tab bar with file icons, modified markers, and LSP diagnostic badges | `bufferline.nvim` |
| Bottom | Status line (mode, git branch, diagnostics, filetype, position) | `lualine.nvim` |
| Left gutter | Line numbers + git change markers (`+` added, `~` changed, `_` deleted) | `gitsigns.nvim` |
| Left gutter | LSP diagnostic signs (errors/warnings) | built-in LSP |
| In-buffer | Faint vertical indent guides | `indent-blankline.nvim` |
| In-buffer | Trailing whitespace highlighted in red | `vim-better-whitespace` |
| Column 80 | A highlighted column marking line-length | built-in (`colorcolumn`) |
| Colorscheme | `oxocarbon` (dark, applied automatically on startup) | `oxocarbon.nvim` |

Mouse support is **disabled** — everything is keyboard-driven.

## Core behavior

- Search (`/`, `?`) is case-insensitive unless you type an uppercase letter (`smartcase`)
- System clipboard is the default register — `y`/`p` interact with it directly
- Undo history persists across sessions (`undofile`)
- `j`/`k` move by *visual* line when no count is given, so they work naturally on wrapped lines
- Indentation (tabs vs. spaces, width) is auto-detected per file by `vim-sleuth`

## Keybindings

### Navigation / buffers

| Key | Action |
|---|---|
| `Tab` | Next buffer |
| `Shift-Tab` | Previous buffer |
| `<leader>bp` | Pick a buffer to jump to (bufferline) |
| `<leader>bd` | Close current buffer |
| `<leader><space>` | Fuzzy-list open buffers (Telescope) |
| `<leader>?` | Fuzzy-list recently opened files |

### Search (Telescope)

| Key | Action |
|---|---|
| `<leader>sf` | Find files |
| `<leader>sg` | Live grep across the project |

### Diagnostics

| Key | Action |
|---|---|
| `[d` / `]d` | Jump to previous / next diagnostic |
| `<leader>e` | Show diagnostic message under cursor (floating) |
| `<leader>q` | Diagnostics in the location list |
| `<leader>xx` | Toggle Trouble diagnostics panel (whole project) |
| `<leader>xX` | Toggle Trouble diagnostics panel (current buffer only) |
| `<leader>xL` | Toggle Trouble location-list view |
| `<leader>xQ` | Toggle Trouble quickfix-list view |

### LSP (active once a language server attaches to the buffer)

| Key | Action |
|---|---|
| `K` | Hover documentation |
| `gd` | Go to definition |
| `<leader>rn` | Rename symbol |
| `<leader>ca` | Code action |
| `:Format` | Format the current buffer |

Only `lua_ls` (Lua) is installed by default. Run `:Mason` to browse and install
other language servers (e.g. for Python, Rust, TypeScript) — once installed,
they attach automatically.

### Insert-mode completion (nvim-cmp)

Triggers automatically as you type when an LSP is attached.

| Key | Action |
|---|---|
| `Ctrl-n` / `Ctrl-p` | Next / previous suggestion |
| `Tab` | Next suggestion, or expand/jump a snippet |
| `Enter` | Confirm selection |

### Commenting (Comment.nvim, default mappings)

| Key | Action |
|---|---|
| `gcc` | Toggle comment on current line |
| `gc` + motion (e.g. `gcap`) | Comment a motion/text object |
| `gc` (visual mode) | Comment selected lines |

### Git

- Change markers show automatically in the sign column — no keymaps are bound for staging/undoing hunks yet
- `:G` / `:Git ...` — full git integration via `vim-fugitive` (status, commit, blame, diff, etc.)
- `:StripWhitespace` — remove trailing whitespace in the current file (`vim-better-whitespace`)

### Which-key

Press `<leader>` and wait — a popup lists available key groups (`b` Buffer,
`c` Code, `s` Search, `x` Trouble/Diagnostics, etc.). A few groups (`d`
Document, `g` Git, `h` Git Hunk, `t` Toggle, `w` Workspace) are reserved
labels with no commands bound yet — room to extend later.

## Plugin management

| Command | Action |
|---|---|
| `:Lazy` | Open the plugin manager UI (install/update/clean) |
| `:Mason` | Open the LSP/tool installer UI |
| `:TSUpdate` | Update Treesitter syntax parsers |
| `:checkhealth` | Diagnose configuration/plugin issues |
