# zsh-bd

Quickly go back to a specific parent directory instead of typing `cd ../../..` redundantly.

---

This is a reimplementation of [Tarrasch](https://github.com/Tarrasch)'s [zsh-bd](https://github.com/Tarrasch/zsh-bd).
It comes with less code,  even more zsh builtin functionality, and a slightly improved [directory choosing algorithm](#algorithm).



## Hint

You may be used to quickly go back one directory with `..`, because of `setopt autocd`.
Well, add `alias ..=bd` to your `.zshrc` and extend your workflow.


## Usage

`bd [OPTIONS] [pattern [pattern2 ... patternN]]`

Multiple patterns will be interpreted as `pattern*pattern2*...*patternN`

Pattern can either be a text to match a parent directory or a number, to go _number_ directories back. [How does bd chooses the directory](#algorithm).


### Options

| Argument | Description |
| -------- | ----------- |
| -f | _bd_ skips textbased sarch. _Useful when a directory begins with a number._ |


## Installation

Use your preferred zsh plugin manager. For installation instructions see their sites.

**Of course, this plugin conflicts with [Tarrasch/zsh-bd](https://github.com/Tarrasch/zsh-bd) and [vigneshwaranr/bd](https://github.com/vigneshwaranr/bd)**

### Manual installation


```sh
d="your preferred location"
mkdir -p $d
cd $d
git clone https://github.com/Shrvi/zsh-bd
print ". \"$d/zsh-bd/zsh-bd.zsh\"" >> "${ZDOTDIR:-$HOME/.zshrc}"
```

## Algorithm

1. If _bd_ is called without arguments, it simply goes one directory back.

2. _bd_ tries to find directory that matches the passed pattern. [\*]

3. _bd_ tries to find a directory beginning with the passed pattern. [\*]

4. If the passed pattern is a _number_, _bd_ goes _number_ directories back.  If the passed _number_ is greater than the possible amount of parent directories, the new pwd will be / and **no** error will be raised. 0 is treated as a shortcut to /.

[\*] If there are more than one, _bd_ chooses the closest to _pwd_.