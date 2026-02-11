# Scheme

## Scheme is a Dialect of Lisp

## Scheme Fundamentals

![image-20241123195938511](../assets/cs61a/image-20241123195938511.png)

```scheme
scm> 2
2
scm> (+ 1 2 3 4)
10
scm> (+)
0
scm> (*)
1
scm> (* 1 2 3 4)
24
scm> (number? 3)
#t
scm> (number? +)
#f
scm> (integer? )
scm> (zero? )
```

## Special Forms

![image-20241123200723904](../assets/cs61a/image-20241123200723904.png)

```scheme
(define (square x) (* x x))

(define (average x y)
  (/ (+ x y) 2))

(define (sqrt x)
  (define (update guess)
    (if (= (square guess) x)
        guess
        (update (average guess (/ x guess)))))
  (update 1))

```

## Lambda Expressions

![image-20241123202116890](../assets/cs61a/image-20241123202116890.png)

```scheme
(define (line) (fd 50))
(define (twice fn) (fn) (fn))
(define (repeat k fn)
  (fn)
  (if (> k 1) (repeat (- k 1) fn)))
(define (tri fn)
  (repeat 3 (lambda () (fn) (lt 120))))
(define (sier d k)
  (tri (labmda () (if (= d 1) (fd k) (leg d k)))))
(define (leg d k)
  (sier (- d 1) (/ k 2))
  (penup) (fd k) (pendown))
```

## Cond & Begin

![image-20241123205330110](../assets/cs61a/image-20241123205330110.png)

while using cond, the 'else' can be omitted, and if you want to use it ,you can put a single one at last

## Let Expression

![image-20241123205942693](../assets/cs61a/image-20241123205942693.png)

## Scheme Lists -- Linked Lists

![image-20241123210341767](../assets/cs61a/image-20241123210341767.png)

```scheme
> (define s (cons 1 (cons 2 nil)))
> s
(1 2)
> (cons (cons 4 (cons 3 nil)) s)
((4 3) 1 2)
> (cons s (cons s nil))
((1 2) (1 2))
> (list? s)
#t
> (list? nil)
#t
> (null? nil)
#t
> (null? s)
#f
> (list 1 2 3 4)
(1 2 3 4)
```

## Symbolic Programming

![image-20241123212530921](../assets/cs61a/image-20241123212530921.png)

## A Scheme Expression is a Scheme List

![image-20241123213143596](../assets/cs61a/image-20241123213143596.png)

```scheme
(define (fact n)
  (if (= n 1) 1 (* n (fact (- n 1)))))
(define (fact-exp n)
  (if (= n 1) 1 (list '* n (fact-exp (- n 1)))))
(define (fib n)
  (if (<= n 1) n (+ (fib (- n 1)) (fib (- n 2)))))
(define (fib-exp n)
  (if (<= n 1) n (list '+ (fib-exp (- n 1)) (fib-exp (- n 2)))))
```

## Quasiquotation

![image-20241123215415679](../assets/cs61a/image-20241123215415679.png)

## Example: While Statements

![image-20241123215749912](../assets/cs61a/image-20241123215749912.png)

```scheme
(define (sum-while initial-x condition add-to-initial update-x)
  (begin
   (define (f x total)
     (if ,condition
         (f ,update-x (+ total ,add-to-total))
         total))
   (f ,initial-x 0)))
```

