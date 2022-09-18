### Curses library used to manipulate something inside the screen

# Code
```python
import curses
from random import randint
#setup window
curses.initscr()
win=curses.newwin(20,60,0,0) #lines,colums, coordinates(y,x)
win.keypad(1) #arrow key
curses.noecho() #not to listen to any input charac
curses.curs_set(0) #hide cursor
win.border(0) #draw border
win.nodelay(1)#-1    #not waiting for next user input


#snake & food  #data strucire
snake=[(4,10),(4,9),(4,8)] #tuple made () bcz the value doesnt change  
#starting coordinate

food=(10,20)   
# in game logic call 
#for c in snake:
#  win.addch(c[0],c[1],"*")  makes a snake
#winaddch(food[0],food[1], "#") creates food

#game logic
win.addch(food[0],food[1],'#') #next input 
score=0
ESC=27 #Asci code
key=curses.KEY_RIGHT #snake moving right

while key!=ESC:
    win.addstr(0,2,'Score'+str(score)+' ') # at string to line 0 colum 2
    win.timeout(150-(len(snake))//5 + len(snake)//10%120)  #increase speed 
    
    prev_key=key
    event=win.getch()
    key= event if event!=-1 else prev_key  #countinue in same direction
    if key not in [curses.KEY_RIGHT,curses.KEY_LEFT,curses.KEY_UP,curses.KEY_DOWN,ESC]: #if noot arrow key,esc then it will keep going right
        key=prev_key
        
    #calculate the next coordinates
    y=snake[0][0] #get (4,10)
    x=snake[0][1]
    if key==curses.KEY_DOWN:
        y+=1  
    if key==curses.KEY_UP:
        y-=1       
    if key==curses.KEY_LEFT:
        x-=1 
    if key==curses.KEY_RIGHT:
        x+=1 
        
    snake.insert(0,(y,x))  #updating coordinates  
    
    
    #check if we hit the border
    if y==0:break
    if y==19:break
    if x==0:break
    if x==59:break
    
    #if snake run over itself
    if snake[0] in snake[1:]:break
    
    if snake[0]==food:
        #eat the food
        score+=1
        
        food=()
        while food==():
            food=(randint(1,18),randint(1,58)) #genertaing food at random
            if food in snake: #not place food in snake
                food=()
            win.addch(food[0],food[1],'#')   
            
    else:
        #move snake
        last=snake.pop()
        win.addch(last[0],last[1],' ')
    
    win.addch(snake[0][0],snake[0][1],'*')    

curses.endwin()  #destroys window
print(f"Final Score={score}") 
