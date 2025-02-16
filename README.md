# Mypage
My first webpage
import pygame
import random

# Initialize Pygame
pygame.init()

# Constants
WIDTH, HEIGHT = 900, 500
WHITE = (255, 255, 255)
RED = (255, 0, 0)
BLUE = (0, 0, 255)
BLACK = (0, 0, 0)

# Game settings
FPS = 60
PLAYER_SPEED = 5
JUMP_POWER = 12
GRAVITY = 0.5
ATTACK_COOLDOWN = 20
ATTACK_DAMAGE = 10
HEALTH = 100

# Initialize screen
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Street Fighter Clone")

# Load assets
player1_img = pygame.image.load("fighter1.png")
player2_img = pygame.image.load("fighter2.png")
bg_img = pygame.image.load("background.jpg")

# Scale images
player1_img = pygame.transform.scale(player1_img, (80, 120))
player2_img = pygame.transform.scale(player2_img, (80, 120))
bg_img = pygame.transform.scale(bg_img, (WIDTH, HEIGHT))

# Player class
class Fighter:
    def __init__(self, x, y, color):
        self.image = pygame.Surface((50, 100))
        self.image.fill(color)
        self.rect = self.image.get_rect(topleft=(x, y))
        self.vel_y = 0
        self.jumping = False
        self.attacking = False
        self.attack_timer = 0
        self.health = HEALTH

    def move(self, keys, left, right, jump):
        if keys[left]:
            self.rect.x -= PLAYER_SPEED
        if keys[right]:
            self.rect.x += PLAYER_SPEED
        if keys[jump] and not self.jumping:
            self.vel_y = -JUMP_POWER
            self.jumping = True

    def apply_gravity(self):
        self.vel_y += GRAVITY
        self.rect.y += self.vel_y
        if self.rect.y >= HEIGHT - 120:
            self.rect.y = HEIGHT - 120
            self.jumping = False

    def attack(self, opponent):
        if not self.attacking and self.attack_timer == 0:
            self.attacking = True
            self.attack_timer = ATTACK_COOLDOWN
            if self.rect.colliderect(opponent.rect):
                opponent.health -= ATTACK_DAMAGE

    def update(self):
        if self.attacking:
            self.attack_timer -= 1
            if self.attack_timer <= 0:
                self.attacking = False

    def draw(self):
        screen.blit(self.image, self.rect)

# Initialize fighters
player1 = Fighter(100, HEIGHT - 120, RED)
player2 = Fighter(700, HEIGHT - 120, BLUE)

# Game loop
running = True
clock = pygame.time.Clock()

while running:
    clock.tick(FPS)
    screen.blit(bg_img, (0, 0))

    keys = pygame.key.get_pressed()
    
    # Player 1 controls
    player1.move(keys, pygame.K_a, pygame.K_d, pygame.K_w)
    if keys[pygame.K_SPACE]:
        player1.attack(player2)

    # Player 2 AI (Simple random movement)
    if random.randint(1, 100) > 98:
        player2.rect.x += random.choice([-PLAYER_SPEED, PLAYER_SPEED])
    if random.randint(1, 100) > 98:
        player2.attack(player1)

    # Apply gravity and update players
    player1.apply_gravity()
    player2.apply_gravity()
    player1.update()
    player2.update()

    # Draw players
    player1.draw()
    player2.draw()

    # Draw health bars
    pygame.draw.rect(screen, RED, (50, 20, player1.health * 2, 20))
    pygame.draw.rect(screen, BLUE, (WIDTH - 50 - player2.health * 2, 20, player2.health * 2, 20))

    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    pygame.display.flip()

pygame.quit()
