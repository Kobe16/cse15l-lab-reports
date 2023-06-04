# CSE 15L Lab Report 5
## By: Kobe Yang

In this lab report, I will be enacting a pretend conversation in an EdStem thread between a student and a TA. The student will pose a question about a bug in their code and the TA will analyze their code and attempt to debug/provide a solution. 
This lab report is based on the CSE 15L [Week 9 Website](https://ucsd-cse15l-s23.github.io/week/week9/). 

1) The student makes a debuggin post on EdStem

What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?
I am using a M2 Macbook Air, which runs MacOS. I am currently using Safari as my web browser, Bash as my terminal shell, and VSCode for my code editor. 


Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.
I am currently trying to write a Java program that, when given a list of integers, will return length of the longest group of consecutive ascending values. Right now, I have a class called Example, which contains a main method and a static method called `numInRow`. In the main method, I am calling upon `numInRow` and passing in a List of Integers: 1, 2, 3, 4, 0, 1, 2. Ideally, `numInRow` should return 4. Instead, it is returning 3. 

![Image](________________)

Terminal input and output: 
```
MacBook-Air-5:cse15-lab5 kobeyang$ bash script.sh 
Result of numInRow() call on list1: 3
```


Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.
In the main method, I am calling upon `numInRow` and passing in a List of Integers: 1, 2, 3, 4, 0, 1, 2. Ideally, `numInRow` should return 4 because the first 4 elements are all consecutively increasing. Instead, it is returning 3. I am using a bash script to compile and run the file `Example.java`. It is simply three lines: 
```
set -e
javac Example.java
java Example.java
```
The bash script and the `Example.java` files are both in the same working directory. I think that there is something wrong with the behavior of my code, but I am not sure what is wrong. 

___

2) 





```
int longestConsecutiveStreak = 1; 
        // int maxStreak = 1; 

        for(int i = 1; i < catchOrder.size(); i++) {
            if(catchOrder.get(i) - catchOrder.get(i - 1) == 1) {
                longestConsecutiveStreak++; 

                // if (longestConsecutiveStreak > maxStreak) {
                //     maxStreak = longestConsecutiveStreak; 
                // }
            }
            else {
                // reset streak
                longestConsecutiveStreak = 1; 
            }
        }

        // return maxStreak; 
        return longestConsecutiveStreak; 
```
