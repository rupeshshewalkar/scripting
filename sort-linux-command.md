## Sort Linux Command

sort command is used to sort a file, arranging the records in a particular order. By default, the sort command sorts file assuming the contents are ascii. Using options in sort command, it can also be used to sort numerically. Let us discuss it with some examples:

File with Ascii data:
 Let us consider a file with the following contents: 

	$ cat file
    Unix
    Linux
    Solaris
    AIX
    Linux
    HPUX

**1. sort simply sorts the file in alphabetical order:**

	$ sort file
    AIX
    HPUX
    Linux
    Linux
    Solaris
    Unix
    All records are sorted alphabetically.

**2. sort removes the duplicates using the -u option:**

    $ sort -u file
    AIX
    HPUX
    Linux
    Solaris
    Unix

The duplicate 'Linux' record got removed. '-u' option removes all the duplicate records in the file. Even if the file have had 10 'Linux' records, with -u option, only the first record is retained.

File with numbers:

Let us consider a file with numbers: 

	$ cat file
      20
      19
      5
      49
      200

**3. The default sort 'might' give incorrect result on a file containing numbers:**

    $ sort file
    19
    20
    200
    49
    5

In the above result, 200 got placed immediately below 20, not at the end which is incorrect. This is because the sort did  ASCII sort. If the file had not contained '200', the default sort would have given proper result. However, it is incorrect to sort a numerical file in this way since the sorting logic is incorrect.

**4. To sort a file numericallly:**

    $ sort -n file
    5
    19
    20
    49
    200

-n option can sort the decimal numbers as well.

**5. sort file numerically in reverse order:**

      $ sort -nr file
      200
      49
      20
      19
      5

'r' option does a reverse sort.

Multiple Files:
 Let us consider examples with multiple files, say file1 and file2, containing numbers: 

    $ cat file1
    20
    19
    5
    49
    200
    $ cat file2
    25
    18
    5
    48
    200

**6. sort can sort multiple files as well.**

    $ sort -n file1 file2
    5
    5
    18
    19
    20
    25
    48
    49
    200
    200

The result of sort with multiple files will be a sorted and merged output of the multiple files.

**7. Sort, merge and remove duplicates:**

    $ sort -nu file1 file2
    5
    18
    19
    20
    25
    48
    49
    200

-u option becomes more handy in case of multiple files. With this, the output is now sorted, merged and without duplicate records.

Files with multiple fields and delimiter:
Let us consider a file with multiple fields: 

    $ cat file
    Linux,20
    Unix,30
    AIX,25
    Linux,25
    Solaris,10
    HPUX,100

**8. sorting a file containing multiple fields:**

    $ sort file
    AIX,25
    HPUX,100
    Linux,20
    Linux,25
    Solaris,10
    Unix,30

As shown above, the file got sorted on the 1st field, by default.

**9. sort file on the basis of 1st field:**

    $ sort -t"," -k1,1 file
    AIX,25
    HPUX,100
    Linux,20
    Linux,25
    Solaris,10
    Unix,30

This is being more explicit. '-t' option is used to provide the delimiter in case of files with delimiter. '-k' is used to specify the keys on the basis of which the sorting has to be done. The format of '-k' is : '-km,n' where m is the starting key and n is the ending key. In other words, sort can be used to sort on a range of fields just like how the group by in sql does. In our case, since the sorting is on the 1st field alone, we speciy '1,1'. Similarly, if the sorting is to be done on the basis of first 3 fields, it will be: '-k 1,3'.

Note: For a file which has fields delimited by a space or a tab, there is no need to specify the "-t" option since the white space is the delimiter by default in sort.

**10. sorting file on the basis of the 2nd field:**

    $ sort -t"," -k2,2 file
    Solaris,10
    HPUX,100
    Linux,20
    AIX,25
    Linux,25
    Unix,30

**11. sorting file on the basis of 2nd field , numerically:**

    $ sort -t"," -k2n,2 file
    Solaris,10
    Linux,20
    AIX,25
    Linux,25
    Unix,30
    HPUX,100

**12. Remove duplicates from the file based on 1st field:**

    $ sort -t"," -k1,1 -u file
    AIX,25
    HPUX,100
    Linux,20
    Solaris,10
    Unix,30

The duplicate Linux record got removed. Keep in mind, the command "sort -u file" would not have worked here becuase both the 'Linux' records are not same, the values were different. However, in the above, sort is told to remove the duplicates based on the 1st key, and hence the duplicate 'Linux' record got removed. According to sort, in case of a group of similar records, except the first one, the rest are considered duplicate.

**13. Sort the file numerically on the 2nd field in reverse order:**

    $ sort -t"," -k2nr,2 file
    HPUX,100
    Unix,30
    AIX,25
    Linux,25
    Linux,20
    Solaris,10

**14. sort the file alphabetically on the 1st field, numerically on the 2nd field:**

    $ sort -t"," -k1,1 -k2n,2 file
    AIX,25
    HPUX,100
    Linux,20
    Linux,25
    Solaris,10
    Unix,30

**15. sort a file based on the 1st and 2nd field, and numerically on 3rd field on  a file containing 5 columns:**

$ sort -t"," -k1,2 -k3n,3 file 


**16. sometime lines having some extra leading blanks which you can easliy ignore in sort with -b flag**

    alan@alan-ubuntu-vm:~/tmp/sort$ cat blank_letters.txt
    b
    D
       c
    A
    C
        B
    d
    a

We can easily ignore those and still sort correctly (using the -b flag):

    alan@alan-ubuntu-vm:~/tmp/sort$ sort -f -s -b blank_letters.txt
    A
    a
    b
        B
       c
    C
    D
    d


**17. Sort Human Readable Numbers using -h option**

If we want to sort on human readable numbers (e.g., 2K 1M 1G), then we can use -h or –human-numeric-sort option.

Create the following test file for this example:

    $ cat test
    2K
    2G
    1K
    6T
    1T
    1G
    2M

The following sort command sorts human readable numbers (i.e 1K = 1 Thousand, 1M = 1 Million, 1G = 1 Giga, 1T = 1 Tera) in test file and displays sorted output.

    $ sort -h test
    1K
    2K
    2M
    1G
    2G
    1T
    6T


**17.Sort Months of an Year using -M option**

If we want to sort in the order of months of year, then we can use -M or –month-sort option.

Create the following test file for this example:

    $ cat test
    sept
    aug
    jan
    oct
    apr
    feb
    mar11

The following sort command sorts lines in test file as per month order. Note, lines in file should contain at least 3 character name of month name at start of line (e.g. jan, feb, mar). If we will give, ja for January or au for August, then sort command would not consider it as month name.

    $ sort -M test
    jan
    feb
    mar11
    apr
    aug
    sept
    oct
