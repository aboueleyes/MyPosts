# Search and replace in vim 
## Basic search and replace

In Vim, you can find and replace text using the `:substitute` `(:s)` command.

To run commands in Vim, you must be in normal mode, the default mode when starting the editor. To go back to normal mode from any other mode, just press the ‘Esc’ key.

The general form of the substitute command is as follows:

``` vim Script
:[range]s/{pattern}/{string}/[flags] [count]
```
The command searches each line in `[range]` for a `{pattern}`, and replaces it with a `{string`}. `[count]` is a positive integer that multiplies the command.

If no `[range`] and `[count]` are given, only the pattern found in the current line is replaced. The current line is the line where the cursor is placed.

### Examples 

`:s/foo/bar/g`
Find each occurrence of 'foo' (in the current line only), and replace it with 'bar'.

`:%s/foo/bar/g`
Find each occurrence of 'foo' (in all lines), and replace it with 'bar'.

`:%s/foo/bar/gc`
Change each 'foo' to 'bar', but ask for confirmation first.

`:%s/\<foo\>/bar/gc`
Change only whole words exactly matching 'foo' to 'bar'; ask for confirmation.

#### Case Sensitivity 

`:%s/foo/bar/gci`
Change each 'foo' (case insensitive due to the i flag) to 'bar'; ask for confirmation.

Another way to force ignore case is to append `\c` after the search pattern. For example, `/Linux\c` performs ignore case search.

`:%s/foo\c/bar/gc` is same as the above 

### Search Range 

When no range is specified the substitute command operates only in the current line.
The range can be either one line or a range between two lines. The line specifiers are separated with the , or ; characters. The range can be specified using the absolute line number or special symbols.
For example, to substitute all occurrences of ‘foo’ to ‘bar’ in all lines starting from line 7 to line 13 you would use:

```vim Script
:7,13s/foo/bar/g
```
The range is inclusive, which means that the first and last lines are included in the range.
The dot `.` character indicates the current line and `$` - the dollar sign the last line. To substitute ‘foo’ in all lines starting from the current line to the last one:

``` vim Script
:.,$s/foo/bar/
```

The line specifier can also be set using the ‘+’ or ‘-’ symbol,followed by a number that is added or subtracted from the preceding line number. If the number after the symbol is omitted, it defaults to 1.

For example to substitute each ‘foo’ with ‘bar’ starting from the current line and the five next lines, type:

``` vim Script
:.,+5s/foo/bar/g
```

When compiled with +visual, change each 'foo' to 'bar' for all lines within a visual selection. Vim automatically appends the visual selection range ('<,'>) for any ex command when you select an area and enter :.

``` vim Script
:'<,'>s/foo/bar/g	
```

## Examples

Comment lines (add # before the line) from 15 to 20:

``` vim Script
:15,20s/^/#/
```

Uncomment lines (remove # before the line) from 15 to 20:
``` vim Script
:5,20s/^#//
```
Replace each match of the last search pattern with 'bar'.
For example, you might first place the cursor on the word foo then press * to search for that word.
The above substitute would then change all words exactly matching 'foo' to 'bar'.

``` vim Script
:%s//bar/g
```
On each line, replace the last occurrence of "foo" with "bar".
``` vim Script
:%s/.*\zsfoo/bar/
```
Remove trailing whitespace at the end of each line:

``` vim Script
:%s/\s\+$//e
```
`:%s` to run `:substitute` over the range `%`, which is the entire buffer.

`\s` to match all whitespace characters.

`\+` to match 1 or more of them.

`$` to anchor at the end of the line.

The `e` flag to not give an error if there is no match (i.e. the file is already without trailing whitespace).
