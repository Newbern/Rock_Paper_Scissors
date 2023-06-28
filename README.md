#Paper, Rock, Scissors
##Modules:
###Python

- pygame
- random
- time
## Mouse Controls
```bash
import pygame
mx, my = pygame.mouse.get_pos()
pygame.mouse.get_pressed()[0: Left button// 1: Middle button// 2: Right button]
if mx >= 400:
  if pygame.mouse.get_pressed()[0]:
    print("Hello,World!")
```
## Pygame Basic Setup
```bash
import pygame
pygame.init()

# Display Size
screen_w = 800
screen_h = 400
screen = pygame.display.set_mode((screen_w, screen_h))

# Title Screen // Icon
pygame.display.set_caption("Paper Rock Scissors")
icon = pygame.image.load("Hands/Rock.png")
icon = pygame.transform.scale(icon, (32,32))
pygame.display.set_icon(icon)

# Clock/fps
Clock = pygame.time.Clock()


loop = True
while loop:
    # fill in with Black
    screen.fill((0, 0, 0))
    
    # events pressed
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            loop = False
            break
            
            
    # update and flip images
    Clock.tick(60)
    pygame.display.flip()
    pygame.display.update()
pygame.quit()
```
This game is a Rock, Paper, Scissors game against you and the bot
it choese which hand to draw by this python class
```bash
# Computer
class Computer:
    def __init__(self, x, y):
        # Most of this function gets filled throughout the program
        self.who = self.img = self.rect = None
        self.hands = ["Rock", "Paper", "Scissors"]
        self.x = x
        self.y = y

        # Goes to the self.new_hand() program but when using the draw() function it gets reset each time
        self.new_hand()

    def new_hand(self):
        # Randomly chooses which hand in the self.hands list
        self.who = random.choice(self.hands)

        # Loads in the self.who image and then transforms it to scale // gets rect of image
        img = pygame.image.load(f"Hands/{self.who}.png")
        self.img = pygame.transform.scale(img, (100, 150))
        self.rect = self.img.get_rect()

    def draw(self):
        # this goes back and picks a random hand to be used and then draws it
        self.new_hand()
        screen.blit(self.img, (self.x, self.y))
        
#then when draw it shows which one was randomly picked
Bot = Computer(150,200)
Bot.draw()
```
then it needs to draw the boxes in order for the ``Player`` to pick
```bash
def hand():
    # lambda creates a smaller like function to run this program to draw it // Shortcut to drawing it
    cho = lambda x, y, img: screen.blit(pygame.image.load(img), (x, y))

    # Draws the hands in different locations
    cho(150, 100, "Hands/Rock.png")
    cho(350, 100, "Hands/Paper.png")
    cho(550, 100, "Hands/Scissors.png")

    # Gets the mouse position for x and y
    mx, my = pygame.mouse.get_pos()
    # this boxes in the chooses before you click on an answer
    if my >= 100:
        if my <= 250:
            # BOX 1
            if mx >= 150:
                if mx <= 150 + 87:
                    # this is 1 of 3 buttons to be pressed on the mouse
                    if pygame.mouse.get_pressed()[0]:
                        # returns str: "Rock"
                        return "Rock"
            # BOX 2
            if mx >= 350:
                if mx <= 350 + 105:
                    if pygame.mouse.get_pressed()[0]:
                        # returns str: "Paper"
                        return "Paper"
            # BOX 3
            if mx >= 550:
                if mx <= 550 + 77:
                    if pygame.mouse.get_pressed()[0]:
                        # return str: "Scissors"
                        return "Scissors"
    else:
        pass

# This Draws all the Box's but returns the Players input
```
So once both have picked there hand the only thing lift to do is decide who wins.
```bash
# this is how to tell if you win or not in this game
def rules():
    # Player checks : Rock, Scissors, then Bot
    if Player == "Paper":
        if Bot.who == "Rock":
            text("YOU WIN!")
        if Bot.who == "Scissors":
            text("YOU LOSE! :(")
        if Player == Bot.who:
            text("OOPS! TIED!")

    # Player checks : Paper, Rock, then Bot
    if Player == "Scissors":
        if Bot.who == "Paper":
            text("YOU WIN!")
        if Bot.who == "Rock":
            text("YOU LOSE! :(")
        if Player == Bot.who:
            text("OOPS! TIED!")

    # Player checks : Paper, Scissors, then Bot
    if Player == "Rock":
        if Bot.who == "Scissors":
            text("YOU WIN!")
        if Bot.who == "Paper":
            text("YOU LOSE! :(")
        if Player == Bot.who:
            text("OOPS! TIED!")
```
and just to finish with a bow on top it tells if you have won the game or not in red
```bash
def text(speak):
    # font: picks the font you want and size // txt: Grabs the text and colors it in // Draws txt on screen
    font = pygame.font.SysFont("cambria", 36)
    txt = font.render(speak, True, (255, 0, 0))
    screen.blit(txt, (325, 275))
```
also a tip if you want to know which font to use you can print all the fonts like so:
```bash
import pygame
font = pygame.font.get_fonts()
for f in font():
    print(f)
```