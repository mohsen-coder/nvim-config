# Neovim Configuration

Hi guys, I'm going to teach you how to configure Neovim like this:

## Installation

To configure Neovim we need a plugin manager. there are some plugin managers like vim-plug, Pathogen, Vundle and etc. We'll use vim-plug for this purpose.

## Install vim-plug

If you use Windows or Flatpack(Linux distribute) as your operating system, go to the vim-plug repository and follow the instruction otherwise copy command below in your terminal and execute it to install vim-plug.

vim-plug repo: [https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug)


```shel
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

after installing vim-plug navigate to `~/.config/nvim` (if nvim directory not exist create yours) then create a file called `init.vim`.

nvim use this file as it's configuration file. so let's start configure it.

## init.vim structure
init.vim has its own structure. here we are not going to dive deep in the structure just you should know basic thing like where you must add plugin or set an option and etc.

the strucure is:

```vim
call plug#begin()
" We add plugins here
Plug 'sonph/onehalf', { 'rtp': 'vim' }
Plug 'https://github.com/preservim/nerdtree'
Plug 'pangloss/vim-javascript'
Plug 'prettier/vim-prettier', { 'do': 'yarn install --frozen-lockfile --production' }
call plug#end()

" set options
:set number

" Global variables
" Note that global variables start with g:[variable's name]
" for example:
let g:javascript_plugin_jsdoc = 1


" wire other config here, like key mapping and etc.
nnoremap <C-f> :NERDTreeFind<CR>
nnoremap <silent> {Previous-Mapping} :TmuxNavigatePrevious<cr>


autocmd BufEnter *.{js,jsx,ts,tsx} :syntax sync fromstart
autocmd BufLeave *.{js,jsx,ts,tsx} :syntax sync clear

```
this configuration file is just an example. don't copy it in your init.vim file :)

after write config file we should run `:PlugInstall` to install plugins.

Note: if `:PlugInstall` not work, once exit the file and again open it and run the command again.

some of plugins has their own options that you should set them in `init.vim` file or you can customize key bindings.

teaching is enough :)

## My Nvim Configuration
you can copy it in your `init.vim` file and run `:PlugInstall`.
```vim
call plug#begin()
Plug 'sonph/onehalf', { 'rtp': 'vim' }
Plug 'https://github.com/preservim/nerdtree'
Plug 'pangloss/vim-javascript'
Plug 'leafgarland/typescript-vim'
Plug 'peitalin/vim-jsx-typescript'
Plug 'styled-components/vim-styled-components', { 'branch': 'main' }
Plug 'jparise/vim-graphql'
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'christoomey/vim-tmux-navigator'
Plug 'alvan/vim-closetag'
Plug 'jiangmiao/auto-pairs'
Plug 'terryma/vim-multiple-cursors'
Plug 'prettier/vim-prettier', { 'do': 'yarn install --frozen-lockfile --production' }
call plug#end()


:set number
:set autoindent
:set tabstop=4
:set shiftwidth=4
:set smarttab
:set softtabstop=4
:set mouse=a
:set cursorline
:colorscheme onehalfdark


let g:javascript_plugin_jsdoc = 1
let g:javascript_plugin_ngdoc = 1
let g:javascript_plugin_flow = 1

let g:coc_global_extensions = [
	\ 'coc-tsserver'
	\]

let g:tmux_navigator_no_mappings = 1
" let g:typescript_indent_disable = 1
let g:closetag_filenames = '*.html,*.xhtml,*.xml,*.vue,*.phtml,*.js,*.jsx,*.ts,*.tsx,*.coffee,*.erb'

let g:multi_cursor_use_default_mapping=0

" Default mapping
let g:multi_cursor_start_word_key      = '<C-n>'
let g:multi_cursor_select_all_word_key = '<A-n>'
let g:multi_cursor_start_key           = 'g<C-n>'
let g:multi_cursor_select_all_key      = 'g<A-n>'
let g:multi_cursor_next_key            = '<C-n>'
let g:multi_cursor_prev_key            = '<C-p>'
let g:multi_cursor_skip_key            = '<C-x>'
let g:multi_cursor_quit_key            = '<Esc>'


nnoremap <leader>n :NERDTreeFocus<CR>
nnoremap <C-n> :NERDTree<CR>
nnoremap <C-t> :NERDTreeToggle<CR>
nnoremap <C-f> :NERDTreeFind<CR>


nnoremap <silent> {Left-Mapping} :TmuxNavigateLeft<cr>
nnoremap <silent> {Down-Mapping} :TmuxNavigateDown<cr>
nnoremap <silent> {Up-Mapping} :TmuxNavigateUp<cr>
nnoremap <silent> {Right-Mapping} :TmuxNavigateRight<cr>
nnoremap <silent> {Previous-Mapping} :TmuxNavigatePrevious<cr>


autocmd BufEnter *.{js,jsx,ts,tsx} :syntax sync fromstart
autocmd BufLeave *.{js,jsx,ts,tsx} :syntax sync clear

```

## Tmux configuration
To use vim with tmux you must install tmux first. then to configure tmux navigate to `home directory` then create a file called `.tmux.conf` finally write configuration below and save it.
```bash
# remap prefix from 'C-b' to 'C-a'
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix


# split panes using | and -
bind | split-window -h
bind - split-window -v
unbind '"'
unbind %

bind r source-file ~/.tmux.conf


# switch panes using Alt-arrow without prefix
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D


# Enable mouse mode (tmux 2.1 and above)
set -g mouse on

######################
### DESIGN CHANGES ###
######################
# Setup status bar
set -g status-justify centre
set -g status-left-length 40
set -g status-left "#[fg=green]Session: #S #[fg=yellow]#I #[fg=cyan]#P"

# Solaried Themeing
set-option -g status-bg colour235 #base02
set-option -g status-fg colour136 #yellow

# pane number display
set-option -g display-panes-active-colour colour33 #blue
set-option -g display-panes-colour colour166 #orange

# clock
set-window-option -g clock-mode-colour colour64 #green

```
to use tmux wirte `tmux` command in terminal and execute it.
to open a horizontal session press `Ctrl + a -` and to open a vertical session press `Ctrl + a |`.
