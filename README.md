# grunt-city

* grunt template

## feature

* coffee (js)
* stylus (css)
* jade (html)
* jshint
* csslint
* uglify
* cssmin
* htmlmin
* watch
* connect
* livereload

## install

```
npm -g install grunt-cli
npm install
```

## usage

```
grunt -h
```

```
Usage: grunt [options]

> grunt with fallback-able simple static server for debug

Options:
  -p, --port  [INT]  server port (3000)
  -m, --mode  [STR]  dev or pro (dev)
  -i, --index [STR]  fallback file (index.html)
  -h, --help         show this message and exit

Example:
  grunt -p 3000 -m dev -i index.html

Tasks:
  Language:
    coffee, stylus, jade
  Lint:
    jshint, csslint
  Minify:
    uglify, cssmin, htmlmin
  Server:
    connect, watch
  Phony:
    default - launch server after build
    build   - execute all tasks without server
```

## mode

* `dev`: route to `dist/` (un-minified assets)
* `pro`: route to `public/` (minified assets)

## server core

request to unexists path, fallback to index file.

```coffee
# route = req.url
# index = path.resolve 'public', 'index.html'

fs.exists route, (exist) ->
  fs.stat route, (err, stat) ->
    if exist and stat.isFile()
      return fs.createReadStream(route).pipe(res)
    return fs.createReadStream(index).pipe(res)
```

## tasks

### watch (and launch server)

```
grunt
```

### build

```
grunt build
```

## livereload

* [livereload extensions](http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions-)

## license

MIT
