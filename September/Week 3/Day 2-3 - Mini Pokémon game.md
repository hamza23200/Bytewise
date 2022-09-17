```python
class Pokemon:
    def __init__(self, name, primary_type, max_hp):
        self.name = name
        self.primary_type = primary_type  # water, fire, grass
        self.max_hp = max_hp
        self.hp = max_hp

    @staticmethod
    def typewheel(type1, type2): #For putting inputs
        result_map = {0 : "lose", 1 : "win", -1 : "tie"} #end results , water loses by grass
        # The mapping between moves and numbers
        game_map = {"water": 0, "fire": 1, "grass": 2} #think of it as rock paper scissor
        # Win-lose matrix
        wl_matrix = [
            [-1, 1, 0],  # water  , [-1=w vs w] [1=w vs f] [0=w vs g] 
            [0, -1, 1],  # fire
            [1, 0, -1]   # grass
        ]
        result = wl_matrix[game_map[type1]][game_map[type2]] # wl_matrix[[game_map[water][game_map[fire]] , sort of like result[0][1]=1
        return result_map[result]
    
    def feed(self):  # to call do b.feed(), self argument bcz calling class variables
        if self.hp < self.max_hp: #so that hp doesnt go beyond max
            self.hp += 1
            print(f"{self.name} recovered 1 HP.")
        else:
            print(f"{self.name} is full.")

    def battle(self, other):
        result = self.typewheel(self.primary_type, other.primary_type)
        if result == 'lose':
            self.hp = 0
            print(f"{self.name} Lost")
        elif result == 'tie':
            self.hp -= 10
            other.hp -= 10
            print(f"Battle between {self.name} and {other.name} is a tie.")
        elif result == 'win':
            other.hp = 0
            print(f"{self.name} won. ")

    def __str__(self):     #to gett ouput in string
        return f"{self.name} ({self.primary_type}): {self.hp}/{self.max_hp}"


if __name__ == "__main__":
    a = Pokemon('bulbasaur', 'grass', 100)
    b = Pokemon('charmander', 'fire', 150)
    a.battle(b) # w vs f =lose
    
    
    
