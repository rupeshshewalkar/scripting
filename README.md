# scripting

Printing terminal

Difference between single quote and double quote while echoing 

This is explained very nicely in the relevant section of the bash manual. Briefly, anything within single quotes is interpreted literally. So, for example:

$ echo '$SHELL'
$SHELL
$ echo '{1..3}'
{1..3}
Compare that to the unquoted versions:

$ echo $SHELL
/bin/bash
$ echo {1..3}
1 2 3
Double quotes allow variable expansion (also history expansion and some other things). Basically, you use them when you are dealing with something that you want to see expanded. For example:

$ echo "$SHELL"
/bin/bash
$ echo "!!"
echo "echo "$SHELL""
echo /bin/bash
In other words, single quotes completely protect a string from the shell while double quotes protect some things (spaces for example) but allow variables and special characters to be expanded/interpreted correctly.



