# SwiftLint-GitHooks

This is an experiment using the `pre-commit` hook with SwiftLint. 

## How it's works?

First, to generate the `swiftlint` log, I added a Build Phase Script on Xcode using the `>` operator to output directly on a file named `swiftlint.txt`.

![](/buildphase.png)

Then, the `pre-commit` script will check if this file has a `warning` string using the `grep` command.

```bash

if grep -q "warning" swiftlint.txt; then
  cecho "RED" "⚠️  Check this warnings before your commit  ⚠️"
  cecho "YELLOW" "$(<swiftlint.txt)"
  exit 0
fi

```

**Note**:  the `cecho` function I found on [this Stackoverflow question](https://stackoverflow.com/a/53463162/2773779) created by [ndrwnaguib](https://github.com/ndrwnaguib).

Then you have a nice output

![](/terminal.png)

There is a typo here, because **this** is just **one** warning, **these** for multiple warnings. You can check the number of occurences and to choose between this or these, warning or warnings.
