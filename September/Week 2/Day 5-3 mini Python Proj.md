# Quiz Game:
This quiz game contains 4 question. At the end it shows how much you got correct Answers and percentage


Let's Play
```python
print("Welcome to my computer quiz!")

playing = input("Do you want to play? ")

if playing.lower() != "yes":
    quit()

print("Okay! Let's play :)")
score = 0

answer = input("What does CPU stands for?")
if answer.lower() == "central processing unit":
    print("Correct!")
    score += 1
else:
    print("Incorrect!")

answer = input("What does PSU stands for?")
if answer.lower() == "power supply unit":
    print("Correct!")
    score += 1
else:
    print("Incorrect!")

answer = input("What does GPU stands for?")
if answer.lower() == "graphics processing unit":
    print("Correct!")
    score += 1
else:
    print("Incorrect!")

answer = input("What does RAM stands for?")
if answer.lower() == "random access memory":
    print("Correct!")
    score += 1
else:
    print("Incorrect!")

print("You got " + str(score) + " questions correct!")
print("You got " + str((score / 4) * 100) + "%.")
```


# Number Guessing Game
This game that will show you make a correct guess of number or not. If you make a guess then message will display either you are above the guess or below the guess. And if we enter any alphabet or negative number then message will appear Please enter a number next time.

```python
import random #random no.

top_of_range = input("Type a number: ")

if top_of_range.isdigit(): #to makesure its digit 
    top_of_range = int(top_of_range)

    if top_of_range <= 0:
        print("Please type a number larger than 0 next time.")
        quit()

else:
    print("Please type a number next time.")
    quit()

random_number = random.randint(0, top_of_range)  # if you use int the no. wil be included
guesses = 0

while True: #keep asking
    guesses += 1
    user_guess = input("Make a guess: ")
    if user_guess.isdigit():
        user_guess = int(top_of_range)
    else:
        print("Please type a number next time.😞")
        continue #countinues loop

    if user_guess == random_number:
        print("Yeah You Got it! 🥳")
        break
    else:
        if user_guess > random_number:
            print("You were above the number!")
        else:
            print("You were below the number!")

print("You got it in ", guesses, "guesses")
```
