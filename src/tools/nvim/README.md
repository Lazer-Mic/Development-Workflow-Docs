# Neovim Keybindings Reference

## Leader Key
**Leader Key**: `<Space>` (default)

## Custom Keybindings from Configuration

### Search & Navigation
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<leader>nh` | Normal | `:nohl<CR>` | Clear search highlights |
| `<C-d>` | Normal | `<C-d>zz` | Scroll down half page, center cursor |
| `<C-u>` | Normal | `<C-u>zz` | Scroll up half page, center cursor |
| `n` | Normal | `nzzzv` | Next search result, center and open folds |
| `N` | Normal | `Nzzzv` | Previous search result, center and open folds |

### Text Editing & Manipulation
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `x` | Normal | `"_x` | Delete character without copying to register |
| `<leader>+` | Normal | `<C-a>` | Increment number under cursor |
| `<leader>-` | Normal | `<C-x>` | Decrement number under cursor |
| `<leader>r` | Visual | `"hy:%s/<C-r>h//gc<left><left><left>` | Replace highlighted text with search/replace |
| `J` | Visual | `:m '>+1<CR>gv=gv` | Move selected text down |
| `K` | Visual | `:m '<-2<CR>gv=gv` | Move selected text up |
| `<` | Visual | `<gv` | Indent left and stay in visual mode |
| `>` | Visual | `>gv` | Indent right and stay in visual mode |

### Mode Switching
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `jk` | Insert | `<ESC>` | Exit insert mode (alternative to Escape) |
| `jk` | Terminal | `<C-\><C-n>` | Exit terminal mode |
| `<ESC><ESC>` | Terminal | `<C-\><C-N>` | Exit terminal mode (double escape) |

### Window Management
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<leader>sv` | Normal | `<C-w>v` | Split window vertically |
| `<leader>sh` | Normal | `<C-w>s` | Split window horizontally |
| `<leader>se` | Normal | `<C-w>=` | Make splits equal size |
| `<leader>sx` | Normal | `:close<CR>` | Close current split |
| `<C-h>` | Normal | `<C-w>h` | Navigate to left window |
| `<C-j>` | Normal | `<C-w>j` | Navigate to bottom window |
| `<C-k>` | Normal | `<C-w>k` | Navigate to top window |
| `<C-l>` | Normal | `<C-w>l` | Navigate to right window |

### Window Navigation in Terminal Mode
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<C-h>` | Terminal | `<C-\><C-n><C-w>h` | Exit terminal, navigate left |
| `<C-j>` | Terminal | `<C-\><C-n><C-w>j` | Exit terminal, navigate down |
| `<C-k>` | Terminal | `<C-\><C-n><C-w>k` | Exit terminal, navigate up |
| `<C-l>` | Terminal | `<C-\><C-n><C-w>l` | Exit terminal, navigate right |

### Window Resizing
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<C-Up>` | Normal | `:resize -2<CR>` | Decrease window height |
| `<C-Down>` | Normal | `:resize +2<CR>` | Increase window height |
| `<C-Left>` | Normal | `:vertical resize -2<CR>` | Decrease window width |
| `<C-Right>` | Normal | `:vertical resize +2<CR>` | Increase window width |

### Tab Management
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<leader>to` | Normal | `:tabnew<CR>` | Open new tab |
| `<leader>tx` | Normal | `:tabclose<CR>` | Close current tab |
| `<leader>tn` | Normal | `:tabn<CR>` | Go to next tab |
| `<leader>tp` | Normal | `:tabp<CR>` | Go to previous tab |
| `<leader>tf` | Normal | `:tabnew %<CR>` | Open current buffer in new tab |

### Buffer Management
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<S-l>` | Normal | `:bnext<CR>` | Next buffer |
| `<S-h>` | Normal | `:bprevious<CR>` | Previous buffer |

## Plugin-Specific Keybindings

### File Explorer (nvim-tree)
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<leader>ee` | Normal | `:NvimTreeToggle<CR>` | Toggle file explorer |
| `<leader>ef` | Normal | `:NvimTreeFindFileToggle<CR>` | Toggle file explorer on current file |

### Fuzzy Finder (Telescope)
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<leader>ff` | Normal | `:Telescope find_files<cr>` | Fuzzy find files in current directory |
| `<leader>fr` | Normal | `:Telescope oldfiles<cr>` | Fuzzy find recent files |
| `<leader>fs` | Normal | `:Telescope live_grep<cr>` | Find string in current directory |
| `<leader>fc` | Normal | `:Telescope grep_string<cr>` | Find string under cursor |

#### Telescope Navigation (Insert Mode)
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<C-k>` | Insert | `actions.move_selection_previous` | Move to previous item |
| `<C-j>` | Insert | `actions.move_selection_next` | Move to next item |
| `<C-q>` | Insert | `actions.send_selected_to_qflist` | Send to quickfix list |

### Git Signs (gitsigns.nvim)
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `]c` | Normal | `gs.next_hunk()` | Next git hunk |
| `[c` | Normal | `gs.prev_hunk()` | Previous git hunk |
| `<leader>gb` | Normal | `gs.blame_line{full=true}` | Show git blame for current line |
| `<leader>gd` | Normal | `gs.diffthis` | Show git diff for current file |

### LSP (Language Server Protocol)
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `gd` | Normal | `vim.lsp.buf.definition` | Go to definition |
| `K` | Normal | `vim.lsp.buf.hover` | Show hover information |
| `<leader>ca` | Normal | `vim.lsp.buf.code_action` | Show code actions |
| `<leader>rn` | Normal | `vim.lsp.buf.rename` | Rename symbol |

### Autocompletion (nvim-cmp)
| Key | Mode | Function | Description |
|-----|------|----------|-------------|
| `<C-j>` | Insert | `cmp.mapping.select_next_item()` | Next completion item |
| `<C-k>` | Insert | `cmp.mapping.select_prev_item()` | Previous completion item |
| `<C-Space>` | Insert | `cmp.mapping.complete()` | Trigger completion |
| `<CR>` | Insert | `cmp.mapping.confirm({ select = false })` | Confirm completion |

## Default Neovim Keybindings (Essential)

### Normal Mode Navigation
| Key | Function | Description |
|-----|----------|-------------|
| `h` | Move left | Move cursor left one character |
| `j` | Move down | Move cursor down one line |
| `k` | Move up | Move cursor up one line |
| `l` | Move right | Move cursor right one character |
| `w` | Next word | Move to beginning of next word |
| `e` | End of word | Move to end of current word |
| `b` | Previous word | Move to beginning of previous word |
| `0` | Beginning of line | Move to beginning of line |
| `^` | First non-blank | Move to first non-blank character |
| `$` | End of line | Move to end of line |
| `gg` | Top of file | Move to first line of file |
| `G` | Bottom of file | Move to last line of file |
| `{` | Previous paragraph | Move to previous paragraph |
| `}` | Next paragraph | Move to next paragraph |
| `%` | Matching bracket | Jump to matching bracket/parenthesis |

### Text Objects
| Key | Function | Description |
|-----|----------|-------------|
| `iw` | Inner word | Select word under cursor |
| `aw` | Around word | Select word and surrounding space |
| `is` | Inner sentence | Select sentence |
| `as` | Around sentence | Select sentence and surrounding space |
| `ip` | Inner paragraph | Select paragraph |
| `ap` | Around paragraph | Select paragraph and surrounding space |
| `i"` | Inner quotes | Select text inside quotes |
| `a"` | Around quotes | Select text and quotes |
| `i(` | Inner parentheses | Select text inside parentheses |
| `a(` | Around parentheses | Select text and parentheses |
| `i{` | Inner braces | Select text inside braces |
| `a{` | Around braces | Select text and braces |
| `i[` | Inner brackets | Select text inside brackets |
| `a[` | Around brackets | Select text and brackets |

### Editing Commands
| Key | Function | Description |
|-----|----------|-------------|
| `i` | Insert mode | Enter insert mode at cursor |
| `a` | Append | Enter insert mode after cursor |
| `o` | Open line below | Create new line below and enter insert mode |
| `O` | Open line above | Create new line above and enter insert mode |
| `r` | Replace character | Replace single character |
| `R` | Replace mode | Enter replace mode |
| `s` | Substitute | Delete character and enter insert mode |
| `S` | Substitute line | Delete line and enter insert mode |
| `c` | Change | Change text (requires motion) |
| `cc` | Change line | Change entire line |
| `C` | Change to end | Change from cursor to end of line |
| `d` | Delete | Delete text (requires motion) |
| `dd` | Delete line | Delete entire line |
| `D` | Delete to end | Delete from cursor to end of line |
| `x` | Delete character | Delete character under cursor |
| `X` | Delete backward | Delete character before cursor |
| `y` | Yank (copy) | Copy text (requires motion) |
| `yy` | Yank line | Copy entire line |
| `Y` | Yank to end | Copy from cursor to end of line |
| `p` | Paste after | Paste after cursor |
| `P` | Paste before | Paste before cursor |
| `u` | Undo | Undo last change |
| `<C-r>` | Redo | Redo last undone change |
| `.` | Repeat | Repeat last command |

### Visual Mode
| Key | Function | Description |
|-----|----------|-------------|
| `v` | Visual mode | Enter visual mode |
| `V` | Visual line | Enter visual line mode |
| `<C-v>` | Visual block | Enter visual block mode |
| `gv` | Reselect | Reselect last visual selection |

### Search and Replace
| Key | Function | Description |
|-----|----------|-------------|
| `/` | Search forward | Search forward for pattern |
| `?` | Search backward | Search backward for pattern |
| `n` | Next match | Go to next search match |
| `N` | Previous match | Go to previous search match |
| `*` | Search word forward | Search for word under cursor (forward) |
| `#` | Search word backward | Search for word under cursor (backward) |
| `:s/old/new/g` | Replace in line | Replace all occurrences in current line |
| `:%s/old/new/g` | Replace in file | Replace all occurrences in file |
| `:%s/old/new/gc` | Replace with confirm | Replace with confirmation |

### Command Mode
| Key | Function | Description |
|-----|----------|-------------|
| `:` | Command mode | Enter command mode |
| `:w` | Write | Save file |
| `:q` | Quit | Quit Neovim |
| `:wq` | Write and quit | Save and quit |
| `:q!` | Force quit | Quit without saving |
| `:e filename` | Edit file | Open file for editing |
| `:help` | Help | Show help |
| `:set` | Set options | Configure Neovim options |

### Marks and Jumps
| Key | Function | Description |
|-----|----------|-------------|
| `ma` | Set mark a | Set local mark 'a' |
| `mA` | Set mark A | Set global mark 'A' |
| `'a` | Jump to mark a | Jump to line with mark 'a' |
| `\`a` | Jump to mark a | Jump to exact position of mark 'a' |
| `<C-o>` | Jump back | Jump to previous location |
| `<C-i>` | Jump forward | Jump to next location |

### Macros
| Key | Function | Description |
|-----|----------|-------------|
| `qa` | Record macro | Start recording macro in register 'a' |
| `q` | Stop recording | Stop recording macro |
| `@a` | Play macro | Play macro from register 'a' |
| `@@` | Repeat macro | Repeat last played macro |

### Folding
| Key | Function | Description |
|-----|----------|-------------|
| `zf` | Create fold | Create fold |
| `za` | Toggle fold | Toggle fold under cursor |
| `zo` | Open fold | Open fold under cursor |
| `zc` | Close fold | Close fold under cursor |
| `zr` | Reduce fold level | Open one level of folds |
| `zm` | More fold level | Close one level of folds |
| `zR` | Open all folds | Open all folds |
| `zM` | Close all folds | Close all folds |

### Registers
| Key | Function | Description |
|-----|----------|-------------|
| `"ay` | Yank to register a | Copy to register 'a' |
| `"ap` | Paste from register a | Paste from register 'a' |
| `"_d` | Delete to black hole | Delete without copying |
| `"+y` | Yank to clipboard | Copy to system clipboard |
| `"+p` | Paste from clipboard | Paste from system clipboard |

## Configuration Details

### Installed Plugins
- **lazy.nvim**: Plugin manager
- **tokyonight.nvim**: Colorscheme with transparency
- **nvim-tree.lua**: File explorer
- **telescope.nvim**: Fuzzy finder
- **which-key.nvim**: Keybinding hints
- **gitsigns.nvim**: Git integration
- **nvim-treesitter**: Syntax highlighting
- **nvim-lspconfig**: Language server support
- **nvim-cmp**: Autocompletion
- **LuaSnip**: Snippet engine

### LSP Servers Configured
- **lua_ls**: Lua language server
- **rust_analyzer**: Rust language server
- **pyright**: Python language server
- **ts_ls**: TypeScript/JavaScript language server

### Treesitter Languages
- Lua, Vim, JavaScript, TypeScript, HTML, CSS, JSON, YAML, Markdown, Bash, Python, Rust, Go, C

---

*Generated from ~/.config/nvim configuration*
*Last updated: $(date)*