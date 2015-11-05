# Heroku buildpack: sh
A [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
that runs shell scripts during deploy process.

## Usage
This buildpack works best with another buildpack for your app.

First, [set the buildpack for your app](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app#setting-a-buildpack), e.g.:

```
$  heroku buildpacks:set heroku/ruby
```

then, [add this buildpack](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app#adding-a-buildpack) to run a script while building your app::

```
$ heroku buildpacks:add --index 1 https://github.com/zunda/heroku-buildpack-sh.git
```

Place shell scripts to be run during deploy into the directory `./.buildpack-sh`
and add execute flag: `chmod +x` to them.
This buildpack runs `run-parts -v .buildpack-sh` to detect and execute them.

### Example
```
$ heroku buildpacks:set heroku/ruby
$ heroku buildpacks:add --index 1 https://github.com/zunda/heroku-buildpack-sh.git
$ heroku buildpacks:add --index 1 https://github.com/heroku/heroku-buildpack-apt.git
Buildpack added. Next release on daigo-pi will use:
  1. https://github.com/heroku/heroku-buildpack-apt.git
  2. https://github.com/zunda/heroku-buildpack-sh.git
  3. heroku/ruby
Run git push heroku master to create a new release using these buildpacks.
$ ls -l .buildpack-sh/source_version
-rwxrwxr-x 1 zunda zunda 48 May 22 19:58 .buildpack-sh/source_version
$ cat .buildpack-sh/source_version
#!/bin/sh

echo SOURCE_VERSION: $SOURCE_VERSION
```

## License
[MIT](LICENSE)
