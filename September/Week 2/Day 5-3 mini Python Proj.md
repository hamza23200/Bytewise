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

# Rock,Paper , Scissor

```python
import random

user_wins = 0
computer_wins = 0

options = ["rock", "paper", "scissors"]

while True:
    user_input = input("Type Rock/Paper/Scissors or Q to quit: ").lower()
    if user_input == "q":
        break

    if user_input not in options:
        continue

    random_number = random.randint(0, 2)
    # rock:0, paper:1, scissors:2
    computer_pick = options[random_number]
    print("computer picked", computer_pick + ".")

    if user_input == "rock" and computer_pick == "scissors":
        print("You Won! ")
        user_wins += 1

    elif user_input == "paper" and computer_pick == "rock":
        print("You Won!")
        user_wins += 1

    elif user_input == "scissors" and computer_pick == "paper":
        print("You Won!")
        user_wins += 1

    else:
        print("You lost!")
        computer_wins += 1

print("You Won", user_wins, "times.")
print("The Computer Won", computer_wins, "times.")
print("Goodbye!")
```

# Create your own adventure
```python
name = input("Type your name: ")
print("welcome", name, "to this adventure!")

answer = input("You are on a dirt road, it has come to an end and you can go left or right. Which way would you like to go? ").lower()

if answer == "left":
    answer = input("You come to a river, you can walk around it or swim across? Type walk to walk around and swim to swim across: ")

    if answer == "swim":
        print("You swam across and were eaten by an alligator.")
    elif answer == "walk":
        print("You walked for many miles, ran out of water and you lost the game.")
    else:
        print("Not a valid option. You lose.")

elif answer == "right":
    answer = input("You come to a bridge, it looks wobbly,do you want to cross it or head back (cross/back)? ")

    if answer == "back":
        print("You go back and lose.")
    elif answer == "cross":
        answer = input("You cross the bridge and meet a stranger. Do you talk to?")

        if answer == "Yes":
            print("You talk to the stranger and they give you gold. You Win!")

        elif answer == "No":
            print("You ignore the stranger and they are offended and you lose.")
    else:
        print("Not a valid option. You lose.")

#elif answer == "right":
    #answer = input("You come to a bridge, it looks wobbly,do you want to cross it or head back (cross/back)? ")

else:
    print("Not a valid option. You lose.")

print("ThankYou for trying", name)
```

# Password Manager 
```python
from cryptography.fernet import Fernet

def load_key():
    file = open("key.key", "rb")
    key = file.read()
    file.close()
    return key


key = load_key()
fer = Fernet(key)


def view():
    with open('passwords.txt', 'r') as f:
        for line in f.readlines():
            data = line.rstrip()
            user, passw = data.split("|")
            print("User:", user, "| Password:",
                  fer.decrypt(passw.encode()).decode())


def add():
    name = input('Account Name: ')
    pwd = input("Password: ")

    with open('passwords.txt', 'a') as f:
        f.write(name + "|" + fer.encrypt(pwd.encode()).decode() + "\n")


while True:
    mode = input("Would you like to add a new password or view existing ones (view, add), press q to quit? ").lower()
    if mode == "q":
        break

    if mode == "view":
        view()
    elif mode == "add":
        add()
    else:
        print("Invalid mode.")
        continue
        ```
