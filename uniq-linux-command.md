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


**6. How to make uniq only print non-repetitive lines**

As you'd have understood by now, by default the uniq command only displays repeated lines in the output. But if you want, you can instead make it to display only non-repeated or unique lines. This can be done using the -u command line option.

    uniq -u [file-name]

So, in our case:
    
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


	$ uniq -u file1
    Non duplicate line

**7. How to make uniq avoid comparing set number of initial characters**

In one of our earlier examples, we discussed how you can make uniq skip fields. However, if you want, you can force the tool to skip a set number of initial characters as well. This feature can be accessed using the -s command line option.

	uniq -s [number-of-char] filename

For example, suppose the file contains following lines:

    MR. Rupesh 
    Shri. Rupesh
    Miss. Kalyani
    Doc. Kalyani
    MR. Amit
    Eng. Amit
    
Now, if you want uniq to skip the first 6 characters in each line before comparing, then this can be done in the following way:

	$ uniq -s 6 file3
    MR.   Rupesh
    Miss. Kalyani
    MR.   Amit

**8. How to limit comparison to set number of chars**

Similar to the way you skip characters, you can also ask uniq to limit the comparison to a set number of characters. For this, you'll have to use the -w command line option.

	uniq -w [num-of-chars] [file-name]

For example, suppose the file contains the following lines:

    $ cat file4
    Rupesh
    Rupesh Shewalkar
    Rupesh Jeewanrao Shewalkar

Now, if the requirement is to limit the comparison to first 5 characters, then this can be done in the following way:

    $ uniq -w 5 file4
    Rupesh
 
 
