# README.md
# general template
class HotelItem :
    def __init__(self,name ,price):
       self.__name=name
       self.__price=price
    #getter
    @property
    def name (self):
        return self.__name 
    @property  
    def price (self):
        return self.__price
    #setter
    @price.setter
    def price(self,price):
        if price > 0 :
            self.__price=price
        else:
            print ("Error: Price must be greater than 0")
    #empty Method
    def display_details(self):
        pass
    def calculate_item_cost(self):
        pass
##own unique feartures
##  HotelRoom iheritance
class HotelRoom(HotelItem):
    def __init__(self, name, price,bed_size):
        super().__init__(name, price)
        self.bed_size=bed_size
    #print detals
    def display_details(self):
        print(f"Name : {self.name}")
        print(f"Price : {self.price}")
        print(f"Bed_size : {self.bed_size}")
    def calculate_item_cost(self):
        service_cost=self.price* (1+.15)
        return service_cost
##   SpaServices iheritance
class SpaServices(HotelItem):
    def __init__(self, name, price,duration):
        super().__init__(name, price)
        self.duration=duration
    #print detals
    def display_details(self):
        print(f"Name : {self.name}")
        print(f"Price : {self.price}")
        print(f"Duration in minutes : {self.duration}")
    def calculate_item_cost(self):
        service_cost=self.price* (1+.2)
        return service_cost
#smart behavior 
class CustomerReservation :
    def __init__(self):
        self.booked_items=[]
    #add services in the bill
    def add_items(self,item):
        self.booked_items.append(item)
        print(f"{item.name} is booked ")
    #print Bill
    def printBill(self):
        total=0
        for item in self.booked_items:
            cost = item.calculate_item_cost()
            print(f"{item.name} : {cost :.2f}")
            total+=cost
        print("_"*20)
        print(f"total price is {total}")
# Objects
room1 = HotelRoom("Single Room", 100, "Single")
room2 = HotelRoom("Duble Room", 200, "King")
room3 = HotelRoom("suite", 200, "Queen")
spa1 = SpaServices("Spa", 80, 60)
spa2 = SpaServices("Massage", 120, 90)
# Store all hotel items
hotel_items = [room1, room2,room3, spa1, spa2]
#reservation object
reservation = CustomerReservation()
while True:
    print("===== HOTEL MENU =====")
    print("1. View Hotel Offerings")
    print("2. Add To Reservation")
    print("3. Print Final Bill")
    print("4. Exit")
    choice = input("Enter your choice : ")
    # View offerings
    if choice == "1":
        for item in hotel_items:
            item.display_details()
    # Add reservation
    elif choice == "2":
        item_name = input("Enter item name : ")
        found = False
        for item in hotel_items:
            if item.name.lower() == item_name.lower():
                reservation.add_items(item)
                found = True
        if not found:
            print("Item not found")
    # Print bill
    elif choice == "3":
        reservation.printBill()
    # Exit
    elif choice == "4":
        print("Thank you!")
        break
    else:
        print("Invalid choice")            

    
