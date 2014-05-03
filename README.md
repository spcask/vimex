Vim Exercises
=============
This directory contains a set of Vim exercises that is designed to help
you to quickly learn and practice all of the essential features of Vim.


Contents
========
* [Introduction][0]
* [Lesson 1: Motions, delete and replace characters][1]
* [Lesson 2: Word motions, delete and insert text, line numbers][2]
* [Lesson 3: Windows, more motion and insert commands][3]
* [Lesson 4: Copy, paste, buffers][4]
* [Lesson 5: Tab pages, search][5]
* [Resources][6]
* [License][7]


Introduction
============
If you are viewing this file with a text editor, all commands would
appear enclosed within backquotes. You should not type the backquotes.
You should type only the commands within the backquotes.

The instructions for each exercise assume the use of Unix or Linux
system. For Windows system, you may replace the usage of `cp` and `diff`
commands with `copy` and `fc` commands respectively.

This document is not a Vim tutorial. You should have a little knowledge
of Vim, especially how to switch between the three popular modes: normal
mode, insert mode and command-line mode. You should know how to touch
type. If you want to learn to touch type, go to
<http://quickqwerty.com/>.


Lesson 1
========
Motions, delete and replace characters

Commands
--------
* `h`       - Move cursor left
* `j`       - Move cursor down
* `k`       - Move cursor up
* `l`       - Move cursor right
* `<BS>`    - Same as `h` but can wrap to the previous line
* `<Space>` - Same as `l` but can wrap to the next line
* `x`       - Delete character under the cursor
* `r`       - Replace character under the cursor
* `u`       - Undo changes
* `Ctrl-r`  - Redo changes that were undone
* `:wq`     - Write the current file and quit
* `:q!`     - Quit without writing (`:quit!`)

Notes
-----
The commands `h`, `j`, `k`, `l`, `<BS>` and `<Space>` are called motion
commands. These commands are entered in normal mode (also known as
command mode). You do not have to press `<Enter>` after typing these
commands. Merely typing the command executes it. The `x`, `r`, `u` and
`Ctrl-r` commands are also normal mode commands.

The commands `:wq` and `:q!` are Ex commands which are entered in
command-line mode. They are called command-line mode commands because as
soon as you press `:`, the command-line at the bottom of the screen is
activated where you can complete the command. You must press `<Enter>`
after typing the command to enter the command. For example, to enter the
Ex command `:wq`, you must type `:wq<Enter>`.

Exercise
--------
* In the shell, enter: `cp doc1.txt work.txt`.
* In the shell, enter: `vim work.txt`.
* Move around the document by pressing `h`, `j`, `k` and `l`.
* Do not use the arrow keys.
* Delete every occurrence of = in the document by pressing `x`.
* Replace every occurrence of _ with an appropriate letter by pressing
  `r` followed by the appropriate letter.
* If you make a mistake, press `u` to undo the mistake.
* Save the document and exit Vim by typing `:wq<Enter>`.
* In the shell, enter `diff -u ref1.txt work.txt`. Ensure that the above
  command returns no output. If you get any output, go to the second
  step in this list and fix the errors.


Lesson 2
========
Word motions, delete and insert text, line numbers

Commands
--------
* `w`               - Move forward to beginning of next word
* `e`               - Move forward to end of word (skips empty line)
* `b`               - Move backward to beginning of word
* `W`               - Move forward to beginning of next WORD
* `E`               - Move forward to end of WORD (skips empty line)
* `B`               - Move backward to beginning of WORD
* `d{motion}`       - Delete text that motion moves over
* `dd`              - Delete line under the cursor
* `i`               - Insert text before the cursor
* `a`               - Insert text after the cursor
* `o`               - Open a new line below the cursor and insert text
* `[count]`         - Optional number prefix to repeat a command
* `:set nu`         - Turn line numbers on (`:set number`)
* `:set {option}`   - Set boolean option; show value of number/string option
* `:set {option}?`  - Show value of option
* `:set no{option}` - Reset boolean option, e.g. `:set nonu`
* `:h`              - Show help (`:help`)
* `:h {subject}`    - Show help on subject (`:help {subject}`)

Notes
-----
The following sequence of characters are considered a word:
  - A continuous sequence of letters, digits or underscores.
  - A continuous sequence of characters that are not letters, digits,
    underscores and blank characters.
  - Empty line

The following sequence of characters are considered a WORD:
  - A continuous sequence of non-blank characters.
  - Empty line

The `w`, `e`, `b`, `W`, `E` and `B` commands are motion commands. The
`d` command is an opeator command. A motion command can be used after an
operator command, to have the operator command operate on the text that
the cursor moves over due to the motion command. Consider the
`d{motion}` command in the list above. An example of `d{motion}` command
is `de` which deletes text from the character under the cursor to the
end of the current or the next word.

A motion command is either exclusive or inclusive. When an operator
command is used with an inclusive motion command, the start and end
position of the motion are included in the operation. When an operator
command is used with an exclusive motion command, the last character
towards the end of the buffer is not included in the operation. There
are, however, some exceptions. Enter the Ex command `:h exclusive` to
learn about these exceptions.

If the previous paragraph was too confusing, move your cursor to the
middle of a word and compare the behaviour of `e` and `de` commands with
`w` and `dw`. The `e` command moves to the last character of a word and
`de` includes the last character of a word while deleting text. The `w`
command moves to the first character of the next word but `dw` does not
include the first character of the next word while deleting text. The
`b` command moves from the character under the cursor to the first
character of the current or previous word, but `db` does not include the
character under the cursor while deleting text. In other words, both
`dw` and `db` commands do not delete either the character where the
motion begins or the character where the motion ends, whichever comes
later in the file. The `e` and `E` commands are inclusive motion
commands whereas the `w`, `W`, `b` and `b` commands are exclusive motion
commands.

Exercise
--------
* In the shell, enter: `cp doc2.txt work.txt`.
* In the shell, enter: `vim work.txt`.
* Move around the document by pressing `w` and `b`.
* Use motion commands from the previous lesson if needed.
* Replace every occurrence of _ with an appropriate letter by pressing `r`.
* Delete every occurrence of ---- by pressing `de`.
* Press `i`, complete a word and press `<Esc>`.
* Save the document and exit Vim by typing `:wq<Enter>`.
* In the shell, enter `diff -u ref2.txt work.txt`. Ensure that the above
  command returns no output. If you get any output, go to the second
  step in this list and fix the errors.


Lesson 3
========
Windows, more motion and insert commands

Commands
--------
* `gg`         - Go to the first line, on the first non-blank character
* `G`          - Go to the last line, on the first non-blank character
* `{N}gg`      - Go to Nth line, on the first non-blank character
* `{N}G`       - Same as `{N}gg`
* `0`          - Go to the first character of the line
* `^`          - Go to the first non-blank character of the line
* `$`          - Go to the end of the line
* `I`          - Insert text before the first non-blank in the line
* `A`          - Append text at the end of the line
* `O`          - Open a new line above the cursor and insert text
* `:!{cmd}`    - Execute command with shell
* `:sp`        - Split current window into two (`:split`)
* `:sp {file}` - Split current window and edit file
* `:vs`        - Vertically split current window into two (`:vsplit`)
* `:vs {file}` - Vertically split current window and edit file
* `:new`       - Split and edit empty buffer
* `:vnew`      - Vertically split and edit empty buffer
* `:only`      - Make current window the only one on the screen
* `:w`         - Write current buffer to the file (`:write`)
* `:q`         - Quit current window; exit on last non-help window (`:quit`)
* `:qa`        - Quit all windows, i.e. exit Vim (`:qall`)
* `:close`     - Quit current window; fail on last window
* `Ctrl-w w`   - Go to the window (left to right, top to bottom)
* `Ctrl-w =`   - Make all windows equally high and wide
* `Ctrl-w _`   - Make current window highest possible
* `Ctrl-w |`   - Make current window widest possible
* `Ctrl-w s`   - Same as `:sp`
* `Ctrl-w v`   - Same as `:vs`
* `Ctrl-w n`   - Same as `:new`
* `Ctrl-w o`   - Same as `:only`
* `Ctrl-w q`   - Same as `:q`
* `Ctrl-w c`   - Same as `:close`

Exercise
--------
* In the shell, enter: `cp doc3.txt work.txt`.
* In the shell, enter: `vim work.txt`.
* Open ref3.txt in a new window by typing `:sp ref3.txt<Enter>`.
* Press `Ctrl-w w` to switch to the window containing work.txt.
* Move to the first line of work.txt by pressing `gg`.
* Use motion commands to move to a line containing hyphens only.
  Every such line containing hyphens only represent two missing lines.
* Then press `dd` to delete such a line.
* Then press `O` to insert the missing lines. Look ref3.txt in the other
  window for the missing lines and then type them in work.txt.
* Press `<Esc>` as soon as you are inserting text.
* When you need to scroll ref3.txt, press `Ctrl-w w` and use motion
  commands.
* Press `Ctrl-w w` to switch between windows.
* Edit work.txt with the steps above to make it identical to ref3.txt.
* Save the document by typing `:w<Enter>`.
* Type `:!diff -u ref3.txt work.txt<Enter>`. Ensure that this
  command returns no output. If you get any output, continue to edit the
  file and fix the errors.
* Type `:qa<Enter>` to quit all windows and exit Vim.


Lesson 4
========
Copy, paste, buffers

* `y{motion}`   - Yank (copy) text that motion moves over
* `yy`          - Yank (copy) line under the cursor
* `p`           - Put (paste) the text after the cursor
* `P`           - Put (paste) the text before the cursor
* `Ctrl-g`      - Show current file name, lines, status and cursor position
* `g Ctrl-g`    - Show column, line, word, character and/or byte positions
* `:ls`         - Show all buffers
* `:hide`       - Quit current window and hide buffer; fail on last window
* `:_%`         - % is replaced with current file name in Ex command
* `:_#`         - # is replaced with alternate file name in Ex command
* `:e`          - Edit the current file (`:edit`)
* `:e {file}`   - Edit file (`:edit {file}`)
* `Ctrl-^`      - Edit the alternate file; equivalent to `:e #`
* `:b [X]`      - Edit current buffer or buffer X (`:buffer [X]`)
* `:bd [X]`     - Unload and delete buffer from buffer list (`:bdelete [N]`)
* `:bn`         - Go to the next buffer in buffer list (`:bnext`)
* `:bp`         - Go to the previous buffer in buffer list (`:bprevious`)
* `:bN`         - Same as `:bp` (`:bNext`)
* `:br`         - Go to the first buffer in the buffer list (`:brewind`)
* `:ba`         - Show each buffer in a separate window (`:ball`)
* `:set hidden` - Hide buffer, instead of unloading it, when it is abandoned
* `:args`       - Show argument list with current file in brackets
* `:n`          - Edit next file in the argument list (`:next`)
* `:n {list}`   - Set new argument list and edit the first file in the list
* `:prev`       - Edit previous file in the argument list (`:previous`)
* `:N`          - Same as `:prev` (`:Next`)
* `:rew`        - Edit the first file in the argument list (:rewind)
* `:all`        - Show every argument in a separate window

Notes
-----
The `Ctrl-g` command shows whether the file is modified, readonly, a new
file, etc as the file status.

If you are editing a file in Vim and any changes have been made to it
outside Vim, the `:e` command may be used to reload the latest copy of
the file from the disk with the new changes. The `:e!` command is useful
in discarding changes to the current buffer and start all over again.

In the list above `:_%` and `:_#` simply means that in Ex commands, at
places where a file name can be used, you can use `%` to represent the
current file name and `#` to represent the alternate file name.

Current file name is defined as the name of the file currently being
edited. It is also known as the name of the buffer. On editing a new
file, the name of the new file becomes the current file name and
existing current file name, if any, becomes altenate file name.

The `Ctrl-^` can be invoked simply by pressing `Ctrl-6` in most
keyboards.

In `:b [X]` and `:bd [X]` commands, X may be a buffer number or buffer
name. While entering buffer name, the buffer name may be entered
partially and then completed by pressing `<Tab>`. For example, if buffer
2 contains the file foo.txt, you can edit this buffer either by typing
`:b 2<Enter>` or by typing `:b oo<Tab><Enter>`.

Use `:n **/*.txt` command to recursively search for all files with
extension name as txt in the current directory and its subdirectories,
set them as the argument list and edit the first one in the list.

If the Vim command is invoked with one or more file name as arguments
(e.g. `vim foo.txt bar.txt baz.txt`), this list of file names is the
argument list. This list can be seen using the `:args` command. Every
file name in the argument list is also present in the buffer list that
can be seen using the `:ls` command.

Multiple buffers in Vim serve the same purpose as multiple tabs do in
other editors like Notepad++, gedit, etc.

Exercise
--------
* In the shell, enter: `cp doc4.txt work.txt`.
* In the shell, enter: `vim work.txt`.
* Load ref4.txt by typing `:e ref4.txt<Enter>`.
* Load README.md by typing `:e README.md<Enter>`.
* Type `:ls<Enter>` and ensure three buffers are loaded.
* Type `:br<Enter>` to go to the first buffer containing work.txt.
* Use `:bn` and `:bN` to switch between work.txt and ref4.txt.
* Order the paragraphs in work.txt as per ref4.txt using the `{count}dd`
  and `p` commands.
* Place the cursor at the beginning of each group of four hyphens, i.e.
  ----, using the `w` command.
* Use other motion commands if required.
* For every group of four hyphens in work.txt, copy text from ref4.txt
  by pressing `ye`.
* Paste the text into work.txt by pressing `P`.
* Then delete the hyphens by pressing `lde`.
* For every line with hyphens only, copy line from ref4.txt by pressing
  `yy`.
* Paste the line into work.txt by pressing `p`.
* Remove the line with hyphens only by pressing `kdd`.
* Save the document by typing `:w<Enter>`.
* Type `:!diff -u ref4.txt work.txt<Enter>`. Ensure that this
  command returns no output. If you get any output, continue to edit the
  file and fix the errors.
* Type `:qa<Enter>` to quit all windows and exit Vim.


Lesson 5
========
Tab pages, search

Commands
--------
* `:tabe`         - Open a new tab page with an empty window (`:tabedit`)
* `:tabe {file}`  - Open a new tab page and edit file
* `gt`            - Go to the next tab page
* `gT`            - Go to the previous tab page
* `{N}gt`         - Go to the Nth tab page
* `:tabclose [N]` - Close current or Nth tab page; fail on last tab page
* `:tabonly`      - Close all other tab pages
* `:tabs`         - List the tab pages and the windows they contain
* `:tabm [N]`     - Move current tab page to after the last one or Nth one
* `:tab {cmd}`    - Execute command; open new tab page instead of window
* `/{pattern}`    - Search forward for pattern
* `?{pattern}`    - Search backward for pattern
* `n`             - Repeat the last / or ? command
* `N`             - Repeat the last / or ? command in opposite direction
* `*`             - Search forward for the word nearest to the cursor
* `#`             - Search backward for the word nearest to the cursor
* `:set hlsearch` - Turn highlighting on for search pattern matches
* `:noh`          - Remove highlighting for matches (`:nohlsearch`)

Exercise
--------
* In the shell, enter: `cp doc5.txt work.txt`.
* In the shell, enter: `vim work.txt`.
* Open ref5.txt in a new tab page by typing `:tabe ref5.txt<Enter>`.
* Open README.md in a new tab page by typing `:tabe README.md<Enter>.`
* Type `:tabs<Enter>` and ensure three tab pages are listed.
* Press `gt` to return to work.txt.
* Press `gt` and `gT` to switch between work.txt and ref5.txt.
* For every '----' in work.txt, copy text from ref5.txt by pressing ye.
* Place the cursor at the beginning of each group of four hyphens, i.e.
  ----, using the `/----` command.
* For every group of four hyphens in work.txt, copy text from ref5.txt
  by pressing `ye`.
* Press `n` command to repeat the search for a group of four hyphens and
  continue to edit the file.
* Paste the text into work.txt by pressing `P`.
* Then delete the hyphens by pressing `lde`.
* For every line with hyphens only, copy line from ref5.txt by pressing
  `yy`.
* Paste the line into work.txt by pressing `p`.
* Remove the line with hyphens only by pressing `kdd`.
* Save the document by typing `:w<Enter>`.
* Type `:!diff -u ref5.txt work.txt<Enter>`. Ensure that this command
  returns no output. If you get any output, continue to edit the
  file and fix the errors.
* Type `:qa<Enter>` to quit all windows and exit Vim.


Coming up
=========
* `J`      - Join lines; remove indent and insert up to two spaces
* `H`      - Go to the first non-blank character of the first line on window
* `M`      - Go to the first non-blank character of the middle line on window
* `L`      - Go to the first non-blank character of the last line on window
* `:ju`    - Show the jump list
* `Ctrl-o` - Go to older position in jump list
* `Ctrl-i` - Go to newer position in jump list


Resources
=========
Here is a list of links to interesting articles and blog posts about
Vim.

* [Why, oh WHY, do those #?@! nutheads use vi?][R1]
* [Why Vim?][R2]


License
=======
Copyright &copy; 2014 Susam Pal

![Creative Commons License](http://i.creativecommons.org/l/by/4.0/88x31.png)

This work is licensed under the [Creative Commons Attribution 4.0
International License][CCBY].

You are permitted to share and adapt this work under the condition that
you must give credit to this work with its URL:
<http://github.com/susam/vimex>.

This work is provided WITHOUT ANY WARRANTY; without even the implied
warranty of TITLE, MERCHANTIBILITY, FITNESS FOR A PARTICULAR PURPOSE,
NON-INFRINGEMENT, ABSENCE OF LATENT OR OTHER DEFECTS, ACCURACY, or the
PRESENCE OR ABSENCE OF ERRORS, whether or not known or discoverable.


<!-- Links -->
[0]: #introduction
[1]: #lesson-1
[2]: #lesson-2
[3]: #lesson-3
[4]: #lesson-4
[5]: #lesson-5
[6]: #resources
[7]: #license
[R1]: http://www.viemu.com/a-why-vi-vim.html
[R2]: http://www.terminally-incoherent.com/blog/2012/03/21/why-vim/
[CCBY]: http://creativecommons.org/licenses/by/4.0/
