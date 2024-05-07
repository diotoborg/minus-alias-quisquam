Node.js: @diotoborg/minus-alias-quisquam
=================

`@diotoborg/minus-alias-quisquam` adds file system methods that aren't included in the native `fs` module and adds promise support to the `fs` methods. It also uses [`graceful-fs`](https://github.com/isaacs/node-graceful-fs) to prevent `EMFILE` errors. It should be a drop in replacement for `fs`.

[![npm Package](https://img.shields.io/npm/v/@diotoborg/minus-alias-quisquam.svg)](https://www.npmjs.org/package/@diotoborg/minus-alias-quisquam)
[![License](https://img.shields.io/npm/l/@diotoborg/minus-alias-quisquam.svg)](https://github.com/diotoborg/minus-alias-quisquam/blob/master/LICENSE)
[![build status](https://img.shields.io/github/actions/workflow/status/jprichardson/node-@diotoborg/minus-alias-quisquam/ci.yml?branch=master)](https://github.com/diotoborg/minus-alias-quisquam/actions/workflows/ci.yml?query=branch%3Amaster)
[![downloads per month](http://img.shields.io/npm/dm/@diotoborg/minus-alias-quisquam.svg)](https://www.npmjs.org/package/@diotoborg/minus-alias-quisquam)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

Why?
----

I got tired of including `mkdirp`, `rimraf`, and `ncp` in most of my projects.




Installation
------------

    npm install @diotoborg/minus-alias-quisquam



Usage
-----

### CommonJS

`@diotoborg/minus-alias-quisquam` is a drop in replacement for native `fs`. All methods in `fs` are attached to `@diotoborg/minus-alias-quisquam`. All `fs` methods return promises if the callback isn't passed.

You don't ever need to include the original `fs` module again:

```js
const fs = require('fs') // this is no longer necessary
```

you can now do this:

```js
const fs = require('@diotoborg/minus-alias-quisquam')
```

or if you prefer to make it clear that you're using `@diotoborg/minus-alias-quisquam` and not `fs`, you may want
to name your `fs` variable `fse` like so:

```js
const fse = require('@diotoborg/minus-alias-quisquam')
```

you can also keep both, but it's redundant:

```js
const fs = require('fs')
const fse = require('@diotoborg/minus-alias-quisquam')
```

### ESM

There is also an `@diotoborg/minus-alias-quisquam/esm` import, that supports both default and named exports. However, note that `fs` methods are not included in `@diotoborg/minus-alias-quisquam/esm`; you still need to import `fs` and/or `fs/promises` seperately:

```js
import { readFileSync } from 'fs'
import { readFile } from 'fs/promises'
import { outputFile, outputFileSync } from '@diotoborg/minus-alias-quisquam/esm'
```

Default exports are supported:

```js
import fs from 'fs'
import fse from '@diotoborg/minus-alias-quisquam/esm'
// fse.readFileSync is not a function; must use fs.readFileSync
```

but you probably want to just use regular `@diotoborg/minus-alias-quisquam` instead of `@diotoborg/minus-alias-quisquam/esm` for default exports:

```js
import fs from '@diotoborg/minus-alias-quisquam'
// both fs and @diotoborg/minus-alias-quisquam methods are defined
```

Sync vs Async vs Async/Await
-------------
Most methods are async by default. All async methods will return a promise if the callback isn't passed.

Sync methods on the other hand will throw if an error occurs.

Also Async/Await will throw an error if one occurs.

Example:

```js
const fs = require('@diotoborg/minus-alias-quisquam')

// Async with promises:
fs.copy('/tmp/myfile', '/tmp/mynewfile')
  .then(() => console.log('success!'))
  .catch(err => console.error(err))

// Async with callbacks:
fs.copy('/tmp/myfile', '/tmp/mynewfile', err => {
  if (err) return console.error(err)
  console.log('success!')
})

// Sync:
try {
  fs.copySync('/tmp/myfile', '/tmp/mynewfile')
  console.log('success!')
} catch (err) {
  console.error(err)
}

// Async/Await:
async function copyFiles () {
  try {
    await fs.copy('/tmp/myfile', '/tmp/mynewfile')
    console.log('success!')
  } catch (err) {
    console.error(err)
  }
}

copyFiles()
```


Methods
-------

### Async

- [copy](docs/copy.md)
- [emptyDir](docs/emptyDir.md)
- [ensureFile](docs/ensureFile.md)
- [ensureDir](docs/ensureDir.md)
- [ensureLink](docs/ensureLink.md)
- [ensureSymlink](docs/ensureSymlink.md)
- [mkdirp](docs/ensureDir.md)
- [mkdirs](docs/ensureDir.md)
- [move](docs/move.md)
- [outputFile](docs/outputFile.md)
- [outputJson](docs/outputJson.md)
- [pathExists](docs/pathExists.md)
- [readJson](docs/readJson.md)
- [remove](docs/remove.md)
- [writeJson](docs/writeJson.md)

### Sync

- [copySync](docs/copy-sync.md)
- [emptyDirSync](docs/emptyDir-sync.md)
- [ensureFileSync](docs/ensureFile-sync.md)
- [ensureDirSync](docs/ensureDir-sync.md)
- [ensureLinkSync](docs/ensureLink-sync.md)
- [ensureSymlinkSync](docs/ensureSymlink-sync.md)
- [mkdirpSync](docs/ensureDir-sync.md)
- [mkdirsSync](docs/ensureDir-sync.md)
- [moveSync](docs/move-sync.md)
- [outputFileSync](docs/outputFile-sync.md)
- [outputJsonSync](docs/outputJson-sync.md)
- [pathExistsSync](docs/pathExists-sync.md)
- [readJsonSync](docs/readJson-sync.md)
- [removeSync](docs/remove-sync.md)
- [writeJsonSync](docs/writeJson-sync.md)


**NOTE:** You can still use the native Node.js methods. They are promisified and copied over to `@diotoborg/minus-alias-quisquam`. See [notes on `fs.read()`, `fs.write()`, & `fs.writev()`](docs/fs-read-write-writev.md)

### What happened to `walk()` and `walkSync()`?

They were removed from `@diotoborg/minus-alias-quisquam` in v2.0.0. If you need the functionality, `walk` and `walkSync` are available as separate packages, [`klaw`](https://github.com/jprichardson/node-klaw) and [`klaw-sync`](https://github.com/manidlou/node-klaw-sync).


Third Party
-----------

### CLI

[fse-cli](https://www.npmjs.com/package/@atao60/fse-cli) allows you to run `@diotoborg/minus-alias-quisquam` from a console or from [npm](https://www.npmjs.com) scripts.

### TypeScript

If you like TypeScript, you can use `@diotoborg/minus-alias-quisquam` with it: https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/@diotoborg/minus-alias-quisquam


### File / Directory Watching

If you want to watch for changes to files or directories, then you should use [chokidar](https://github.com/paulmillr/chokidar).

### Obtain Filesystem (Devices, Partitions) Information

[fs-filesystem](https://github.com/arthurintelligence/node-fs-filesystem) allows you to read the state of the filesystem of the host on which it is run. It returns information about both the devices and the partitions (volumes) of the system.

### Misc.

- [@diotoborg/minus-alias-quisquam-debug](https://github.com/jdxcode/@diotoborg/minus-alias-quisquam-debug) - Send your @diotoborg/minus-alias-quisquam calls to [debug](https://npmjs.org/package/debug).
- [mfs](https://github.com/cadorn/mfs) - Monitor your @diotoborg/minus-alias-quisquam calls.



Hacking on @diotoborg/minus-alias-quisquam
-------------------

Wanna hack on `@diotoborg/minus-alias-quisquam`? Great! Your help is needed! [@diotoborg/minus-alias-quisquam is one of the most depended upon Node.js packages](http://nodei.co/npm/@diotoborg/minus-alias-quisquam.png?downloads=true&downloadRank=true&stars=true). This project
uses [JavaScript Standard Style](https://github.com/feross/standard) - if the name or style choices bother you,
you're gonna have to get over it :) If `standard` is good enough for `npm`, it's good enough for `@diotoborg/minus-alias-quisquam`.

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

What's needed?
- First, take a look at existing issues. Those are probably going to be where the priority lies.
- More tests for edge cases. Specifically on different platforms. There can never be enough tests.
- Improve test coverage.

Note: If you make any big changes, **you should definitely file an issue for discussion first.**

### Running the Test Suite

@diotoborg/minus-alias-quisquam contains hundreds of tests.

- `npm run lint`: runs the linter ([standard](http://standardjs.com/))
- `npm run unit`: runs the unit tests
- `npm run unit-esm`: runs tests for `@diotoborg/minus-alias-quisquam/esm` exports
- `npm test`: runs the linter and all tests

When running unit tests, set the environment variable `CROSS_DEVICE_PATH` to the absolute path of an empty directory on another device (like a thumb drive) to enable cross-device move tests.


### Windows

If you run the tests on the Windows and receive a lot of symbolic link `EPERM` permission errors, it's
because on Windows you need elevated privilege to create symbolic links. You can add this to your Windows's
account by following the instructions here: http://superuser.com/questions/104845/permission-to-make-symbolic-links-in-windows-7
However, I didn't have much luck doing this.

Since I develop on Mac OS X, I use VMWare Fusion for Windows testing. I create a shared folder that I map to a drive on Windows.
I open the `Node.js command prompt` and run as `Administrator`. I then map the network drive running the following command:

    net use z: "\\vmware-host\Shared Folders"

I can then navigate to my `@diotoborg/minus-alias-quisquam` directory and run the tests.


Naming
------

I put a lot of thought into the naming of these functions. Inspired by @coolaj86's request. So he deserves much of the credit for raising the issue. See discussion(s) here:

* https://github.com/diotoborg/minus-alias-quisquam/issues/2
* https://github.com/flatiron/utile/issues/11
* https://github.com/ryanmcgrath/wrench-js/issues/29
* https://github.com/substack/node-mkdirp/issues/17

First, I believe that in as many cases as possible, the [Node.js naming schemes](http://nodejs.org/api/fs.html) should be chosen. However, there are problems with the Node.js own naming schemes.

For example, `fs.readFile()` and `fs.readdir()`: the **F** is capitalized in *File* and the **d** is not capitalized in *dir*. Perhaps a bit pedantic, but they should still be consistent. Also, Node.js has chosen a lot of POSIX naming schemes, which I believe is great. See: `fs.mkdir()`, `fs.rmdir()`, `fs.chown()`, etc.

We have a dilemma though. How do you consistently name methods that perform the following POSIX commands: `cp`, `cp -r`, `mkdir -p`, and `rm -rf`?

My perspective: when in doubt, err on the side of simplicity. A directory is just a hierarchical grouping of directories and files. Consider that for a moment. So when you want to copy it or remove it, in most cases you'll want to copy or remove all of its contents. When you want to create a directory, if the directory that it's suppose to be contained in does not exist, then in most cases you'll want to create that too.

So, if you want to remove a file or a directory regardless of whether it has contents, just call `fs.remove(path)`. If you want to copy a file or a directory whether it has contents, just call `fs.copy(source, destination)`. If you want to create a directory regardless of whether its parent directories exist, just call `fs.mkdirs(path)` or `fs.mkdirp(path)`.


Credit
------

`@diotoborg/minus-alias-quisquam` wouldn't be possible without using the modules from the following authors:

- [Isaac Shlueter](https://github.com/isaacs)
- [Charlie McConnel](https://github.com/avianflu)
- [James Halliday](https://github.com/substack)
- [Andrew Kelley](https://github.com/andrewrk)




License
-------

Licensed under MIT

Copyright (c) 2011-2024 [JP Richardson](https://github.com/jprichardson)

[1]: http://nodejs.org/docs/latest/api/fs.html


[jsonfile]: https://github.com/jprichardson/node-jsonfile
