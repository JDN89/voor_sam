### KEYS
spatie + sk : search keybindings
spatie + sh : searh help  (je kan zo documentatie van neovim en plugins opzoeken en openen in neovim zelf)
spatie + sg : search grep
spatie + ff : search files

ctrl + w : opties om screen te splitte etc. zie je onderaan verschijnen

spatie + db :breakpoint zetten
step,... zijn zelfde keybindings als in intelij

in normal mode en denk ook visual triggert s de flash plugin. Zo kan je exact naar een positie in de codebase springen

Ik heb gisterenavond nog de Go debug adapter kunnen laten werken.
Ik moest gewoon delve zelf nog installeren op mijn pc

voor python zal je volgende doc moeten lezen 
- https://github.com/mfussenegger/nvim-dap-python
- Requires __debugpy__

### PYthon LSP
- pyright installeren op je laptop
- toevoegen aan de locatie waar de andere lsp configs staan

  ```
  ---@brief
---
--- https://github.com/microsoft/pyright
---
--- `pyright`, a static type checker and language server for python

local function set_python_path(path)
  local clients = vim.lsp.get_clients {
    bufnr = vim.api.nvim_get_current_buf(),
    name = 'pyright',
  }
  for _, client in ipairs(clients) do
    if client.settings then
      client.settings.python = vim.tbl_deep_extend('force', client.settings.python, { pythonPath = path })
    else
      client.config.settings = vim.tbl_deep_extend('force', client.config.settings, { python = { pythonPath = path } })
    end
    client.notify('workspace/didChangeConfiguration', { settings = nil })
  end
end

---@type vim.lsp.Config
return {
  cmd = { 'pyright-langserver', '--stdio' },
  filetypes = { 'python' },
  root_markers = {
    'pyproject.toml',
    'setup.py',
    'setup.cfg',
    'requirements.txt',
    'Pipfile',
    'pyrightconfig.json',
    '.git',
  },
  settings = {
    python = {
      analysis = {
        autoSearchPaths = true,
        useLibraryCodeForTypes = true,
        diagnosticMode = 'openFilesOnly',
      },
    },
  },
  on_attach = function(client, bufnr)
    vim.api.nvim_buf_create_user_command(bufnr, 'LspPyrightOrganizeImports', function()
      client:exec_cmd({
        command = 'pyright.organizeimports',
        arguments = { vim.uri_from_bufnr(bufnr) },
      })
    end, {
      desc = 'Organize Imports',
    })
    vim.api.nvim_buf_create_user_command(bufnr, 'LspPyrightSetPythonPath', set_python_path, {
      desc = 'Reconfigure pyright with the provided python path',
      nargs = 1,
      complete = 'file',
    })
  end,
}
  ```
