* Used for GUI
* Build in package 
* Everything is a widget in it 

# Hello.py
```python
from tkinter import *  #import everything 

root = Tk()

# Creating a Label Widget
myLabel = Label(root, text="Hello World!") #always create root widget first

# Shoving it onto the screen
myLabel.pack() # pack used to pack stuff in the GUI

root.mainloop() # on your screen your text is always looping in
```

# Grid.py 
POSITION USING TKINTER GRID SYSTEM (grid.py)
In grid system the output is relative to the first one if you do column 5 for label2 it will still be on colum 2 if there are 2 labels 
If you want  on column 5 you can just put label 2,3,4 as " "  

```python
from tkinter import *

root = Tk()

# Creating a Label Widget
myLabel1 = Label(root, text="Hello World!").grid(row=0, column=0)
myLabel2 = Label(root, text="LOLOL").grid(row=1, column=5)
# Shoving it onto the screen

#myLabel1.grid(row=0, column=0)
#myLabel2.grid(row=1, column=5)

root.mainloop()
```

# Buttons

For size do :
Padx=50, pady=20
Colour: fg="red"

```python
from tkinter import *

root = Tk()

def myClick():
	myLabel = Label(root, text="Look! I clicked a Button!!")
	myLabel.pack()

myButton = Button(root, text="Click Me!", command=myClick,padx=50,pady=50) #State =disabled ( turns button gray)
#myButton = Button(root, text="Click Me!", command=myClick,padx=30,pady=30,fg='green',bg='red')
myButton.pack()

root.mainloop()
```

# Entry.py
To get a txt box
```python
from tkinter import *

root = Tk()

e = Entry(root, width=50, font=('arial', 24)) #Borderwidth=5
e.pack()
e.insert(0, "Enter Your Name: ")

def myClick():
	hello = "Hello " + e.get()
	myLabel = Label(root, text=hello)
	e.delete(0, 'end')
	myLabel.pack()

myButton = Button(root, text="Enter Your Stock Quote", command=myClick)
myButton.pack()

root.mainloop()
```

# Calculator
```python 
from tkinter import *

root = Tk()
root.title("ILYAS Calculator")

e = Entry(root, width=35, borderwidth=5)
e.grid(row=0, column=0, columnspan=3, padx=10, pady=10)


# e.insert(0, "")

def button_click(number):
    # e.delete(0, END)
    current = e.get()
    e.delete(0, END)
    e.insert(0, str(current) + str(number))


def button_clear():
    e.delete(0, END)


def button_add():
    first_number = e.get()
    global f_num
    global math
    math = "addition"
    f_num = int(first_number)
    e.delete(0, END)


def button_equal():
    second_number = e.get()
    e.delete(0, END)

    if math == "addition":
        e.insert(0, f_num + int(second_number))

    if math == "subtraction":
        e.insert(0, f_num - int(second_number))

    if math == "multiplication":
        e.insert(0, f_num * int(second_number))

    if math == "division":
        e.insert(0, f_num / int(second_number))


def button_subtract():
    first_number = e.get()
    global f_num
    global math
    math = "subtraction"
    f_num = int(first_number)
    e.delete(0, END)


def button_multiply():
    first_number = e.get()
    global f_num
    global math
    math = "multiplication"
    f_num = int(first_number)
    e.delete(0, END)


def button_divide():
    first_number = e.get()
    global f_num
    global math
    math = "division"
    f_num = int(first_number)
    e.delete(0, END)


# Define Buttons

button_1 = Button(root, text="1", padx=40, pady=20, command=lambda: button_click(1))
button_2 = Button(root, text="2", padx=40, pady=20, command=lambda: button_click(2))
button_3 = Button(root, text="3", padx=40, pady=20, command=lambda: button_click(3))
button_4 = Button(root, text="4", padx=40, pady=20, command=lambda: button_click(4))
button_5 = Button(root, text="5", padx=40, pady=20, command=lambda: button_click(5))
button_6 = Button(root, text="6", padx=40, pady=20, command=lambda: button_click(6))
button_7 = Button(root, text="7", padx=40, pady=20, command=lambda: button_click(7))
button_8 = Button(root, text="8", padx=40, pady=20, command=lambda: button_click(8))
button_9 = Button(root, text="9", padx=40, pady=20, command=lambda: button_click(9))
button_0 = Button(root, text="0", padx=40, pady=20, command=lambda: button_click(0))
button_add = Button(root, text="+", padx=39, pady=20, command=button_add)
button_equal = Button(root, text="=", padx=91, pady=20, command=button_equal)
button_clear = Button(root, text="Clear", padx=79, pady=20, command=button_clear)

button_subtract = Button(root, text="-", padx=41, pady=20, command=button_subtract)
button_multiply = Button(root, text="*", padx=40, pady=20, command=button_multiply)
button_divide = Button(root, text="/", padx=41, pady=20, command=button_divide)

# Put the buttons on the screen

button_1.grid(row=3, column=0)
button_2.grid(row=3, column=1)
button_3.grid(row=3, column=2)

button_4.grid(row=2, column=0)
button_5.grid(row=2, column=1)
button_6.grid(row=2, column=2)

button_7.grid(row=1, column=0)
button_8.grid(row=1, column=1)
button_9.grid(row=1, column=2)

button_0.grid(row=4, column=0)
button_clear.grid(row=4, column=1, columnspan=2)
button_add.grid(row=5, column=0)
button_equal.grid(row=5, column=1, columnspan=2)

button_subtract.grid(row=6, column=0)
button_multiply.grid(row=6, column=1)
button_divide.grid(row=6, column=2)

root.mainloop()
```
![image](https://user-images.githubusercontent.com/102249128/196057565-08a1bddb-8c30-4d15-8cf0-426a2dddc1f5.png)
