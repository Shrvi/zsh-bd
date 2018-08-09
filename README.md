# zsh-bdi

Quickly go back to a specific parent directory instead of typing `cd ../../..` redundantly.

---

This is a reimplementation of [Tarrasch](https://github.com/Tarrasch)'s [zsh-bd](https://github.com/Tarrasch/zsh-bd).
It comes with less code, even more zsh builtin functionality, and a slightly improved parent choosing algorithm.

## Tip

 To get the feel of `setopt autocd` back, add `alias ..=bdi` to your `zshrc`.



## Usage

`bdi [OPTIONS] [n|parent|{pattern ...}]`

Multiple patterns will be interpreted as `pattern*pattern2*...*patternN`

Pattern can either be a text, to match a parent, a number to go _number_ directories back, or a sequence of dots.



## Installation

Use your preferred zsh plugin manager. For installation instructions see their sites.

For manual installation download [zsh-bdi.zsh](./zsh-bdi.zsh) and `source` the file in your `zshrc`.  
For completions download [\_bdi.zsh](./\_bdi.zsh) and add the directory where the file is located to `$fpath`.



## Order of finding the best matching parent

1. If no arguments are given, go one directory back.

2. Find parent that matches the passed pattern.¹

3. Find parent that begins with the passed pattern.¹

4. If the passed pattern is a sequence of dots `$\.+^`, go amount of dots +1 parents back.²

5. If the passed pattern is a _number_, go _number_ directories back. 0 is a shortcut to /.²

6. return 1

[1] If there are more than one, _bdi_ chooses the closest to _pwd_.  
[2] If the amount of dots, or number is greater than the amount of parents, the resulting directory is /, and no error will be raised.

