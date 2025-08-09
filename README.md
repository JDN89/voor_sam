### KEYS
spatie + sk : search keybindings \
spatie + sh : searh help  (je kan zo documentatie van neovim en plugins opzoeken en openen in neovim zelf) \
spatie + sg : search grep \
spatie + ff : search files \

ctrl + w : opties om screen te splitte etc. zie je onderaan verschijnen \

spatie + db :breakpoint zetten \
ste. intop,... zijn zelfde keybindings als in intelij \  f6 f7 f8 f9

in normal mode en denk ook visual triggert 's' de flash plugin. Zo kan je exact naar een positie in de codebase springen

Ik heb gisterenavond nog de Go debug adapter kunnen laten werken.
Ik moest gewoon delve zelf nog installeren op mijn pc

voor python zal je volgende doc moeten lezen 
- https://github.com/mfussenegger/nvim-dap-python
- Requires __debugpy__

### PYthon LSP
- pyright installeren op je laptop
- toevoegen aan de locatie waar de andere lsp configs staan

https://github.com/neovim/nvim-lspconfig/blob/master/lsp/pyright.lua \
kopieer pyright.lua naar nvim/lsp/pyright.lua \
- zet boven return __---@type vim.lsp.Config__
