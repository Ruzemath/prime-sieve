#|

Author: Ruze

Date: September 23, 2022

Description: We are building functions that create lists, functions that create other functions using currying, and building higher order
functions such as filtering a list. Then using all of that to build a Sieve of Eratosthenes function that finds the primes in a list.

|#

; Part 1 – Making a list of numbers from 2 to n
(define make-2-n-list (lambda (maxNum) (if (= maxNum 2) ; Base Case: Once maxNum equals 2 we return 2 in the form of a list that will start off our list creation
                                         (list 2)
                                         (append (make-2-n-list (- maxNum 1) ) (list maxNum) ) ; Recursive Case: Recursively call the function with maxNum minus one 
                                       )                                                       ; and combining it with the current maxNum in the form of a list (Backwards Right Fold Recursion)
                                     )) 


; Part 2 – Checking if a number is divisible
(define divisible-by? (lambda (num1 num2) (if (= num1 num2) ; If the first number and second number are the same we return false since it's needed for the prime-sieve function
                                            #f
                                            (if (eq? (modulo num1 num2) 0) ; If num1 % num2 equals 0 that means the first number is divisible by the second number
                                              #t
                                              #f
                                            ) 
                                          ) 
                                       )) 


; Part 3 – Adding some curry to our math
(define not-divisible-by (lambda (divisibleNum)
                            (lambda (num1) (not (divisible-by? num1 divisibleNum) ) ) )) ; This function will take the divisible number and create a function that will take a number
                                                                                         ; that will check if that number is NOT divisible by the divisibleNum


; Part 4 – Writing a simple filter-list function                   
(define filter-list (lambda (funct myList) (if (null? myList)  ; Base Case: Once the list is empty that means we went through the entire list
                                             '()               ; and will return an empty list that will be used to start appending our recursive cases
                                             (if (funct (car myList) )
                                               (append (list (car myList) ) (filter-list funct (cdr myList) ) ) ; Recursive Cases: If the function returns true for the first item in the current list then append that item 
                                               (filter-list funct (cdr myList) )                                ; while recursively calling the function and cdr the list. If false just cdr the list and recursively call the function
                                             ) 
                                           ) 
                                         )) 


; Part 5 - Writing the Simplified Sieve
(define prime-sieve (lambda (maxNum) (prime-sieve-helper (make-2-n-list maxNum) maxNum 2) )) ; Interface that will give the helper function a list from 2 - maxNum, the maxNum and 2 (that will be our starter divisible number)

(define prime-sieve-helper (lambda (primeList maxNum divisibleNum) (if (> divisibleNum (sqrt maxNum) ) ; Base Case: Once the divisible number is greater than the square root of the maxNum that means we have reached our final recursive iteration
                                                                        (filter-list (not-divisible-by divisibleNum) primeList) ; This will return our completed list
                                                                        (prime-sieve-helper (filter-list (not-divisible-by divisibleNum) primeList) ; Recursive Case: Recursively call the function with a list that is filtered with the current divisibleNum, 
                                                                                             maxNum (+ divisibleNum 1) )                            ; the maxNum (never changes), and adding one to the divisibleNum
                                                                   ) 
                                                                 ))
