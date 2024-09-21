# Shell
In computing, a shell is a computer program that exposes an operating system's services to a human user or other programs. In general, operating system shells use a command-line interface (CLI). It is named a shell because it is the outermost layer around the operating system.<br>
Shell scripts can be written in '.sh' files. Most programming languages can also execute shell commands.

## Shell commands
ls -> list current directory files<br>
ls -la -> list current directory files and also hidden files<br>
pwd -> show absolute path of current directory<br>
cd -> change current directory by using relative or absolute path<br>
cd - -> change directory back to last directory<br>
cd *without_params* -> change directory to home directory<br>
vim -> create and edit a file with vim<br>
vim -p file1 file2 ... -> open multiple files in multiple tabs<br>
touch -> create a file<br>
mkdir -> create a directory<br>
rm -> delete a file<br>
rm -rf -> delete files and directories<br>
cat -> show content of file<br>
mv path1 path2 -> move file from 'path1' to 'path2', can also be used to change name of a file<br>
cpy -> copy file to another file<br>
yes -> create infinite loop of yes which can be used to answer prompts automatically<br>
env -> view environment variables<br>
export -> change value of environment variables<br>
\>> or << -> redirect output to<br>
| -> pipe output of first command to input of second command<br>
clear -> clear terminal<br>
cmd + d -> split new vertical window<br>
shift + cmd + d -> split new horizontal window<br>
cmd + w -> close window<br>
cmd + n -> create new terminal window<br>
`$?` -> return of last program, `echo $?` to display it<br>
grep -> often used combined with a pipe to find lines/words that contain word you want to grep/find, for example if you want to verify if a specific file exists in current directory you could do 'ls | grep "main"'<br>
wc -l -> often used in combination with pipe to count lines from given input<br>
ulimit -a -> indicates all computer resource limits for currently opened shell<br>
ulimit -n -> limits max number of file descriptors, can be used to test non-closed file descriptors<br>
ulimit -v -> limits max memory space and can make malloc fail, but on MACOSX it does not seem to fail<br>
time -> used before program name and calculates time/speed of program<br>
control + a -> brings cursor to begin of command<br>
tree -> same as 'ls' but with subdirectories<br>
diff file1 file2 -> see difference between two files<br>
cmd + mouse + link -> go to link directly<br>
\* -> often used to indicate all, can be combined with extension to choose all files with this extension for example '*.c'<br>
*/ -> is used to indicate in a path all the directories from a directory, '**/' is used to indicate all the possible directories and those that follow<br>
brew -> has to be downloaded and can be used on mac to install or uninstall external software on local environment<br>

## Exercises
Here is a [first day of exercises](https://github.com/artainmo/c/tree/main/shell00) followed by a [second day of exercises](https://github.com/artainmo/c/tree/main/shell01).

## References
[View other interesting commands](https://github.com/LeCoupa/awesome-cheatsheets/blob/master/languages/bash.sh)
