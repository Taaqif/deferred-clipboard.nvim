<h1>
  deferred-clipboard.nvim
  <a href="https://github.com/EtiamNullam/deferred-clipboard.nvim/tags" alt="Latest SemVer tag">
    <img src="https://img.shields.io/github/v/tag/EtiamNullam/deferred-clipboard.nvim" />
  </a>
</h1>

## Overview

This plugin synchronizes the clipboard of your operating system with [`Neovim`](https://neovim.io)'s `unnamed` register, while avoiding the performance issue of `clipboard=unnamed` and `clipboard=unnamedplus`, by delaying it until focus change or `Neovim` exit.

It works both ways so you can `y`ank something in `Neovim` to be available in your OS, but also copy something in your OS and `p`ut in `Neovim`.

Apparently the performance issue is specific to `Neovim` and does not apply to `Vim`. See more details and track the status of the issue here:
https://github.com/neovim/neovim/issues/11804

## Requirements

- `Neovim`
- `Neovim` client which supports both focus change events - `FocusGained` and `FocusLost`

## Installation

Use your favorite package manager. For example [`vim-plug`](https://github.com/junegunn/vim-plug):

```vimscript
Plug 'EtiamNullam/deferred-clipboard.nvim'
```

## Usage

Basic example:

```lua
require('deferred-clipboard').setup()
```

NOTE: Some terminals and `Neovim` UIs do not support focus change events, so you might want to rely on `clipboard=unnamed` or `clipboard=unnamedplus` on them.

In that case set the `clipboard` option before running the `.setup()` function, this way it will be automatically disabled when focus change events support is detected and will stay enabled if they are not supported.

Example with the continuous sync as a fallback:

```lua
vim.o.clipboard = 'unnamedplus'

require('deferred-clipboard').setup()
```

## Known issues

- Won't trigger when `cmdline` is open/busy
