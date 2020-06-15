---
title: individual
date: 2020-05-07
---
Example Python program individual.py

## Modules

* import random
* from PIL import Image, ImageDraw
* import copy

## Classes

* class Individual:

## Methods

* def __init__(self, image, complexity=3, num_shapes=50, col_mut_rate=0.01, shape_mut_rate=0.01, seed=0):
* def make_first(self):
* def do_next(self, thread):
* def flip_bit(bit):
* def mutate(self, genome):
* def calculate_fitness(self, image):
* def gen_random_genome(self):
* def gen_color():
* def create_xgene(self):
* def create_ygene(self):
* def draw_self(self):
* def convert_fill(colour):
* def convert_shape(shape):

## Code

Python example

    import random
    from PIL import Image, ImageDraw
    import copy
    
    class Individual:
        """Class that handles the actual generating of images and the mutation and fitness calculations.
        'Individual' is not really the best name as in this case it is not entirely correct"""
        def __init__(self, image, complexity=3, num_shapes=50, col_mut_rate=0.01, shape_mut_rate=0.01, seed=0):
            if image.mode != 'RGBA':
                image = image.convert('RGBA')
            self.perf = image
            self.complexity = complexity
            self.num_shapes = num_shapes
            self.col_mut_rate = col_mut_rate
            self.shape_mut_rate = shape_mut_rate
            random.seed(seed)
            self.w, self.h = self.perf.size
            self.xgene_len, self.ygene_len = len(bin(self.w)) - 2, len(bin(self.h)) - 2
            self.cur_index = 1
            self.new_fitness = 0
    
            # self.temp_im = Image.new('RGB', (self.w + 300, self.h + 300), (0, 0, 0))
            self.temp_im = Image.new('RGB', (self.w + self.w//3 , self.h + self.w//3), (0, 0, 0))
            self.draw = ImageDraw.Draw(self.temp_im, 'RGBA')
    
        def make_first(self):
            """Generates the first image completely randomly"""
            self.prev_genome = self.gen_random_genome()
            self.shapes = self.prev_genome['shapes']
            self.fill = self.prev_genome['fill']
            self.prev = self.draw_self()
            self.prev_fitness = self.calculate_fitness(self.prev)
    
            return (1, self.prev, self.prev_fitness)
    
        def do_next(self, thread):
            """Mutates the current image until one more like the supplied is image is made at which point that becomes
            the next generation and is sent to the GUI. Is not a very optimised function as it just mutates randomly
            until something works"""
            while self.new_fitness < self.prev_fitness and thread.is_running:
                while thread.paused:
                    thread.msleep(100)
                self.new_genome = self.mutate(self.prev_genome)
                self.shapes = self.new_genome['shapes']
                self.fill = self.new_genome['fill']
                self.new = self.draw_self()
                self.new_fitness = self.calculate_fitness(self.new)
                thread.current_attempt.emit(str(self.new_fitness))
    
            self.prev_fitness = self.new_fitness
            self.new_fitness = 0
            self.prev_genome = copy.deepcopy(self.new_genome)
            self.prev = self.new.copy()
            self.cur_index += 1
    
            return (self.cur_index, self.prev ,self.prev_fitness)
    
        @staticmethod
        def flip_bit(bit):
            """Simple utility function to make a one a zero and a zero a one"""
            if bit:
                return 0
            else:
                return 1
    
        def mutate(self, genome):
            """Mutates the genome according to the shape and colour mutation rates"""
            shapes = copy.deepcopy(genome['shapes'])
            fill = copy.deepcopy(genome['fill'])
    
            for shape in shapes:
                for point in shape:
                    for val in point:
                        for index, bit in enumerate(val):
                            if random.random() < self.shape_mut_rate:
                                val[index] = self.flip_bit(bit)
    
            for colour in fill:
                for channel in colour:
                    for index, bit in enumerate(channel):
                        if random.random() < self.col_mut_rate:
                            channel[index] = self.flip_bit(bit)
    
            return dict(shapes=shapes, fill=fill)
    
        def calculate_fitness(self, image):
            """Calculates the fitness. Currently one of the biggest issues with the program aside from how the genome was
            implemented. It tests both images pixel by pixel for how different they are. Extremely slow"""
            fitness = 0
            for x in range(self.w):
                for y in range(self.h):
                    r, g, b = image.getpixel((x, y))
                    r2, g2, b2, a2 = self.perf.getpixel((x, y))
                    dr = r2 - r
                    dg = g2 - g
                    db = b2 - b
                    pixel_fitness = dr * dr + dg * dg + db * db
                    fitness += pixel_fitness
    
            if fitness == 0:
                return float('inf')
            else:
                return (1 / fitness) * (10 ** 12)
    
        def gen_random_genome(self):
            """Creates a randomised genome for the first individual"""
            points = []
            shape_list = []
            fill_list = []
            tmp_fill = []
            for chromosome in range(self.num_shapes):
                for point in range(self.complexity):
                    for coord in range(2):
                        x = self.create_xgene()
                        y = self.create_ygene()
                    points.append([x, y])
                shape_list.append(points)
                points = []
    
            for i in range(self.num_shapes):
                for j in range(4):
                    tmp_fill.append(self.gen_color())
                fill_list.append(tmp_fill)
                tmp_fill = []
    
            genome = dict(shapes=shape_list, fill=fill_list)
            return genome
    
        @staticmethod
        def gen_color():
            """Generates a random 'gene' to represent an RGBA value"""
            gene = []
            for i in range(9):
                gene.append(random.choice([0, 1]))
            return gene
    
        def create_xgene(self):
            """Generates a random 'gene' to represent a vertex x point"""
            gene = []
            for i in range(self.xgene_len):
                gene.append(random.choice([0, 1]))
            return gene
    
        def create_ygene(self):
            """Generates a random 'gene' to represent a vertex y point"""
            gene = []
            for i in range(self.ygene_len):
                gene.append(random.choice([0, 1]))
            return gene
    
        def draw_self(self):
            """Uses the genome to actually create the image"""
            for i, j in zip(self.shapes, self.fill):
                try:
                    self.draw.polygon(self.convert_shape(i), fill=self.convert_fill(j))
                except:
                    pass
    
            # box = (60, 60, self.w + 60, self.h + 60)
            box = (self.w//2//8, self.h//2//8, self.w + self.w//2//8, self.h + self.h//2//8)
            # self.temp_im = self.temp_im.convert('RGBA')
            return self.temp_im.crop(box)
    
        @staticmethod
        def convert_fill(colour):
            """Converts a color gene to an actual colour value"""
            col = tuple(int(''.join(map(str, val)), 2) for val in colour)
            return col
    
        @staticmethod
        def convert_shape(shape):
            """Converts a shape gene to a value that can be used to place it on the image"""
            # [(x, y), (x, y)...]
            points = []
    
            for point in shape:
                x = int(''.join(map(str, point[0])), 2)
                y = int(''.join(map(str, point[1])), 2)
                points.append((x, y))
            return points
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
