---
title: Setup your shell
author: Sra9Ziit
author_link: https://profile.intra.42.fr/users/aeddaoud
description: Using the default config fo any shell in a nightmare for me, in
  this article ill share with you how i setup my shell config and the plugins i
  use.
tags:
  - tools
  - tricks
published: true
date: 2021-12-03T20:28:42.518Z
---
Having a proper shell config is critical to me, so i decided to share with you how i setup my config and plugins that saves me a ton of time every day.

Since i do every thing in the terminal it is so important to have a beautiful and a smart one.

if you use zsh you may want to give oh my zsh a try, it is to feature rich and can make your life easier.

so let's start by installing it.

*before doin't so you may consider doing a backup. just in case.*

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

now that we have oh my zsh installed and ready to use you may want to choose a deferent theme than the default one.

here you can find a list of themes comes preinstalled with oh my zsh, but you can find other themes or even make your own. [oh my zsh themes](https://github.com/ohmyzsh/ohmyzsh/tree/master/themes)

now we have a beautifully looking shell, but that's not enough we need to be helpful, and then when plugins comes into the picture.

with oh my zsh plugins you can save your self a ton of time of searching in the man pages for the flags you forget all the time just by clicking the tab button, it will list if front of you the different flags and options and you can choose between them using the arrow keys.

oh my zsh by default comes with a set of plugins and aliases pre installed and activated.

now let's start by installed a few plugins of those, starting by auto completion oooh yeah.

run the command below to install the auto completion plugin for zsh.

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

now that we have the plugins properly installed we need to activate it, to do so you need to its name to a plugins list in your **~/.zshrc** file in your home directory.

```shell
plugins=( 
    # other plugins...
    zsh-autosuggestions
)
```

after adding the name of the plugins you need to reload your shell session by closing and opening ur terminal or just by running the command below.

```shell
source ~/.zshrc
```

after installing your first plugins you can do the same process with any oh my zsh plugin.

i suggestion the following plugins.

* [Zsh Syntax Highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
* [You should use](https://github.com/MichaelAquilina/zsh-you-should-use)
* [Sudo](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/sudo)

if you want to take if further you take a look on this list of plugins and pick what fits you.

[Oh My Zsh Plugins](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/)

also if you use a lot of command with the same flags every time. maybe it's time to make a [shell functions](https://www.gnu.org/software/bash/manual/html_node/Shell-Functions.html) for them, you will thank me later.

for example if you forget to compile using the flags like me you can make a function that will add the flags for you.

this is an example.

```shell
function fcc() {
	gcc -Wall -Wextra -Werror -fsanitize=address $@ && ./a.out
}
```

this function will compile the given files with the **\-Wall -Werror -Wextra -fsanitize=address** flags also run the binary file if the compilation succeed.

now we have a proper shell, we need a proper files editor, i use vim to do every thing if you also use vim, i suggestion to take a look on this [neovim](https://github.com/neovim/neovim) config. [Lunar Vim](https://github.com/LunarVim/LunarVim).

> i bet my vim is better than your vscode.

unfortunately you can't install **Lunar vim** on 42 iMac's easily, you need some pre installed such rust, cargo, npm,

but that's not a problem you can make your own config.