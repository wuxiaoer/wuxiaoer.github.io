---
published: true
layout: post
title: Using the Vundle to Manage Vim Plugins
category: Tech 
tags: 
  - vim 
time: 2016.05.27 23:18:19
excerpt: NULL

---

Use the Vundle tools to manage the vim plugins

First, Download Vundle

> git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim 


Second, Add the Vundle.vim path to the .vimrc file, as following:

```
" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/vundle/
call vundle#rc()

" alternatively, pass a path where Vundle should install plugins "let path = '~/some/path/here'
"call vundle#rc(path) " let Vundle manage Vundle, required
Plugin 'gmarik/vundle'
```

There are two ways to install the vim plugins:

- Install from github

if you install the vim plugins from github, first searching the plugin in the github, and then using the following command to install it.

> Plugin 'user/plugin_name'

- Install from vim-scripts websites

if you install plugins from vim-scripts from the website  http://vim-scripts.org/vim/scripts.html , using the following the command:

> Plugin 'plugin_name'

or you can use PluginSearch to search for you wanted plugins. 

using VIM to open any files, and then under the command mode, input the following command:

> :PluginSearch

and then select the plugin that you wanted, the last enter the "i" key to install the selected plugin.

