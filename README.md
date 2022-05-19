# SwiftLint-GitHooks

This is an experiment using the `pre-commit` hook with SwiftLint. 

## How it's works?

First, to generate the `swiftlint` log, I added a Build Phase Script on Xcode using the `>` operator to output directly on a file named `swiftlint.txt`.

![](/buildphase.png)

Then, the `pre-commit` script will check if this file has a `warning` string using the `grep` command.

```bash

warnings="$(grep -q "warning" swiftlint.txt)"

if $warnings > 0 ; then
  if $warnings > 1; then
    cecho "RED" "⚠️  Check these warnings before your commit  ⚠️"
  else
    cecho "RED" "⚠️  Check this warning before your commit  ⚠️"
  fi
  cecho "YELLOW" "$(<swiftlint.txt)"
  exit 0
fi

```

**Note**:  the `cecho` function I found on [this Stackoverflow question](https://stackoverflow.com/a/53463162/2773779) created by [ndrwnaguib](https://github.com/ndrwnaguib).

Then you have a nice output

![](/terminal.png)
