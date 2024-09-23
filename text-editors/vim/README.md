# VIM

Vim is an editor used by programmers to edit a text file.<br>
Its first advantage is that while using it only the keyboard is necessary, thus you don't even need to lift hand to the mouse which is faster.<br>
Its second advantage is that it is very customizable.<br>
Its disadvantage is that a learning curve exists for its use.

## Use

There are two modes in vim. One is the command mode and another is the insert mode.<br>
In the command mode, the user can move around the file, delete text, etc.<br>
In the insert mode, the user can insert text.<br>
To go from command mode to insert mode use [a text entry command](#).<br>
To go from insert mode to command mode type 'Esc'.

## Commands

###### Text Entry Commands (Used to start text entry)

a -> Append text following current cursor position

A -> Append text to the end of current line

i -> Insert text before the current cursor position

I -> Insert text at the beginning of the cursor line

s -> delete current char and write new char

S -> Delete current line and start writing new line

o -> Open up a new line following the current line and add text there

O -> Open up a new line in front of the current line and add text there

*Cursor Movement Commands

gg -> Top file

G -> Bottom file

h -> Moves the cursor one character to the left

l -> Moves the cursor one character to the right

k -> Moves the cursor up one line

j -> Moves the cursor down one line

nG or :n -> Cursor goes to the specified (n) line

(ex. 10G goes to line 10)

upper case + right/left arrow -> move cursor one word

^F (CTRl F) -> Forward screenful

^B Backward -> screenful

^f -> One page forward

^b -> One page backward

^U -> Up half screenful

^D -> Down half screenful

$ -> Move cursor to the end of current line

0 -> (zero) Move cursor to the beginning of current line

w -> Forward one word

b -> Backward one word

*Exit Commands

:wq -> Write file to disk and quit the editor

:q! -> Quit (no warning)

:q -> Quit (a warning is printed if a modified file has not been saved)

ZZ -> Save workspace and quit the editor (same as :wq)

: 10,25 w temp -> write lines 10 through 25 into file named temp. Of course, other line numbers can be used. (Use :f to find out the line numbers you want.

*Text Deletion Commands

x -> Delete character going the right

X -> Delete character going to the left

dw -> Delete and copy word from cursor on

db -> Delete and copy word backward

dd -> Delete line and copy

5dd -> deletea and copy, for example, 5 lines

d$ -> Delete to end of line

d^ (d caret, not CTRL d) -> Delete to beginning of line

yy -> yank/copy current line

y$ -> yank to end of current line from cursor

yw -> yank from cursor to end of current word

5yy -> yank, for example, 5 lines

p -> paste below cursor

P -> paste above cursor

u -> Undo last change

control + r -> redo

U -> Restore line

J -> Join next line down to the end of the current line

*File Manipulation Commands

:w -> Write workspace to original file

:w file -> Write workspace to named file

:e file -> Start editing a new file

:r file -> Read contents of a file to the workspace

*Other Useful Commands

Most commands can be repeated n times by typing a number, n, before the command. For example 10dd means delete 10 lines. gg and G can be used to indicate start and end of file for example gg=G to indent whole file.

. -> Repeat last command

cw -> Change current word to a new word

r -> Replace one character at the cursor position

R -> Begin overstrike or replace mode � use ESC key to exit

'esc' followed by '/' -> search for pattern

:/ pattern -> Search forward for the pattern

:? pattern -> Search backward for the pattern

:g/pat1/s//pat2/g -> replace every occurrence of pattern1 (pat1) with pat2. Example :g/tIO/s//Ada.Text_IO/g. This will find and replace tIO by Ada.text_IO everywhere in the file.  :g/a/s// /g replace the letter a, by blank :g/a/s///g replace a by nothing

option + mouse -> copy/paste outside shell

gg=G -> =, the indent command can take motions. So, gg to get the start of the file, = to indent, G to the end of the file, gg=G. So line numbers can be used instead of gg/G.

v -> visual mode to mark text for copy, delete, ....

:sp file -> splits the window horizontally [and opens the file],

:vs file -> splits the window vertically [and opens the file]

esc + control-w-w (hold control and tap w two times) to jump between windows

:tabs -> display and access all open tabs, windows, ...

:n -> jump to next tab

:prev -> jump to previous tab

:tabe file -> create new tab

## Setup
:syntax on -> set color syntax
:colorscheme pablo -> favorite colorscheme
:set number -> set numbers
:set mouse=a -> install ability to use mouse


filetype plugin indent on -> init indent cmds
set tabstop=4 -> show existing tab with 4 spaces width
set shiftwidth=4 -> spaces after returnline indent


write down cmds in .vimrc in home directory to constantly have same setup or setup from VIM file by using the CMMs for one-time setup.

## Resources
[VIM Editor Commands](https://www.radford.edu/~mhtay/CPSC120/VIM_Editor_Commands.htm)
