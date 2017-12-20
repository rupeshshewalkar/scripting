**Tr linux commands**

the tr command stands for translate is used to provide a level of swapping or translation, suppression or deletion of files. The tr command just translates one character to another character. In this article, we’ll share a couple of examples demonstrating some exciting things that we can do with the tr command.

The basic syntax of tr linux command

    tr [OPTION] [SET1] [SET2]

SET1 denotes what we wish to translate in the input file, and SET2 means what we want to convert SET1 as the output of the translation. So the sets can be a single character or multiple characters.


Examples:

**1) Suppose you just want to replace R in “Rupesh Shewalkar” with B we can use tr sets. We use echo command to send “Rupesh Shewalkar” to tr command. The tr command by default is not able to read data stream. We use Linux inbuilt redirection operators to feed data to tr command**

    	echo "rupesh Shewalkar" | tr 'r' 'b'
        bupesh Shewalkab
        
**2)Suppose if you want to replace multiple characters one after the other then we can use below-set examples. Suppose you want to replace r with a, u with b and p with c, below is the case you are looking at.**

    echo "rupesh Shewalkar" | tr 'rup' 'abc'
	abcesh Shewalkaa

**3)Convert all characters in input from lower to upper case and viceversa.**

    echo "rupesh Shewalkar" | tr 'a-z' 'A-Z'
    RUPESH SHEWALKAR

    echo "RUPESH SHEWALKAR" | tr 'A-Z' 'a-z'
    rupesh shewalkar

**4) We can translate individual characters as well. Translate braces into parenthesis.**

    [root@linuxnix ~]# echo "{ Hello World }" > infile 
    [root@linuxnix ~]# tr '{}' '()' < infile > outfile 
    [root@linuxnix ~]# cat outfile 
    ( Hello World )
 
**5)Translate spaces to new lines. We use infile as our test file. Use cat command to display the content of the file.**

    [root@linuxnix ~]# cat infile 
    solaris linux aix 
    [root@linuxnix ~]# cat infile | tr " " "\n" 
    solaris 
    linux 
    aix 
    [root@linuxnix ~]# cat infile | tr "[:space:] " "\n"
    solaris 
    linux 
    aix

**6) Replace white space with a different delimiter.**

    [root@linuxnix ~]# cat infile | tr " " ":"
    solaris:linux:aix
    [root@linuxnix ~]# cat infile | tr " " "|"
    solaris|linux|aix
    
**7)Replace multiple occurrences of a character with a single appearance of the character. In below example, we replaced numerous spaces with separate space.**

    [root@linuxnix ~]# cat infile
    solaris      linux   aix
    [root@linuxnix ~]#
    [root@linuxnix ~]# tr -s " " < infile
    solaris linux aix

In the above case, we used the tr command with -s option to indicate a squeeze operation.
This replaces multiple occurrences of a character with a single appearance of the same character


**8)Replace multiple occurrences of a character with a different character.**

	[root@linuxnix ~]# cat infile
    solaris linux aix
    [root@linuxnix ~]# tr -s " " ";" < infile
    solaris;linux;aix

The above tr command squeezes multiple occurrences of white space into one semicolon character.

**9)Delete all occurances of a character.**

To delete occurrences of a character we use the -d option with the tr command followed by the character to be removed.

    [root@linuxnix ~]# echo "linuxunix" | tr -d 'u'
    linxnix

The above command removes all occurrences of the character u from the input string.

**10)Remove all digits from the input.**

  	[root@linuxnix ~]# echo "james bond 007" | tr -d '0-9'
	james bond
    
**11)Remove all alphabets from the input.**

	[root@linuxnix ~]# echo "james bond 007" | tr -d 'a-zA-Z'
	007


**12) Remove all characters except the given set with tr.**

We used -d option to delete characters we mentioned from the input.
We may use the -c option with the -d option to delete all characters except those that we mention.

    [root@linuxnix ~]# echo "solaris linux hp-ux" | tr -cd 'slh'
    slslh[root@linuxnix ~]#

The above tr command removed all characters including the new line leaving behind the characters s,l and h which we mentioned to be removed.
Using the -c option is also sometimes referred to as complimenting the set.

**13: Remove all non-alphanumeric and space characters.**

    [root@linuxnix ~]# echo "solaris | linux 007 ; hp-ux :::: aix" | tr -cd "[:alpha:][:space:][:digit:]"
    solaris linux 007 hpux aix

This example could prove to be especially useful when dealing with a file having a lot of junk characters.

**14: Translate non-alphanumeric characters into a single newline character.**

    [root@linuxnix ~]# echo "james bond 007" | tr -cs 'a-zA-Z0-9' '\n'
    james
    bond
    007

 
**15: Join all lines in a file into a single line.**

    [root@linuxnix ~]# cat infile
    solaris
    linux
    aix
    [root@linuxnix ~]#
    [root@linuxnix ~]# tr -s '\n' ' ' < infile
    solaris linux aix [root@linuxnix ~]#

The above tr command squeezes the new line character into a single space character.
This option can be useful when attempting to consolidate scattered text in a file.
