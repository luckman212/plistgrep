# plistgrep

Parse and search (grep) Apple Plist files, leveraging the builtin [`plistlib`](https://docs.python.org/3/library/plistlib.html) standard library. The search string is specified as a regex.

Accepts one or more filenames.

# Syntax

```
plistgrep <regex> <filename> [filename...]
```

# Example

```
$ plistgrep 'Shown?' ~/Library/Preferences/com.apple.AddressBook.plist
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
