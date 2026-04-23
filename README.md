8085 microprocessor assembly language program to find the perfect square root of the given integer.


```
LDA 2000H        ; Store the value of integer here

MVI C, 01H       ; C starts at 1 because square numbers are formed by
                 ; sum of odd numbers → 1 + 3 + 5 + 7 ...
                 ; So we subtract these step by step

MVI D, 00H       ; D is used as a counter to track how many times subtraction succeeds
                 ; This count directly becomes the square root

LP: SUB C        ; We subtract current odd number to reduce the original value
                 ; Each successful subtraction represents one step toward sqrt

    JZ LP2       ; We check ZERO because perfect squares reduce exactly to 0
                 ; That exact hit means we found the square root

    INR D        ; Increase counter because one valid subtraction happened
                 ; This is how we build the sqrt result

    INR C        
    INR C        ; We increase C by 2 to generate next odd number (1→3→5→7...)
                 ; This follows the mathematical property of squares

    JMP LP       ; Repeat process until number becomes exactly zero

LP2: INR D       ; Final increment because last subtraction also counts
                 ; Without this, result would be one less

     MOV A, D 
     STA 2051H   ; Result will be stored at this location

HLT              ; Stop
```



**Explanation**  
A number is a perfect square if it can be written as:

N = 1 + 3 + 5 + 7 + ... (sum of consecutive odd numbers)
👉 Example:
9 = 1 + 3 + 5
16 = 1 + 3 + 5 + 7
⚙️ Core Idea
Instead of multiplying numbers, we:
Start with the given number N
Subtract odd numbers one by one:
1, then 3, then 5, then 7...
Count how many subtractions we can do until the result becomes zero
👉 That count = square root
📌 Example (N = 9)

9 - 1 = 8
8 - 3 = 5
5 - 5 = 0  ← stop
Total steps = 3
👉 √9 = 3
⚠️ Important Note
Works only for perfect squares
If the number is not a perfect square, it will not reach exactly zero
