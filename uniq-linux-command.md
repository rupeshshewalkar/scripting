## uniq-linux-command

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

2. How to display number of repetitions for each line
