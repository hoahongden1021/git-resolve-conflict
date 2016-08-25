> Resolve merge conflict in one file, using given strategy (--ours, --theirs, --union)
>
>     git resolve-conflict --ours package.json
>     git resolve-conflict --theirs package.json
>     git resolve-conflict --union package.json
>
>     git resolve-ours package.json
>     git resolve-theirs package.json
>     git resolve-union package.json

Installation
-----------

  - copy `/lib/git-resolve-conflict.sh` to your `.bashrc` (this adds just `git resolve-conflict`)
  - or `npm install -g git-resolve-conflict` (this also adds 3 other helpers)

 [![Get it on npm](https://nodei.co/npm/git-resolve-conflict.png?compact=true)](https://www.npmjs.org/package/git-resolve-conflict)

TL;DR
=====

It's just a tiny wrapper around [git-merge-file](https://git-scm.com/docs/git-merge-file) to simplify the API. See `./lib/git-resolve-conflict.sh`.
(I used temp files instead of process substitution to make it msys/mingw-friendly).

It's better than `git merge -Xours` because that would resolve conflicts for all files. Here we can resolve conflict for just one file.

It's better than `git checkout --ours package.json` because that would lose changes from `theirs` even if they are not conflicted.
Here we can resolve conflict using a three-way merge and keep the non-conflicted changes from both sides.

See also http://stackoverflow.com/q/39126509/245966

Description
===========

**Check `./lib/git-resolve-conflict.sh` in this repo!**
    me@mymachine /d/gh/merge-file-ours-poc (merge_master_to_develop +|MERGING)
    $ git diff --cached
    diff --git a/added-in-master.txt b/added-in-master.txt
    new file mode 100644
    index 0000000..9cef8af
    --- /dev/null
    +++ b/added-in-master.txt
    @@ -0,0 +1 @@
    +added in master
    diff --git a/package.json b/package.json
    index 75c469b..03f513b 100644
    --- a/package.json
    +++ b/package.json
    @@ -6,6 +6,10 @@
       "scripts": {
         "test": "echo \"Error: no test specified\" && exit 1"
       },
    +  "dependencies": {
    +    "foobar": "1.0.0",
    +    "quux": "2.0.0"
    +  },
       "author": "",
       "license": "ISC"
     }

            modified:   package.json