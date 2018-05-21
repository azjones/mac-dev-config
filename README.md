# macdev

This document describes how to set up a local developer environment on a new MacBook or iMac. We will set up popular programming languages (for example Node (JavaScript), Python, and Ruby). You may not need all of them for your projects, although I recommend having the first three set up as they always come in handy.

The document assumes you are new to Mac, but can also be useful if you are reinstalling a system and need some reminders. The steps below were tested on macOS High Sierra (10.13.4). But should be suitable for older OS X version.

(**Note** This is a modified version of the mac-dev-setup found at [here](https://github.com/nicolashery/mac-dev-setup). Shamelessly copied and modified for VS Code and AWS needs.)

## System Update

First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > About This Mac** then **Software Update...**.

## System preferences

If this is a new computer, there are a couple tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

* Trackpad > Tap to click
* Keyboard > Key Repeat > Fast (all the way to the right)
* Keyboard > Delay Until Repeat > Short (all the way to the right)
* Dock > Automatically hide and show the Dock

## Security

I recommend checking that basic security settings are enabled. You will be happy to have done so if ever your Mac is lost or stolen.

In **Apple Icon > System Preferences**:

* Users & Groups: If you haven't already set a password for your user during the initial set up, you should do so now
* Security & Privacy > General: Require password immediately after sleep or screen saver begins (you can keep a grace period of a couple minutes if you prefer, but I like to know that my computer locks as soon as I close it)
* Security & Privacy > FileVault: Make sure FileVault disk encryption is enabled
* iCloud: If you haven't already done so during set up, enable Find My Mac

## Google Chrome

Install a primary browser, mine happens to be Chrome.

Download from [www.google.com/chrome](https://www.google.com/chrome/). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Google Chrome** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

## Mozilla Firefox

Install a secondary browser, let's go with Firefox.

Download from [www.mozilla.org/firefox](https://www.mozilla.org/firefox). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Firefox** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

## Postman

Install an API development tool, my choice is Postman. But I hear good things about Insomnia as well.

Download from [www.getpostman.com](https://www.getpostman.com/apps). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Postman** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

## iTerm2

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/).

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm2 > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Under the section **General** set **Working Directory** to be **Reuse previous session's directory**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.

When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.

## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the **Command Line Developer Tools** for **Xcode**. These include compilers that will allow you to build things from source. You can install them directly from the terminal with:

```
xcode-select --install
```

Once that is done, we can install Hombrew by copy-pasting the installation command from the [Homebrew](http://brew.sh/) homepage inside the terminal.

Follow the steps on the screen. You will be prompted for your user password so Homebrew can set appropriate permissions.

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**Ref**: https://github.com/Homebrew/install

Once installation is complete, you can run the following command to make sure everything works:

```
brew doctor
```

### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

```
brew install <formula>
```

To update Homebrew's directory of formulae, run:

```
brew update
```

**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

```
cd /usr/local
git fetch origin
git reset --hard origin/master
```

To see if any of your packages need to be updated:

```
brew outdated
```

To update a package:

```
brew upgrade <formula>
```

Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

```
brew cleanup
```

To see what you have installed (with their version numbers):

```
brew list --versions
```

### Homebrew Services

A nice extension to Homebrew is [Homebrew Services](https://github.com/Homebrew/homebrew-services). It will automatically launch things like databases when your computer starts, so you don't have to do it manually every time.

To install it, simply run:

```
brew tap homebrew/services
```

After installing a service (for example a database), it should automatically add itself to Hombrew Services. If not, you can add it manually with:

```
brew services <formula>
```

Start a service with:

```
brew services start <formula>
```

At anytime you can view which services are running with:

```
brew services list
```

## Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

First let's add some color. There are many great color schemes out there, but if you don't know where to start you can try [Oceanic Next](https://github.com/mhartington/oceanic-next-iterm). Download the iTerm presets for the theme by running:

```
cd ~/Downloads
curl -O https://raw.githubusercontent.com/mhartington/oceanic-next-iterm/master/Oceanic-Next.itermcolors
```

Then, in **iTerm2 Preferences**, under **Profiles** and **Colors**, go to **Load Presets... > Import...**, find and open the **Oceanic-Next.itermcolors** file we just downloaded. Go back to **Load Presets...** and select **Oceanic Next** to activate it. Voila!

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on OS X and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](https://raw.githubusercontent.com/azjones/macdev/master/.bash_profile), [.bash_prompt](https://raw.githubusercontent.com/azjones/macdev/master/.bash_prompt), [.aliases](https://raw.githubusercontent.com/azjones/macdev/master/.aliases) attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others):

```
cd ~
curl -O https://raw.githubusercontent.com/azjones/macdev/master/.bash_profile
curl -O https://raw.githubusercontent.com/azjones/macdev/master/.bash_prompt
curl -O https://raw.githubusercontent.com/azjones/macdev/master/.aliases
```

With that, open a new terminal tab (Cmd+T) and see the change! Try the list commands: `ls`, `ls -lh` (aliased to `ll`), `ls -lha` (aliased to `la`).

Now we have a terminal we can work with!

(Thanks to Mathias Bynens for his awesome [dotfiles](https://github.com/mathiasbynens/dotfiles).)

## Git

Mac OS X comes with a pre-installed version of [Git](http://git-scm.com/), but we'll install our own through Homebrew to allow easy upgrades and not interfere with the system version. To do so, simply run:

```
brew update
brew install git
```

When done, to test that it installed fine you can run:

```
which git
```

The output should be `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/azjones/macdev/master/.gitconfig) file to your home directory:

```
cd ~
curl -O https://raw.githubusercontent.com/azjones/macdev/master/.gitconfig
```

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/))

```
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
```

They will get added to your `.gitconfig` file.

On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your project `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/azjones/macdev/blob/master/.gitignore) file for inspiration. You can also set it up in a global `.gitignore` file by cloning it into your home directory (but you'll want to make sure any collaborators also do it):

```
cd ~
curl -O https://raw.githubusercontent.com/azjones/macdev/master/.gitignore
```

## VS Code

Along with the terminal, the IDE is a developer's most important tool. Everyone has their preference, but if you're just getting started and focus modern languages and want something simple, [VS Code](https://code.visualstudio.com/) is a good option.

First, lets [download](https://code.visualstudio.com/Download) VS Code. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shortcut on the OS X Dock for both for VS Code and iTerm. To do so, right-click on the running application and select **Options > Keep in Dock**.

As with iTerm, VS Code is customizable. Before we do, let's get it working in the command line. Do this by opening the **Command Palette** ⇧⌘P (**View > Command Palette**) then type 'shell command' and select **Shell Command**: Install 'code' command in PATH.

VS Code makes it very easy to customize the IDE just the way you like. And I've added some extensions to get you going. Once you download the extensions bash script, run it. Running it will install the listed extensions. Feel free to update with the extensions that suit your needs.

```
cd ~
curl -O https://raw.githubusercontent.com/azjones/macdev/master/vscode-extensions.sh
```

I've also added some user settings that will get you started customizing the IDE UI. Once you've downloaded the user settings json file, copy the content and go back to VS Code and open the **Settings** panel to paste. Get there by **Code > Preferences > Settings** or ⌘, as the shortcut.

```
cd ~
curl -O
https://raw.githubusercontent.com/azjones/macdev/master/vscode-usersettings.json
```

Let's make VS Code beatiful. As with the terminal we will be going with Oceanic Next color theme. You can [install](https://marketplace.visualstudio.com/items?itemName=mhartington.Oceanic-Next) it here. Once installed, be sure to _reload_ VS Code.

## Python

OS X, like Linux, ships with [Python](http://python.org/) already installed. But you don't want to mess with the system Python (some system tools rely on it, etc.), so we'll install our own version using [pyenv](https://github.com/yyuu/pyenv). This will also allow us to manage multiple versions of Python (ex: 2.7 and 3) should we need to.

Install `pyenv` via Homebrew by running:

```
brew install pyenv
```

When finished, you should see instructions to add something to your profile. Open your `.bash_profile` in the home directory (you can use `$ subl ~/.bash_profile`), and add the following line:

```bash
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
```

Save the file and reload it with:

```
source ~/.bash_profile
```

We can now list all available Python versions by running:

```
pyenv install --list
```

Look for the latest 2.7.x version (or 3.x), and install it:

```
pyenv install 2.7.13 # the latest version might be different
```

List the Python versions you have locally with:

```
pyenv versions
```

The start (`*`) should indicate we are still using the `system` version. We should set the one we installed to be the default:

```
pyenv global 2.7.13
```

You should now see that version when running:

```
python --version
```

For more information, see the [pyenv commands](https://github.com/yyuu/pyenv/blob/master/COMMANDS.md) documentation.

### pip

[pip](https://pip.pypa.io) was also installed by `pyenv`. It is the package manager for Python.

Here are a couple Pip commands to get you started. To install a Python package:

```
pip install <package>
```

To upgrade a package:

```
pip install --upgrade <package>
```

To see what's installed:

```
pip freeze
```

To uninstall a package:

```
pip uninstall <package>
```

### virtualenv

[virtualenv](https://virtualenv.pypa.io) is a tool that creates an isolated Python environment for each of your projects. For a particular project, instead of installing required packages globally, it is best to install them in an isolated folder, that will be managed by `virtualenv`.

The advantage is that different projects might require different versions of packages, and it would be hard to manage that if you install packages globally. It also allows you to keep your global `site-packages` folder clean, containing only big packages that you always need (for example Numpy and Scipy).

Instead of installing and using `virtualenv` directly, we'll use the dedicated `pyenv` plugin [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv) which will make things a bit easier for us. Install it via Homebrew:

```
brew install pyenv-virtualenv
```

After installation, add the following line to your `.bash_profile`;

```bash
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

And reload it with:

```
source ~/.bash_profile
```

Now, let's say you have a project called `myproject`. You can set up virtualenv for that project and the Python version it uses (for example 2.7.13):

```
pyenv virtualenv 2.7.13 myproject
```

See the list of virtualenvs you created with:

```
pyenv virtualenvs
```

To use your project's virtualenv, you need to **activate** it first (in every terminal where you are working on your project):

```
pyenv activate myproject
```

You should see a `(myproject)` appear at the baeginning of your terminal prompt indicating that you are working inside the virtualenv. Now when you install something:

```
pip install <package>
```

It will get installed in that virtualenv's folder, and not conflict with other projects.

### IPython

[IPython](http://ipython.org/) is an awesome project which provides a much better Python shell than the one you get from running `$ python` in the command-line. It has many cool functions (running Unix commands from the Python shell, easy copy & paste, creating Matplotlib charts in-line, etc.) and I'll let you refer to the [documentation](http://ipython.org/ipython-doc/stable/index.html) to discover them.

Before we install IPython, we'll need to get some dependencies. Run the following:

    $ brew update # Always good to do
    $ brew install zeromq # Necessary for pyzmq
    $ brew install pyqt # Necessary for the qtconsole

It may take a few minutes to build these.

Once it's done, we can install IPython with all the available options:

    $ pip install ipython[zmq,qtconsole,notebook,test]

You can launch IPython from the command line with `$ ipython`, but what's more interesting is to use its [QT Console](http://ipython.org/ipython-doc/stable/interactive/qtconsole.html). Launch the QT Console by running:

    $ ipython qtconsole

You can also customize the font it uses:

    $ ipython qtconsole --ConsoleWidget.font_family="Consolas" --ConsoleWidget.font_size=13

And since I'm lazy and I don't want to type or copy & paste that all the time, I'm going to create an alias for it. Create a `.extra` text file in your home directory with `$ subl ~/.extra` (I've set up `.bash_profile` to load `.extra`), and add the following line:

```bash
alias ipy='ipython qtconsole --ConsoleWidget.font_family="Consolas" --ConsoleWidget.font_size=13'
```

Open a fresh terminal. Now when you run `$ ipy`, it will launch the QT Console with your configured options.

To use the in-line Matplotlib functionality (nice for scientific computing), run `$ ipy --pylab=inline`.

### Numpy and Scipy

The [Numpy](http://numpy.scipy.org/) and [Scipy](http://www.scipy.org/SciPy) scientific libraries for Python are always a little tricky to install from source because they have all these dependencies they need to build correctly. Luckily for us, [Samuel John](http://www.samueljohn.de/) has put together some [Homebrew formulae](https://github.com/samueljohn/homebrew-python) to make it easier to install these Python libraries.

First, grab the special formulae (which are not part of Homebrew core):

    $ brew tap samueljohn/python
    $ brew tap homebrew/science

Then, install the `gfortran` dependency (now in `gcc`) which we will need to build the libraries:

    $ brew install gcc

Finally, you can install Numpy and Scipy with:

    $ brew install numpy
    $ brew install scipy

(It may take a few minutes to build.)

## Node.js

The _recommended_ way of installing Node.js and NPM is using Node Version Manager (nvm). I prefer a better solution that is easier to setup and easier to manage. We install node using Homebrew. Then installed the Node package, n.

### Install Node.js via Homebrew

```bash
$ brew install node
```

Installing Node also installs the [npm](https://npmjs.org/) package manager.

### Npm usage

To install a package:

```
npm install <package> # Install locally
npm install -g <package> # Install globally
```

To install a package and save it in your project's `package.json` file:

```
npm install <package> --save
```

To see what's installed:

```
npm list # Local
npm list -g # Global
```

To find outdated packages (locally or globally):

```
npm outdated [-g]
```

To upgrade all or a particular package:

```
npm update [<package>]
```

To uninstall a package:

```
npm uninstall <package>
```

### Install n

```bash
$ npm i -g n
```

### Install serverless

```bash
$ npm i -g serverless
```

### Instal eslint

```bash
$ npm i -g eslint
```

## Ruby

Like Python, [Ruby](http://www.ruby-lang.org/) is already installed on Unix systems. But we don't want to mess around with that installation. More importantly, we want to be able to use the latest version of Ruby.

### Install

When installing Ruby, best practice is to use [RVM](https://rvm.io/) (Ruby Version Manager) which allows you to manage multiple versions of Ruby on the same machine. Installing RVM, as well as the latest version of Ruby, is very easy. Just run:

```
curl -sSL https://get.rvm.io | bash -s stable --ruby
```

When it is done, both RVM and a fresh version of Ruby are installed.

Open a new terminal and run:

```
type rvm | head -1
```

You should get the output `rvm is a function`.

### Usage

The following command will show you which versions of Ruby you have installed:

```
rvm list
```

The one that was just installed, Ruby 2, should be set as default. When managing multiple versions, you switch between them with:

```
rvm use system # Switch back to system install (ex: 2.0)
rvm use 2.3 --default # Switch to 2.3 and sets it as default
```

Run the following to make sure the version you want is being used:

```
which ruby
ruby --version
```

You can install another version with:

```
rvm install 2.2
```

To update RVM itself, use:

```
rvm get stable
```

[RubyGems](http://rubygems.org/), the Ruby package manager, was also installed:

```
which gem
```

Update to its latest version with:

```
gem update --system
```

To install a "gem" (Ruby package), run:

```
gem install <gemname>
```

To install without generating the documentation for each gem (faster):

```
gem install <gemname> --no-document
```

To see what gems you have installed:

```
gem list
```

To check if any installed gems are outdated:

```
gem outdated
```

To update all gems or a particular gem:

```
gem update [<gemname>]
```

RubyGems keeps old versions of gems, so feel free to do come cleaning after updating:

```
gem cleanup
```

## Redis

[Redis](http://redis.io/) is a blazing fast, in-memory, key-value store, that uses the disk for persistence. It's kind of like a NoSQL database, but there are a lot of [cool things](http://oldblog.antirez.com/post/take-advantage-of-redis-adding-it-to-your-stack.html) that you can do with it that would be hard or inefficient with other database solutions. For example, it's often used as session management or caching by web apps, but it has many other uses.

To install Redis, use Homebrew:

```
brew update
brew install redis
```

Start it through Homebrew Services with:

```
brew services start redis
```

I'll let you refer to Redis' [documentation](http://redis.io/documentation) or other tutorials for more information.

## MongoDB

[MongoDB](http://www.mongodb.org/) is a popular [NoSQL](http://en.wikipedia.org/wiki/NoSQL) database.

Installing it is very easy through Homebrew:

```
brew update
brew install mongo
```

Start it through Homebrew Services with:

```
brew services start mongo
```

I'll let you refer to MongoDB's [Getting Started](http://docs.mongodb.org/manual/tutorial/getting-started/) guide for more!

## Elasticsearch

As it says on the box, [Elasticsearch](http://www.elasticsearch.org/) is a "powerful open source, distributed real-time search and analytics engine". It uses an HTTP REST API, making it really easy to work with from any programming language.

You can use elasticsearch for such cool things as real-time search results, autocomplete, recommendations, machine learning, and more.

### Install

Elasticsearch runs on Java, so check if you have it installed by running:

```bash
java -version
```

If Java isn't installed yet, a window will appear prompting you to install it. Go ahead and click "Install".

Next, install elasticsearch with:

```bash
$ brew install elasticsearch
```

**Note**: Elasticsearch also has a `plugin` program that gets moved to your `PATH`. I find that too generic of a name, so I rename it to `elasticsearch-plugin` by running (will need to do that again if you update elasticsearch):

```bash
$ mv /usr/local/bin/plugin /usr/local/bin/elasticsearch-plugin
```

Below I will use `elasticsearch-plugin`, just replace it with `plugin` if you haven't followed this step.

As you guessed, you can add plugins to elasticsearch. A popular one is [elasticsearch-head](http://mobz.github.io/elasticsearch-head/), which gives you a web interface to the REST API. Install it with:

```bash
$ elasticsearch-plugin --install mobz/elasticsearch-head
```

### Usage

Start a local elasticsearch server with:

```bash
$ elasticsearch -f
```

(The `-f` option tells it to run in the foreground, so you can stop it with `Ctrl+C`.)

Test that the server is working correctly by running:

```bash
$ curl -XGET 'http://localhost:9200/'
```

If you installed the elasticsearch-head plugin, you can visit its interface at `http://localhost:9200/_plugin/head/`.

Elasticsearch's [documentation](http://www.elasticsearch.org/guide/) is more of a reference. To get started, I suggest reading some of the blog posts linked on this [StackOverflow answer](http://stackoverflow.com/questions/11593035/beginners-guide-to-elasticsearch/11767610#11767610).

## Projects folder

This really depends on how you want to organize your files, but I like to put all my version-controlled projects in `~/Projects`. Other documents I may have, or things not yet under version control, I like to put in `~/Dropbox` (if you have Dropbox installed), or `~/Documents`.

## Install aws-cli via Homebrew

```bash
brew install awscli
```
