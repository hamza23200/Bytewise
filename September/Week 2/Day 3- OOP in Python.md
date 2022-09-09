## Use:
It is used to represent complex data in our codes. Some other ways inorder to represent data  Jason , XML

## Examples of classes:
Classes are structure with attributes like Customer class with two attributes 
*name 
*membership type 

Now this customer class can have two objects 
* Caleb Gold 
* Brad Bronze

``` python
class Customer:
    def __init__(self,name,membership):
        self.name = name  # first name is for class and the 2nd is for variable
        self.membership = membership
        print(" Valued Customer: ")

c = Customer("Caleb" , "Gold")
print(c.name,c.membership)

c2 = Customer("Brad" , "Premium")
print(c2.name,c2.membership)
```
### Better version of code
```python
class Customer:
    def __init__(self,name,membership):
        self.name = name
        self.membership = membership
        
customer = [Customer("Caleb","Gold"),Customer("Brad","Premium")]
print(customer[0].name, customer[0].membership)
```

## Methods 

init() method: Also known as initializer or constructor Initializer is a method or section code whenever we create a new class in python

Example:
Customer() init(self,anything extra e.g name,membership etc)

Difference between Parameters and Arguments
* Parameters are variables attached to the method we are creating e.g name, membership are parameters 
* Argumets are values assigned to the parameters e.g Customer("Caleb","Gold") ,here Caleb and Gold are arguments assigned to membership

Note:
Parameters are definition while Arguments are invocation .
* upgrade_membership(self,new-membership) e.g c.upgrade_membership("Bronze")  self.membership = new-membership

```python
class Customer:
    def __init__(self,name,membership_type):
        self.name = name
        self.membership_type = membership_type

    def update_membership(self,new_membership):
        self.membership_type = new_membership

    def __str__(self):   # to activate this print(customer[0])
        return self.name + " " + self.membership_type

    def print_all_customers(self):  #print all customers 
        for customers in customer:
           print(customer)

    def __eq__(self, other): #same ccustomers
        if self.name == other.name and self.membership_type == other.membership_type:
            return  True
    __repr__== __str___

        return  False
customer = Customer("Caleb","Gold"), Customer("Brad","Bronze")
print(customer[0].membership_type,customer[1].membership_type)        # Gold Bronze
print(customer[1].membership_type) # old type of membership
customer[1].update_membership("Platinum")  # new type of membership mantained
print(customer[1].membership_type) # display of new membership
print(customer[0] == customer[1])  # checking if first customer and second customer's attribute is same or not
```

3 Principles of OOP: 📚
* Encapsulation 
* Inheritance 
* Polymorphism

if you dont need it dont try to do it , code will get more complicated 

Encapsulation:
Hiding the inner details of class or certain data and we only need to expose what is neeeded for user of class to use that class Methods to get access of data: 
* getter 
* setter 
*Specific way to do Encapsulation in python is **Property** We can add in the property and nothing is changed.

Inheritance:
Allows to provide certain attributes to objects from base class e.g User base class has two derived classes  Customer & Teacher

Polymorphism:
* Kind of just extra step of inheritance where we can treat customers and teachers as same thing if we approach them as Users.
* Ability to create code that works with general users but is fully functional when you pass somethinng more specific e.g a teacher or a customer
```python
@property
def name(self):
 return self._name #name is private
 
 @name.setter
 def(self,name):
 self._name=name
 ```
 
 ```python
class User:
    def log(self):
        print(self)   #inheritance code

class Teacher(User):  #polymorphism
    def log(self):
        print("I m a teacher")

class Customer(User):
    def __init__(self,name,membership_type):
        self.name = name
        self.membership_type = membership_type

        @property
        def name(self):                       # Getter function
            print("Getting name")
            return self._name

        @name.setter
        def name(self,name):                  # Setter function
            print("Setting name")
            self._name = name

    def update_membership(self,new_membership):
        self.membership_type = new_membership

    def __str__(self):
        return self.name + " " + self.membership_type

    def print_all_customers(self):
        for customers in customer:
           print(customer)

    def __eq__(self, other):
        if self.name == other.name and self.membership_type == other.membership_type:
            return  True

        return  False

    __hash__ = None
    __repr__ = __str__
users = [Customer("K","Gold"), Customer("O","Luxury"), Teacher()]
for user in users:
    user.log()
    ```



























