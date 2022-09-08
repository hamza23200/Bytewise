# Python

## input

```python
animal = input("animal ")
print("Cute " + animal) #concatenation
```

## Type conversion
Sometimes we need to change datatypes i.e int, strings etc . .Example: #wrong code:

```python 
birth_year = input("Dear customer Enter your birthyear ")
age = 2022 - int(birth_year)
print("Your Age is " + age)
```

## Strings:
strings are like real world objects e.g you can capitalize, lower, find and append our code to desired thinking
```python
course = 'Python for beginners'
print(course.upper())
course = 'Python for beginners'
print(course.lower())
course = 'Python for beginners'
print(course.find('y'))
course = 'Python for beginners'
print('Python' in course)
course = 'Python for beginners'
print(course.replace('for','4'))
```

## Arithmetic operators in Python:
* Addition 
* Subtraction 
* Multiplication 
* Division (float)
* Division (int) 
* Remainder % 
* Power of **

# Arithmetic operations in code
```python
print(10 + 2) # Addition
print(10 - 3) # Subtraction
print(10 * 2) # Multi*plication
print(10 / 2) # Division float
print(10 // 2) # Division int
print(10 % 2) # Remainder
print(10 ** 3) # Raise to the power of
```

## Comparison Operators
>=,<,<+,==,!=

x = 10
print(x < 20 and x > 23) # Logic AND falso
print(x < 20 or x > 23) # Logic OR true


```python
weight = float(input("Enter your weight in Kg or Lb "))
typy = input(" K or L? ")
if typy.upper() == 'K' :
    print("Weight in lbs")
    print(weight / 0.45)
elif typy.lower() == 'L' :
    print("Weight in Kg")
    print(weight * 0.45)
else:
    print("Enter correct weight")
print("END")
```

## while loop
i = 1
while i <=5:
    print(i*'*')
    i = i + 1  #give triangle
    
```python
shareholders = ["A", "B", "C", "D"]
print(shareholders[0]) #A
print(shareholders) #full list
print(shareholders[0:3]) #ABC
```
## For loop
```python
numbers = [1,2,3,4,5,6,7]
for item in  numbers:
    print(item)

    i=0
    while i < len(numbers):
        print(numbers[i])
        i = i + 1
```

## Tuples
Tuples are like lists used to store sequence of objects but they cannot be changed
```python
numbers = (1,2,3)
numbers.count(3)
numbers.index(2)
```















