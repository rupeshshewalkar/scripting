## join-linux-command


Join command is yet another example of text processing utility under GNU/Linux. Join command combines two files based on the matching content lines found in each file. Using join command is quite straight forward and if used currently and in the right situation it can save lots of time and effort. This article requires very basic command line experience.

Frequently used options

    -1 FIELD 
    Join on specified field found in file 1
    -2 FIELD 
    Join on specified field found in file 2
    -t CHAR 
    Use CHAR as an input and output separator

Basics

Basic usage of join command is usage without any options. All what is required is to specify 2 files as an arguments. Let’s say we have two files A.txt and B.txt with a following content:

     $ cat A.txt
    10 Rupesh rupesh.shewalkar@gmail.com
    20 Ketki  ketki.lakhane@gmail.com
    30 Amit   Amit.shewalkar@gmail.com
    40 Kalyani kalyani.shewalkar@gmail.com
    50 Amol   amol.shewalkar@gmail.com

    $ cat B.txt
    10 Kharadi,Pune
    20 Bcolony,Pune
    30 Ccolony,Nagpur
    40 Vashi,Mumbai
    50 Sugoan,Pune

Here we can see that first field is a perfect candidate to perform a join operation upon. By default join command will perform join operation on a first FIELD where field separator is single space character or TAB. Therefore, by executing a following command our two files are joined based on FIELD 1:

 	 $ join A.txt B.txt
    10 Rupesh rupesh.shewalkar@gmail.com Kharadi,Pune
    20 Ketki ketki.lakhane@gmail.com Bcolony,Pune
    30 Amit Amit.shewalkar@gmail.com Ccolony,Nagpur
    40 Kalyani kalyani.shewalkar@gmail.com Vashi,Mumbai
    50 Amol amol.shewalkar@gmail.com Sugoan,Pune

