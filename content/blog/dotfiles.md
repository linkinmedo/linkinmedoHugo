---
title: "The journey to dotfiles ZEN"
date: 2017-08-19T23:40:57+03:00
draft: false
---
## The problem with dotfiles
As a new developer you will learn that using the cli will mean that you have to deal with what's called dotfiles which are usually used as configuration files.

The name dotfiles come from the fact that these files names start with a dot eg: .zshrc which makes them hidden by default in file explorers.

It's simple enough at first but problems starts to rise when you are forced to use multiple devices and want to keep your dotfiles synced between them.

This post is here to help you with keeping your dotfiles in sync and reach your dotfiles zen.

## The journey begins
It all starts with a git repository with all your dotfiles symlinked to it.

What is symlinking you might ask, welp you can think of it as shortcut of sort to your file and that's the extent of knowledge you need to have to use it.

Now lets make a new directory and cd into it.

```
$ mkdir dotfiles

$ cd dotfiles
```

Then let's choose the dotfiles we want to symlink, for this blog we are going to use .bash_profile as an example.

It's usually located at your home directory, so to symlink it we use

```
$ ln -sf ~/.bash_profile ~/.bash_profile
```

This will create .bash_profile file in our directory and link it to the one in the home directory so that both of them will always have the same data.

You should do this to all the files that you want to be easily synced between your devices.

## The linking automation

Now that we have all our files linked we want an easy way to link them on other devices, and this is where writing a simple shell script comes into play.

A simple shell script is a .sh file with a sequence of shell commend written in it, yup it's that simple.

So let's make our install.sh script.

```
$ touch install.sh
```

Now open it with your favorite text editor and write the linking command in it but reversed.

```
ln -sf ~/dotfiles/.bash_profile ~/.bash_profile
```

You notice that I wrote the full path to our directory in the linking command, this save you a lot of permission headache but also means that you'll have to be careful and clone your repository to the path you've specified in the install.sh 

## The remote repository

