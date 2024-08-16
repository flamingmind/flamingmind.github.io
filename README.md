pip install pillow numpy
from PIL import Image, ImageDraw, ImageFont
import numpy as np
import math

# Image dimensions
width, height = 800, 600

# Create a new image with white background
image = Image.new('RGB', (width, height), 'white')
draw = ImageDraw.Draw(image)

# Draw a simple brain shape (ellipse for simplicity)
brain_bbox = [200, 150, 600, 450]
draw.ellipse(brain_bbox, fill='lightgray', outline='black')

# Function to add flames
def draw_flame(draw, center, size, color):
    flame_points = []
    for i in range(0, 360, 10):
        angle = math.radians(i)
        radius = size * (1 + 0.5 * math.sin(3 * angle))  # Flame wave effect
        x = center[0] + int(radius * math.cos(angle))
        y = center[1] - int(radius * math.sin(angle))
        flame_points.append((x, y))

    draw.polygon(flame_points, fill=color, outline='black')

# Draw flames around the brain
flame_colors = ['red', 'orange', 'yellow']
flame_positions = [
    (400, 150),  # Top of the brain
    (300, 200),  # Left of the brain
    (500, 200),  # Right of the brain
]

for i, pos in enumerate(flame_positions):
    draw_flame(draw, pos, 100, flame_colors[i % len(flame_colors)])

# Save the image
image.save('flaming_brain.png')

# Display the image
image.show()
