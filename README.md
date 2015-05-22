# Heroku buildpack: sh
A [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
that runs shell scripts during deploy process.

## Usage
This buildpack works best with
[heroku-buildpack-multi](https://github.com/heroku/heroku-buildpack-multi)
so that it can be used with your app's existing buildpacks.
Add a line

```
https://github.com/zunda/heroku-buildpack-sh.git
```

into the file `.buildpacks` anywhere you want to run the scripts.

Place shell scripts to be run during deploy into the directory `./.buildpack-sh`
and add execute flag: `chmod +x` to them.
This buildpack runs `run-parts -v .buildpack-sh` to detect and execute them.

### Example
```
$ heroku buildpacks
=== <app-name> Buildpack URL
https://github.com/heroku/heroku-buildpack-multi.git
$ cat .buildpacks
https://github.com/heroku/heroku-buildpack-apt.git
https://github.com/zunda/heroku-buildpack-sh.git
https://github.com/heroku/heroku-buildpack-ruby.git
$ ls -l .buildpack-sh/printenv
-rwxrwxr-x 1 zunda zunda 48 May 22 19:58 .buildpack-sh/source_version
$ cat .buildpack-sh/source_version
#!/bin/sh

echo SOURCE_VERSION: $SOURCE_VERSION
```

## License
[MIT](LICENSE)
