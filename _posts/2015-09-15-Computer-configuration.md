---
layout: post
title: Configuring a Mac OS X Computer
---

---

Set up bash
------------

### Make a ~/bin ###

Do:

{% highlight bash %}
$ cd
$ mkdir bin
{% endhighlight %}


### Bash Profile ###

Create a ~/.bash_profile:

{% highlight bash %}
if [ -f ~/.bashrc ]; then
	source ~/.bashrc
fi
{% endhighlight %}


### Alias file ###

Create an ~/.alias file:

{% highlight bash %}
alias brown='ssh -Y brant@brown.as.arizona.edu'
alias orange='ssh -X brant@orange.as.arizona.edu'
alias crimson='ssh -Y brant@128.114.67.60'
{% endhighlight %}

### Bashrc ###

Create a hacked ~/.bashrc, setting a fancy terminal prompt, source ~/.alias includes ~/bin in your $PATH.

{% highlight bash %}
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
{% endhighlight %}

### Make SSH keys ###

{% highlight bash %}
$ cd
$ ssh-keygen -t rsa
{% endhighlight %}

***

Sublime Text 2
--------------

### Download ###
Get Sublime Text 2 at

<http://www.sublimetext.com>

and install the license.

### Short cut ###

{% highlight bash %}
$ cd ~/bin
$ ln -s /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl sublime
{% endhighlight %}

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

{% highlight bash %}
$ xcode-select --install
{% endhighlight %}

And follow the prompts to install Xcode.

### Bundler ###

{% highlight bash %}
$ gem install bundler
{% endhighlight %}

CD into the github io directory, and then

{% highlight bash %}
$ bundle install
{% endhighlight %}

***

Install pip
-----------

Download pip from

<https://pypi.python.org/pypi/pip>

Expand the tarball, and then 

{% highlight bash %}
$ sudo python setup.py install
{% endhighlight %}

Install Pygments
{% highlight bash %}
$  sudo pip install Pygments
{% endhighlight %}