---
layout: post
title: The Postfix Calculator Lab
subtitle: Due November 7, 2020
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [lab]
---

# The Iris Lab!

#### Calculate what each line in calculate_me.csv evaluates to. The only operators are +, -, and *! There is no /. What is the average of all the final values?
This is a list of the solutions to the 100 expressions. The average solution for the 100 expressions is 529.91
![Solution List 1](https://imgur.com/6gPwrma.jpg)
![Solution List 2](https://imgur.com/J11XzOi.jpg)

#### Describe your process of how you worked on this lab. Include details such as who you worked with, what methods you tried, what worked or didn’t work, what could have gone better, and what you learned during this lab. Feel free to attach images, screenshots, pseudocode, etc to elaborate on your response!

##### Step One: The Setup 
1. I first imported csv into my file. This was so I could use csv commands in order to read iris.csv files.
2. Then, I imported the stack class we used previously. This was done in order to use stacks to solve postfix expressions.
![Step One](https://imgur.com/CbnhYKp.jpg)

##### Step Two: The Evaluate Function
1. In the evaluate function, a list is given, and the stack class is used iterate through the list and find the solution.
2. What lines 20-43 mean:
    -`def evaluate(list):` is a for loop that iterates through data, and takes count of the index number of each element in the list data.
    -`s1 = Stack():` this establish s1, which is a new stack.
    -`for i in list:` is a for loop that iterates through data, and takes count of the index number of each element in the list data.
    -`if(i) in ["+", "-", "*"]:` if there is an operand in the expression, go through the follow motions:

        -if(i) == "+":
            if(i) == "+":
            numA = s1.pop()
            numB = s1.pop(): 
            s1.push(numB + numA)
        numA is saved as the first number and numB is saved as the last number, push them both into the stack. if a + is detected, push the sum.

        -if(i) == "-":
            if(i) == "+":
            numA = s1.pop()
            numB = s1.pop(): 
            s1.push(numB - numA)
        numA is saved as the first number and numB is saved as the last number, push them both into the stack. if a - is detected, push the difference.

        -if(i) == "*":
            if(i) == "+":
            numA = s1.pop()
            numB = s1.pop(): 
            s1.push(numB * numA)
        numA is saved as the first number and numB is saved as the last number, push them both into the stack. if a * is detected, push the product.

    -`else:s1.push(int(i)):` if there is no longer an operand, push the final number into the stack as an int variable.
    -`return s1.peek():` once all the numbers are pushed into the stack, peek the stack. There will only be one number left, and this number in the stack will be the solution to the postfix expression.
![Step Two](https://imgur.com/vF3pG4g.jpg)

##### Step Three: Reading calculate_me.csv
1. `with open("calculate_me.csv", "r") as f:` is used to first analyze calculate_me.csv. 
2. `data = csv.reader(f)` is used to read the csv file as a list, where its elements are lists (postfix expressions)
3. Determining the values of the postfix expressions (lines 41-55):
    -`for index, row in enumerate(data):` is a for loop that iterates through data, and takes count of the index number of each element in the list data.
    -`expressionNumber = index + 1` establishes expresssionNumber, a variable that represents the index number of data. Every element in data is a postfix expression, and the indexes starts at 0. 1 is added so it can show the actual placement of the lists. For example, instead of saying the first element is the 0th element, it is the 1st with this variable.
    -`finalSolution = evaluate(row)` this establishes finalSolution, which is the return value of evaluate with the parameters row, which is the specific element or postfix expression
    -`print("The solution to expression #{} is {}".format(expressionNumber, finalSolution))` This prints out the solution as well as informing the user what number expression in the list of expression they are looking at.
4. Determining the average of the solutions of postfix expressions (line 44, 49, 53-55):
    -`totalSolution = 0` This establishes totalSolutions, which is the variable use to store the average of all the solutions.
    `totalSolution += finalSolution` In the for loop, this adds the finalSolution, the solution of an individual expression, to the variable totalSolution. As the for loop iterates through data, all the solutions of every element (postfix expression) are added to totalSolution.
    `expressionAverage = totalSolution/expressionNumber` This establishes expresionAverage, which is totalSolution/expressionNumber.
    `print("The average solution of all the expresions is {}".format(expressionAverage))` This prints out the average of the postfix expressions.
![Step Three](https://imgur.com/YauEQwd.jpg)

##### My Struggles 
My biggest struggle during this lab was actually finding out the syntax for the code. My pseudocode was great, I had an understanding of how the evaluate function and the iteration of calculate_me.csv should work in theory. 
For example, I was unsure how the conditionals in the evaluate function would work using the stacks. I knew that the function had to determine if the functions had a +, -, or *, then it would have to push out solutions, but I was unsure of how the function would iterate through each element of data. I was unsure of what the parameter of evaluate should be. Once meeting with Mr. Lee, I realized that a list had to be the parameter of evaluate(), and a for loop would have to be used to iterate through each element of the list. 
Then, I discussed with Mr. Lee how I would iterate through calculate_me.csv. I knew I had to use csv.reader() in order to read data as a list of lists, but I was unsure how evaluate would know how to use this list of list. But, becasue the evaluate function only needs a list as a parameter, I learned that row was the parameter of evaluate. Mr. Lee also thought me what the purpose of "for index, row in enumerate(data):" was. I wanted to be able to inform the user what expression number they were looking at, so my code would be user-friendly. I now know that "for index, row in enumerate(data):" iterates through not only a variable, but also counts the index values of said variable. From there, I could finish the lab with no problems.
However, after talking with Chandler Reyes, I realized an error in my code. In theory, the stack should to the last number +/-/x the first number. This did not matter when adding or mutiplying, but it does when subtracting. In the code `s1.push(s1.pop() - s1.pop())` this is the first number - the last number. After discussing with Chandler, I realized I should establish variables numA, which is the first number, and numB, the last number. Then I can push numB - numA. 


##### What I Learned 
1. How to use stacks to evaluate expressions
2. How to use for index, variable loops
