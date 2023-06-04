# CSE 15L Lab Report 5
## By: Kobe Yang

In this lab report, I will be enacting a pretend conversation in an EdStem thread between a student and a TA. The student will pose a question about a bug in their code and the TA will analyze their code and attempt to debug/provide a solution. 
This lab report is based on the CSE 15L [Week 9 Website](https://ucsd-cse15l-s23.github.io/week/week9/). 

**1) The student makes a debuggin post on EdStem**

*What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?*
I am using a M2 Macbook Air, which runs MacOS. I am currently using Safari as my web browser, Bash as my terminal shell, and VSCode for my code editor. 


*Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.*
I am currently trying to write a Java program that, when given a list of integers, will return length of the longest group of consecutive ascending values. Right now, I have a class called Example, which contains a main method and a static method called `numInRow`. In the main method, I am calling upon `numInRow` and passing in a List of Integers: 1, 2, 3, 4, 0, 1, 2. Ideally, `numInRow` should return 4. Instead, it is returning 3. 

![Image](________________)

Terminal input and output: 
```
MacBook-Air-5:cse15-lab5 kobeyang$ bash script.sh 
Result of numInRow() call on list1: 3
```


*Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.*
In the main method, I am calling upon `numInRow` and passing in a List of Integers: 1, 2, 3, 4, 0, 1, 2. Ideally, `numInRow` should return 4 because the first 4 elements are all consecutively increasing. Instead, it is returning 3. I am using a bash script to compile and run the file `Example.java`. It is simply three lines: 
```
set -e
javac Example.java
java Example.java
```
The bash script and the `Example.java` files are both in the same working directory. I think that there is something wrong with the behavior of my code, but I am not sure what is wrong. 

___

**2) The TA responds to the student.**

Hello, 
I agree with you that there is something wrong with the behavior of your code. I see that your bash script and main method and are both looking correct, so I do not believe that there are any errors in those parts of your code. I noticed that your goal is to find the length of the **longest** group of consecutive ascending values in the integer array. I want to emphasize the word **longest**. Perhaps you may have forgotten to implement a feature in your code to track the **longest** group? Please think about this idea and let me know what you come up with. Additionally, try testing your code with another test list to see if it works. 

___

**3) Student responds to the TA with results.**
Hello, 
Thank you for letting me know. I now understand what went wrong with my code. Originally, I would loop through the given list and increment the variable `longestConsecutiveStreak` everytime the current element had increased by a value of 1. I would also reset the `longestConsecutiveStreak` variable anytime the current element had not increased by a value of 1. However, I did not account for the fact that this solution would only give the length of the *last* group of consecutive ascending values. This is because the `longestConsecutiveStreak` variable is reset anytime a consecutive ascending streak is broken. This could mean that we could have, at one time in the loop, had the maximum consecutive streak stored in the `longestConsecutiveStreak` variable, but we would reset it once the streak was broken. In the example above, my method would loop through the array and see that there was a consecutive ascending streak of `1, 2, 3, 4` at first (`longestConsecutiveStreak` = 4), but that would reset to 1 when it encountered the value `0`. In the end, my method would return `3` because it would see that that the *last* group of consecutive ascending values was of length `3` (`0, 1, 2`). 

To fix this error, I have added another variable called `maxStreak`. In each iteration of the loop, I will check if the current value of `longestConsecutiveStreak` is greater than `maxStreak`. If it is, I will replace the value of `maxStreak` with the current value of `longestConsecutiveStreak`. In the end, I will return `maxStreak`. In this new solution, I have found a way to keep track of the length of the *largest* group of consecutive ascending values, independent from other smaller groups/resets in the list of integers. 

I have also added two more test cases to demonstrate that my method works well. In the second test, the maximum length of a group of consecutive ascending values is 2 (It appears at the start of the list: `6, 7`). In the third test, the maximum length of a group of consecutive ascending values is 3 (It appears at the start of the list: `0, 1, 2`). 



New 
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
