title: New Vim Hack
date: 2016-10-14 12:51:18
tags: Tools 
categories: R&D
---


Previously I am using [spf13](https://github.com/spf13/spf13-vim) for my vim configuration. However it is a bit sluggish for me since it includes too much settings and plugins which might not be needed for my daily usage, therefore I deicide to move to this [vimrc](https://github.com/amix/vimrc).

New plugins installed manually such as vim-rails, vim-autoformat, YouCompleteMe, tagbar, vim-ctrlp-tjump etc.

Ctags is also needed for go to definition.

<!--more-->

I remove/comment out the line to have deafault key mapping for multiple selection in plugins_config.vim 

    let g:multi_cursor_next_key="\<C-s>"


Here is how it looks for my_configs.vim

{% gist chuanjin/f302b7c4d852f13bdaaaaea366b3dbac%}


Final look:

![](/images/new_vim.png)
