Lesson 1
========
Deleting and replacing characters

Commands
--------
h       - Move cursor left
j       - Move cursor down
k       - Move cursor up
l       - Move cursor right
<BS>    - Same as h but can wrap to the previous line
<Space> - Same as l but can wrap to the next line
x       - Delete character under the cursor
r       - Replace character under the cursor
u       - Undo changes
Ctrl-r  - Redo changes that were undone
:wq     - Write the current file and quit
:q!     - Quit without writing (:quit!)

Exercise
--------
cp doc1.txt work.txt
vim work.txt

Move around the document by pressing h, j, k, l.
Do not use arrow keys.
Delete every occurrence of '=' in the document by pressing x.
Replace every occurrence of '_' with an appropriate letter by pressing r.
If you make a mistake, press u to undo the mistake.
Save the document by typing :wq<Enter>.

diff -u ref1.txt work.txt
rm work.txt


Lesson 2
========
Deleting and inserting words and lines

Commands
--------
w               - Move forward to beginning of next word
e               - Move forward to end of word (skips empty line)
b               - Move backward to beginning of word
W               - Move forward to beginning of next WORD
E               - Move forward to end of WORD (skips empty line)
B               - Move backward to beginning of WORD
d{motion}       - Delete text that motion moves over
dd              - Delete line under the cursor
i               - Insert text before the cursor
a               - Insert text after the cursor
o               - Open a new line below the cursor and insert text
[count]         - Optional number prefix to repeat a command
:set nu         - Turn line numbers on (:set number)
:set {option}   - Set boolean option; show value of number/string option
:set {option}?  - Show value of option
:set no{option} - Reset boolean option, i.e. turn it off, e.g. :set nonu
:h              - Show help (:help)
:h {subject}    - Show help on subject (:help {subject})

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

Exercise
--------
cp doc2.txt work.txt
vim work.txt

Move around the document by pressing w, b.
Use motion keys from previous lessons if needed.
Replace every occurrence of '_' with an appropriate letter by pressing r.
Delete '----' by pressing de.
Press i, complete a word and press <Esc>.
Save the document by typing :wq<Enter>.

diff -u ref2.txt work.txt
rm work.txt


Lesson 3
========
Windows, navigation and inserting text

Commands
--------
gg         - Go to the first line, on the first non-blank character
G          - Go to the last line, on the first non-blank character
{N}gg      - Go to Nth line, on the first non-blank character
{N}G       - Same as {N}gg
0          - Go to the first character of the line
^          - Go to the first non-blank character of the line
$          - Go to the end of the line
I          - Insert text before the first non-blank in the line
A          - Append text at the end of the line
O          - Open a new line above the cursor and insert text
:!{cmd}    - Execute command with shell
:sp        - Split current window into two (:split)
:sp {file} - Split current window and edit file
:vs        - Vertically split current window into two (:vsplit)
:vs {file} - Vertically split current window and edit file
:new       - Split and edit empty buffer
:vnew      - Vertically split and edit empty buffer
:only      - Make current window the only one on the screen
:w         - Write current buffer to the file (:write)
:q         - Quit current window; exit on last non-help window (:quit)
:qa        - Quit all windows, i.e. exit Vim (:qall)
:close     - Quit current window; fail on last window
Ctrl-w w   - Go to the window (left to right, top to bottom)
Ctrl-w =   - Make all windows equally high and wide
Ctrl-w _   - Make current window highest possible
Ctrl-w |   - Make current window widest possible
Ctrl-w s   - Same as :sp
Ctrl-w v   - Same as :vs
Ctrl-w n   - Same as :new
Ctrl-w o   - Same as :only
Ctrl-w q   - Same as :q
Ctrl-w c   - Same as :close

Exercise
--------
cp doc3.txt work.txt
vim work.txt

Type :sp ref3.txt<Enter>.
Press Ctrl-w w to switch to the window containing work.txt.
Move to the first line of work.txt by pressing gg.
Each line containing hyphens only represent two missing lines.
Use motion keys to move to the lines containing hyphens only.
Delete a line containing hyphens by pressing dd.
Then press O to insert text in work.txt.
Press <Esc> whenever you are done inserting text.
When you need to scroll ref3.txt, press Ctrl-w w and use motion keys.
Press Ctrl-w w to switch between windows.
Make work.txt identical to ref3.txt.
Save the document by typing :w<Enter>.
Type :!diff -u ref3.txt work.txt<Enter>.
Ensure that the output is blank.
Type :qa<Enter> to quit both windows.

rm work.txt


Lesson 4
========
Copy, paste and buffers

y{motion}   - Copy text that motion moves over
yy          - Copy line under the cursor
p           - Put the text after the cursor
P           - Put the text before the cursor
Ctrl-g      - Show current file name, lines, status and cursor position
g Ctrl-g    - Show column, line, word, character and/or byte positions
:buffers    - Show all buffers
:ls         - Same as above
:hide       - Quit current window and hide buffer; fail on last window
:_%         - % is replaced with current file name
:_#         - # is replaced with alternate file name
:e          - Edit the current file (:edit)
:e {file}   - Edit file (:edit {file})
Ctrl-^      - Edit the alternate file (:e #)
:b [X]      - Edit current buffer or buffer X (:buffer [X])
:bd [X]     - Unload and delete buffer from buffer list (:bdelete [N])
:bn         - Go to the next buffer in buffer list (:bnext)
:bp         - Go to the previous buffer in the buffer list (:bprevious)
:bN         - Same as :bp (:bNext)
:br         - Go to the first buffer in the buffer list (:brewind)
:ba         - Show one buffer in each window (:ball)
:set hidden - Hide buffer, instead of unloading it, when it is abandoned
:args       - Show argument list with current file in brackets
:n          - Edit next file in the argument list (:next)
:n {list}   - Set new argument list and edit the first file in the list
:N          - Edit previous file in the argument list (:Next)
:prev       - Same as :N (:previous)
:rew        - Edit the first file in the argument list (:rewind)
:all        - Show one argument in each window

Notes
-----
Ctrl-g shows modified, readonly, new file, etc as file status. :e! is
useful in discarding changes to the current buffer and start all over
again.

Current file name is defined as the name of the file currently being
edited.  It is also known as the name of the buffer. On editing a new
file, the name of the new file becomes the current file name and
existing current file name, if any, becomes altenate file name.

Ctrl-^ can be typed as Ctrl-6.

In :b [X] and :bd [X] commands, X may be a buffer number or buffer name.
While entering buffer name, the buffer name may be entered partially and
then completed by pressing <Tab>.

Use :n **/*.txt command to recursively search for all files with
extension name as txt in the current directory and its subdirectories,
set them as the argument list and edit the first one in the list.

Every file name in the argument list is also pesent in the buffer list.

Exercise
--------
cp doc4.txt work.txt
vim work.txt

If you are repeating the lesson, type :set hidden<Enter>.
Type :e ref4.txt<Enter>.
Type :e README.txt<Enter>.
Type :ls<Enter> and ensure three buffers are loaded.
Type :br<Enter> to go to work.txt.
Use :bn and :bN to switch between work.txt and ref4.txt.
Order the paragraphs in work.txt as per ref4.txt using {count}dd and p.
Place the cursor at the beginning of each '----' using w.
Use other motion commands if required.
For every '----' in work.txt, copy text from ref4.txt by pressing ye.
Paste the text into work.txt by pressing P.
Then delete '----' by pressing lde.
For every line with hyphens only, copy line from ref4.txt using yy.
Paste the line into work.txt by pressing p.
Remove the line with hyphens only by pressing kdd.

Save the document by typing :w<Enter>.
Type :!diff -u ref4.txt work.txt<Enter>.
Ensure that the output is blank.
Type :qa<Enter> to quit all windows.

rm work.txt


Lesson 5
========
Tab pages, search

Commands
--------
:tabe         - Open a new tab page with an empty window (:tabedit)
:tabe {file}  - Open a new tab page and edit file
gt            - Go to the next tab page
gT            - Go to the previous tab page
{N}gt         - Go to the Nth tab page
:tabclose [N] - Close current or Nth tab page; fail on last tab page
:tabonly      - Close all other tab pages
:tabs         - List the tab pages and the windows they contain
:tabm [N]     - Move current tab page to after the last one or Nth one
:tab {cmd}    - Execute command; open new tab page instead of window
/{pattern}    - Search forward for pattern
?{pattern}    - Search backward for pattern
n             - Repeat the last / or ? command
N             - Repeat the last / or ? command in opposite direction
*             - Search forward for the word nearest to the cursor
#             - Search backward for the word nearest to the cursor
:set hlsearch - Turn highlighting on for search pattern matches
:noh          - Remove highlighting for matches (:nohlsearch)

Exercise
--------
cp doc5.txt work.txt
vim work.txt

Type :tabe ref5.txt<Enter>.
Type :tabe README.txt<Enter>.
Type :tabs<Enter> and ensure three tab pages are listed.
Type gt to return to work.txt.
Press gt and gT to switch between work.txt and ref5.txt.
Use motion commands, /{pattern} and n commands to move around the file.
Use other motion commands if required.
For every '----' in work.txt, copy text from ref5.txt by pressing ye.
Paste the text into work.txt by pressing P.
Then delete '----' by pressing lde.
For every line with hyphens only, copy line from ref5.txt using yy.
Paste the line into work.txt by pressing p.
Remove the line with hyphens only by pressing kdd.

Save the document by typing :w<Enter>.
Type :!diff -u ref5.txt work.txt<Enter>.
Ensure that the output is blank.
Type :qa<Enter> to quit all windows.

rm work.txt

TODO
====
J
H
L
M
vim -o
vim -O
:jumps
.
