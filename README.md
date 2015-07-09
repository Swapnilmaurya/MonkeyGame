# MonkeyGame
A simple game made in Python and Pygame Module

#I am Swapnil. My Id : maurya.swapnil@gmail.com 
#This is simple "Monkey catching banana" game
# By this you can learn how to make simple game in python and pygame module 


# GAME COAD-

import pygame, sys , random
from pygame.locals import *

pygame.init()

FPS = 30
fpsClock = pygame.time.Clock()
screen = pygame.display.set_mode((500,400),0,32)
pygame.display.set_caption('monkey')
monkey = pygame.image.load('monkey.jpg').convert()
background = pygame.image.load('garden.jpg').convert()
banana = pygame.image.load('banana.jpg').convert()
coconut = pygame.image.load('coconut.jpg').convert()


RED = (255,0,0)
WHITE = (255,255,255)
Green = (0,255,0)

monkey_x = 100
monkey_y = 320
banana_x = 200
banana_y = 0
coconut_x = 200
coconut_y = 0
direction = 1
count = 0
count1= 0
banana_pos = [0,100,150,200,300,400]
coconut_pos = [0,100,150,200,300,400]

#font 
fontObj = pygame.font.Font('arial.ttf',32)

textHealthObj = fontObj.render('Health',True,WHITE,Green)


score = 0


#main loop

running = True

while  running:
    
#falling banana
    count = count+1
    if count == 120:
             random.shuffle(banana_pos)
             banana_x = banana_pos[0]
             banana_y = 0
             count = 0
    
    banana_y += 4
    
# Collision of monkey and banana

    textSurfaceObj = fontObj.render('Score :' + str(score),True,Green,RED)
    if monkey_x <= banana_x <= monkey_x+100 and monkey_y <=banana_y <= monkey_y+100 :  
        score = score + 1
        
    
        
#moving monkey  
    keys = pygame.key.get_pressed()
    if keys[K_UP]:
        monkey_y -=5
            
    if keys[K_DOWN]:
        monkey_y +=5

    if keys[K_RIGHT]:
        monkey_x +=5

    if keys[K_LEFT]:
        monkey_x -=5
        

        
    
# falling coconut
    count1 = count1 + 1

    if count1  == 200:
            random.shuffle(coconut_pos)
            coconut_x = coconut_pos[0]
            coconut_y = 0
            count1 = 0
    coconut_y +=2
    
# Put on screen

    screen.blit(background,(0,0))    
    screen.blit(monkey,(monkey_x,monkey_y))
    screen.blit(banana,(banana_x,banana_y))
    screen.blit(coconut,(coconut_x,coconut_y))
    screen.blit(textSurfaceObj,(10,10))
    screen.blit(textHealthObj,(400,10))
    text = fontObj.render('GAME OVER',True,RED,WHITE)

# Collison of coconut and monkey

    if monkey_x <=coconut_x  <= monkey_x +100 and monkey_y <=coconut_y  <= monkey_y +100 :
       
      
        screen.blit(text,(200,100))
        running = False
    
    
    for event in pygame.event.get():
        if event.type == QUIT:            
            pygame.quit()
            sys.exit()
    pygame.display.update()
    fpsClock.tick(FPS)
            
            

