8085 microprocessor assembly language program to find the perfect square root of the given integer.


```
LDA 2000H        ; Store the value of integer here
MVI C, 01H       ; C starts at 1 because square numbers are formed by sum of odd numbers → 1 + 3 + 5 + 7 ...
MVI D, 00H       ; D is used as a counter to track how many times subtraction succeeds and this count directly becomes the square root

LP: SUB C        ; We subtract current odd number to reduce the original value and each successful subtraction represents one step toward sqrt
    JZ LP2       ; We check ZERO because perfect squares reduce exactly to 0, that exact hit means we found the square root
    INR D        ; Increase counter because one valid subtraction happened
    INR C        
    INR C        ; We increase C by 2 to generate next odd number (1→3→5→7...) and this follows the mathematical property of squares
    JMP LP       ; Repeat process until number becomes exactly zero

LP2: INR D       ; Final increment because last subtraction also counts and if we ignore this, result would be one less
     MOV A, D 
     STA 2051H   ; Result will be stored at this location

HLT              ; Stop
```



**Explanation**   

A number is a perfect square if it can be written as:
N = 1 + 3 + 5 + 7 + ... (sum of consecutive odd numbers)  
For Example
9 = 1 + 3 + 5 or 16 = 1 + 3 + 5 + 7   

Instead of multiplying numbers, we start with the given number N and subtract odd numbers one by one: 1, then 3, then 5, then 7...  
Count how many subtractions we can do until the result becomes zero and finally that count = square root.   
For example we will try to find out square root of 9 here-  
Step-1 9 - 1 = 8  
Step-2 8 - 3 = 5  
Step-3 5 - 5 = 0  ← stop  
Total steps = 3  
so we can say √9 = 3


**Important Note**   
Works only for perfect squares  
If the number is not a perfect square, it will not reach exactly zero
