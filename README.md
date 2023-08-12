# Snake-Game
Snake Game using python in VS Code


PROGRAMMED BY- ANKAN PAUL 

REVISED AND DESIGNED BY – Riya Jana





import pygame
from pygame import *
import random

pygame.init()

game_over = False
left_pressed = False
right_pressed = False
up_pressed = False
down_pressed = False
snake_size = 10
width = 50 * snake_size
height = 45 * snake_size
play_width = 50 * snake_size
play_height = 40 * snake_size
score = 0

screen = pygame.display.init()



size = (width,height)
largeText = pygame.font.Font('freesansbold.ttf',30)
smallText = pygame.font.Font('freesansbold.ttf',15)
scoreText = pygame.font.Font('freesansbold.ttf',30)
high_scoreText = pygame.font.Font('freesansbold.ttf',10)

x = play_width/2
y = play_height/2
a = x
b = y

x_change = 0
y_change = 0

def the_snake(snake_size, snake_list):
    for x in snake_list:
        
        # print(x)
        pygame.draw.rect(screen,(202, 224, 31),(x[0],x[1],snake_size,snake_size))
        pygame.display.update()


def game_finished():
    global x,y,a,b, score, high_score
    TextSurf, TextRect = text_objects("* Game Over *", largeText, (255,255,255))
    TextRect.center = ((width/2),height/2)
    screen.blit(TextSurf, TextRect)
    

    
    pygame.display.update()
    time.delay(3000)
    x = a
    y = b
    #printscore
    return



def play():
    global game_over, x, y, x_change, y_change, screen, a, b, score, left_pressed, right_pressed, up_pressed, down_pressed
      
    screen = pygame.display.set_mode(size)

    pygame.display.set_caption('Snake Game')

    food_x = int((random.randint(1,width -snake_size))/snake_size)*snake_size  #random values of food
    food_y = int((random.randint(60,height-snake_size))/snake_size)*snake_size

    
    
    snake_list = []
    length_snake = 1
    score = 0

    speed_of_snake = 30

    clock = pygame.time.Clock()
    

    while not game_over:
        
        # speed_of_snake = int(50/(length_snake*0.5))

        screen.fill((255,255,255))

        TextSurf, TextRect = text_objects("Snake Game", largeText, (0,0,0))     #display snake game
        TextRect.center = ((width/2),(int(30)))
        screen.blit(TextSurf, TextRect)

        TextSurf, TextRect = text_objects("Score: ", smallText, (0,0,0))        #display score
        TextRect.center = ((5*width/6),int(30))
        screen.blit(TextSurf, TextRect)

        TextSurf, TextRect = text_objects(str(score), scoreText, (0,0,0))        #display score
        TextRect.center = ((10*width/11),int(28))
        screen.blit(TextSurf, TextRect)


        # score_Text = pygame.font.Font('freesansbold.ttf',30)
        # score_display = score_Text.render(str(score), 5, (0,0,0))
        # screen.blit(score_display,((5*width/6 + 50),(1.5*snake_size)))                   #score display 

        pygame.draw.rect(screen,(0,0,0),(0,60,play_width,play_height))
        pygame.draw.rect(screen, (255,0,0), (food_x, food_y, snake_size, snake_size))  #food draw
        pygame.draw.rect(screen,(202, 224, 31),(x,y,snake_size,snake_size))
        pygame.display.update()
        
        #to prevent crashing
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True

        keys = pygame.key.get_pressed()
        
        
        if keys[K_LEFT] and not right_pressed:
            x_change = -10
            y_change = 0
            left_pressed = True
            right_pressed = False
            up_pressed = False
            down_pressed = False

            
        if keys[K_RIGHT] and not left_pressed:
            x_change = 10
            y_change = 0
            left_pressed = False
            right_pressed = True
            up_pressed = False
            down_pressed = False
        if keys[K_UP] and not down_pressed:
            x_change = 0
            y_change = -10
            left_pressed = False
            right_pressed = False
            up_pressed = True
            down_pressed = False
        if keys[K_DOWN] and not up_pressed:
            x_change = 0
            y_change = 10
            left_pressed = False
            right_pressed = False
            up_pressed = False
            down_pressed = True

        x = x + x_change
        y = y + y_change

        snake_head = []             #clear the list
        snake_head.append(x)        #add new positions to list
        snake_head.append(y)        #add new positions  to list
        # print(snake_head)
        snake_list.append(snake_head)       ##add the head to snake list/ snake body
        if len(snake_list) > length_snake:
            del snake_list[0]
        
        for i in snake_list[:-1]:           #game over if snake collides with its own body
            if i == snake_head:
                game_finished()
                score = 0
                play()
        
        the_snake(snake_size,snake_list)    #draw the snake body with snake size
        

        
        if x == food_x and y== food_y:     #food eat condition
            food_x = int((random.randint(1,width -snake_size))/snake_size)*snake_size   #random values of position of food
            food_y = int((random.randint(60,height-snake_size))/snake_size)*snake_size

            score = score + 1
            length_snake = length_snake + 1
            print(score)
            pygame.display.update()
            
               
        if x == play_width or x == 0 or y == 50 or y == height:         #snake collides with the boundary check
            game_finished()
            score = 0
            play()
        

        time.delay(speed_of_snake)
        # print(speed_of_snake)
        pygame.display.update()

#define text   
def text_objects(text, font, color):       
    textSurface = font.render(text, True, color)
    return textSurface, textSurface.get_rect()   

play()






# Snake-Game
Snake Game using python in VS Code


PROGRAMMED BY- ANKAN PAUL 

