# Mac OSX Dev Setup

This document describes my favorite dev setup on Mac OSX, especially but not only for a programmer or data scientist(engineer). Inspired by [nicolashery/mac-dev-setup](https://github.com/nicolashery/mac-dev-setup), we will do some customizes and updates base on it. We will setup:

- System preferences.
- Tools: [Homebrew](https://brew.sh/), [iTerm2](https://www.iterm2.com/index.html), [Git](https://git-scm.com/), [Google Chrome](https://www.google.com/chrome/).
- Languages: [Java](https://www.java.com), [Python](http://www.python.org/), [Scala](https://www.scala-lang.org/), [Go](https://golang.org/), [Node](http://nodejs.org/) (JavaScript), [Ruby](http://www.ruby-lang.org/), [R](https://www.r-project.org), [zsh](http://www.zsh.org/).
- Editors and IDEs: [IntelliJ IDEA](https://www.jetbrains.com/idea/), [Pycharm](https://www.jetbrains.com/pycharm/), [Visual Studio Code](https://code.visualstudio.com/), [Sublime Text](https://www.sublimetext.com), [Vim](www.vim.org/), [Typora](https://typora.io/) or [MacDown](https://macdown.uranusjr.com/).
- Infrastructures: [Anaconda](https://www.continuum.io), [Docker](https://www.docker.com/), [HDP Sandbox](https://hortonworks.com/).
- Themes: [Powerline Fonts](https://github.com/powerline/fonts), [Dracula](https://github.com/dracula/dracula-theme), [Solarized](https://github.com/altercation/solarized)
	
The steps below were tested on **macOS Sierra**. If you have any comments or suggestions, feel free to file a [issue](https://github.com/jackode/mac-dev-setup/issues/new)!

- [Tools](#tools):
	- [Google Chrome](#google-chrome)
	- [iTerm2](#iterm2)
	- [Homebrew](#homebrew)
	- [Git](#git)
- [Languages](#languages)
	- [Java](#java)
		- [JDK](#jdk)
		- [Maven](#maven)
	- [Scala](#scala)
	- [Python](#python)
		- [Anaconda](#anaconda)
		- [Numpy, Pandas, Scipy and Sklearn](#numpy-pandas-scipy-sklearn)
		- [Tensorflow](#tensorflow)
	- [Ruby](#ruby)
		- [Ruby SDK](#ruby-sdk)
		- [RVM](#rvm)
	- [Javascript](#javascript)
		- [NodeJs](#nodejs)
		- [Less](#less)
	- [zsh](#zsh)
		- [oh-my-zsh](#oh-my-zsh)
		- [zsh plugins](#zsh-plugins)
- [Editors and IDEs](#editor-and-ide):
	- [IntelliJ IDEA](#idea)
	- [Pycharm](#pycharm) 
	- [Visual Studio Code](#vscode)
	- [Sublime Text or Atom](#sublime-atom)
	- [Vim](#vim)
	- [Typora or MacDown](typora-macdown) 
- [Infrastructures](#infrastructures):
	- [Anaconda](#anaconda)
	- [Docker](#docker)
	- [HDP Sandbox](#hdp-sandbox)
- [Themes](#themes):
	- [Powerline Fonts](#powerline-fonts)
	- [Dracula](#dracula)
	- [Solarized](#solarized)

## Tools


### Google Chrome

Install your favorite browser, mine happens to be Chrome since many useful plugins and can synch data and bookmarks via google account.

Download from [www.google.com/chrome](https://www.google.com/intl/en/chrome/browser/). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Google Chrome** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

Here is a blog about some plugins for your references: [41 Best Google Chrome Extensions](http://www.tomsguide.com/us/pictures-story/283-best-google-chrome-extensions.html)

### iTerm2

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/) (the newest version, even if it says "beta release").

iTerm2 has many amazing [features](http://www.iterm2.com/features.html). 

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.


### Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

#### Install

An important dependency before Homebrew can work is the **Command Line Tools** for **Xcode**. These include compilers that will allow you to build things from source.

Either you can install **Xcode** from [http://developer.apple.com/downloads](http://developer.apple.com/downloads), or install **Command Line Tools** without **Xcode** by execute `$ xcode-select --install` in terminal.

Then, we can install Hombrew! In the terminal paste the following line (without the `$`), hit **Enter**, and follow the steps on the screen:

    $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"


One thing we need to do is tell the system to use programs installed by Hombrew (in `/usr/local/bin`) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH` environment variable:

    $ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.profile

Open a new terminal tab with **Cmd+T** (you should also close the old one), then run the following command to make sure everything works:

    $ brew doctor
    
#### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

    $ brew install <formula>
        
To update Homebrew's directory of formulae, run:

    $ brew update
    
**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

    $ cd /usr/local
    $ git fetch origin
    $ git reset --hard origin/master

To see if any of your packages need to be updated:

    $ brew outdated
    
To update a package:

    $ brew upgrade <formula>
        
Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

### Git

What's a developer without [Git](http://git-scm.com/)? To install, simply run:

    $ brew install git
    
When done, to test that it installed fine you can run:

    $ git --version
    
And `$ which git` should output `/usr/local/bin/git`.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain
    
**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/nicolashery/mac-dev-setup/blob/master/.gitignore) file for inspiration.
    
## Languages

A programmer or data scientists(engineer) should master multiple programming languages: Object Oriented Programming language **Java**, Functional Programming language **Scala** or **Haskell**, Data Analysis language **Python** or **R**, Web Development language **Ruby** or **Node**, Ops Scripts **Shell** or **AWK**. 

### Java

Java is the most popular and important OOP language, applied in many popular open source projects: [Spring](), [Hadoop](), [Flink]() .etc.

#### JDK

JDK stands for Java SE Development Kit. Currently the new released stable JDK version is 1.8, while many projects are still on version 1.7. Then we will setup both JDK1.8 and JDK1.7. You can download them from [Oracle Java SE](http://www.oracle.com/technetwork/java/javase/downloads/). Click and accept to install them by default options. You can test it in command line:
	
	$ java --version
Default is higher version 1.8, to switch 1.7 version run by:

	$ export JAVA_HOME=`/usr/libexec/java_home -v 1.7`

You can setup your default **JAVA_HOME** environment by:
	
	$ echo "export JAVA_HOME=`/usr/libexec/java_home -v 1.8`" >> ~/.profile
	
#### Maven

[Maven](https://maven.apache.org/) Maven is a software project management and comprehension tool, especially for Java, to install it simply run:

    $ brew install maven
    
When done, to test that it installed fine you can run:

    $ mvn --version
 
User's global maven setting is located in ~/.m2/settings.xml, you can directly modify it on your demand.

### Scala

[Scala](https://www.scala-lang.org) is a mixed language of both Object-Oriented and Functional. Many popular Open Source Projects are written in Scala, such as [Spark](https://github.com/apache/spark), [Kafka](https://github.com/apache/kafka), [Akka](https://github.com/akka/akka), to install it simply run:

	$ brew install scala
	
To test Scala installed status by:

	$ scala -version
	
Sbt is also a software project management, sbt for Scala is like maven for Java.    You can also install it by brew:

	$ brew install sbt
	
To test Sbt installed status by:

	$ sbt -help
