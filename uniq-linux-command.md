## uniq-linux-command

## Note: ’uniq’ does not detect repeated lines unless they are adjacent.  You  may  want to  sort  the  input first, or use ‘sort -u’ without ‘uniq’
       
       
the uniq command reports or omits repeated lines. Here's the general syntax of this command:

    uniq [OPTION]... [INPUT [OUTPUT]]

According to the utility's man page: "Filter adjacent matching lines from INPUT (or standard input), writing to OUTPUT (or standard output). With no options, matching lines are merged to the first occurrence."


**1. How to delete repeated lines using uniq command**

Suppose the file contains following lines:

    $ cat file1
    Welcome to gitlab
    Welcome to gitlab
    Welcome to gitlab
    We are learning uniq command
    We are learning uniq command
    We are learning uniq command
    thanks
    thanks

Clearly, each line is repeated. Now let's run Uniq on this file, and see what happens.

    $ uniq file1
    Welcome to gitlab
    We are learning uniq command
    thanks

So as you can see, the output the command produced contains no repeated lines. Please note that the original file - 'file1' in our case - remains unaffected. You can redirect the tool's output to another file in case you want to save and work on it

**2. How to display number of repetitions for each line**

If you want, you can also make uniq display in output the number of times a line is repeated. This can be done by using the -c command line option. For example, the following command:

    $  uniq -c file1
          3 Welcome to gitlab
          3 We are learning uniq command
          2 thanks

**3. How to only print duplicate lines using uniq**

To make uniq print only duplicate lines, use the -D command line option. For example, suppose file1 now contains an extra line at the bottom (note that this line is not repeated).

    $ cat file1
    Welcome to gitlab
    Welcome to gitlab
    Welcome to gitlab
    We are learning uniq command
    We are learning uniq command
    We are learning uniq command
    thanks
    thanks
    Non duplicate line

Now, when I run the following command:

	$ uniq -D file1

The following output is produced:

    $ uniq -D file1
    Welcome to gitlab
    Welcome to gitlab
    Welcome to gitlab
    We are learning uniq command
    We are learning uniq command
    We are learning uniq command
    thanks
    thanks

As you can see, the -D option makes uniq display all repeated lines in output, including all their repetitions. To better segregate, you can have an empty line after each group of repeated lines, something which can be done using the --all-repeated option.
 
 	uniq --all-repeated[=METHOD] file1

This option requires a method name to be entered by the user. The values could be prepend (to prepend empty line) or separate (to append an empty line). For example, here's this option in action with prepend method.

    $ uniq --all-repeated=prepend file1

    Welcome to gitlab
    Welcome to gitlab
    Welcome to gitlab

    We are learning uniq command
    We are learning uniq command
    We are learning uniq command

    thanks
    thanks


**4. How to make uniq avoid comparing first few fields**

Sometimes, depending on the situation, the similarity of two lines is defined by a small part of those lines. For example, consider the contents of the following file

    $ cat file2
    Rupesh Pune
    Sudeep Pune
    Kalyani Pune
    Amit Mumbai
    Abhishek Mumbai
    Rahul Mumbai
    Dhiraj Hyderabad
    Pankaj Hyderabad
    Pranav Hyderabad

Now, suppose the lines are considered similar or different based on their second field, and you want to convey this to uniq, then this can be done using the -f command line option.

	uniq -f [number-of-fields-to-skip] [file-name]

The -f option requires you to pass a number that represents the number of fields you want the command to skip. For example, in our case, we can pass '1' as argument to -f as it's only the first field that we want uniq to skip.

     $ uniq -f 1 file2
    Rupesh Pune
    Amit Mumbai
    Dhiraj Hyderabad


**5. How to make uniq display all lines, while separating repetitive groups with empty line**

In case the requirement is to display all lines, while separating repetitive groups of lines with an empty line, then you can use the --group option. Like the --all-repeated option we discussed earlier, --group also requires you to tell the position of empty line (prepend, append, or both).
Here's an example:

