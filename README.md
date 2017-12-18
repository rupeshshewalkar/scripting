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
      
**Math in shell**

- We can perform math operation using let command,expr command, [] and (())

example:
        
        let result=4+5
        echo $result
        9
        
        result=$[ 3+5 ]
        echo $result
        8
       
       result=$(( 3-1))
       echo $result
       2
 
**File descriptors and Redirection**

File descriptors are integer assoicated with file input and output. 0,1,2 are reserved as file descriptors

	- 0 stdin (standard input)
    - 1 stdoutput (standard output)
    - 2 stderr (standard error)


**Array and associated array**

- Stores a collection of data as seperate entity using indexes
- Associative arrays can take a string as their array index

 		- Declarartion of array 
        
        array_emp=(1 Rupesh 23901)
        
        - Print array element 
         
         echo ${array_emp[1]}
         Rupesh

		- Print entire array 
          echo ${array_emp[*]} or echo ${array_emp[@]}
          1 Rupesh 23901
        
        - Calculate length of array 
          echo ${#array_emp[*]}
          3
        
        - Know indexes of array 
          echo ${!array_emp[*]}
          0 1 2

        - add or update element in a array 
         array_employee[3]="Pune"
 
 
 - Associative array declaration 
 
         declare -A fruit_value
         fruit_value=( [Apple]='$10' [orange]='$5' )
         echo ${fruit_value[Apple]}
		 $10

**Alias**

- Alias command used to create shortcut of long command/commands for quick access

- syntax for creating alias of any command or commands
   	
      alias new_command='command Sequence'
      
- creating alias for rm so that if we delete any file it will take backup in ~/backup

      alias rm='cp $@ ~/backup && rm $@'

- temporarily disable alias command facility run command with escape \ like
   
      \rm test1.txt 
      
-   unalias command used to remove aliases of any command or commands


**Grabbing information of Terminal**

- Collecting and manipulation terminal setting such finding out number of column,row,cursor position, password masking etc

- tput and stty command helps to terminal manipulating settings.

Example:

		- Print the number of columns for the current terminal
        tput cols
        103
       
       - Print the number of lines for current terminal 
        tput lines
        33
       
       - Send  the  sequence to move the cursor to row 100, column 100 
       tput cup 100 100
       
 
 **Debugging Bash script**

- -x option enable debug tracing for shell script 
- +x option disable debug tracing for shell script
- Running the script with the -x flag will print each source line with the current status. Note that you can also use sh-x script. Debug only portions of the script using the set -x and set +x. For example, in the preceding script the debug information for echo $I will only be printed, as debugging is restricted to that section using the -x and +x.

example:
 
        #!/bin/bash
        #Filename: debug.sh
        for i in {1..6};
        do
            set -x
            echo $i
            set +x
        done
        echo "Script executed"

example2 : In this example debug information only disable when we asked to debug 

    #!/bin/bash
    function DEBUG()
    {
        [ "$_DEBUG" == "on" ] && $@ || :
    }

    for i in {1..10}
    do
        DEBUG echo $i
    done


