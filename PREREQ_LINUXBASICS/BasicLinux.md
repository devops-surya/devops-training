## LINUX :
* Linux is developed by  Linus Torvalds

```
Linux is a kernal 
```
EX: ubuntu , REDHAT , centos 


### OS Works :

![preview](../MAR-2021/images/l1.png)

### MAJOR COMPONENTS OF Operating System :

* 1. HARDWARE COMPONENTS:
     * RAM 
     * CPU 
     * HARDDISK
     * NETWORK
* 2. LINUX KERNAL :
     * sytem calls 
     * memory allocation 
     * process allocation
     ...
* 3. USER INTERFACE :
     * GUI 
     * CLI
     
     .........



```
pwd ------present working directory 
ls ------ list the things in the present path
cd ---- change directory 
mkdir  ----- create a directory (folder)
touch -- create a file

```


## LINUX COMMANDS:

* ls -al  --- to list the files or folders with the data stating ,who created it , when it is created , permissions to that folder/file, and time stamp.

* rm -rf <foldername>   -- to remove a file or folder 

* touch <filename>   ---- to create a file

* vi -- IT is one of the most pupular editor. To create a file , edit a file.
If you are using vi , it creates a file and opens the file for editing.

* MODES in VI 
  1. Insert    ---- to write/edit the content on the file
  2. SAVE      ---- esc : wq
  3. quit without save  ---- esc : q!

* cat -- it is used to see the content in the file opening it 

* cp   -- it is used to copy the file from one location to another location

```
cp <source> <destination>
```

* mv  -- it is used to move the file from one location to another location.

```
mv <source> <destination>
```
* locate ---- to locate any file/folder in your machine 

```
locate <filename>
```

* To clear the screen :
```
clear or ctrl+l
```
* echo  -- it is used to print the content 

```
echo "devops"
```



## List of Linux Commands :

### SUDO 

```
This command operates only that command by root/ superuser privileges.

Syntax:

$ sudo

$ sudo

sudo useradd - To add a new user

sudo passwd - Creating a password for the new user

sudo groupadd - To add a new group

sudo userdel - To delete the user

sudo groupdel - To delete the  group

sudo usermod -g - To add a user to a primary group
```


### Ls

```
This command indexes all the contents in the present working directory.

Syntax: 

$ ls

ls - By mentioning the path after ls, the content in that path will be shown

ls –a - Using ‘a’ flag, indexes all the hidden contents in the particular directory

ls –l - Using ‘l’ flag, indexes all the contents with its permissions, owner settings, and time

stamp (long format)
```

### Sort

```
This command sorts the outcomes of a search either numerically or alphabetically. It also sorts file contents, files, and directories.

Syntax:

$ sort {filename}

sort -f - the flag does case insensitive sorting 

sort -r - the flag returns the results in reverse order

sort -n - the flag returns the results as per numerical order
```

### Grep

```
This command searches for a particular string/ word in a text file. It is similar to “Ctrl+F” but operated through a CLI.

Syntax:

$ grep {filename}

grep -n - Returns the matching strings along with their line number

grep -i - Returns the results for case insensitive strings

grep -c - Returns the number of lines in which the results matched the search string

grep -v - Returns the result of lines not matching the search string
```

### Tail/Head
```
It is corresponding to head command. The tail command prints the last N number of information of the given info. Of course, it prints the last 10 lines of the predefined documents. In the event that you provide more than one file name, at that point information from each document goes before by its record name. 

Syntax:

head [OPTION]... [FILE]...
tail [OPTION]... [FILE]...
 

* -n num: Prints the first ‘num’ lines instead of first 10 lines. num is mandatory to be specified in command otherwise it displays an error. 
* -c num: Prints the first ‘num’ bytes from the file specified. Newline count as a single character, so if head prints out a newline, it will count it as a byte. num is mandatory to be specified in command otherwise displays an error. 
* -q: It is used if more than 1 file is given. Because of this command, data from each file is not precedes by its file name. 


tail -n 3 filename
```

### Cat

```
This command could read, alter or concatenate text files. It also shows file contents.

Syntax:

$ cat {filename}

cat -n - It adds line numbers to all lines

cat -b - It adds line numbers to non-blank lines

cat -s - It squeezes blank lines into one line

cat –E - It shows $ at the end of line
```

### Chmod

```
The command is utilized to alter the access authorizations of files and directories.

Syntax:

chmod {filename}

4 – read permission

2 – write permission

1 – execute permission

0 – no permission
```

```
Reference   Class     Description
u          owner      file's owner

g          group      users who are members of
                      the file's group

o          others     users who are neither the
                      file's owner nor members of 
                      the file's group

a          all       All three of the above, same as ugo
```

### Chown

```
Various clients in the operating system have proprietorship and authorization to guarantee that the records are secure and put limitations on who can alter the contents of the documents. In Linux, there exist various clients who utilize the framework:

Every client has a few properties related to them, for example, a client ID and a home registry. We could add clients into a team to make the way toward dealing with clients in a simple manner. 
A group can have at least zero clients. A predetermined client is related with a default group. It can likewise be an individual from different teams on the system also.
The chown command is utilized to aalter the file Owner or group. 

Syntax:

chown [OPTION]… [OWNER][:[GROUP]] FILE…

chown [OPTION]… –reference=RFILE FILE…

Example: To change owner of the file:

chown owner_name file_name

chown master file1.txt

Here, master is another user in the system. Consider that if you are user named user1 and you require to alter ownership to root (where your current directory is user1). You can use “sudo” before the syntax.

sudo chown root file1.txt

```

### Ifconfig

```
ifconfig(interface configuration) command is utilized to design the kernel occupant network interfaces. It is utilized at the boot time to organize the interfaces as required. From that point onward, it is typically utilized when required during investigating or when you need framework tuning. It is also utilized to allot the IP address and netmask to an interface or to empower or cripple a given interface.

Syntax:

ifconfig [...OPTIONS] [INTERFACE]

Syntax: ifconfig -a

-a : It is used to show all the interfaces accessible, even if they are down.

Syntax: ifconfig -s

-s : Display a short list, instead of details.
```

### Cut

```
Cut command is utilized for separating a part of a file utilizing segments and delimiters. If you need to list everything in a chosen section, utilize ‘- c’ with cut order. For instance, let's select the initial two columns from our demo1.txt document. 

cut -c1-2 demo1.txt
```

### Sed

```
Sed is a text manager which can execute editing activities in a non-intuitive manner. The sed command gets its contribution from standard input or a document to play out the editing procedure on a record. It is an extremely ground-breaking utility and you could do a great deal of document controls utilizing sed. In the event that you need to supplant a text in a file via looking through it in a document, you can utilize the sed command with a substitute ‘s’ to look for the particular pattern and alter it.

To replace  “mikesh” in test.txt file to “Mukesh”, you can do as:

sed 's/mikesh/mukesh/' test.txt
```

### dd

```
dd is a command-line utility for Unix and Unix-like operating systems whose main role is to change over and duplicate records.

On Unix, gadget drivers for hardware, and exceptional gadget files, show up in the record system simply like typical files. 
dd commands can also be read and/or write from/to these documents, given that capacity is executed in their individual drivers 
Thus, dd can be utilized for undertakings like supporting the boot area of a hard drive, and getting a fixed measure of random information. 
The dd program can likewise perform transformations on the information as it is replicated, including byte request trading and change to and from the EBCDIC and ASCII  text encodings.
```

### History

```
history command is utilized to see the recently operated command. This component was not accessible in the Bourne shell. Slam and Korn uphold this element where each command executed is considered as an event and is related with an occasion number utilizing which they can be reviewed and altered whenever required. These commands are stored in a set of history records. In Bash shell history command shows the entire list of the commands.

Syntax:

$ history : To display the limited number of commands which are executed prior as follows:

$ history 10
```


### Find

```
find command in UNIX is a command-line utility for strolling a file progressive system. It may very well be utilized to discover documents and indexes and perform the resulting procedure on them. It upholds searching by file, envelope, name, creation date, alteration date, proprietor and consents. By utilizing the '- executive' other UNIX commands could be operated on files or folders found.

Syntax :

$ find [where to start searching from]

[expression determines what to find] [-options] [what to find]

Options :

-ok CMD : It operates the same as -exec except the user is prompted first.
-inum N : It searches for files with inode number ‘N’.
-links N : It searches for files with ‘N’ links.
-exec CMD: The file being searched that meets the given criteria and returns 0 for as its exit status for accurate command execution.
```

### Diff

```
diff command is utilized to discover the distinction between two files. It investigations the documents and prints the lines that are not comparative. Let’s state that we have two documents, test and test1. Syntax –  diff test.txt test1.txt
```

### Free

```
In LINUX, there exists a command-line utility for this and that is free command that shows the aggregate sum of free space accessible alongside the measure of memory utilized and trade memory in the framework, and furthermore the buffers utilized by the kernel. 

Syntax:

$free [OPTION]

Options for free command

-b, – -bytes :It shows the memory in bytes.
-k, – -kilo :It shows the amount of memory in kilobytes(default).
-m, – -mega :It shows the amount of memory in megabytes.
-g, – -giga :It shows the amount of memory in gigabytes
```

### tr

```
The tr command in UNIX is a command-line utility for translating  or erasing characters. It bolsters a scope of changes including capitalized to lowercase, pressing rehashing characters, erasing explicit characters and fundamental find and replace. It may be utilized with UNIX pipes to help more intricate interpretation. tr represents translate. 

Syntax:

$ tr [flag] SET1 [SET2]

Options

-c : parallels the collection of characters in string.i.e., functions apply to characters not in the provided set.
-d : delete the characters in the first set from the output.
-s : replaces the repeated characters listed in the set1 having single events
-t : truncates set1
```

### telnet

```
Telnet aids to connect to a remote Linux computer and execute programs remotely and operate administration.

Syntax

telnet hostname=”” or=””
Example:
telnet localhost
```

### kill

```
kill command in Linux, is an underlying command that is utilized to end processes physically. This imparts a sign to a process that ends the process. In the event that the client doesn't indicate any sign that is to be sent alongside the kill command, at that point the default TERM signal is sent which ends the process.

kill -l :To show all the accessible signals you could utilize below command option:

Syntax:$kill -l

kill pid: To display how to utilize a PID using the kill command.

Syntax: $kill pid
```

### ps

```
The ps command without arguments lists the running processes in the current shell

Syntax: ps -ef           ---- list all running process 

```



