# Programming the Farming Drone (Report)
## Introduction
- The Farmer Was Replaced puts you in the shoes of the robot drone that has taken over farm work. The objective is to program the drone to complete a series of farming tasks, such as planting seeds, watering, and harvesting crops, on a field that is on a grid, directing its moves on the grid. You are provided a set of commands (move forward, turn, plant, water, etc.) and you combine them to program your drone for the task at hand.

- Each puzzle becomes increasingly challenging, encouraging you to think outside the box and leverage loops and conditions to solve each puzzle in the fastest manner possible as the game advances. This is a good way to establish problem-solving ability skill with basic coding logic.

# Table of Contents
- [Code Snippets and Explanation](#code-snippets-and-explanation)
- [Challenges and Learnings](#challenges-and-learnings)
- [References](#references)
# Code-Snippets-and-Explanation
## Step 1: Farming on 1 tile
**Code:**
```python
# test harvest() and do_a_flip()
harvest()
do_a_flip() 

```
```python
# test while loop
while True:
	harvest()
```
```python
# final code
while True:
	if can_harvest():
		harvest()
	else:
	  do_a_fliP()
```
```python
# harvest hays
while True:
	if can_harvest():
		harvest()
```
		
```python
# harvest wood
while True:
	plant(Entities.Bush)
	if can_harvest():
		harvest()
	else:
		 do_a_fliP()

```
**Explanation:**
The code runs an infinite number of times and checks if grass can be harvested or not.

**Demo:**

Video Demo:


![video1](1tile.pt1.mp4)

![video2](1tile.pt2.mp4)

![video3](1tile.pt3.mp4)

**Notes**
- Using the code above I was able to unlock new plant(bush)  
- Unlocked senses which is a collection of  `get_pos_x()` and `get_pos_y()`, `num_items(item)` and `get_entity_type() `which basically gives the position of drone and items below it.
- I also upgraded the grass
- The field size was expanded to 3x1 tile.
- New functions like `move()` to move the drone North, South, East, West.
- Extracted wood to  upgrade speed and unlock debug(`breakpoints` and `print()`) and carrots were unlocked.
- New functions like `till()` and `trade()` were also unlocked

## Step 2: Farming on 3x1 tile
**Code:**

```python
# harvest and traverse
while True:
	if can_harvest():
		harvest()
	else:
		do_a_flip()
		move(North)
```

```python
while True:
	if can_harvest():
		harvest()
	else:
		do_a_flip()

	plant(Entities.Bush)# plant for next harvest
	move(North)

```

**Explanation:**

Modified the code using `move(North)` and `plant(Entities.Bush)` to traverse the entire field,plant and harvest the field.

**Demo:**

Video Demo:

![video4](tile(3X1).pt1.mp4)

**Notes**
- I unlocked the operators like `+, -, *, /, //, %, **,`, `==, !=, <=, >= <, >` and `not, and, or`

## Step 3: Farming on 3x3 tile
**Code:**

```python
clear()
while True:
	for i in range(3):
		for j in range(3):
			# harvest when available
			if can_harvest():
				harvest()
				
				# determine plant type by column
				if i == 0:
					plant(Entities.Bush)
				elif i == 1:
					plant_carrots()
			# move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
```

```python
def plant_carrots():
	has_seeds = num_items(Items.Carrot_Seed)
	#trade seeds
	if not has_seeds:
		has_seeds = trade(Items.Carrot_Seed)
	# till the ground
	if get_ground_type() != Grounds.Soil:
		till()
	if has_seeds:
		plant(Entities.Carrots)

```

**Explanation:**

- Here I used for loop to traverse both North and East .
- the i is column and j the row .
- the main loop moves to right after completing the statements in inner loop.
- Improvised the loop to harvest three things:
     * column1(i == 0) for bush
     * column2(i == 1) for carrots
     * column3(i == 2) for grass
- The inner loop handles northward movement of drone.
- The outer loop handles eastward movement of drone.
- The carrots required seeds and ground to be tilled before planting .
  Thus, we defined a function to plant carrots; `plant_carrots`

  * Trading for seeds if seed count becomes 0
      ```python
      if num_items(Items.Carrot_Seed) < 1 :
	     trade(Items.Carrot_Seed)
     ```


- Till the ground and plant by checking the ground status under drone with
    ```python
      if get_ground_type() != Grounds.Soil:
	     till()
      if has_seeds:
         plant(Entities.Carrots)
    ```
- We used `has_seeds` variable to keep track of carrot seeds in our function `plant_carrots`and accordingly follow steps to plant.


**Demo:**

Video Demo:

![video5](3X3%20tile%20pt1.mp4)

![video6](3X3tilept2.mp4)

![video7](3X3pt3.mp4)


**Notes**
- The above code helped me unlock variables which was used to modify the above code and some upgrade to grass.
- I also unlocked functions and implemented in the code above to have better readability.
- Unlocked watering and upgraded the speed of drone.
- Then I expanded to 4 x 4 tile field.

## Step 4: Farming on 4x4 tile
**Code:**

```python
clear()
while True:
	for i in range(4):
		for j in range(4):
			# harvest when available
			if can_harvest():
				harvest()
				
				# determine plant type by column
				if i <= 1:
					plant(Entities.Bush)
				elif i == 2:
					plant_carrots()
			# move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
```

**Explanation:**

- Increased the loop range by 4 
- Then  I planted column1 and column 2 with bush , column 3 with carrots and column 4 with grass.
```python
# defined a function to plant trees
def plant_trees(row):
	if j % 2 == 0 :
		plant(Entities.Bush)
	else:
		plant(Entities.Tree)
```
```python
clear()
while True:
	for i in range(4):
		for j in range(4):
			# harvest when available
			if can_harvest():
				harvest()
				
				# determine plant type by column
				if i == 0:
					plant_trees(j)
				elif i <= 2:
					plant_carrots()
			# move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
```

**Explanation:**

- Trees need to have one tile of gap between them or be at diagonal tiles to grow faster.
   Hence, I defined a function to plant trees  with row as an argument.
- Planted tree at columm 1, keeping one tile of gap and planting a bush in that gap.


```python
# main code
clear()

while True:
	if num_items(Items.Carrot) > num_items(Items.Pumpkin):
		plant_pumpkins()
	else:
		plant_basics()
```

```python
def plant_basics():
	for i in range(4):
		for j in range(4):
			# harvest when available
			if can_harvest():
				harvest()
				
				# determine plant type by column
				if i == 0:
					plant_trees(j)
				elif i <= 2:
					plant_carrots()
			# move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
	
```
```python
def plant_pumpkins():
	ripe_pumpkins = 0
	
	for i in range(4):
		for j in range(4):
			if get_entity_type() != Entities.Pumpkin:
				has_seeds = num_items(Items.Pumpkin_Seed)
				
				if not has_seeds:
					has_seeds = trade(Items.Pumpkin_Seed)
				
				if get_ground_type() != Grounds.Soil:
					till()
				if has_seeds:
					plant(Entities.Pumpkin)
			elif can_harvest():
				ripe_pumpkins += 1
			
			# move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
	
	if ripe_pumpkins == 16:
		harvest()
	
```
**Explanation:**
- Two different functions were used `plant_pumpkins` and `lant_basics`
- The main code checks if there is more carrots than pumpkin (carrots are traded for pumpkin seed).
- otherwise it plants the initial code(plant_basics) for harvesting carrots for cyclic harvest.
- For planting the pumpkins the processes are similar to carrots.but the pumpkins should only be harvested when it grows on all tiles (pumpkin yield = Cube of tile with pumpkin) to maximize the yield.

- Note : some pumpkins die before harvesting so we need to find a way to plant pumpkins on the tile where there was negative growth(dissapeared pumpkin).
- Initialize the `ripe_pumpkins` to 0
- Then we check if the plant below drone is pumpkin or not
- If not we follow same steps as growing carrot but use `Pumpkin_Seed`and increment the `ripe_pumpkins` by 1 when it can be harvested but we don't harvest .
- This continues till all the tiles(`ripe_pumpkins == 16`) have a pumpkin each and a mega pumpkin is harvested.

**Demo:**

Video Demo:

![video8](4x4%20pt1.mp4)

![video9](./4x4pt2.mp4)

**Notes**
- Through the code I unlocked trees,multitrade(specify number of items in second arg of `trade()`),sunflowers, `measure()` to measure petals of sunflower, pumpkins and lists.
- Then I upgraded trees by 3 times , carrot by 1 times and grass yield by 3 times.
- Expanded the farm to 5x5 tiles

## Step 5: Farming on 5x5 tile
**Code:**

```python
def plant_pumpkins():
	ripe_pumpkins = 0
	field_height, field_width = get_world_size(), get_world_size()
	
	for i in range(field_width):
		for j in range(field_height):
			if get_entity_type() != Entities.Pumpkin:
				# harvest when available
				if can_harvest():
					harvest()
					
				# check seeds
				has_seeds = num_items(Items.Pumpkin_Seed)
				
				# buy seeds when needed
				if not has_seeds:
					has_seeds = trade(Items.Pumpkin_Seed)
					
				# till ground when needed
				if get_ground_type() != Grounds.Soil:
					till()
					
				# plant
				if has_seeds:
					plant(Entities.Pumpkin)
					
			elif can_harvest():
				ripe_pumpkins += 1
			
			# move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
	
	if ripe_pumpkins == (field_width * field_height):
		harvest()

```
**Explanation:**

- Improvised the `plant_pumpkins`function for harvesting pumpkin in 5 x 5 tile field.
- Making use of list and variable we defined and assigned  `field_height, field_width = get_world_size(), get_world_size()` and validated the loop range accordingly.
- This makes it easier for the programmer to get the loop range and not insert it manually as field dimension increases.
- Max yield  = (field_width * field_height);only harvests when this condition is met.
```python
def plant_basics():
	field_height, field_width = get_world_size(), get_world_size()
	
	for i in range(field_width):
		for j in range(field_height):
			# harvest when available
			if can_harvest():
				harvest()
				
				# determine plant type by column
				if i == 0:
					plant_trees(j)
				elif i == 1:
					plant_trees(j + 1)
				elif i <= 5:
					plant_carrots()
			
		    # move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
```

**Explanation:**

- We did similar adjustments for our `plant_basics` function 
- To make sure we don't slow down the tree growth, we made the loop range for next column j +1 ; trees need to have one tile of gap between them or be at diagonal tiles.
- Since we were short on carrots we planted carrots starting from 3rd columns(i<= 5) which can be changed accordingly with harvest requirement.
- This loop runs infinitely planting and harvesting in the field with` move(East) `and `move(North)`to traverse the field.

```python
clear() # resets the field

while True:
	field_height, field_width = get_world_size(), get_world_size()
	for i in range(field_width):
		for j in range(field_height):
			# harvest when available
			if can_harvest():
				harvest()
				
			# move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
```

**Explanation:**
- We ran short on hays so i craeted another code just to farm hays
- Reset the field with `clear`  and we used `field_height` and `feild_width` as loop range to traverse the whole field

**Demo:**

Video Demo:

![video10](5x5%20pt1.mp4)

**Notes**
- Unlocked fertilizers(functions unlocked `use_item(Items.Fertilizer)` and `trade(Items.Fertilizer)`.) - reduces growth time of plants under the drone by 2 seconds
- Upgraded pumpkins to 800%, grass to max level,carrots to max level and pumpkins to max level
-  unlocked Polyculture :
   * functions `get_companion()`
   returns the plant companion of plant under drone and the position of the companion (x,y) . Returns None for no plants under drone.
- Expanded the size of the field to 6x6 field.

## Step 6: Farming on 6x6 tile
**Code:**

```python
grass_harv
clear()

while True:
	field_height, field_width = get_world_size(), get_world_size()
	for i in range(field_width):
		for j in range(field_height):
			# harvest when available
			if can_harvest():
				harvest()
				
			# move north infinitely	
			move(North)
			# j loop end
		# move east infinitely	
		move(East)
		# i loop end
```
```python
# pumpkin plantation
clear()

while True:
	if num_items(Items.Carrot) > num_items(Items.Pumpkin):
		plant_pumpkins()
	else:
		plant_basics()
```

**Explanation:**

- We used the `grass_harv` function and pumpkin plantation and harvest code since we were short of hays and pumpkins to unlock the next stages
**Demo:**

Video Demo:
![video11](6x6pt1.mp4)

**Notes**
- The code helped me to unlocked mazes and upgrade trees to max
- Upgraded mazes to max




# Challenges and Learnings
## Challenges
* 1. The first challenge was to make the drone harvest and give the products to grow.
    - I over came this hurdle by using if statements to check if the plant to be harvest is ready.
* 2. Second obstacle was to plant different plants as the field  size increased. I made use of loops and conditions to plant a specific plant in a column and change the columns of plants according to the need to advance in the game.

* 3. Inserting the loop ranges everytime the field size increased was hectic so I made use of variables and list of grid tile positions to get the data of the field size and saved it to variables . Then these variables are passed down as loop ranges.

* 4. Seeds were required to plant some of the plants ;drone would not plant the plants once the seeds were finished and the seeds were to be traded for other harvests . Therefore, I used variables and conditions to store the data of seeds and swap between plants to be plants which helped the process to be automated and cyclic.

* 5. The long codes were getting lengthier as the game progressed and it became difficult to interpret. Thus, I created functions to handle micro-processes like planting trees , carrots and pumpkins which had different conditions to grow and condensed the main code, enhancing readability and reusabilty of that code.
## Learnings

- Started with a 1x1 field, learning basic commands.
    - Used a simple `while` loop with `harvest()`.
    - Refined to use `if can_harvest()` to harvest only when needed.
    - Added `do_a_flip()` to wait until crops were ready.
  
- Expanded to a 3x1 grid and gained `move()` commands.
    - Used loops to navigate the rows and logic to move north or east.
    - Unlocked more resources and tools like `print()` for debugging, tilling soil, and trading seeds.

- Unlocked `for` loops, enabling navigation of larger 3x3 fields.
    - Used nested loops with `i` and `j` counters to cover every tile.
    - Began planting different crops in each column for resource management.

- Gained access to variables for seed counts and other resources.
    - Created custom functions like `plant_carrots()` to automate planting.
    - Streamlined main loop for easy strategy adjustments.

- As field sizes grew (4x4, then 5x5), learned to generalize code.
    - Used `get_world_size()` to dynamically adjust loop ranges.
    - Developed a strategy to maximize pumpkin yield by harvesting fully grown crops.

- Unlocked trees and adjusted code to allow for spacing requirements.
    - Added logic to plant bushes between trees for optimal growth.
    - Balanced resources by trading when low on specific seeds and timing harvests.

- Reached a modular and efficient approach on 6x6 grids.
    - Managed tasks like maintaining hay supplies and rotating crop types based on conditions.
  
- Each level introduced new coding and optimization challenges.
    - Created a more strategic, hands-on way to learn programming.
    - With each unlocked function, code reached higher levels of efficiency.
## References
List any resources, articles, or libraries you used or referenced while working on this project.
1. [codeWonderland](http://www.youtube.com/playlist?list=PL6V9A4LF9jNWTwW-0xLoqfiJRn5-C6xkN)
2. [Zahait](https://youtu.be/v3M8rqMS0_M?si=2WqZishznQj4xufA)
3. [Steam](https://store.steampowered.com/app/2060160/The_Farmer_Was_Replaced/)


Google Drive link :

[The Farmer was Replaced](https://drive.google.com/drive/folders/18RmkFl3AYuczp8Iyp7G04BhE0abdEhLW?usp=drive_link)