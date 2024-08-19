---
title: "The best beginnger zsh configuration"
meta_title: ""
description: "this is meta description"
date: 2023-08-19
image: "https://img.youtube.com/vi/8PRP1Z5s2WY/0.jpg"
categories: ["Software Engineering"]
author: "Sam Ly"
tags: ["Unix Configuration"]
draft: false
---

[Watch full video here.](https://www.youtube.com/watch?v=8PRP1Z5s2WY)

#  The best beginner zsh configuration

This article will detail a super beginner friendly zsh configuration, including all the background information you will need to create your own zsh configuration.

## Defining the shell and terminal

Before w get started with the actual configuration, it is important to understand the difference between the shell and the terminal. Although closely related, they are actually distinct programs on your computer.

According to wikipedia

>A **shell** is a computer program that exposes an [operating system](https://en.wikipedia.org/wiki/Operating_system "Operating system")'s services to a human user or other programs.

In other words, a shell is a type of program that lets the user interact with the computer. 

Bash and zsh are examples of CLI shell programs. They take your commands in the form of text, then executes it.

Now, in order to actually send your commands to this shell, you will need a terminal.

A terminal (aka terminal emulator) is a program that you type into, which then sends your command to the shell. 

<blockquote class="imgur-embed-pub" lang="en" data-id="a/Oj30OVF"  ><a href="//imgur.com/a/Oj30OVF">command demo</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

Remember, the terminal and shell are separate programs. But you will need both to actually use your computer's CLI. This is important to understand because some configuration happen at the shell, while others happen at the terminal.

## Install zsh, and make it your default shell

If you haven't already, you will need to install zsh and make it your default shell. 

On macOS, zsh is installed by default. However, on systems, you may need to install zsh yourself.

You can check also what shell you are by typing `echo $SHELL`

## Configuration 

Zsh configuration starts in a file named `.zshrc` located in the home directory. Make a backup of this file if it already exists and create a new `.zshrc` file.

This file is a startup script for zsh. Whenver a new shell environment is created, this script is executed. We can include a series of commands in this file to achieve our desired configuration. 

*Side note: this type of configuration is known as imperative configuration as your are configuring a program by giving it a series of instructions that modify the system's state. Some programs can be configured declaratively. Learn more about imperative vs declarative code here [Imperative vs Declarative Code](/blog/post-1)*

To demonstrate this, you can add `echo "hello world"` to your new `.zshrc` file. All this command does is print "hello world" to the terminal.

Now, when you open a new terminal window you will notice a "hello world" printed before the prompt.

## Plugins

Plugins are how we will achieve most of our additional features. Plugins are a shell level configuration because they modify the underlying behavior of zsh and will persist even after changing your terminal application.

We will be installing 3 plugins:
1. [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
2. [zsh-autocomplete](https://github.com/zsh-users/zsh-syntax-highlighting)
3. [p10k](https://github.com/romkatv/powerlevel10k)

To get started, create a directory named `zsh_plugins`.

Now, `cd` into this directory and clone the following repos with the following commands

```sh
git clone --depth=1 git@github.com:marlonrichert/zsh-autocomplete.git
git clone --depth=1 git@github.com:zsh-users/zsh-syntax-highlighting.git
git clone --depth=1 git@github.com:romkatv/powerlevel10k.git
```

### Enabling autocomplete and syntax highlighting

Now that we have the plugins downloaded, we can enable them using our `.zshrc`.

``` zsh
setopt interactivecomments
source ~/zsh_plugins/zsh-autocomplete/zsh-autocomplete.plugin.zsh

source ~/zsh_plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

Add these lines to enable autocomplete and syntax highlighting. 

Do not yet enable p10k as that requires additional configuration.

Now save your changes to `.zshrc` and open a new terminal. Your prompt will have an autocomplete menu that you can navigate with your arrow keys and syntax highlighting.

*Side note: There is another popular plugin called autosuggestions, however this plugin might not work as expected. Instead of a true autocomplete, it saves your previous commands and can only give suggestions based on your previous commands, leading to some unexpected behavior. *

### Enabling p10k

This plugin requires the use of a nerdfont. A nerdfont is just a font that includes some extra icons that are used as decorations in the terminal.

So before you actually enable this plugin, change your terminal font to a nerd font which can be found at www.nerdfonts.com.

Now that we have our font installed and enabled, we can enable our p10k plugin the same way we have enabled all our other plugins. 

```sh
source ~/zsh_plugins/powerlevel10k/powerlevel10k.zsh-theme
```

Now, when you open a new terminal, you will be greeted with the p10k configuration wizard.  These configurations are saved to a file called `.p10k.zsh` in your home directory.

If you want my exact configurations, my `.p10k.zsh` file can be found [here](https://github.com/samly100405/zsh-config)

Once you reach the page asking about instant prompt, I recommend enabling it, and applying these changes to your .zshrc file. 

Your `.zshrc` file should now look something like this.
```sh
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.

if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

source ~/zsh_plugins/powerlevel10k/powerlevel10k.zsh-theme

setopt interactivecomments
source ~/zsh_plugins/zsh-autocomplete/zsh-autocomplete.plugin.zsh

source ~/zsh_plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh
```

I recommend moving the lines around so that the commands for each plugin are grouped together.
```sh
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.

if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

source ~/zsh_plugins/powerlevel10k/powerlevel10k.zsh-theme
# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

setopt interactivecomments
source ~/zsh_plugins/zsh-autocomplete/zsh-autocomplete.plugin.zsh

source ~/zsh_plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

```

## Other configuration

This line gives the autocomplete menu some color. 
```sh
# zsh-autocomplete configs
zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"
```

We can improve our command history feature with the following configurations

These 3 lines explicitly where our history is stored. That way we always know where our command history is.
```sh
HISTSIZE=5000
HISTFILE=~/.zsh_history
SAVEHIST=$HISTSIZE
```

These lines work together to prevent duplicate commands from being saved into your history. 
```sh
HISTDUP=erase
setopt hist_ignore_all_dups
setopt hist_save_no_dups
setopt hist_ignore_dups
setopt hist_find_no_dups
```

This line allows you to prevent a command from being saved to the history by adding a space in front. I rarely use this feature, but it does come in handy every once in a while.
```sh
setopt hist_ignore_space
```

These two lines bind control p and n to history search because I'm too lazy to move my hand to the arrow keys. 
```sh
bindkey '^p' history-search-backward
bindkey '^n' history-serach-forward
```

## Aliases

An alias is a tool we can use in shell environments to rename commands. 

A common one is this
```sh
alias ls="ls --color"
```
This makes it so that every time you run ls, you are actually running ls--color.

Aliases can also be used to to make long commands shorter.

```sh
alias ga="git add"
alias gc="git commit -m"
glias gst="git status"
```
This way, you can reduce the amount of keystrokes needed for commands you use often.

You can put these aliases in your `.zshrc` file so that they are always there when you open a new terminal.

## Color Schemes

Configuring the color scheme happens at the terminal, and will vary for the different terminal emulators.

Some terminal emulators make this easier, and some make it harder.

For now, you can manually change the colors in order to your desired color scheme. I use Atom One Dark Pro's color palette. 

## About Plugin managers

Plugin managers are a programs that help you install and enable zsh plugins. I personally don't use nor recommend using these programs because of the following reasons.

### Reason 1: Overcomplicates things

Learning how about how UNIX works and how to configure it is already a pretty difficult thing to do. The last thing you need is more things to learn about. 

In order to use a plugin manager, you need to specifically put in time and effort into learn said plugin manager. Not only that, but you also have to decide on which plugin manager you are going to use. Even for a UNIX nerd like me, I don't want to spend time doing things like that.

### Reason 2: More places for things to go wrong

Plugin managers themselves are pieces of software. They can have bugs too. Although rare, these bugs can make it into releases. 

Take a look at the GitHub issues page for oh-my-zsh. There are constantly new issues with the bug label being added.

Granted, a lot of these aren't actually bugs and are user errors, but that just feeds back into my previous point. These plugin managers are actually a lot harder for beginners to learn than what most people think.

Furthermore, some plugins don't play nice with plugin managers, and are recommended to be installed manually. 

### Reason 3: I don't need it

These plugin managers only really become useful once you start using a lot of plugins. But I've only ever needed these three. And in my opinion, if you need that many plugins, your config is a little bit unreasonable. 

## Conclusion

I hope you found this article helpful. Feel free to let me know if you run into any issues.