# General
Terminal is the window
Shell is the software that helps you execute command
Eg: In ubuntu, it's bash shell; In Mac OS its zsh; windows has PowerShell

**returns the word after echo i.e., hello**
echo hello

**clears the terminal but can access history still**
clear

Just do **Ctrl + C** in between lines to not execute the line & go to the next line instead of backspacing what you wrote

In the path "/#" the / means the root which is the most up you can go

# Common Linux Commands
## Navigating Directory

**print working directory, no need to echo**
pwd

**change directory**
cd

**Will get you into root folder represented by "~#" instead of "/#"**
cd root

*Earlier, the root means the most up directory, here, root is the folder*

**For relative path, directly mention folder name, no /**
*goes to "myfolder" relative to current directory*
cd myfolder

**Absolute path, start with "/"**
cd /root/photos

*Goes to most up root directory*
cd /

**Go one directory back i.e., parent folder**
cd ..
**Go inside another sibling folder inside the parent directory**
cd ../myfolder/
**Go 2 parent directory above**
cd ../..

**Go to the directory in which you were working before i.e., previous working directory**
cd -

**Use tab key to autocomplete file or folder names**

## List Files & permissions
ls

**Shows the read write execute permissions & if its a director or file for list of files using -l**
ls -l

**Show hidden files using -a**
ls -la

*Hidden files usually start with . (dot). Eg: .bashrc*

**Notations on left side of file names in the list**
d means directory (folder), if it's a file, it'll be '-' (dash)
l means a shortcut to some other file or folder (like windows desktop shortcut)
r means read permission
w means write permission
x means executable permission
'-' (dash) means nothing or not present

**Show permissions for specific file or folder**
ls -l myFile

**Change permissions using chmod**
chmod 734 test

The numbers are for 3 user levels respectively: **admin, group, public**
1 = execute (x)
2= read (r)
4 = write (w)
(Higher permission equals higher number)

Add the numbers of corresponding permissions to get the number for chmod
Eg: To give read & execute permission; write 3 (2+1)

chmod 734 test
So the above means, for "test" file, give rwx permission to admin, rx to group, x to public
Represented by ls -l command as
rwxr-x--x (means rwx for admin, r-x means rx for group, --x means only executable permission to public)

## Read Files
**All files in linux may not have any extension; use "cat " to read or do operations**
cat filename

## Determine your OS by reading /etc/os-release file
**Change directory to "etc" from root /**
cd etc

**Read os-release file which has the OS info**
cat os-release

**Absolute path In 1 line**
cat /etc/os-release

## Reading long files
**Use up down arrow keys to preview less or more lines in terminal; keyword "less " with filename**
less BigTextFileName

## Create Directory & Nested Directories & Files
**cd to your folder, use "mkdir" and folder name to create it**
mkdir folderName

*flag is an extra command you pass using '-' (dash)*

**Create nested folders using the flag '-p'**
mkdir -p folder1/folder2/folder3

*will create folder1 then folder 2 inside it and nest it*

**Create a file using touch**
touch fileName

## Remove
**With rm, it doesn't go to trash but permanently deletes the file**
rm fileName

**Deleting folder by deleting all its files**
rm -r myFolder/

rmdir folderName (works only if folder is empty)

*-r makes it open and delete all file from myFolder, and then delete the folder itself*
*-r means recursively which does the command you specify on all files present; the '/' at end of myFolder is not mandatory*

**Removing all files BE CAREFUL, DON'T use /**
rm -r *

**DON'T DO THIS i.e., Absolute path using / will delete the whole root**
rm -r /*

Preferrably create your folder, and create all other files inside that so you can just delete the folder directly
## Copy files
**Copy files using cp fileNameToCopy CopiedFileName**
cp bigtext BigText.backup

**Copy folders along with all files inside it**
cp -r folder1/ folder2

## Move or Rename files
**Renaming is just moving the file in same directory with different name**
mv myfile My-Renamed-File

**Moving file to another folder**
mv myFile folder1

**Move file 1 directory up**
mv myFile ..

*Here you don't need -r like in copying and removing*

## Find binary path (commands itself)
The commands like ls,rm,cp,echo are all inside the /bin/ folder
so when calling echo, you're doing /bin/echo 'abc'
Almost all commands are inside /bin/ but not all may be there, different systems have different locations

**Use 'which' keyword to find where that command exists** 
which echo
*will return /usr/bin/echo*

# Nano Text Editor in Terminal
**Installing nano in docker ubuntu**
Run the ubuntu container, run "apt update", then run "apt install nano"; update command allows you to install nano. If still not working, exit and run "docker pull nano" to get nano image

Vim is similar, nano is easier

**Command to edit a file or create if it doesn't exist**
nano fileName

*The same above command will **create the file** if it doesn't exist*

**Notations**
^ means press ctrl with the key given in instructions
M- means press alt or options key with the 2nd key mentioned

Eg: ^C means press Ctrl+C
M-C means press Alt+C
">" arrow at sides means there's more text in the line & it's clipped

Use Ctrl+O to save the file i.e., "write out", write the file name, enter to confirm
Ctrl+K to Copy
Ctrl+U to Paste

**Searching in nano instead of taking cursor over there**
Use Ctrl+W to search for a word instead of manually using arrow keys to go there.

It'll go to 1st instance, if you want to go next one, press Ctrl+W again, up arrow key to get previous search string, hit enter, it'll go to the next match

Home or End key to go to start or end of a line; Use Ctrl with it to go to start or end of entire doc

# Shell Scripting
"#" sign is used to comment a line in bash in any file

You can directly write scripts or conditions in terminal, it'll let you continue on new line, when you write "fi", it will exit the if block and give you the output.
## Running simple bash script
**Create a file using nano, write the code inside it**
nano script
echo "Hi I'm a file named script"

**Use bash keyword to execute the file name**
bash script

## Variables
**Creating variable in bash using equal to (=) sign WITHOUT any spaces**
myVariable="This is cool text"

**Using the variable by prepend(adding before) $ sign to it**
echo $myVariable

**Will output**
This is cool text

## Arguments
**In the script file, use $ sign with any number to define arguments but don't save them as variables**
echo $1 $2 $3

**Note:** Only number with a $ sign before it can be argument, you can't take argument by having "$arg" but "$1" any number

**Example execution**
bash script "hi" "hello" "how" "are" "you"

**Output**
hi hello how

*Only first 3 words because there are only 3 arguments, rest get ignored*

## Reading user input & printing it
**Example code**
echo "Enter your name: "
read name

echo "Your name was: "
echo $name

echo "Your name is $name"

**Read keyword then variable name in which you want to store the input**
read keyword halts your program and tells user to input something, and whatever is entered is stored in variable named defined after 'read' keyword

**Using variables in 1 line using double quotes**
Use double quotes "" to access variables names using $
Use single quotes '' to not access the variable but literally print the $ sign

echo "Your name is $name"
*will return the input from the user asked at start*

echo 'Your name is $name'
*will return Your name is $name ; literally the string only*

## Building username password interface without echo & hiding password
**Example code**
read -p "Username: " username
read -sp "Password: " password

echo "Your username is $username"
echo "Your password will not be shown"

**Explanation**
"-p" means placeholder, the text after that is the variable in which it is stored
So while asking, it'll print "Username: " and accept the input, then store it in username variable

-s means it'll silent, the input will not be shown at all, not even in asterisk, just like you've typed nothing

You can still access the silent variable in echo statement

**Note:** For silent input and placeholder "-sp" will work but "-ps" will NOT; s should be before p

## If else statement
**Example code**
if [  "$username" = "admin" ] && [ "$password" = "admin" ]
then 
	echo "Hey, you entered your username and password same"
elif [ "$password" = "test" ]
then
	echo "Hey, your password is insecure"
else
	echo "Good luck next time"
fi

**Basic rules**
- **Condition** should be in **square brackets** [  ] Make sure there **space between bracket & condition** otherwise it'll be invalid
- multiple conditions **joined by &&** , square brackets for each
- **Variable names** should be **in double quotations** "" because it works in that & if the variable in empty, then it won't throw an error because of quotations still being there
- **Comparison** is done using **single equal to sign "="** & not the double equal to
- Number comparison is like => if [ $x -gt 20 ] then echo "greater than"
- **-gt, -lt, -eq** means greater than, less than, equal to (for numbers)
- Use **if** [condition] **then** **elif then** **else** format
- **To close the if block, write the opposite i.e., "fi" at the end**

## Logical operators and exit status
*Some times you may not know if the command was valid or not*
*Status code of 0 means it was valid command, if any other, then it was invalid*

**Command to check status after running a command**
echo $?

*echo means print, $ means variable, ? means previous command; It'll output status code of previous command*

**Put exit status in code**
if [ "$username" = "admin"] && ["$password" = "admin"]
then 
	echo "Hey, you entered your username and password same"
exit 0
else
	echo "Good luck next time"
exit 1
fi

After running the file using bash, run "echo $?"
It'll return 0 or 1 based on the condition satisfied. Just like if it was success or failure in short

**Using && || to return status code directly in bash command (Bitwise operators)**
bash script && echo "everything went right"

*The above means, it'll execute the first part to run the script, because of &&, if the 1st condition gives status code 1, then it'll run the 2nd part as well*
*The returning of 1 & 0 is set using exit keyword in the code*
The range of exit code is 0-255 only

## For Loop
**Example 1 - spaces between values**
for i in 1 2 3
do
echo "Welcome. Your number is $i"
done

**Example 2 - ranges**
for i in {1..100}
do
echo "Printing 100 lines. Your current line number is $i"
done

**Example 3 - ranges but with skips**
for i in {1..100..10}
do
echo "will print 11 multiples because starts at 1 & keeps adding 10. Number is $i"
done

**Example 4 - read multiple files**
You create a files called "myFileList" containing name of files you want to read. Eg: It has text "file1 file2 file3"
Then you actually have those files created

for f in $(cat myFileList)
do
echo "reading $f"
cat $f

*The 1st line reads the myFileList, get the file names that's stored in $f, & in last command, it's reading those file names that were specified using cat command*

**Rules**
- for loop **works on the spaces between values outside quotes if any**. The 1st line an be => for i in "abc" "pqr" "xyz" ; will run code 3 times because there are 3 values & it is stored in variable i as defined
- **"do" keyword** for the for loop; **"done" keyword to end the for loop**
- **To use a range like 1-100 use {1..100}**, => for i in {1..100} do echo "number $i"
- To **skip numbers in a range** like multiples of 11 in range 1-100 => if i in **{1..100..10}** (will print 11 multiples because starts at 1, then adds 10 = 11, adds 10 = 21)

## Functions
Think of bash functions like a command, so you can't call a function but just write the name. They're written like regular JavaScript functions

**Example 1**
function greetUserAndCreateFile() {
	echo "Hello user. I'm greeting you"
	sleep 2
	touch greetFile
	echo "File created"
}

greetUserAndCreateFile

**Example 2 - passing arguments**
function firstAndLastName() {
	echo "Your firstname is $1"
	echo "Your lastname is $2"
	return 1
}

firstAndLastName Abc Pqr

*Output*
Your firstname is abc
Your lastname is pqr

**Rules**
- *You **don't use parenthesis to call a function** but just write the name like a command **in the file itself NOT the terminal**.*
- You can **pass arguments inline after calling** it as well but **NOT in parenthesis of the function** like in JS. Refer them using $1 $2, etc (number only variable names) directly in the function body
- **"return" keyword** will do nothing but just **return the exit code** => return 0, it'll not get printed anywhere but shown when you execute the file using bash, then run "echo $?"




# Misc
## Package Manger
When using Docker ubuntu image for example, you won't have tools like nano (text editor), etc. apt is the package manager for ubuntu

**Update ubuntu sources to get or find new packages**
apt update

**Run commands as root user using sudo**
sudo apt udpate

**Install an application like nano which you can run directly**
apt install nano
nano

**Uninstall an application like nano for example**
apt uninstall nano

## .bashrc file (commands on shell initialization)
You can define variables or commands to be executed & it runs when the shell starts
Edit using nano.

If you define variable inside the file like: myVar=1000
Then in terminal, you can get the variable by running: echo $myVar

To run the commands in the .bashrc file, just run the command "bash"

**Refresh changes from .bashrc file**
For example, you set a variable and then change it, then on running bash, it'll the old value for the variable.

**Easier way to refresh** changes is to **run the command**: source .bashrc
Or you can close and open the window again

## top & htop command (view all running processes)
**Run the command to view running processes**
top

**To exit, press the "q" key**

For trial, you can run a script which sleeps for some time but put in background using & sign at end of bash script

**Example "script" named file code**
sleep 10000

**Run script in background using & sign at end**
bash script &

**Install htop**
apt install htop

*It makes the top look good & gives more insight*

## Kill command (stop any stuck process)
**Get the process ID or PID using top command**
top

**kill command**
kill -9 271

*-9 means immediately kill; 271 is PID displayed in 1st column after running the top command*
