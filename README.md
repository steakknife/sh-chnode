Chnode
=========
[![NPM version][npm-badge]](http://badge.fury.io/js/chnode)

[npm-badge]: https://badge.fury.io/js/chnode.png

Change between installed Node versions in your current shell with a simple
`chnode VERSION`. Leaves the system version untouched. Works out of the box with
Mac's [Homebrew][homebrew].

[homebrew]: https://github.com/Homebrew/homebrew

### Tour
- Change only the current shell without affecting the rest of the system
- Works out of the box with paths used by Mac's [Homebrew][homebrew]
- Extendable by adding more Node paths to the `NODES` variable
- Leaves installing Node versions to your package manager thereby adhering to
  the *do one thing and do it well* principle
- Works in Bash and Zsh, and possibly other POSIX compatible shells
- Does not pollute your shell namespaces with internal functions
- Lightweight
- Written in the shell language ([KISS][kiss])
- Able to automaticallly-switch `node`s (source `chnode-auto` instead of `chnode`)
- Able to run under a node without hooking the shell (via `chnode-exec`)
- Doesn't hook `cd`

Side note: I'm terribly ashamed of not yet having tests!

[kiss]: https://en.wikipedia.org/wiki/Keep_it_simple_stupid

### Differences
There are a few existing tools for switching Node versions, so how does
Chnode differ?
- It **does not** manage installations.  
  Existing package managers (GNU/Linux distros', Homebrew etc.) do a better job
  of installing or compiling securely than such scripts.
- It's **really lightweight** — just a single shell function.  
  No build tools or compilers necessary.
- It changes the node version **only for the current shell session**.  
  Tools like [n][n] or [nvm][nvm] affect the entire system or all open shells.
  That's why if you need to test a single app in multiple Node versions,
  Chnode comes very handy.

### Alternatives
If you do insist on compiling and installing Nodes via 3rd-party tools, check
these out:
- [nvm][nvm]
- [n][n]
- [nodist][nodist]
- [nodenv][nodenv]
- [node-build][node-build] (node-env plugin)

[nvm]: https://github.com/brianloveswords/nvm
[n]: https://github.com/visionmedia/n
[nodist]: https://github.com/marcelklehr/nodist
[nodenv]: https://github.com/nodenv/nodenv
[node-build]: https://github.com/nodenv/node-build


Installing
----------
Install Chnode globally with:
```sh
npm install --global steakknife/chnode
```

Then source it in your shell:
```sh
. "$(npm bin --global)/chnode"
```

For convenience you might want to put the **output** of the following in your
`.zshrc` or `.bashrc`.  
It'll be faster than running the line above with `npm bin` which will slow down
your shell loading.
```sh
echo ". \"$(npm bin --global)/chnode\""
```

Installing automatic-switching
------------------------------
If `.nvmrc` or `.node-version` are available, use the following to switch nodes automatically:

```sh
. "$(npm bin --global)/chnode-auto"
```

Run using a specific node version (without switching)
---------------------------------------------------------
```sh
"$(npm bin --global)/chnode-exec" 6.9 -- node ...
```

Using
-----
Change between installed Node versions with:
```sh
chnode 0.12.2
```

To change to the latest installed v0.11.x (e.g. Node 0.11.15):
```sh
chnode 0.11
```

To change to the latest v0.x:
```sh
chnode 0
```

To go back to the system version:
```sh
chnode system
```

### Options
Option           | Description
-----------------|------------
`-h, -?, --help `| Display this help.
`-l, --list     `| List all available Node versions.
`-r, --refresh  `| Refresh and find all available Node versions.
`-v, --verbose  `| Be verbose when changing versions.
`-V, --version  `| Display version information.


Configuring
-----------
On the Mac, Chnode will find installed Nodes in `/usr/local/Cellar/node`.  
If you've got installations somewhere else, set the `NODES` variable to an
**array of paths** of **individual versions**:
```sh
NODES+=(~/.nodes/*)
```

For example, if you've got Node compiled from the source at
`~/Development/node-master`, append that:
```sh
NODES+=(~/Development/node-master)
```

If you think Chnode should detect some of your paths automatically, please
let me know by [creating an issue][issues]. Thanks!

License
-------
Chnode is released under a *Lesser GNU Affero General Public License*, which
in summary means:

- You **can** use this program for **no cost**.
- You **can** use this program for **both personal and commercial reasons**.
- You **do not have to share your own program's code** which uses this program.
- You **have to share modifications** (e.g bug-fixes) you've made to this
  program.

For full legalese, see the [LICENSE](LICENSE) file.


About
-----
**[Andri Möll](http://themoll.com)** typed this and the code.  
[Monday Calendar](https://mondayapp.com) supported the engineering work.

If you find Chnode needs improving, please don't hesitate to type to me now
at [andri@dot.ee][email] or [create an issue online][issues].

[email]: mailto:andri@dot.ee
[issues]: https://github.com/steakknife/chnode/issues
