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

