# Questions to check your understanding

Our HOWTO documents contain quite a bit of cut-and-paste code.  
You don't have to write that code, but you do need to understand it. 
The purpose of these questions is to check your understanding as you 
work through the HOWTO.  

### 1 

Consider the following code. 
```python
five = IntConst(5)
print(5 == five)   # Comparison 1
print(five == 5)   # Comparison 2
```

Does the `__eq__` method of `IntConst` get called only in Comparison 
1, only in Comparison 2, in both, or in neither? 
__eq__ only gets called in Comparison 1 
### 2

I noted that `__str__` method of
`Plus` is recursive, but I don't see an explicit call to `__str__`. 
Where is it? 
when typing left and right, the new object will also recursively call __str__
### 3

How do we know that the `eval` method will not loop forever (i.e., 
it will eventually reach a base case)?
when 'left' or 'right' reaches a IntConst to call on, that is the base case as eval just returns its value
### 4

The constructor for a `Plus` node says that it takes two `Expr` nodes
as arguments, but we are passing it `IntConst` and `Plus` nodes.  Is 
this ok?  Why or why not? 
This is ok because IntConst and Plus are subclasses of Expr.
### 5

Method `_apply` returns an `int` rather than an `IntConst`.
How does the result of a binary operation become an
`IntConst` object? 
This is due to the eval method which returns the IntConst value of the int given from _apply.
### 6

We noted earlier that an expression like `2+(5*3)` could
be expressed algebraically (this is also called "infix" notation),
in reverse Polish notation (also called "postfix") like `2 5 3 * +`, or
in "prefix" notation like `+ 2 * 5 3` or `(+ (2 (* 5 3))`.  Which of 
these notations
have we adopted for the `__str__` methods of our `Expr` classes?
the __str__ methods have adopted infix notation
### 7 

Our postfix notation uses "~" for negation and reserves
"-" for subtraction.  Why? Can you give an example 
postfix (reverse Polish notation) expression that
would be ambiguous if we used "-" as both a 
unary and binary operation? 
This is because ~ is unary and - is binary, this is an important distinction because if you had an expression such as 6 3 - -, it would be unclear to the program whether you were trying to subract or negate and would return an error declaring a missing operand for the expression
### 8

Suppose we wanted to add exponentiation to our calculator, so
that the RPN expression `5 2 ^` would evaluate to 25 (5 squared)
and `5 3 ^` would evaluate to 125 (5 cubed).  Assume the lexer
returns a token `lex.TokenPat.POWER`.  What new class would I
need to add to `expr.py`, and what would it be a subclass of? 
What change would I need to make to `rpncalc.py`?
This would be a subclass of BinOp called Expo and it would take the base number and the exponent. You then need to add this into the BinOps dict within `rpncalc.py`.
