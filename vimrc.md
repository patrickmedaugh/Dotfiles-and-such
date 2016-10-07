" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

" let Vundle manage Vundle, required
Plugin 'gmarik/Vundle.vim'
Plugin 'tpope/vim-endwise'
Plugin 'Raimondi/delimitMate'
Plugin 'scrooloose/nerdtree'
Plugin 'skalnik/vim-vroom'
Plugin 'kien/ctrlp.vim'
Plugin 'Yggdroot/indentLine'
Plugin 'Valloric/YouCompleteMe'
Plugin 'hwartig/vim-seeing-is-believing'
call vundle#end()            " required

" =========================== Settings ===========================
set nocompatible              " be iMproved, required
filetype off                  " required

syntax on
set noswapfile

"No sounds
set visualbell

set shortmess+=I
set softtabstop=2
set tabstop=2 shiftwidth=2 expandtab
set expandtab " use spaces, not tabs (optional)
colorscheme peachpuff
set nu
set nowrap
set splitbelow
set guifont=Monaco:h16

let g:ctrlp_working_path_mode = 'cr'

" Detect file type for indentation below
:filetype indent on
" Use 2 space indentation on Ruby and YAML files
:autocmd FileType ruby,eruby,yaml,javascript,css,scss,html set ai sw=2 sts=2 et


" ================ Leader and other mappings =======================

"open files in new tabs by default"
let NERDTreeMapOpenInTab='t'

"save with leader w
nnoremap <Leader>w :w<CR>
"save and quit with w q
nnoremap wq :wq!<CR>
"quit with no save q q"
nnoremap qq :q!<CR>

"esc with j f quickly
inoremap jf <esc>
inoremap fj <esc>

"search highlighted word with K"
nnoremap K :grep! "\b<C-R><C-W>\b"<CR>:cw<CR>

map <C-i> :NERDTreeToggle<CR>

"easy pasting
map <Leader>p :r !pbpaste<CR>

"shortcuts for Ruby debugging
map <Leader>bb orequire 'byebug'; byebug<esc>:w<cr>
map <Leader>yy orequire 'pry'; binding.pry<esc>:w<cr>

"pane navigation
nnoremap w <C-w>

"seeing is believing
nmap  <M-r> <Plug>(seeing-is-believing-run)
xmap  <M-r> <Plug>(seeing-is-believing-run)
imap  <M-r> <Plug>(seeing-is-believing-run)

nmap  <M-m> <Plug>(seeing-is-believing-mark)
xmap  <M-m> <Plug>(seeing-is-believing-mark)
imap  <M-m> <Plug>(seeing-is-believing-mark)

" ================ Delete whitespace function =======================
function! <SID>StripTrailingWhitespaces()
    " Preparation: save last search, and cursor position.
    let _s=@/
    let l = line(".")
    let c = col(".")

    "associate the .es6 file extension with JavaScript
    autocmd BufRead,BufNewFile *.es6 setfiletype javascript

    " Do the business:
    %s/\s\+$//e
    " Clean up: restore previous search history, and cursor position
    let @/=_s
    call cursor(l, c)
endfunction

autocmd BufWritePre * :call <SID>StripTrailingWhitespaces() " strip trailing whitespace on save

