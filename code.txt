# MawandeNcamane
# declaration of honesty and zero plagiarism
# programme has no bugs. For testing, please utilise this original format.




# Imports
import os, random

# Welcome to Terminopoly
print("Welcome to Terminopoly\n")

# Player class
class Player:
    def __init__(self,name,token):
        self.name = name
        self.token = token
        self.location = 0
        self.money = 500 # currency: wtc
        self.properties = {}
        self.sentence = 0
        self.cards = ["Get our of jail free card"]
    
    def rollDie(self):
        return random.randint(1, 6)
        
    def bankruptCheck(self):
        if self.money == 0:
            print("You are now bankrupt")
            players.remove(self)
        
        
    def pay(self, other, location, amount = None):
        if location != None:
            payment = min(self.money, other.properties[location])
        if amount != None:
            payment = min(self.money, amount)
            
        self.money -= payment
        other.money += payment
        print("You payed {} wtc{}".format(other.name, payment))
        
        self.bankruptCheck()
    
    def pickChance(self):
        chanceCard = chanceCards.pop(0) # Take first card
        
        input("Press Enter to read card...")
        print(chanceCard)
        
        if chanceCard == "Get our of jail free card":
            self.cards.append(chanceCard)
            print("You now keep that card")
            return
        if chanceCard == "Advance to Begin":
            self.location = 0
            print("Collect wtc200")
            self.money += 200
            
        if chanceCard == "Go back 3 spaces":
            self.location = (self.location - 3 + len(board)) % board
            return
        
        if chanceCard == "Pay poor tax of wtc15":
            self.money -= min(self.money, 15)
            bankruptCheck()
            return
            
        if chanceCard == "Bank pays you dividend of wtc50":
            self.money += 50
            return
        
        if chanceCard == "Go directly to jail":
            self.goToJail()
            return
            
        if chanceCard == "You have been elected chairman of the board. Pay each player wtc50":
            others = len(players) - 1
            payment = min(self.money, 50 * others) // others
            
            for other in players:
                if other != self:
                    self.pay(other, None, payment)
                    
            bankruptCheck()
            return
            
        if chanceCard == "Advance to Free Parking":
            self.location = board.index("Free Parking")
            return
        
    
    def pickCommunity(self):
        
        communityCard = communityCards.pop(0) # Take first card
        input("Press Enter to read card...")
        
        print(communityCard)
        
        if communityCard == "Pay school tax of wtc150":
            self.money -= min(self.money, 150)
            bankruptCheck()
            return
        
        if communityCard == "You win 2nd place in a beauty contest. Collect wtc50.":
            self.money += 50
            return
            
        if communityCard == "You inherit wtc100":
            self.money += 100
            return
            
        if communityCard == "Pay hospital wtc100":
            self.money -= min(self.money, 100)
            bankruptCheck()
            return
        
        if communityCard == "Go directly to jail":
            self.goToJail()
            return            
            
        if communityCard == "Advance to Begin":
            self.location = 0
            print("Collect wtc200")
            self.money += 200
            return 
        
        if communityCard == "Bank error in your favour - collect wtc200":
            self.money += 200
            return            
        
        if communityCard == "Get our of jail free card":
            self.cards.append(chanceCard)
            print("You now keep that card")
            return
        
    def goToJail(self):
        self.location = board.index("Jail")
        self.sentence = 3
        print("You are now in jail for 3 turns.")
        
    def rollInJail(self):
        input("Press Enter to roll...")
        roll = player.rollDie()
        print("You rolled a", str(roll)+".")
        
        if roll == 6:
            self.sentence = 0
            print("You get to leave")
        else:
            self.sentence -= 1
            if self.sentence == 0:
                amount = min(player.money, 50)
                self.money -= amount
                print("You paid a fine of wtc{}.".format(amount))
                
                print("You get to leave")
                self.bankruptCheck()

    def buyOrPass(self, location): 
        locationIndex = board.index(location)
        
        print("No one owns this place.")
        
        buyOrPass = input("Buy or pass? (b/p)")
        while buyOrPass not in ["b", "p"]:
            print("Please enter a valid response")
            buyOrPass = input("Buy or pass? (b/p)")
            
        if buyOrPass == "b":
            price = boardPrices[locationIndex]
            print("This place costs wtc{}.".format(price))
            if self.money <= price:
                print("You cannot afford this place")
            else:
                confirm = input("Are you sure? (y/n)")
                while confirm not in ['y', 'n']:
                    print("Please enter a valid response")
                    confirm = input("Are you sure? (y/n)")
                
                if confirm == 'y':
                    self.money -= price
                    self.properties[newLocation] = boardRents[locationIndex]
                    print("Congrads, you bought", location + "!")
                else:
                    print("You chose to pass.")
    
    
# Get your players
players = []
tokens = ['@','#','$','%']

numPlayers = int(input("How many are playing? (2 - 4 players): "))

while numPlayers not in range(2, 5):
    print("Only 2 to 4 players allowed.")
    numPlayers = int(input("How many are playing? (2 - 4 players): "))

for n in range(numPlayers):
    # Get player's name
    name = input("Player {} name: ".format(n+1))

    # Get player's token
    token = input("Choose token: (" + " ".join(tokens) + ") ")
    while token not in tokens:
        print("Please choose a valid token")
        token = input("Choose token: (" + " ".join(tokens) + ") ")
    tokens.remove(token)

    # Add a new player
    players.append(Player(name, token))
    
print("Everyone gets wtc500 to start off! Good luck.")
    
# Ready
print("Ready?")
input("Press Enter to continue...")

# Clear the terminal
os.system("clear")

# Let's get started
print("Let's get started")

# Create board
board = [
    'Begin',
    'Python hotel',
    'Chance',
    'OOP-sy B&B',
    'Jail',
    'CSS Heights',
    'Community Chest',
    'JS Inn',
    'Free Parking',
    'Memory Space',
    'Chance',
    'RAM house',
    'Go to Jail',
    'Cache de Cookie',
    'Community Chest',
    'ROM-ance Inn'
]

boardPrices = [0, 50, 0, 60, 0, 90, 0, 100, 0, 130, 0, 140, 0, 180, 0, 200]
boardRents = [int(price * 0.15) for price in boardPrices]

# # Function to show board
# def showBoard():
#     #THIS CODE IS SUBJECT TO CHANGE
#     print("<BOARD GOES HERE>")
    
# Chance cards
chanceCards = [
    "Get our of jail free card",
    "Advance to Begin",
    "Go back 3 spaces",
    "Pay poor tax of wtc15",
    "Bank pays you dividend of wtc50",
    "Go directly to jail",
    "You have been elected chairman of the board. Pay each player wtc50",
    "Advance to Free Parking"
]

# Community chest cards
communityCards = [
    "Pay school tax of wtc150",
    "You win 2nd place in a beauty contest. Collect wtc50.",
    "You inherit wtc100",
    "Pay hospital wtc100",
    "Go directly to jail",
    "Advance to Begin",
    "Bank error in your favour - collect wtc200",
    "Get our of jail free card"
]

# Shuffle cards
random.shuffle(chanceCards)
random.shuffle(communityCards)


# Game loop
playing = True
turn = 0
while playing:
    
    # Player turn
    player = players[turn]
    print(player.name, "is playing.")
    
    # Check if in jail
    if player.sentence > 0:
        print("You are in jail.")
        if len(player.cards) != 0:
            useCard = input("Use your get out jail free card? (y/n) ")
            while useCard not in "yn":
                print("Please enter a valid response")
                useCard = input("Use your get out jail free card? (y/n) ")
                
            if useCard == "y":
                player.sentence = 0
                communityCards.append(player.cards.pop(0)) # Put card back in deck
                print("You get to leave. Hooray!")
            else:
                player.rollInJail()
                    
        else:
            player.rollInJail()
    else:
        # Player choices
        print("What do you want to do?")
        print("1 - Roll")
        print("2 - Check balance")
        print("3 - Check properties")
        print("4 - Check current location")
        print("0 - Quit game")
        
        choice = ""
     
        while choice != "1" or choice != "0":
    
    	    choice = input("")
    	    while choice not in "12340":
    		    print("Please enter a valid response")        
    		    choice = input("")
    
    	    if choice == "1":
    	        
        		roll = player.rollDie()
        		print("You rolled a", str(roll)+".")
        		break
        		
    	    elif choice == "2":
    	        
        		print("You have wtc{}.".format(player.money))
        		
    	    elif choice == "3":
                if len(player.properties) > 0:
                    print("You own the following: ")
                    print(", ".join([property_ for property_ in player.properties]))
                else:
                    print("You don't own anything.")
        		
    	    elif choice == "4":
        		print("You are at", board[player.location])
    	    elif choice == "0":
        		print("You chose to quit. Good bye!")
        		break
    
        if choice == "0":
        	playing = False	
        	break
    
        # Update location
        previous = player.location
        player.location = (player.location + roll) % len(board)
        # Passing BEGIN
        if player.location - previous < 0:
            print("You passed BEGIN and received wtc200")
            player.money += 200
            
        # New location
        newLocation = board[player.location]
        print("You landed on", newLocation + ".")
        
        # Pay, buy or pass, take chance/community chest or go to jail
        owned = False
        for other in players:
            if newLocation in other.properties:
                if other == player:
                    print("You already own this place.")
                else:
                    player.pay(other, newLocation)
                owned = True
                break
        if not owned:
            if newLocation in ["Begin", "Free Parking", "Jail"]:
                pass
            elif newLocation == "Chance":
                player.pickChance()
            elif newLocation == "Community Chest":
                player.pickCommunity()
            elif newLocation == "Go to Jail":
                player.goToJail()
            else:
                player.buyOrPass(newLocation)
    
    end = "_"
    end = input("Press Enter to end turn...")
    if end == "":
        os.system("clear")
    
    # Change turn
    if roll != 6:
        turn = (turn + 1) % len(players)
        
    # End Game
    if len(players) == 1:
        print(players[0].name, "wins the game!")

