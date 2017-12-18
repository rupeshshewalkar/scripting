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


**Printf funcation**

it is same of C and C++ prinf funcation.

    #!/bin/bash
    printf "%-3s %-16s %s\n" No Name Marks
    printf "%-3d %-16s %2.2f\n" 1 Rupesh 67.9865
    printf "%-3d %-16s %2.3f\n" 2 Shewalkar 77.5999999999

   output
  
      No  Name             Marks
      1   Rupesh           67.99
      2   Shewalkar        77.600


 **Echo escape sequences**

Escaping special character we need to use -e option along with echo linux command.

	echo -e "hello\t's"

output 

	hello   's

