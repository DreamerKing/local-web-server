[![view on npm](http://img.shields.io/npm/v/local-web-server.svg)](https://www.npmjs.org/package/local-web-server)
![npm module downloads per month](http://img.shields.io/npm/dm/local-web-server.svg)
[![Dependency Status](https://david-dm.org/75lb/local-web-server.svg)](https://david-dm.org/75lb/local-web-server)
![Analytics](https://ga-beacon.appspot.com/UA-27725889-12/local-web-server/README.md?pixel)

local-web-server
================
Fires up a simple, static web server on a given port. A pure Javascript (and more reliable) alternative to `$ python -mSimpleHTTPServer 8000`.

Use for local web development or file sharing (directory browsing enabled). Plays well with Google Chrome Workspaces.

Install
-------
Install [Node.js](http://nodejs.org), then run

```sh
$ npm install -g local-web-server
```

*Linux/Mac users may need to run the above with `sudo`*

Usage
-----
```
ws [--directory|-d <directory>] [--port|-p <port>] [--log-format|-f dev|default|short|tiny] [--compress|-c]
```

From the folder you wish to serve, run:
```sh
$ ws
serving at http://localhost:8000
```

If you wish to serve a different directory, run:
```sh
$ ws -d ~/mysite/
serving /Users/Lloyd/mysite at http://localhost:8000
```

If you wish to override the default port (8000), use `--port` or `-p`:
```sh
$ ws --port 9000
serving at http://localhost:9000
```

Use a built-in or custom [Connect logger format](http://www.senchalabs.org/connect/logger.html) with `--log-format`:
```sh
$ ws --log-format short
```

To add compression, reducing bandwidth, increasing page load time (by 10-15% on my Macbook Air)
```sh
$ ws --compress
```

Storing default options
-----------------------
To store per-project options, saving you the hassle of inputting them everytime, store them in the `local-web-server` property of your project's `package.json`:
```json
{
  "name": "my-project",
  "version": "0.11.8",
  "local-web-server":{
    "port": 8100
  }
}
```

Or in a `.local-web-server.json` file stored in the directory you want to serve (typically the root folder of your site):
```json
{
  "port": 8100,
  "log-format": "tiny"
}
```

Or store global defaults in a `.local-web-server.json` file in your home directory.
```json
{
  "port": 3000
}
```

All stored defaults are overriden by options supplied at the command line. 

Use with Logstalgia
-------------------
The "default" log-format is compatible with [logstalgia](http://code.google.com/p/logstalgia/). 

###Install Logstalgia
On MacOSX, install with [homebrew](http://brew.sh):
```sh
$ brew install logstalgia
```

Alternatively, [download a release for your system from github](https://github.com/acaudwell/Logstalgia/releases/latest).

Then pipe the `default` output directly into logstalgia for real-time visualisation:
```sh
$ ws -f default | logstalgia -
```

![local-web-server with logstalgia](http://75lb.github.io/local-web-server/logstagia.gif)

Use with glTail
---------------
To use with [glTail](http://www.fudgie.org), write your log to disk using the "default" format:
```sh
$ ws -f default > web.log
```

Then specify this file in your glTail config:

```yaml
servers:
    dev:
        host: localhost
        source: local
        files: /Users/Lloyd/Documents/MySite/web.log
        parser: apache
        color: 0.2, 0.2, 1.0, 1.0
```
