# fish-simulation
import pygame
import random

# Initialize pygame
pygame.init()

# Screen settings
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("🐟 Vobla Fish Simulation 🐟")

# Load fish image
fish_image = pygame.image.load("vobla.png")  # Make sure you have an image file
fish_image = pygame.transform.scale(fish_image, (80, 40))

# Fish class
class Fish:
    def __init__(self):
        self.x = random.randint(50, WIDTH - 50)
        self.y = random.randint(50, HEIGHT - 50)
        self.speed = random.uniform(1, 3)
        self.direction = random.choice([-1, 1])  # -1 left, 1 right

    def move(self):
        self.x += self.speed * self.direction
        if self.x <= 0 or self.x >= WIDTH - 80:
            self.direction *= -1  # Change direction when hitting the edge

    def draw(self, screen):
        flipped_image = pygame.transform.flip(fish_image, self.direction == -1, False)
        screen.blit(flipped_image, (self.x, self.y))

# Create a list of fish
fish_list = [Fish() for _ in range(5)]

running = True
clock = pygame.time.Clock()

while running:
    screen.fill((0, 100, 255))  # Water background
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    for fish in fish_list:
        fish.move()
        fish.draw(screen)
    
    pygame.display.flip()
    clock.tick(30)

pygame.quit()
