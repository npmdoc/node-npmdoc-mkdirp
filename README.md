# api documentation for  [mkdirp (v0.5.1)](https://github.com/substack/node-mkdirp#readme)  [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-mkdirp.svg)](https://travis-ci.org/npmdoc/node-npmdoc-mkdirp)
#### Recursively mkdir, like `mkdir -p`

[![NPM](https://nodei.co/npm/mkdirp.png?downloads=true)](https://www.npmjs.com/package/mkdirp)

[![apidoc](https://npmdoc.github.io/node-npmdoc-mkdirp/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-mkdirp_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-mkdirp/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-mkdirp/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "James Halliday",
        "email": "mail@substack.net",
        "url": "http://substack.net"
    },
    "bin": {
        "mkdirp": "bin/cmd.js"
    },
    "bugs": {
        "url": "https://github.com/substack/node-mkdirp/issues"
    },
    "dependencies": {
        "minimist": "0.0.8"
    },
    "description": "Recursively mkdir, like 'mkdir -p'",
    "devDependencies": {
        "mock-fs": "2 >=2.7.0",
        "tap": "1"
    },
    "directories": {},
    "dist": {
        "shasum": "30057438eac6cf7f8c4767f38648d6697d75c903",
        "tarball": "https://registry.npmjs.org/mkdirp/-/mkdirp-0.5.1.tgz"
    },
    "gitHead": "d4eff0f06093aed4f387e88e9fc301cb76beedc7",
    "homepage": "https://github.com/substack/node-mkdirp#readme",
    "keywords": [
        "mkdir",
        "directory"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "substack",
            "email": "mail@substack.net"
        }
    ],
    "name": "mkdirp",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/substack/node-mkdirp.git"
    },
    "scripts": {
        "test": "tap test/*.js"
    },
    "version": "0.5.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module mkdirp](#apidoc.module.mkdirp)
1.  [function <span class="apidocSignatureSpan"></span>mkdirp (p, opts, f, made)](#apidoc.element.mkdirp.mkdirp)
1.  [function <span class="apidocSignatureSpan">mkdirp.</span>mkdirP (p, opts, f, made)](#apidoc.element.mkdirp.mkdirP)
1.  [function <span class="apidocSignatureSpan">mkdirp.</span>sync (p, opts, made)](#apidoc.element.mkdirp.sync)



# <a name="apidoc.module.mkdirp"></a>[module mkdirp](#apidoc.module.mkdirp)

#### <a name="apidoc.element.mkdirp.mkdirp"></a>[function <span class="apidocSignatureSpan"></span>mkdirp (p, opts, f, made)](#apidoc.element.mkdirp.mkdirp)
- description and source-code
```javascript
function mkdirP(p, opts, f, made) {
    if (typeof opts === 'function') {
        f = opts;
        opts = {};
    }
    else if (!opts || typeof opts !== 'object') {
        opts = { mode: opts };
    }

    var mode = opts.mode;
    var xfs = opts.fs || fs;

    if (mode === undefined) {
        mode = _0777 & (~process.umask());
    }
    if (!made) made = null;

    var cb = f || function () {};
    p = path.resolve(p);

    xfs.mkdir(p, mode, function (er) {
        if (!er) {
            made = made || p;
            return cb(null, made);
        }
        switch (er.code) {
            case 'ENOENT':
                mkdirP(path.dirname(p), opts, function (er, made) {
                    if (er) cb(er, made);
                    else mkdirP(p, opts, cb, made);
                });
                break;

            // In the case of any other error, just see if there's a dir
            // there already.  If so, then hooray!  If not, then something
            // is borked.
            default:
                xfs.stat(p, function (er2, stat) {
                    // if the stat fails, then that's super weird.
                    // let the original error be the failure reason.
                    if (er2 || !stat.isDirectory()) cb(er, made)
                    else cb(null, made);
                });
                break;
        }
    });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.mkdirp.mkdirP"></a>[function <span class="apidocSignatureSpan">mkdirp.</span>mkdirP (p, opts, f, made)](#apidoc.element.mkdirp.mkdirP)
- description and source-code
```javascript
function mkdirP(p, opts, f, made) {
    if (typeof opts === 'function') {
        f = opts;
        opts = {};
    }
    else if (!opts || typeof opts !== 'object') {
        opts = { mode: opts };
    }

    var mode = opts.mode;
    var xfs = opts.fs || fs;

    if (mode === undefined) {
        mode = _0777 & (~process.umask());
    }
    if (!made) made = null;

    var cb = f || function () {};
    p = path.resolve(p);

    xfs.mkdir(p, mode, function (er) {
        if (!er) {
            made = made || p;
            return cb(null, made);
        }
        switch (er.code) {
            case 'ENOENT':
                mkdirP(path.dirname(p), opts, function (er, made) {
                    if (er) cb(er, made);
                    else mkdirP(p, opts, cb, made);
                });
                break;

            // In the case of any other error, just see if there's a dir
            // there already.  If so, then hooray!  If not, then something
            // is borked.
            default:
                xfs.stat(p, function (er2, stat) {
                    // if the stat fails, then that's super weird.
                    // let the original error be the failure reason.
                    if (er2 || !stat.isDirectory()) cb(er, made)
                    else cb(null, made);
                });
                break;
        }
    });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.mkdirp.sync"></a>[function <span class="apidocSignatureSpan">mkdirp.</span>sync (p, opts, made)](#apidoc.element.mkdirp.sync)
- description and source-code
```javascript
function sync(p, opts, made) {
    if (!opts || typeof opts !== 'object') {
        opts = { mode: opts };
    }

    var mode = opts.mode;
    var xfs = opts.fs || fs;

    if (mode === undefined) {
        mode = _0777 & (~process.umask());
    }
    if (!made) made = null;

    p = path.resolve(p);

    try {
        xfs.mkdirSync(p, mode);
        made = made || p;
    }
    catch (err0) {
        switch (err0.code) {
            case 'ENOENT' :
                made = sync(path.dirname(p), opts, made);
                sync(p, opts, made);
                break;

            // In the case of any other error, just see if there's a dir
            // there already.  If so, then hooray!  If not, then something
            // is borked.
            default:
                var stat;
                try {
                    stat = xfs.statSync(p);
                }
                catch (err1) {
                    throw err0;
                }
                if (!stat.isDirectory()) throw err0;
                break;
        }
    }

    return made;
}
```
- example usage
```shell
...
'cb(err, made)' fires with the error or the first directory 'made'
that had to be created, if any.

You can optionally pass in an alternate 'fs' implementation by passing in
'opts.fs'. Your implementation should have 'opts.fs.mkdir(path, mode, cb)' and
'opts.fs.stat(path, cb)'.

## mkdirp.sync(dir, opts)

Synchronously create a new directory and any necessary subdirectories at 'dir'
with octal permission string 'opts.mode'. If 'opts' is a non-object, it will be
treated as the 'opts.mode'.

If 'opts.mode' isn't specified, it defaults to '0777 & (~process.umask())'.
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
