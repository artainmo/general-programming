# Vim

Vim is an editor used by programmers to edit a text file.<br>
Its first advantage is that while using it only the keyboard is necessary, thus you don't even need to lift hand to the mouse which is faster.<br>
Its second advantage is that it is very customizable.<br>
Its disadvantage is that a learning curve exists for its use.

## Use

There are two modes in vim. One is the command mode and another is the insert mode.<br>
In the command mode, the user can move around the file, delete text, etc, basically execute the commands detailed below.<br>
In the insert mode, the user can insert text.<br>
To go from command mode to insert mode use [a text entry command](#text-entry-commands-used-to-start-text-entry).<br>
To go from insert mode to command mode type 'Esc'.

## Commands

###### Text Entry Commands (Used to start text entry)
a -> Append text following current cursor position<br>
A -> Append text to the end of current line<br>
i -> Insert text before the current cursor position<br>
I -> Insert text at the beginning of the cursor line<br>
s -> Delete current char and write new char<br>
S -> Delete current line and start writing new line<br>
o -> Open up a new line under the current line and add text there<br>
O -> Open up a new line above the current line and add text there<br>
cw -> Change current word to a new word, it deletes following word and puts you in insert mode.<br>

###### Cursor Movement Commands
gg -> Moves cursor to top file<br>
G -> Moves cursor to bottom file<br>
h -> Moves the cursor one character to the left<br>
l -> Moves the cursor one character to the right<br>
k -> Moves the cursor up one line<br>
j -> Moves the cursor down one line<br>
nG or :n -> Cursor goes to the specified (n) line (ex. 10G goes to line 10)<br>
upper case + right/left arrow -> Move cursor one word<br>
w -> Forward one word<br>
b -> Backward one word<br>
$ -> Move cursor to the end of current line<br>
0 -> (zero) Move cursor to the beginning of current line<br>
^F (CTRl F) -> Forward screenful<br>
^B -> Backward screenful<br>
^U -> Up half screenful<br>
^D -> Down half screenful<br>
^f -> One page forward<br>
^b -> One page backward<br>

###### Exit Commands
:wq -> Write file to disk and quit the editor<br>
ZZ -> Save workspace and quit the editor (same as :wq)<br>
:q -> Quit (a warning is printed if a modified file has not been saved)<br>
:q! -> Quit (no warning)<br>
: 10,25 w temp -> Write lines 10 through 25 into file named temp. Of course, other line numbers can be used.<br>

###### Text Deletion Commands
x -> Delete character going to the right<br>
X -> Delete character going to the left<br>
dw -> Delete and copy following word from cursor<br>
db -> Delete and copy word backwards<br>
dd -> Delete line and copy<br>
5dd -> Delete and copy a number of lines, for example here 5 lines<br>
d$ -> Delete to end of line<br>
d^ (d caret, not CTRL d) -> Delete to beginning of line<br>
yy -> Yank, which means copy, current line<br>
y$ -> Yank to end of current line from cursor<br>
yw -> Yank from cursor to end of current word<br>
5yy -> Yank multiple lines, for example here 5 lines<br>
p -> Paste below the cursor<br>
P -> Paste above the cursor<br>
u -> Undo last change<br>
control + r -> Redo<br>
U -> Restore line<br>
J -> Join next line down to the end of the current line<br>

###### File Manipulation Commands
:w -> Write workspace to original file (save file)<br>
:w file -> Write workspace to named file<br>
:e file -> Start editing a new file<br>
:r file -> Read contents of a file to the workspace<br>

###### Workspace windows setup
:sp file -> Splits the window horizontally and opens the file<br>
:vs file -> Splits the window vertically and opens the file<br>
control-w-w (hold control and tap w two times) -> To jump between windows<br>
:tabs -> Display and access all open tabs, windows, ...<br>
:n -> Jump to next tab<br>
:prev -> Jump to previous tab<br>
:tabe file -> Create new tab<br>

###### Other Useful Commands and Tips
. -> Repeat last command<br>
r -> Replace one character at the cursor position with another one without entering insert mode. For example if the cursor is on the character 'a' and you type 'rX', the character 'a' will be replaced with 'X'<br>
R -> Enters replace mode where you can continuously replace multiple characters as you type. Use ESC key to exit this mode<br>
/ pattern -> Search for a pattern<br>
:/ pattern -> Search forward for the pattern<br>
:? pattern -> Search backward for the pattern<br>
:g/pat1/s//pat2/g -> Replace every occurrence of pattern 1 ('pat1') with 'pat2'. For example ':g/tIO/s//Ada.Text_IO/g' will find and replace 'tIO' by 'Ada.text_IO' everywhere in the file. Other examples, ':g/a/s// /g' replaces the letter 'a' by blank and ':g/a/s///g' replaces 'a' by nothing<br>
gg=G -> The indent command ('=') can take motions. So, 'gg' to get the start of the file, '=' to indent, 'G' to get the end of the file, to indent the whole file. Also, line numbers can be used instead of 'gg' and 'G'<br>
v -> Visual mode to mark text for copy or delete.<br>
option + mouse -> Copy for and paste from outside the shell<br>

Most commands can be repeated n times by typing a number, n, before the command. For example 10dd means delete 10 lines. gg and G can be used to indicate start and end of file. For example gg=G to indent whole file.

## Setup
:syntax on -> Set color syntax<br>
:colorscheme pablo -> Choose a colorscheme, 'pablo' is my favorite colorscheme<br>
:set number -> Indicate line numbers<br>
:set mouse=a -> Install ability to use mouse to move cursor<br>
filetype plugin indent on -> This command tells vim to automatically detect the type of file you're working on, load file type-specific plugins, apply appropriate indentation rules based on the file type. This command enhances the overall editing experience by providing file type-specific features and behavior.<br>
set tabstop=4 -> Configures how many spaces a tab character ('\t') visually represents in the editor<br>
set shiftwidth=4 -> Configures spaces after return-line indentation<br>

You can write down setup commands in '.vimrc' file in home directory to constantly have same setup when launching vim. Else, you can use those commands from within vim for them to be active only during that vim session.

## Resources
[VIM Editor Commands](https://www.radford.edu/~mhtay/CPSC120/VIM_Editor_Commands.htm)
