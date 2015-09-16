---
layout: post
title: Configuring a Mac OS X Computer
---

---

Usability Configuration
---------------------

Undo natural scroll, set fast tract, right click.

Deactivate all iCloud.

Add ucsc google account: mail, contacts, calendars, messages.

Mission Control->Hot corners, bottom left Mission Control, upper left Desktop, uncheck group windows by applications.

Turn on magnification in the Dock.

Add Applications, Documents to the Dock.

Fix Finder sidebar.

Clear crap off dock.

---

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

Turn off the visual and audio bells.

Put a terminal link in the dock.

***


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
	export CLICOLOR
	export LSCOLORS

	PS1="\[\033[1;37m\][\t][\u@\h:\w]$\[\033[0m\] "
    # If this is an xterm set the title to user@host:dir
    case $TERM in
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

Then source ~/.bashrc

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

Install pip and Pygments
------------------------

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

***

Install CMake
-------------

Go to 

<http://www.cmake.org/download/>

and get and run the binary installer.

Drag the icon to Applications.

Install the cmake symlinks to /usr/local/bin:

{% highlight bash %}
$ sudo "/Applications/CMake.app/Contents/bin/cmake-gui" --install
{% endhighlight %}


***

Install clang-omp, OpenMP runtime, OpenMPI binaries
-----------------

### clang-omp ###

Get clang-omp:

<http://clang-omp.github.io>

Install it:

{% highlight bash %}
$  cd ~/code
$  mkdir clang-omp
$  cd clang-omp/
$  git clone https://github.com/clang-omp/llvm
$  git clone https://github.com/clang-omp/compiler-rt_trunk llvm/projects/compiler-rt
$  git clone -b clang-omp https://github.com/clang-omp/clang llvm/tools/clang
$  cd ~/code/clang-omp/
$  mkdir build
$  cd build
$  cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX:PATH=/Users/brant/code/clang-omp/ ../llvm
$  make all install
{% endhighlight %}


### Change ~/.bashrc ###

Add these to .bashrc:

{% highlight bash %}
export PATH=/Users/brant/code/clang-omp/bin:$PATH
export C_INCLUDE_PATH=/Users/brant/code/clang-omp/include:$C_INCLUDE_PATH
export CPLUS_INCLUDE_PATH=/Users/brant/code/clang-omp/include:$CPLUS_INCLUDE_PATH
export LIBRARY_PATH=/Users/brant/code/clang-omp/lib:$LIBRARY_PATH
export DYLD_LIBRARY_PATH=/Users/brant/code/clang-omp/lib:$DYLD_LIBRARY_PATH
{% endhighlight %}

Source ~/.bashrc
{% highlight bash %}
$ source ~/.bashrc
{% endhighlight %}

### Install the Intel OpenMP Runtime Library ###

Get the OpenMP runtime library code:

<https://www.openmprtl.org/download#stable-releases>

{% highlight bash %}
$  cd ~/code
$  mkdir libomp
$  cd libomp/
$  cp ~/Downloads/libomp_20150701_oss.tar .
$  tar -zxvf libomp_20150701_oss.tar 
$  mkdir build
$  cd build
$  cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX:PATH=/Users/brant/code/libomp/ -DCMAKE_CXX_COMPILER=clang++ -DCMAKE_CC_COMPILER=clang ../libomp_oss
$  make all install
{% endhighlight %}

### Revise ~/.bashrc ###

Revise ~/.bashrc, adjusting these lines:

{% highlight bash %}
export PATH=/Users/brant/code/clang-omp/bin:$PATH
export C_INCLUDE_PATH=/Users/brant/code/clang-omp/include:/Users/brant/code/libomp/include:$C_INCLUDE_PATH
export CPLUS_INCLUDE_PATH=/Users/brant/code/clang-omp/include:/Users/brant/code/libomp/include:$CPLUS_INCLUDE_PATH
export LIBRARY_PATH=/Users/brant/code/clang-omp/lib:/Users/brant/code/libomp/lib:$LIBRARY_PATH
export DYLD_LIBRARY_PATH=/Users/brant/code/clang-omp/lib:/Users/brant/code/libomp/lib:$DYLD_LIBRARY_PATH
{% endhighlight %}

Source ~/.bashrc
{% highlight bash %}
$ source ~/.bashrc
{% endhighlight %}

### Verify clang-omp + the OpenMP runtime is working ###
{% highlight bash %}
$  cd ~/code
$  mkdir test_omp
$  cd test_omp/
$  echo "#include <omp.h>" > main.c
$  echo "#include <stdio.h>" >> main.c
$  echo "int main() {" >> main.c
$  echo "#pragma omp parallel" >> main.c
$  echo "printf(\"Hello from thread %d, nthreads %d\\n\", omp_get_thread_num(), omp_get_num_threads());" >> main.c
$  echo "}" >> main.c
$  clang -fopenmp main.c -o hello
$  ./hello
{% endhighlight %}

You should see something like:

{% highlight shell-session %}
$ ./hello 
Hello from thread 0, nthreads 4
Hello from thread 1, nthreads 4
Hello from thread 3, nthreads 4
Hello from thread 2, nthreads 4
{% endhighlight %}

### Download and install OpenMPI ###

Download OpenMPI at:

<http://www.open-mpi.org/software/ompi/>

Get the latest tarball, place in ~/code/openmpi/

{% highlight bash %}
$  cd ~/code
$  mkdir openmpi
$  cd openmpi/
$  cp ~/Downloads/openmpi-1.10.0.tar.bz2 .
$  tar -zxvf openmpi-1.10.0.tar.bz2 
$  cd openmpi-1.10.0
$  CC=clang CXX=clang++ CXXFLAGS="-stdlib=libstdc++" LDFLAGS="-stdlib=libstdc++" ./configure --prefix=/Users/brant/code/openmpi 
$  make -j 4
$  make install
{% endhighlight %}


### Revise ~/.bashrc ###

Revise ~/.bashrc for openmpi, adjusting these lines:

{% highlight bash %}
    export PATH=/Users/brant/code/clang-omp/bin:/Users/brant/code/openmpi/bin:$PATH
    export C_INCLUDE_PATH=/Users/brant/code/clang-omp/include:/Users/brant/code/libomp/include:/Users/brant/code/openmpi/include:$C_INCLUDE_PATH
    export CPLUS_INCLUDE_PATH=/Users/brant/code/clang-omp/include:/Users/brant/code/libomp/include:/Users/brant/code/openmpi/include:$CPLUS_INCLUDE_PATH
    export LIBRARY_PATH=/Users/brant/code/clang-omp/lib:/Users/brant/code/libomp/lib:/Users/brant/code/openmpi/lib:$LIBRARY_PATH
    export DYLD_LIBRARY_PATH=/Users/brant/code/clang-omp/lib:/Users/brant/code/libomp/lib:/Users/brant/code/openmpi/lib:$DYLD_LIBRARY_PATH

{% endhighlight %}


### Test OpenMPI ###
{% highlight bash %}
$  cd ~/code
$  mkdir test_mpi
$  cd test_mpi/
$  echo "#include <mpi.h>" > main.c
$  echo "#include <stdio.h>" >> main.c
$  echo "int main(int argc, char **argv) {" >> main.c
$  echo "int myid, numprocs, i;" >> main.c
$  echo "MPI_Init(&argc,&argv);" >> main.c
$  echo "MPI_Comm_rank(MPI_COMM_WORLD,&myid);" >> main.c
$  echo "MPI_Comm_size(MPI_COMM_WORLD,&numprocs);" >> main.c
$  echo "for(i=0;i<numprocs;i++){" >> main.c
$  echo "if(myid==i){printf(\"Hello from proc %d\\n\",i);}}" >> main.c
$  echo "MPI_Finalize();" >> main.c
$  echo "}" >> main.c
$  mpicc main.c -o hello
$  mpirun -np 4 ./hello
{% endhighlight %}


You should see something like:

{% highlight shell-session %}
$  mpirun -np 4 ./hello 
Hello from proc 1
Hello from proc 2
Hello from proc 0
Hello from proc 3
{% endhighlight %}