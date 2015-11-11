# teknahlohjeez

Mac-centric, high level overview of new/current tools and technologies used in front-end web development.

## Items covered here:
- The Command Line
- Node, NPM, and the `n` Package
- Bower (non-node package manager)
- Bundler (Ruby package manager)
- Taskrunners (Grunt/Gulp/NPM Scripts)
- Static Site Generators (Jekyll)
- Project Generators (Yeoman)
- SASS/SCSS
- PostCSS
- Commonly Used NPM Modules
- Git
- Communication (Slack, HipChat)

### The Command Line (or Command Prompt if in Windows)
I don't really use Windows Command Prompt (DOS) much anymore, so my skills are limited there.  I know how to do some basic commands but, they aren't listed here because they're explained pretty well [here](http://www.computerhope.com/issues/chusedos.htm).

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
Occasionally, you'll encounter permissions errors.  These usually looks something like, `EACCESS blah blah blah`.  There are two easy ways and one hard way to fix this:

##### Easy
- `sudo` <- Type this before whatever command gives you the permissions error, then type your computer's administrator password (you won't see the password as you're typing but, it's there).  Your computer will recognize you as the root user for a limited time after you use the `sudo` command.  *If you want to repeat a command but use `sudo`, type `sudo !!`.
- `sudo su` <- Type this without any other command to login as the root user and stay logged in as long as your Terminal session is open or until you type `exit`.  Be careful because it leaves you all kinds of vulnerable.  Your prompt path will change when you're logged in as the root user.

##### Hard
Give your user full rights and privileges on your computer.  This is kind of like permanently enabling `sudo su` for your user.  It's not the easiest in the world to get set on a mac.  There are plenty of tutorials that tell you different ways to do it so, if you want to go down that path, google it.

Typically, I do everything in my power not to use `sudo` and only use it when required.  Whenever possible, I don't install applications using `sudo` because I don't want to have to log in as the root user everytime I use that application.

#### `$PATH`
Scenario: You are in `/MyComputer/MyName/`.  In `/MyComputer/MyName/` there is a program called `awesome.app` that has a command line interface tool called 'awesome'.  You change directories `cd Sites` so that you're now in `/MyComputer/MyName/Sites`.  You list the files `ls -a` and see a file called `ohmanthisis.awesome`.  You run the file `awesome ohmanthisis.awesome` but get an error that your computer can't find `awesome`.  That's because the context of your command is your current working directory, which doesn't include the `awesome` app.  To run your command, you need to type `/MyComputer/MyName/awesome ohmanthisis.awesome` or something much more convoluted depending on where the `awesome` command line tool is actually installed.

This is where $PATH comes in.  You can set a $PATH for `awesome` so that no matter where you are in the file system, whenever you ask `awesome` to do something, the computer uses the $PATH that you set for it.

#### Some lingo
- 'cwd' <- Current Working Directory

### Node, NPM, and the `n` package

#### Node
[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient.

##### Why node?
- Designed to build fast, event-driven, scalable network applications
- JavaScript
- Non-blocking

##### Installation

###### Prerequisites
- XCode

###### This (this is the way I do it but, I'm anti-homebrew for no good reason)
- Head over to [the node.js website](https://nodejs.org/en/) and download the latest stable installer package.
- Install node :)
- Optional: You might need to add node to your $PATH.  You can do that by opening Terminal and typing `open -a 'YourFavoriteTextEditor.app' .` and adding `/local/node/bin:` to your $PATH.  If you don't have a $PATH setup already, look [here](http://dandean.com/nodejs-npm-express-osx/) for more details.

###### or That
If you have [homebrew](http://brew.sh/) installed, from the command line type `brew install node`.

One advantage of using homebrew is that you avoid using `sudo` to install node.

There's a great, detailed tutorial how to set this up on [the treehouse site](http://blog.teamtreehouse.com/install-node-js-npm-mac).

##### Basics (the bare minimum)
You don't really need to know much about node to use it - or npm, for that matter.  What's important is that you know how to check what version you're using and that you understand npm.

You can check what version you're using with `node -v`.  This is helpful for two reasons: 1. Checking to see what version of node you have installed.  2. Checking to see if node is installed.  TIP: You can use the `-v` flag on all sorts of applications to find out what version you're using.

##### Going further
If you want to learn more, I highly recommended a visit to [nodeschool.io](http://nodeschool.io/).  Complete the learnyounode `npm install -g learnyounode` tutorial.

#### NPM
Node.js' package ecosystem, [npm](https://www.npmjs.com/), is the largest ecosystem of open source libraries in the world.

##### Why NPM?
- Quick, easy way to install node packages (like plugins) in your project without worrying about dependencies.
- Find pretty much anything you want
- Save time and energy by using other people's work

##### `package.json`
Create a `package.json` file by running `npm init`.  Anytime you install a local npm package with a `--save` or `--save-dev` flag, it gets installed *and* written to the `package.json` file.  At the end of the day, the most important thing to know about `package.json` is that running `npm install` by itself tells npm to look for `package.json` and install all listed dependencies.

Example `package.json` file:
```
{
  "private": true,
  "engines": {
    "node": ">=0.10.0"
  },
  "devDependencies": {
    "browser-sync": "^1.9.1",
    "del": "^1.1.1",
    "gulp": "^3.8.11",
    "gulp-autoprefixer": "^2.1.0",
    "gulp-concat": "^2.4.3",
    "gulp-gh-pages": "^0.4.0",
    "gulp-htmlmin": "^1.0.0",
    "gulp-if": "^1.2.5",
    "gulp-imagemin": "^2.1.0",
    "gulp-jshint": "^1.9.0",
    "gulp-load-plugins": "^0.8.0",
    "gulp-minify-css": "^0.4.3",
    "gulp-replace": "^0.5.3",
    "gulp-rev": "^3.0.1",
    "gulp-rev-replace": "^0.3.4",
    "gulp-sass": "^1.3.2",
    "gulp-size": "^1.2.0",
    "gulp-uglify": "^1.1.0",
    "gulp-useref": "^1.1.1",
    "node-neat": "^1.7.1-beta1",
    "run-sequence": "^1.0.2"
  }
}
```

##### Usage
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
[Node Version Manager](https://www.npmjs.com/package/n).  `n` gives you the ability to switch quickly between versions of Node.

##### Why `n`?
It's helpful when you're working on a project with outdated dependencies (like if you need to use a plugin/package that doesn't support the current Node version) and you need to run an old version of Node.

##### Installation
Once you have Node (and consequently NPM) installed, from the command line type, `npm install -g n`
A list of node versions for install can be found [here](https://nodejs.org/docs/)

##### Usage
Type `n` from the command line, use your keyboard arrows to choose which version of node you want to run, and hit the `return` key.

### Bower
Bower works by fetching and installing packages from all over, taking care of hunting, finding, downloading, and saving the stuff you’re looking for.

#### Installation
Install Bower globally `npm install -g bower`

#### Usage
`bower install *` where `*` is the name of the package you want to install.  <- Install a single package locally.
`bower install` <- Looks for a `bower.json` file (like npm's `package.json`) and installs all packages listed there.

Example `bower.json` file:
```
{
  "name": "teknahlohjeez",
  "version": "0.0.0",
  "dependencies": {
    "modernizr": "~2.8.3"
  },
  "devDependencies": {
    "normalize-css": "~3.0.2",
    "jquery": "~2.1.3"
  }
}

```

##### `bower_components` and `.bowerrc`
By default, bower installs packages into a `bower_components` directory.  You can override this default by creating a `.bowerrc` file and pointing to a directory of your choosing.

Example `.bowerrc` file:
```
{
  "directory": "vendor"
}
```

-------------------------------

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
