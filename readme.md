# smudge and clean

## the basic idea

git provides filters which you can access via
your `attributes` and `config` files.

This project sets up simple smudge and clean
filters to demonstrate how they work.

## context

More info here:

http://git-scm.com/book/ch7-2.html

## how it works

Filters are arbitrary Unix software. They must
conform to the standard interface for all Unix
software: take input via `stdin`, write output to
`stdout`, exit with a 0 for success or any number
up to 255 for failure, etc. Unfortunately, git
seems to suppress filter output whether it happens
on `stdout` or `stderr`.

However, "arbitrary Unix software" means you can
implement these filters in a huge range of ways.
You could easily use a Node.js "binary"
prepared in the `npm` way, or a Ruby "binary"
prepared in the `gem` way.

The `clean` and `smudge` filters in this directory
are simple bash scripts which run simple one-line
Ruby commands. They convert tabs into spaces when
you check a file out, and convert spaces into tabs
when you commit a file. They read from `stdin`
and write to `stdout` using Ruby's `$stdin` and
`$stdout` global variables.

The files `git.config.sample` and
`git.attributes.sample` show lines you should
add to your `config` and `attributes` files in
order to make this work. Those files live at
either `.git/info/attributes` (project-local)
or `.gitattributes` (global), for `attributes`,
and either `.git/config` (project-local) or
`.gitconfig` (global), for `config`.

