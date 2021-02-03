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
