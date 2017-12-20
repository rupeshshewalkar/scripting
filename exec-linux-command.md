the exec command

The exec command will replace the parent process by whatever the command is typed.

Try the following:

exec ls -l
            
As you will have noticed, this closes the shell you are currently using. Why?

The exec command terminated the parent process and started (executed) the ls command and the ls command did what it was supposed to do and exited with a zero status, but ls has no parent process to return to, and thereby the shell is shut down.

If for example, we ran our eatout.sh script, but instead of running it as we have previously, we exec'd it, the script would run but would also close our terminal from which we ran the script.

exec eatout.sh
            
This means that when the person finally types exit to exit the menu, they are sent back to the login prompt.

To see this in action, let's consider the following sequence of commands:

pstree -p |less
            
You will notice that "pstree" starts with the init command or the init process. Somewhere further down this 'tree', init starts a shell (bash/ksh/csh) which is then going to run the pstree and the less command.

Now, in order to see exec at work, we need to find out the current process id.

Use:

echo $$
            
to determine this (the ps command would give you the same information).

Now type the pstree command again, producing a diagram of your process tree.

pstree -p | less
            
Search for your process id recorded from the echo above. Once you have located it, quit pstree and type:

exec bash
            
This would replace our current shell (our parent) with a new shell, and thus a new process id (PID).

echo $$
            
You can also look at the pstree again.

By using the exec command, instead of making the new shell's parent your original shell, the new shell will be owned by init.

Other methods of executing a script or a series of commands

Execution with Round brackets

The shell has two further constructs: round brackets () and curly brackets{}. Round brackets means execute the commands in the round brackets in a NEW subshell.

So if you type:

pwd
                    
You'll probably be in your home directory, something similar to:

/home/hamish
                    
If you now say:

(cd /bin; pwd)
                    
It will say on the command line:

/bin
                    
Once this is complete, we type:

pwd 
                    
We are still in:

/home/hamish
                    
Why?

The command executed in a subshell, the cd command happened in the subshell. Once the shell is complete (once the pwd command has been run), control is passed back to the parent shell, which had never left the /home/hamish directory.

Enclosing commands in round brackets will run these commands in a subshell. One of the places this can be used in is in copying the contents of one subdirectory on a partition into a new subdirectory on a different partition:

tar cvf - /oldpart | (cd /newpart; tar xvf - .)
                    
The minus signs mean send the output to stdout.

In this example, we create a new tape archive (tar) of our old partition, being sent to stdout instead of a file.

We pipe this standard output to the standard input of the next tar command, but because this is part of a subshell, we can cd to the new directory and untar (extract) the files here instead of /oldpart.

The process would copy the entire contents of /oldpart directory to /newpart, preserving all links, modes, ownerships, everything! Note that the above example is a single command which we can run in the background by appending an ampersand (&) to the end of the command:

(tar cvf - /oldpart | (cd /newpart; tar xvf - .))&amp;
                    
Earlier, we were reading from a file using a while loop, but we were forced to change the IFS. At that point, we simply:

IFS=","
while read type, place .....
do
	etcetera....
                    
This changed our IFS for the shell too, which is not necessarily a good thing for future commands in that log in session or until IFS is reset again back to a space, tab or <return>.

Now, using the (), we can modify the commands as follows:

( IFS=",";while read type, place .....
	do
	etcetera....
)
                    
which would run the entire expression in a subshell and on completion, our IFS would remain unchanged.

Execution with Curly brackets

The curly brackets {} on the other hand mean "execute the commands within the current shell - do not use a new subshell".

So for example, we could say:

{program1;program2;program3;} 2>/tmp/errors
                    
Any errors would go to /tmp/errors. Note that the above command is equivalent to:

program1 2>/tmp/errors
program2 2>/tmp/errors
program3 2>/tmp/errors
                    
Where the errors of program2 and program3 are appended to the same place where program1's errors are.

Clearly there is a lot more typing involved in the second option than in the first option.

[Note]	Note
Each single command that you use within the curly brackets must be followed by a semi colon( ; ).

So:

{ ls -l; pwd }
                    
will produce an error, while

{ls -l; pwd; }
                    
will work as desired.

An example Comparing round brackets against curly brackets

By way of example, assuming we have a script called myscript.sh and we wish to set some environmental variables prior to running the script, we could simply set them and enclose the whole bang shoot in curlies or round brackets. Try:

echo Before subshell: $NAME $COMPANY
(NAME=Hamish COMPANY='QED Technologies CC'; pwd)
echo After subshell: $NAME $COMPANY

echo Before : $NAME $COMPANY
{NAME=Hamish COMPANY='QED Technologies CC'; pwd;}
echo After : $NAME $COMPANY
                    
Obviously, in the second instance, the variables NAME and COMPANY will be present AFTER the script has executed, while in the former case, they will not be set.

That would set up those environment variables before the start of that script.

Alternatively, we could source these variables from a file during the script.
