import pygame
pygame.init()


screen = pygame.display.set_mode((700,500))
pygame.display.set_caption("pong")

doExit = False #Runs game loop

clock = pygame.time.Clock() ##controls how fast screen updates

#variables to hold paddle position
#these go above game loop
p1x = 20
p1y = 200
p2x = 660
p2y = 200

#ball variables
bx = 350 #xposition
by = 250 #yposition
bVx = 5 #x velocity (horizontal speed)
bVy = 5 #y velocity (vertical speed)

#ball movement
bx += bVx
by += bVy

#reflect ball off side walls of screen
if bx < 0 or bx + 20 > 700:
    bVx *= -1
while not doExit:  #game loop---------------------
    
    #event qeueu stuff----------------------
    clock.tick(60) #set the FPS
    
    for event in pygame.event.get(): #check if user did something
        if event.type == pygame.QUIT: #check if user clicked close
            doExit = True #flag that we are done so we exit game loop
            
    #game logic goes here-------------------
    keys = pygame.key.get_pressed()
    if keys[pygame.K_w]:
        p1y-=5
    if keys[pygame.K_s]:
        p1y+=5
    if keys[pygame.K_UP]:
        p2y-=5
    if keys[pygame.K_DOWN]:
        p2y+=5
    #Render section goes here---------------
    screen.fill((0,0,0)) #wipe screen black
            
            #draw a line down the middle
    pygame.draw.line(screen, (76, 0, 153), [349, 0], [349, 500], 5)
    
    #paddle 1
    pygame.draw.rect(screen, (255, 255, 255), (p1x, p1y, 20, 100), 1)    
            #update the screen
    
    #paddle 2
    pygame.draw.rect(screen, (255, 255, 255), (p2x, p2y, 20, 100), 1)
    
    pygame.display.flip()
#END GAME LOOP------------------------------------
            
pygame.quit()#when game is done close down pygame
