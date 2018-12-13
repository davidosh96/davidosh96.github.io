---
title: Assessment 1 - Model preview
---
[Return to the homepage](https://davidosh96.github.io/index.html)

The code used to display/embed model on this page was adapted from code found [here](https://websemantics.uk/articles/displaying-code-in-web-pages/).

<figure>
  <figcaption>Model preview:</figcaption>
  <pre>
    <code contenteditable spellcheck="false">
#import modules to be used in the program
import random 
import matplotlib.pyplot
import matplotlib.animation 
import agentframework 
import csv 
import time


start=time.process_time() #starts the timer


#create environment list to put rowlist in:
environment = []



#Reading in the csv DEM raster data from text file:
f = open('in.txt', newline='')
reader = csv.reader(f, quoting=csv.QUOTE_NONNUMERIC)
for row in reader:
    rowlist = []  
    for value in row:
        rowlist.append(value)
        #print(value) 
    environment.append(rowlist)    
f.close()

    
neighbourhood = 50
num_of_agents = 50 
num_of_iterations = 100
agents = []


fig = matplotlib.pyplot.figure(figsize=(12, 12))
ax = fig.add_axes([0, 0, 1, 1])



for i in range(num_of_agents):
    agents.append(agentframework.Agent(environment, neighbourhood, agents))


#animating the movement of agents:
carry_on = True	
            
def update(frame_number):
    fig.clear()
    global carry_on    
    #call eat for each agent
    #for j in range(num_of_iterations):
        #random.shuffle(agents)
    for i in range(num_of_agents):
        agents[i].move()
        agents[i].eat()
        #agents[i].share_with_neighbours(neighbourhood)
    
    matplotlib.pyplot.xlim(0, 300)
    matplotlib.pyplot.ylim(300, 0)
    matplotlib.pyplot.imshow(environment)
    for i in range(num_of_agents):
        matplotlib.pyplot.scatter(agents[i]._x,agents[i]._y)
    #print(agents[i]._x, agents[i]._y)
    
    
#setting the stopping conditions for the animation:   
  
#This stopping condition which will stop the animation if any agent
    #is generated a random.random value of less than 0.01 in the agent framework.
    #random.random generates values between 0 and 1.    
    if random.random() < 0.01:
        carry_on = False
        print("Stopping condition met: the sheep weren't very hungry.")

#If the random.random stopping condition is not met, the animation will continue
    #until the specified number of frames is reached, at which point carry_on will become False.
def gen_function(b = [0]):
    a = 0
    global carry_on 
    while (a < 50) & (carry_on) :
        yield a			
        a = a + 1
        
        if a == 1:
            print("The sheep start eating...")
        if a == 50:
            print("The sheep are full.")

            
#if repeat=True, the animation will continue unless the alternate stopping condition is met
animation = matplotlib.animation.FuncAnimation(fig, update, frames=gen_function, repeat=False)
matplotlib.pyplot.show()


end=time.process_time()
print("processing time = "+str(end-start))
    </code>
  </pre>
</figure>

<figure>
  <figcaption>Model preview:</figcaption>
  <pre>
    <code contenteditable spellcheck="false">
#import modules to be used in the program
import random 
import matplotlib.pyplot
import matplotlib.animation 
import agentframework 
import csv 
import time


start=time.process_time() #starts the timer


#create environment list to put rowlist in:
environment = []



#Reading in the csv DEM raster data from text file:
f = open('in.txt', newline='')
reader = csv.reader(f, quoting=csv.QUOTE_NONNUMERIC)
for row in reader:
    rowlist = []  
    for value in row:
        rowlist.append(value)
        #print(value) 
    environment.append(rowlist)    
f.close()

    
neighbourhood = 50
num_of_agents = 50 
num_of_iterations = 100
agents = []


fig = matplotlib.pyplot.figure(figsize=(12, 12))
ax = fig.add_axes([0, 0, 1, 1])



for i in range(num_of_agents):
    agents.append(agentframework.Agent(environment, neighbourhood, agents))


#animating the movement of agents:
carry_on = True	
            
def update(frame_number):
    fig.clear()
    global carry_on    
    #call eat for each agent
    #for j in range(num_of_iterations):
        #random.shuffle(agents)
    for i in range(num_of_agents):
        agents[i].move()
        agents[i].eat()
        #agents[i].share_with_neighbours(neighbourhood)
    
    matplotlib.pyplot.xlim(0, 300)
    matplotlib.pyplot.ylim(300, 0)
    matplotlib.pyplot.imshow(environment)
    for i in range(num_of_agents):
        matplotlib.pyplot.scatter(agents[i]._x,agents[i]._y)
    #print(agents[i]._x, agents[i]._y)
    
    
#setting the stopping conditions for the animation:   
  
#This stopping condition which will stop the animation if any agent
    #is generated a random.random value of less than 0.01 in the agent framework.
    #random.random generates values between 0 and 1.    
    if random.random() < 0.01:
        carry_on = False
        print("Stopping condition met: the sheep weren't very hungry.")

#If the random.random stopping condition is not met, the animation will continue
    #until the specified number of frames is reached, at which point carry_on will become False.
def gen_function(b = [0]):
    a = 0
    global carry_on 
    while (a < 50) & (carry_on) :
        yield a			
        a = a + 1
        
        if a == 1:
            print("The sheep start eating...")
        if a == 50:
            print("The sheep are full.")

            
#if repeat=True, the animation will continue unless the alternate stopping condition is met
animation = matplotlib.animation.FuncAnimation(fig, update, frames=gen_function, repeat=False)
matplotlib.pyplot.show()


end=time.process_time()
print("processing time = "+str(end-start))
    </code>
  </pre>
</figure>

[Return to the homepage](https://davidosh96.github.io/index.html)
