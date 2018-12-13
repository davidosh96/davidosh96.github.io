---
title: Assessment 1 - Model preview
---
[Return to the homepage](https://davidosh96.github.io/index.html)

The code used to display/embed model on this page was adapted from code found [here](https://websemantics.uk/articles/displaying-code-in-web-pages/).

<figure>
  <figcaption>Model preview: figcaption>
  <pre>
    <code contenteditable spellcheck="false">
#import modules to be used in the program
import random #import random is used to generate random integers/values to specify locations for the agents
import matplotlib.pyplot #import pyplot from the matplotlib library, used to plot graphs/agent locations
import matplotlib.animation #imported in order to plot the agents and envrinoment as an animation
import agentframework #import agents module from the file "agentframework.py"
import csv #imported in order to read in the csv file
import time #in order to time how long it takes for the code to be processed/read


start=time.process_time() #starts the timer


#create environment list to put rowlist in:
environment = []



#Reading in the csv DEM raster data from text file and appending it to the environment list:
f = open('in.txt', newline='')
reader = csv.reader(f, quoting=csv.QUOTE_NONNUMERIC)
for row in reader:
    rowlist = []         #create a list for each row
    for value in row:
        rowlist.append(value)  #appends each row of values into a list for each row
        #print(value)      #prints the data as raw values in the console
    environment.append(rowlist)    #appends the rowlist to the environment list:    
f.close()



#using matplotlib to show the data has been read in correctly:
#matplotlib.pyplot.imshow(environment)
#matplotlib.pyplot.show()


    
neighbourhood = 50
#controlling how many agents there are:
num_of_agents = 50
#specifies the number of times the agents are to be moved. 
    #This is different from the number of frames in the animated plot:
num_of_iterations = 100
#create list "agents" to append the agents to:
agents = []



#specifies the size of the figure and axes:
fig = matplotlib.pyplot.figure(figsize=(12, 12))
ax = fig.add_axes([0, 0, 1, 1])



#takes agents created in "agentframework" module
#puts them in list "agents"
for i in range(num_of_agents):
    agents.append(agentframework.Agent(environment, neighbourhood, agents))


#animating the movement of agents:
#carry_on is a Boolean value, i.e it is either True or False
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
    
    #specifying the x and y limits for the graph:
    matplotlib.pyplot.xlim(0, 300)
    matplotlib.pyplot.ylim(300, 0)
    #plotting the environment (from the csv file) on the graph:
    matplotlib.pyplot.imshow(environment)
    #plots the agent locations on the graph:
    for i in range(num_of_agents):
        matplotlib.pyplot.scatter(agents[i]._x,agents[i]._y)
    #print values of the agents to the console:
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
#The number of frames for the animation depends on the maximum value specified for
    # "a" in "gen_function" below, in this case 50. "a" gains a value of +1 for every frame displayed,
    #until it reaches 50.
def gen_function(b = [0]):
    a = 0
    global carry_on 
    while (a < 50) & (carry_on) :
        yield a			
        a = a + 1
        
        #Prints to the console when the animation begins:
        if a == 1:
            print("The sheep start eating...")
        #Prints to the console if full model animation is completed.
            #change this value to match the value for "a" in "gen_function" above.
        if a == 50:
            print("The sheep are full.")

            
#calls and displays the animation
#if repeat=True, the animation will continue unless the alternate stopping condition is met
animation = matplotlib.animation.FuncAnimation(fig, update, frames=gen_function, repeat=False)
matplotlib.pyplot.show()


#stops the timer after all the code has been read, prints time to the console:
end=time.process_time()
print("processing time = "+str(end-start))
    </code>
  </pre>
</figure>


<figure>
  <figcaption>Agents module:</figcaption>
  <pre>
    <code contenteditable spellcheck="false">
import random
#The class for the agents/sheep:
class Agent():
    def __init__ (self, environment, neighbourhood, agents):
#defining the agents and environment:        
        self.environment = environment
        self.store = 0
        #making the labels "self._x" and "self._y", assigning them the value "random.randint(0,299)":
        #this makes the agent coordinates a random integer between and including 0 and 299:
        self._x = random.randint(0, 299)
        self._y = random.randint(0, 299)
        self.neighbourhood = neighbourhood
        self.agents = agents


    def __str__(self):
        return " x " + str(self._x) + " y " + str(self._y)

       
    def eat(self):
        if self.environment[self._y][self._x] > 10:
            self.environment[self._y][self._x] -= 10
            self.store += 10

#moves the agents +/-1 space depending on the value of random.random().
#The "% 300" creates a torus environment, creating a boundary to prevent agents leaving the space.
#If an agent leaves the space on one edge of the graph it will re-enter on the opposite edge. 
    def move(self): 
        if random.random() < 0.5:
            self._y = (self._y + 1) % 300
        else:
            self._y = (self._y - 1) % 300
            
        if random.random() < 0.5:
            self._x = (self._x + 1) % 300
        else:
            self._x = (self._x - 1) % 300

#conditions for sharing with neighbours (although this is not used in this version of the program)
    def share_with_neighbours(self, neighbourhood):
            for agent in self.agents:
                dist = self.distance_between(agent) 
                if dist <= neighbourhood:
                    sum = self.store + agent.store
                    ave = sum /2
                    self.store = ave
                    agent.store = ave
                    print("sharing " + str(dist) + " " + str(ave))

#phythagoras func for calculating distance between 2 agents (also not used in this version):
    def distance_between(self, agent):
            return (((self._x - agent._x)**2) + ((self._y - agent._y)**2))**0.5
    </code>
  </pre>
</figure>

[Return to the homepage](https://davidosh96.github.io/index.html)
