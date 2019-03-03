title: Setup develop environment on Mac
date: 2015-07-02 22:03:29
tags: Tools
categories: R&D
---

# XCode
Install XCode from Apple App store, and you might need XCode Command Line Developer Tools, which is needed to build e.g. Ruby gem native extensions and install other system packages.

    xcode-select --install

To check it after installation

    gcc --version

<!--more-->

# HomeBrew

We need packages manager on Mac

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"


# iTerm2

[iTerm2](http://www.iterm2.com/#/section/home) is a replacement for the native Terminal app that ships with Mac OS X.
Download and install it. And go to iTerm 2 => Preferences => Profiles => General, check “Copy to clipboard on selection”, check [themes](http://iterm2colorschemes.com/) for fancy colors, "Solarized Dark Higher Contrast" is the one I am using.

# Zsh
[Oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) is the awesome Zsh framework.

Install it via curl

    sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

or via wget

    sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

and change zsh to be default:

    chsh -s $(which zsh)

Enable plugins from .zshrc file

    plugins=(git rails ruby gem rake bundler brew osx vagrant wd)

and choose a theme

    ZSH_THEME="blinks"

More themes could be found from oh-my-zsh github page.


# Tmux

Tmux is a terminal multiplexer, which lets you switch between several programs in one terminal and easily attach and detach session towards remote server

    brew install tmux

and just grab someone's config file, e.g. [this one](https://github.com/tony/tmux-config)

# Vim

    brew install Vim

Might need to `rehash` after the latest version installed.

Configuration is time consuming, so I just take from [spf13](https://github.com/spf13/spf13-vim)

My personal created .vimrc.bundles.local looks like:

    Bundle 'Chiel92/vim-autoformat'
    Bundle 'avakhov/vim-yaml'
    Bundle 'jmcantrell/vim-virtualenv'
    Bundle 'elixir-lang/vim-elixir'

And customized .vimrc.local

```
    set shell=/bin/zsh

    nnoremap gV gUiW
    nnoremap gv guiW

    nnoremap <C-h> ^
    nnoremap <C-l> $

    set guifont=DejaVu\ Sans\ Mono\ for\ Powerline\ 9
    set laststatus=2

    noremap <F3> :Autoformat<CR>

    au BufWrite * :Autoformat

    let g:ackprg = 'ag --vimgrep'
```

and my .vimrc.before.local file is

    let g:spf13_no_autochdir = 1
    let g:spf13_bundle_groups = ['general', 'programming', 'misc', 'html', 'python', 'ruby', 'javascript', 'youcompleteme']
    let g:airline_powerline_fonts = 1

Furthermore, your might need [the silver searcher](https://github.com/ggreer/the_silver_searcher) to speedup your searching.

And if you get a warning message like

    "ycm_client_support.[so|pyd|dll] and ycm_core.[so|pyd|dll] not detected; you need to compile YCM before using it."

Then just do

    cd .vim/bundle/YouCompleteMe
    ./install.sh

should solve it!

Install Powerline

    pip install powerline-status

Download [Powerline Fonts](https://github.com/powerline/fonts) and run `./install`, then from "Profiles" => "Text" => "Font" => "Change Font", to e.g. "Source Code Pro for Powerline".

And you might find it's convenient to map ESC key to CapsLock, I manage to do so using [Seil](https://pqrs.org/osx/karabiner/seil.html.en). 

![](/images/Seil.png)

Furthermore, [Karabiner](https://pqrs.org/osx/karabiner/) could be interesting if you want to customize your keyboard more.

To make the solarized theme work properly in terminal, it is good to download from [solarized](http://ethanschoonover.com/solarized) home page. Then import it form iTerm 2 => Preferences => Profiles => profiles => Colors => Load Presets... => Import...

Finally a screen shot
![](/images/dev_env.png)
Enjoy! :)
