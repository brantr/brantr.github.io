---
layout: post
title: Configuring a Mac OS X Computer
---

---

Set up bash
------------

### Make a ~/bin ###

Do:

```
$cd
$mkdir bin
```

### Bash Profile ###

Create a ~/.bash_profile:

```
if [ -f ~/.bashrc ]; then
	source ~/.bashrc
fi
```

### Alias file ###

Create an ~/.alias file:

```
alias brown='ssh -Y brant@brown.as.arizona.edu'
alias orange='ssh -X brant@orange.as.arizona.edu'
alias crimson='ssh -Y brant@128.114.67.60'
```

### Bashrc ###

Create a hacked ~/.bashrc, setting a fancy terminal prompt, source ~/.alias includes ~/bin in your $PATH.

```
if [ "$PS1" ]; then
	TERM="xterm-color"
	export TERM
	CLICOLOR=1
	LSCOLORS="GxfxcxdxCxegedabagacad"
	export CLICOLORin
	export LSCOLORS

	PS1="\[\033[1;37m\][\t][\u@\h:\w]$\[\033[0m\] "
    # If this is an xterm set the title to user@host:dir
    case $TERM 
    xterm*)
        PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME}: ${PWD}\007"'
        ;;
    *)
        ;;
    esac

    # prompt function
    function proml {
    local BLUE="\[\033[1;34m\]"
    local RED="\[\033[1;32m\]"
    local LIGHT_RED="\[\033[0;037m\]"
    local WHITE="\[\033[1;37m\]"
    local NO_COLOUR="\[\033[0m\]"
    case $TERM in
         xterm*|rxvt*)
                      TITLEBAR=''
                       ;;
         *)
                      TITLEBAR=""
                      ;;
    esac

    PS1="${TITLEBAR}$BLUE[$RED\t$BLUE]\$BLUE[$LIGHT_RED\u@\h:\w$BLUE]\$WHITE\$$NO_COLOUR "
    PS2='> '
    PS4='+ '
    }
    
    #set prompt 
    proml

    source ~/.alias
    PATH=~/bin:"${PATH}"

fi
```

### Make SSH keys ###

```
$cd
$ssh-keygen -t rsa
```

***

Sublime Text 2
--------------

### Download ###
Get Sublime Text 2 at

<http://www.sublimetext.com>

and install the license.

### Short cut ###

```
$cd ~/bin
$ln -s /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl sublime
```

***

Install Deja Vu Fonts
---------------------

Download Deja Vu Fonts from

<http://dejavu-fonts.org/wiki/Main_Page>

and then use the Font Book app to add them.

***

Configure Terminal
------------------

Open the Terminal program, then -> Preferences

Under "Text" tab, select Deja Vu Sans Mono 11pt.

Under "Shell" tab, select "Close the window" from the dropdown.

Under "Window" tab, click the Color & Effect under Background, then set 70% opacity, 50% blur.

***

Install GitHub Desktop
----------------------

Get the GitHub Desktop app at

<https://desktop.github.com>

and link to your github account.

***

Install Xcode
--------------

Get Xcode through the Apple App Store.

Then, in a terminal

```
$ xcode-select --install
```
And follow the prompts to install Xcode.

### Bundler ###

```
$gem install bundler
```

CD into the github io directory, and then

```
$bundle install
```