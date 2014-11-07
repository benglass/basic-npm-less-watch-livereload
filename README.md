# Setup

Install bower for managing frontend packages. Then use bower to install the frontend
assets from bower.json (in this case its just twitter bootstrap). Then install the node
packages (less, live reload, server, watch).

```
npm install -g bower
bower install
npm install
```

# How to use this setup

Whenever you want to start coding you will want to tell npm to watch for changes in your
less and automatically recompile and also start up the web server with live reload so
it will automatically refresh your browser when there are changes.

```
npm run serve
npm run watch
```

You can run these commands in 2 separate terminals or you can background them by adding &
to the end of the line when you run them:

```
npm run serve&
npm run watch&
```

Grunt is a very complicated task runner that requires a ton of configuration.
In addition to that we were using a config which was specifically used by the developers
of bootstrap to build bootstrap itself.

The node package manager (npm) provides its own simple task running mechanism which
is more than sufficient for many projects. It runs off of the package.json file, specifically
the scripts section. Each key in scripts just defines a command that can be run by calling

```
npm run command
```

For example in the package.json file here there is a command for compiling the file 
www/assets/less/main.less to www/assets/css/main.css which looks like this

```
"scripts": {
    "less": "lessc www/assets/less/main.less www/assets/css/main.css"
},
```

You can run this command directly by running the following on the command line

```
npm run less
```

Additionally, this setup has scripts for watching for changes in the less files and 
automatically regenerating the css files. You can see this in the packages.json file:

```
  "watch": {
    "less": "www/assets/less/main.less"
  },
  "scripts": {
    "less": "lessc www/assets/less/main.less www/assets/css/main.css",
    "watch": "npm-watch"
  }
```

This does a few things:

1. Create an alias so you can run "npm run watch install" of "npm run npm-watch"
2. Configure watch to watch the file www/assets/less/main.less and run the script called "less"
whenever it changes, which in our case regenerates the css file.

Finally this script includes a basic web serve that has livereload built in, so it will serve up your static files from the www folder and automatically reload them whenever any of the files
in that folder change.
