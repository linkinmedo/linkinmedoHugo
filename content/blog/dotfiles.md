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

It starts with initializing a git repository locally, assuming you have git installed you just have to type:
```
$ git init
```
while you are in the dotfiles directory.

Next you have to go to your favorite git repository hosting site (in our case github.com) and create a new repository called dotfiles.

When you are done creating the remote repository, the next step is to link and push your local repository to it which is as simple as writing two lines in your terminal.

```
$ git remote add origin git@github.com:yourusername/dotfiles.git
$ git push -u origin master
```
And that's pretty much it.

## Using your dotfiles repository

To use your newly created dotfiles repository on a new device, you just have to clone it to your new device in the same location you had it on you original device.

In our case it's the home directory, so while in your home directory run:

```
$ git clone git@github.com:yourusername/dotfiles.git
```

After you clone the repository, you should cd into it and run the install.sh:

```
$ cd dotfiles
$ ./install.sh
```
and voila you have your local dotfiles synced with your repository dotfiles.

## Making changes

Let's say you made some changes to your dotfiles and want to sync them, all you have to do is commit your new changes and push them to your remote repository:

```
$ cd ~/dotfiles
$ git add .
$ git commit -m 'your message'
$ git push
```
then on the other devices you should pull the changes and run the install.sh:

```
$ git pull
$ ./install.sh
```
Now you have to do this whenever you make changes to your dotfiles, and they will be the same between all your devices.

Please note that we used .bash_profile in this tutorial but you can use this method with as many files you want you just add the symlink the files and add them to your install.sh.
