# 简单插件使用

记录一些开箱即用的vim插件

## airline(状态栏)

地址：[https://github.com/vim-airline/vim-airline](https://github.com/vim-airline/vim-airline "vim 状态栏插件")

依赖：需要PowerlineFonts

> ubuntu：`sudo apt-get install fonts-powerline`

设置：在vimrc启用PowerlineFonts

> `let g:airline_powerline_fonts=1`

## indentLine(缩进线)

地址：[https://github.com/Yggdroot/indentLine](https://github.com/Yggdroot/indentLine "vim缩进线")

设置：可以自定义颜色，背景，缩进字符

```vim
" 默认情况下indentLine会用灰色覆盖配色主题的颜色,如下可以使用配色方案的颜色
let g:indentLine_setColor=0

" 自定义颜色
" Vim
let g:indentLine_color_term = 239

" GVim
let g:indentLine_color_gui = '#A4E57E'

" none X terminal
let g:indentLine_color_tty_light = 7 " (default: 4)
let g:indentLine_color_dark = 1 " (default: 2)

" Background (Vim, GVim)
let g:indentLine_bgcolor_term = 202
let g:indentLine_bgcolor_gui = '#FF5F00'

" 设置自定义字符
let g:indentLine_char = 'c'

" 设置不同缩进级别使用不同字符
let g:indentLine_char_list = ['|', '¦', '┆', '┊']

" 默认不启用indentLine
let g:indentLine_enabled = 0
```

其他：对启用vim conceal功能的设置，看文档

## Completor(自动补全)

地址：[https://github.com/maralla/completor.vim](https://github.com/maralla/completor.vim "自动补全插件")

设置：completor对常见语言需指定解释器

```vim
" python 先使用pip安装jedi
let g:completor_python_binary='/usr/bin/python3'

" c/c++ 安装clang
let g:completor_clang_binary='/path/to/clang'

" go 安装gocode
let g:completor_gocode_binary='/path/to/gocode'

" js 安装tern、node和yarn或者npm,然后运行make js
let g:completor_node_binary='/path/to/node'

" Rust 安装racer
let g:completor_racer_binary='/path/to/racer'

" other languages
let g:completor_{filetype}_omni_trigger='<python regex>'

" example to css
let g:completor_css_omni_trigger='([\w-]+|@[\w-]*|[\w-]+:\s*[\w-]*)$'

" 使用tab键来选择补全
inoremap <expr> <Tab> pumvisible() ? "\<C-N>":"\<Tab>"
inoremap <expr> <S-Tab> pumvisible() ? "\<C-p>":"\<S-Tab>"
inoremap <expr> <cr> pumvisible() ? "\<C-y>":"\<cr>"

" 关闭自动补全，使用tab补全
let g:completor_auto_trigger = 0
inoremap <expr> <Tab> pumvisible() ? "<C-N>" : "<C-R>=completor#do('complete')<CR>"
```

其他：还支持以下的补全，需要安装对应的插件

> Ulitisnips：[ultisnips](https://github.com/SirVer/ultisnips)
>
> neosnippet：[completor-neosnippet](https://github.com/SirVer/ultisnips)
>
> neoinclude：[neoinclude](https://github.com/Shougo/neoinclude.vim)
>
> dictionary：[completor-dictionary](https://github.com/masawada/completor-dictionary)
>
> shell：[completor-shell](https://github.com/tokorom/completor-shell)
>
> tmux：[completor-tmux](https://github.com/ferreum/completor-tmux)
>
> swift：[completor-swift](https://github.com/maralla/completor-swift)
>
> Elixir：[alchemist.vim](https://github.com/slashmili/alchemist.vim)
>
> vim script：[completor-necovim](https://github.com/kyouryuukunn/completor-necovim)
>
> type script：[completor-typescript](https://github.com/maralla/completor-typescript)

Tips：compltetor还支持跳转定义，见wiki

## UltiSnips和vim-snippets(代码段补全)

地址：
[https://github.com/SirVer/ultisnips](https://github.com/SirVer/ultisnips "代码段补全插件，但不提供代码段")
[https://github.com/honza/vim-snippets](https://github.com/honza/vim-snippets "配合UltiSnips,提供设置好的代码段")

## Vim-gitgutter(对git追踪的文件显示已添加、修改、删除的行)

地址：[https://github.com/airblade/vim-gitgutter](https://github.com/airblade/vim-gitgutter "在符号列显示已操作的行")

## Vim-multiple-cursors(多行操作)

地址：[https://github.com/terryma/vim-multiple-cursors](https://github.com/terryma/vim-multiple-cursors "比原生多行操作方便")

## Codi(交互式便签)

地址：[https://github.com/metakirby5/codi.vim](https://github.com/metakirby5/codi.vim "支持多款脚本语言的交互式便签")

## Ctrlp(快速搜索)

地址：[https://github.com/kien/ctrlp.vim](https://github.com/kien/ctrlp.vim "可搜索文件、缓冲区、最近使用和tags")

## 更多插件，存放在opt目录下

coc.nvim：补全插件

delimitMate：智能补全符号

emmet：片段补全，比较多用于html和css

nerdcommenter：快速注释

undotree：强大的撤销功能

vim-easy-align：快速对齐

vim-signature：vim标签插件，和在标签之间跳转

vim-surround：快速给词添加环绕符号，如各种括号和标签配合repeat

vim-repeat：重复上一个插件的操作，只支持几款插件

vim-table-mode：插入表格，和将内容格式化为表格

goyo.vim：专注写作，去掉屏幕上的其他显示。配合limelight

limelight.vim：除当前正在编辑的行，其他颜色全部变暗

## 主题

vim-one：带powerline主题

nord-vim：有配套的bash主题，也带powerline主题
