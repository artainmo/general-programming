shell_commands & different_types_of_shell

--------------------------
SHELL CMDS
--------------------------
A Shell is ....
The ability to create a shell script exists too.....

ls -> list current directory files
ls -la -> list current directory files and also hidden files
pwd -> SHow absolute path current directory
cd -> change current directory by using relative or absolute path
cd - -> change directory back to last directory
cd without_params -> change directory to home directory
vim -> create and edit a file with vim
vim -p file1 file2 ... -> open multiple files in multiple tabs
touch -> create a file
mkdir -> create a directory
rm -> delete a file
rm -rf -> delete files and directories
cat -> show content of file
mv path1 path2 -> move file from path1 to path2, can also be used to change name of file
cpy -> copy file to another file
yes -> create infinite loop of yes
env -> view env variables
export -> change value of env variables
>> or << -> redirect output to
| -> pipe output of first command to input of second command
clear -> clear terminal
cmd + d -> split new vertical window
shift + cmd + d -> split new horizontal window
cmd + w -> close window
cmd + n -> create new terminal window
$? -> view return of last program
grep -> often used combined with a pipe to take lines/words that contain letter/word you want to grep/find
wc -l -> often used in combination with pipe to count lines from given input
ulimit -a -> Indicates all computer resource limits for currently opened shell
ulimit -n -> Limits max number of file descriptors, can be used to test non-closed file descriptors
ulimit -v -> Limits max memory space and can make malloc fail, but on MACOSX it does not seem to fail
time -> Used before program name calculates time/speed of program
control-a -> brings cursor to begin of command
tree -> Same as ls but with subdirectories
diff file1 file2 -> see difference between two files
cmd + mouse + link -> go to link directly
* -> often used to indicate all can be combined with extension to choose all files with this extension for example '*.c'
*/ is used to indicate in a path all the directories from a directory, **/ is used to indicate all the possible directories and those that follow...
brew -> has to be downloaded and can be used on mac to install or uninstall external software on local environment
tree -> Has to be installed. Can be installed with 'brew install tree'. It displays not only all files in current but also in following directory. It also supports the '--la' option for hidden files.

https://github.com/LeCoupa/awesome-cheatsheets/blob/master/languages/bash.sh -> view other interesting commands
