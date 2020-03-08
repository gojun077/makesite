<!-- title: Setting up vim syntastic on various linux distros -->

I use several different notebooks at home and at work that have different Linux distros installed, namely, Archlinux, Ubuntu 16.04 and Fedora 26. As a systems engineer, using vi/vim is a necessity as it is installed by default on every *nix machine even if no other editor is available. While I prefer Emacs with Flycheck when programming, I use vim extensively day-to-day to edit shell scripts, yaml files, and other structured text. During this work a syntax-checker is very helpful for catching errors. For this I use the vim plugin syntastic.

Syntastic provides vim with linter/syntax-checking integration for various programming languages and markup formats. While it doesn't work on-the-fly like the syntax checkers in traditional IDE's or Emac's Flycheck, it does check syntax every time a file is saved with :w

Recent versions of vim have a native plugin manager enabled by default. Vim plugin files installed through your package manager (pacman, apt-get, dnf / yum) are usually written to /usr/share/vim/vimfiles/plugin/ but you can also set the plugin directory to a location under ~/.vim if you add it to your runtimepath. You can check the current setting of your runtimepath (rtp) in vim by entering:

```
: set rtp

runtimepath=~/.vim,/usr/share/vim/vimfiles,/usr/share/vim/vim80,/usr/share/vim/vimfiles/after,~/.vim/after,/usr/share/vim/vimfiles/plugin/
```

To enable the default vim plugin manager, edit `~/.vimrc` and add the following directory to your default run time path:

`set rtp+=/usr/share/vim/vimfiles`

Note that on Fedora, in addition to installing the `vim-syntastic` package, you also have to install a package for each language or DSL you want to use with syntastic; i.e. `vim-syntastic-python` for Python 2 and 3 linting, `vim-syntastic-sh` for shellcheck integration, `vim-syntastic-ansible` for checking ansible `yaml` files and playbooks, etc.

On Archlinux, instead of setting `rtp`, you need to specify `packpath` in your `.vimrc` as follows:

`set packpath=/usr/share/vim/vimfiles/plugin/`

If you create a `~/.vim` directory (where you should place manually downloaded or git-cloned plugins), vim will also check this path as part of `rtp`.

You can see my personal .vimrc from my dotfiles repo at the link below:
https://github.com/gojun077/jun-dotfiles/blob/master/vimrc

Here is a screenshot of vim + syntastic with shellcheck output for a Bash shell script:

![shellcheck](../../files/blog/vim_syntastic_shellcheck.png)
