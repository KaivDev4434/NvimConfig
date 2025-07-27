# NvimConfig

A **plug-and-play Neovim 0.9+ distribution** built around Lazy .nvim for instant startup, rich language tooling and a sleek UI. Drop folder into `~/.config/nvim`, launch **nvim**, and enjoy LSP, autocompletion, formatting and linting for Python, JavaScript/TypeScript, Svelte, Markdown and more—without touching a plugin manager or writing Lua.

## Highlights
* **Zero-config bootstrap** – Lazy .nvim is downloaded automatically on first launch [1].
* **40+ curated plugins** loaded on-demand for a snappy feel.
* **One-command language setup** – Mason installs servers, linters and formatters listed in `ensure_installed` [2].
* **Modern editing UX**
  * Telescope-powered fuzzy search & live-grep [3].
  * Nvim-tree file explorer with git icons and custom arrows [4].
  * Tokyonight colour scheme tweaked for a deep-blue UI [5].
  * Lualine statusline showing pending Lazy updates [6].
  * Alpha-nvim dashboard with quick actions on start .
* **Productive defaults**
  * Sensible options (`relativenumber`, `smartcase`, clipboard=unnamedplus, etc.) [7].
  * Space as *leader* plus ergonomic window & tab splits [8].
* **Safe code ⇢ Save file**
  * Treesitter highlighting/indent for >20 languages [9].
  * Nvim-cmp + LuaSnip completion with VS-Code icons [10].
  * Conform auto-formats on write (Prettier, Black, Stylua…) [11].
  * Nvim-lint runs ESLint _d_ / Pylint automatically [12].

## Folder Layout
```
~/.config/nvim
├── init.lua                → bootstrap core + Lazy [2]
├── lazy-lock.json          → pinned plugin versions
└── lua/ill_pickle
    ├── lazy.lua            → Lazy self-installer & plugin imports [3]
    ├── core
    │   ├── options.lua     → editor settings [5]
    │   └── keymaps.lua     → global key-mappings [6]
    └── plugins             → lazy specs
        ├── init.lua        → essential utils (plenary, tmux nav) [23]
        ├── *.lua           → UI & workflow plugins (telescope, nvim-tree …)
        └── lsp
            ├── mason.lua   → server / tool installer [9]
            └── lspconfig.lua → LSP handlers & keybinds [10]
```

## Quick Start

```bash
# 1. backup any existing config
mv ~/.config/nvim ~/.config/nvim.bak 2>/dev/null

# 2. clone
git clone https://github.com/KaivDev4434/NvimConfig ~/.config/nvim

# 3. launch – Lazy.nvim will sync everything
nvim
```

### External prerequisites
| Tool | Purpose | Install |
|------|---------|---------|
| **Neovim 0.9+** | core editor | `brew install neovim` / distro pkg |
| **make & gcc** | build Telescope fzf-native | system pkg |
| **Node ≥ 18 & npm** | Prettier, ESLint _d_ | `brew install node` |
| **Python 3** | Black, Isort, Pylint | `brew install python` |
| **ripgrep** | Telescope live-grep | `brew install ripgrep` |

> Mason will pull the exact LSP/formatter binaries on first run [2].

## Fast-lane Key-map Cheat-Sheet

| Key (normal) | Action |
|--------------|--------|
| `ff` / `fr` / `fs` / `fc` | Telescope **find files / recent / live-grep / grep word** [3] |
| `ft` | Telescope TODO-comments [3] |
| `ee` `ef` `ec` `er` | Toggle / reveal / collapse / refresh **nvim-tree** [4] |
| `gD` `gd` `gi` `gR` / `gt` | LSP *declaration / definition / implementation / references / type* [13] |
| `ca` / `rn` | Code action / smart rename [13] |
| `d` `[d` `]d` / `D` | Line / prev / next / file diagnostics [13] |
| `mp` | **Format** buffer/selection via Conform [11] |
| `l` | Manual **lint** current file [12] |
| `sv` `sh` `se` `sx` | Vertical / horizontal split, equalise, close [8] |
| Leader is **Space** [8] – combine with Telescope (`<leader>f*`), nvim-tree (`<leader>e*`) etc.

## Language Support Matrix

| Language | Parser (Treesitter) | LSP (Mason) | Formatter | Linter |
|----------|--------------------|-------------|-----------|--------|
| Python | ✅ [9] | **pyright** [2] | Black, Isort [11] | Pylint [12] |
| JavaScript / TS / React | ✅ [9] | **tsserver** [2] | Prettier [11] | eslint_d [12] |
| Svelte | ✅ [9] | **svelte-ls** [2] | Prettier [11] | eslint_d [12] |
| HTML / CSS / Tailwind | ✅ [9] | html, cssls, tailwindcss [2] | Prettier [11] | — |
| Lua | ✅ [9] | lua_ls [13] | Stylua [11] | — |
| Markdown / YAML / JSON | ✅ [9] | — | Prettier [11] | — |

*(plus GraphQL, Prisma, Dockerfile, Bash, C, Vimdoc… see `ensure_installed`) [9][2]*

## Customisation Tips
1. **Change theme:** swap `style = "night"` or install a different colourscheme spec.
2. **Add / remove plugins:** create a new spec under `lua/ill_pickle/plugins`—Lazy autodetects on restart.
3. **Override keymaps:** append to `core/keymaps.lua`; leader-space namespace is mostly free.
4. **Pin tool versions:** edit `lazy-lock.json` then `:Lazy sync`.

## Updating
```
:Lazy update      " pull plugin updates
:Mason            " open tool manager UI
```
Lualine shows pending plug-ins ⚡ in real time [6].

## License
MIT—see the upstream repository. Enjoy the ride!
