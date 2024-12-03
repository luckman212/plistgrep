# plistgrep

Parse and search (grep) Apple Plist files, leveraging Python's builtin [`plistlib`](https://docs.python.org/3/library/plistlib.html) standard library.

The search string is specified as a case-insensitive regex.

Accepts one or more filenames.

Output is in JSON format.

## Syntax

```
plistgrep <regex> <filename> [filename...]
```

## Example use

```
plistgrep 'Shown?' ~/Library/Preferences/com.apple.AddressBook.plist
```

#### Sample output 1

```
{
  "filename": "/Users/luke/Library/Preferences/com.apple.AddressBook.plist",
  "match_count": 4,
  "matches": [
    {
      "matched_string": "Show",
      "key": "ABShowPeoplePickerDebugPanel",
      "value": false
    },
    {
      "matched_string": "Shown",
      "key": "NSToolbar Configuration NSPreferences/TB Is Shown",
      "value": 1
    },
    {
      "matched_string": "Shown",
      "key": "ABLastImportShown",
      "value": true
    },
    {
      "matched_string": "Show",
      "key": "ABShowDebugMenu",
      "value": true
    }
  ]
}
```

## Silent mode

If no matches are found, the program's exitcode will be 1. So, by redirecting its output to the bitbucket, it can be used "quietly" in a shell script (similar to `grep -q`):

```
if ! plistgrep Foo /path/to/bar.plist &>/dev/null ; then
  echo "nothing found, proceeding to Baz the Quuxes..."
  ...
fi
```

## Emulating plutil -p output

If you have [jq](https://jqlang.github.io/jq/) installed, you can emulate the plaintext output of `plutil -p` with something like:

```
plistgrep 'Shown?' ~/Library/Preferences/com.apple.AddressBook.plist |
jq -r '.matches[] | "\(.key) => \(.value)"'
```

#### Sample output 2

```
ABShowPeoplePickerDebugPanel => false
NSToolbar Configuration NSPreferences/TB Is Shown => 1
ABLastImportShown => true
ABShowDebugMenu => true
```

## Why?

This tool was inspired by [this](https://apple.stackexchange.com/questions/476842/is-there-any-way-to-grep-a-binary-plist) StackExchange/AskDifferent post.
