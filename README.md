# teknahlohjeez

High level overview of new/current tools and technologies used in front-end web development

## Items covered here:
- The Command Line
- Node & NPM & the `n` Package
- Taskrunners (Grunt/Gulp/NPM Scripts)
- Static Site Generators (Jekyll)
- Project Generators (Yeoman)
- SASS/SCSS
- PostCSS
- Commonly Used NPM Modules
- Git
- Communication (Slack, HipChat)

### The Command Line (or Command Prompt if in Windows)
I don't really use Windows Command Prompt (DOS) much anymore, so my skills are limited there.  I know how to do some basic commands but, they aren't listed here because they're explained pretty well [here](http://www.computerhope.com/issues/chusedos.htm)

#### Basic Commands (Unix)
- `ls` <- List files in a directory (excludes hidden files)
- `ls -a` <- pass the `a` flag to list ALL files in a directory (includes hidden files)
- `cd` <- Change directory
- `cd ..` <- Move back a directory

#### Creating/deleting files/folder
- `touch nameOfFile.withExtension` <- Create an empty file.
- `mkdir nameOfDirectory` <- Create an empty folder.
- `rm` <- Delete file
- `rm -rf` <- Delete folder and all it's contents (`-rf` flag means to recursively delete files)

#### The 'root' user
Occasionally, you'll encounter permissions errors.  These usually looks something like, `EACCESS blah blah blah`.  There are two easy ways and one hard way to fix this.

##### Easy
- `sudo` <- Type this before whatever command gives you the permissions error, then type your computer's administrator password (You won't see the password as you're typing but, it's there).  Your computer will recognize you as the root user for a limited time after you use the `sudo` command.  *If you want to repeat a command but use `sudo`, type `sudo !!`.
- `sudo su` <- Type this without any other command to login as the root user and stay logged in as long as your Terminal session is open or until you type `exit`.  Be careful because it leaves you all kinds of vulnerable.  Your prompt path will change when you're logged in as the root user.

##### Hard
Give your user full rights and privileges on your computer.  This is kind of like permanently enablilng `sudo su` for your user.  It's not the easiest in the word to get set on a mac.  There are plenty of tutorials that tell you different ways to do it so, if you want to go down that path, go for it.

Typically, I do everything in my power not to use `sudo` and only use it when required.  Whenever possible, I don't install applications using `sudo` because I don't want to have to log in as the root user everytime I use that application.

#### `PATH`
Scenario: You are in `/MyComputer/MyName/`.  In `/MyComputer/MyName/` there is a program called `awesome.app` that has a command line interface tool called 'awesome'.  You change directories `cd Sites` so that you're now in `/MyComputer/MyName/Sites`.  You list the files `ls -a` and see a file called `ohmanthisis.awesome`.  You run the file `awesome ohmanthisis.awesome` but get an error that your computer can't find `awesome`.  That's because the context of your command is your current working directory, which doesn't include the `awesome` app.  To run your command, you need to type `/MyComputer/MyName/awesome ohmanthisis.awesome` or something much more convoluted depending on where the `awesome` command line tool is actually installed.

This is where PATH comes in.  You can set a PATH for `awesome` so that no matter where you are in the file system, whenever you ask `awesome` to do something, the computer uses the PATH that you set for it.

#### Some lingo
- 'cwd' <- Current Working Directory

### Node & NPM


#### Node

##### What is it?

##### Why node?

##### Installation
nodejs.org or homebrew


#### NPM

##### What is it?

##### Why NPM?

##### `package.json`

##### Common NPM actions/flags
- `npm` <- Everything you write after this is what you are asking npm to do
- `install` <- Install an NPM package
- `npm install` <- Without any flags or specific package listed, this installs everything listed in `package.json`
- `-g` or `-global` <- Perform your requested action on your root directory so that it is accessible anywhere on your computer (in any project)
- `--save` <- Add the installed package to `package.json`'s dependencies list.
- `--save-dev` <- Add the installed package to `package.json`'s dev dependencies list.

Example - Globally install a specific package: `npm install -g n`
Example - Install a specific package: `npm install postcss`
Example - Install all packages in the `package.json` file: `npm install`
Example - Install a specific package and save it as a development dependency: `npm install --save-dev postcss`

##### Installation
No installation necessary.  NPM comes with node.  NOTE: If you accidentally delete NPM, you'll need to reinstall Node to get it back.  Node is pretty much useless without NPM unless you are a Gandalf the Gray or David Bowie from Labrynth.


#### The `n` package

##### What is it?
`n` gives you the ability to switch quickly between versions of Node.

##### Why `n`?
It's helpful when you're working on a project with outdated dependencies (like if you need to use a plugin/package that doesn't support the current Node version) and you need to run an old version of Node.

##### Installation
Once you have Node (and consequently NPM) installed, from the command line type, `npm install -g n`

## Project Setup
This project utilizes Playbook, reference Playbook's [setup guide](https://github.com/centresource/generator-playbook#get-started).

1. Clone this repository
2. `npm install`
3. `bower install`
4. `bundle install`

## Usage

### Gulp Tasks
##### gulp serve
Serve your source locally into your browser. BrowserSync automatically loads any changes to HTML, CSS and JavaScript that you make.

##### gulp build
Build the concatenated, minified production version of your source into the `dist` directory.

##### gulp deploy
Deploy the production version of your source to [GitHub Pages](http://pages.github.com/).
