##Equi-Join operation using MapReduce (Java) on multi-node Hadoop filesystem

Implemented Equi-Join operation on tuples using MapReduce on multi node hadoop cluster to (1 Master & 3 Slaves). 


###Instructions: { Coder: Jasdeep }
----------------------------------------------------------------------------------------------------------------

Assumption: The code assumes that the data is given for two tables only.

command to run the code on hadoop cluster:
sudo -u <username> <path_of_hadoop> jar equijoin.jar dds.assignment4.App <HDFSinputFile> <HDFSoutputFile>

----------------------------------------------------------------------------------------------------------------
Folder contains:
1: App.java (containing Map class, Reduce class and main class)
2: equijoin.jar
3: ReadMe.txt
-----------------------------------------------------------------------------------------------------------------

MAPPER CLASS: Map
This class will receive data in key which I save in String line variable. I got the data in a String array, splitted by comma: ",". I get the JoinColumn from second character of string array. Then I am take table1Name and table2Name first from character in the string array. Using context.write I write JoinColumn and ValueLine(which has the data)   

REDUCER CLASS: Reduce
This class will make two arraylists for two tables based on tablenames(table1Name and table2Name). Then running for loops in each table I made the join and added that to string strData variable. Then I put the String strData variable's data into new Text variable called joinResult. Then I am clearing joinResult everytime.   

DRIVER CLASS: main 
In Main class, conf is created using Configuration. Then Job variable is created using conf variable. After that I set the names of mapperclass and reducerclass. Then I set the outputkeyclass, outputvalueclass, mapoutputkeyclass, mapoutputvalueclass, Inputformatclass and outputformatclass. After that I set the inputfileformat with the input path: args[0] and outputfileformat with the output path: args[1]. In the end I set the boolean for waitforcompletion to true. 

-----------------------------------------------------------------------------------------------------------------
Input file 
R, 2, Don, Larson, Newark, 555-3221
S, 1, 33000, 10000, part1
S, 2, 18000, 2000, part1
S, 2, 6958, 454, pJ
R, 3, Sal, Maglite, Nutley, 555-6905
S, 3, 24000, 5000, part1
S, 3, 985, 67, part8
S, 4, 22000, 7000, part1
R, 4, Bob, Turley, Passaic, 555-8908

Output
R, 2, Don, Larson, Newark, 555-3221, S, 2, 18000, 2000, part1
R, 2, Don, Larson, Newark, 555-3221, S, 2, 6958, 454, pJ
R, 3, Sal, Maglite, Nutley, 555-6905, S, 3, 24000, 5000, part1
R, 3, Sal, Maglite, Nutley, 555-6905, S, 3, 985, 67, part8
R, 4, Bob, Turley, Passaic, 555-8908, S, 4, 22000, 7000, part1
------------------------------------------------------------------------------------------------------------------



