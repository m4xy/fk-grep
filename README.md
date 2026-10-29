# fk-grep

grep, in [fckt](https://github.com/m4xy/fckt): the lines of each file that match a pattern. It's an
example of a real program in fckt, made of [fk-regex](../fk-regex) and [fk-cli](../fk-cli), and
small: what it takes and what searching comes to are in `Grep`, which is pure, and `main` only reads
the files and prints.

```
$ kiln build
$ build/bin/fk-grep -n 'Diagnostics\.\w+' Checker.fk
16:  typeNames(...) = Diagnostics.collecting {
$ build/bin/fk-grep --help
usage: fk-grep [options] PATTERN FILE...
...
```

Its patterns are fk-regex's, matched in time linear in the text, whatever the pattern. It takes
grep's `-F -i -v -w -c -o -l -n -h`, reads standard input when there are no files, and exits as grep
does: 0 if a line matched, 1 if none did, and 2 if something went wrong, as a file that can't be read
or a pattern that isn't one, having searched the files it could.

It needs fckt's `Channels.standardInput` and `printError`, on the branch `std-standard-streams`.
`kiln build` runs the tests in `test/`, which search text in memory through `Grep`.
