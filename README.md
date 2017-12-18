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

**Variable and Environment Variable**

- In scripting langauge,usually not required to initialize variables
- Environment variables used by shell environment, which stores specially value
- env command help to find out environment variables
- Environment variable not defined by current process, it get from parent process
- Well know Enovironment variables are HOME,UID,PATH,SHELL etc

- Assign variable with equal sign has different meaning 

      var=23 assigns 23 to the variable var.
      var =23 tries to run command (or alias, or function) var with argument =23
      var = 23 ditto, but arguments = and 23
      var= 23 sets var environment variable to blank string, then runs command 23

- Variables are declared and assigned without $ and without {}. You have to use

	  var=10

to assign. In order to read from the variable (in other words, 'expand' the variable), you must use $.

    $var      # use the variable
    ${var}    # same as above
    ${var}bar # expand var, and append "bar" too
    $varbar   # same as ${varbar}, i.e expand a variable called varbar, if it exists.

- Curly braces are also unconditionally required when:

      - expanding array elements, as in ${array[42]}
      - using parameter expansion operations, as in ${filename%.*} (remove extension)
      - expanding positional parameters beyond 9: "$8 $9 ${10} ${11}"
 