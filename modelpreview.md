---
title: Assessment 1 - Model preview
---
[Return to the homepage](https://davidosh96.github.io/index.html)

The code used to display/embed model on this page was adapted from code found [here](https://websemantics.uk/articles/displaying-code-in-web-pages/).

<figure>
  <figcaption>Model preview:</figcaption>
  <pre>
    <code contenteditable spellcheck="false">
import random
import operator
import matplotlib.pyplot
import matplotlib.animation
import agentframework5 as abm


def distance_between(agents_row_a, agents_row_b):
    return (((agents_row_a[0] - agents_row_b[0])**2) + 
        ((agents_row_a[1] - agents_row_b[1])**2))**0.5
          
import csv
environment = []

#reading in some csv data (DEM points):
f = open('in.txt', newline='') 
reader = csv.reader(f, quoting=csv.QUOTE_NONNUMERIC)
for row in reader:				# A list of rows
    rowlist = []
    for value in row:				# A list of value
        rowlist.append(value)
        #print(value) 				# Floats
    environment.append(rowlist)
f.close() 	# Don't close until you are done with the reader;
		# the data is read on request.


#matplotlib.pyplot.imshow(environment)
#matplotlib.pyplot.show()


#random_seed = 50
neighbourhood = 20
num_of_agents = 10
num_of_iterations = 100
agents = []

#make the graph
fig = matplotlib.pyplot.figure(figsize=(7, 7))
ax = fig.add_axes([0, 0, 1, 1])

'''
# Make the agents.
for i in range(num_of_agents):
    random_seed += 1
    agents.append(abm.Agent(random_seed, environment, neighbourhood, agents))
    #agents.append([random.randint(0,99),random.randint(0,99)])
    print(agents[i])


#call eat for each agent
for j in range(num_of_iterations):
    random.shuffle(agents)
    for i in range(num_of_agents):
        agents[i].move()
        agents[i].eat()
        agents[i].share_with_neighbours(neighbourhood)
'''

#display environment data
#matplotlib.pyplot.xlim(0, 99)
#matplotlib.pyplot.ylim(0, 99)
#matplotlib.pyplot.imshow(environment)
#for i in range(num_of_agents):
#    matplotlib.pyplot.scatter(agents[i].x,agents[i].y)
#matplotlib.pyplot.show()


for i in range(num_of_agents):
    # Make the agents.
        agents.append(abm.Agent(environment, neighbourhood, agents))
        #agents.append([random.randint(0,99),random.randint(0,99)])
        #print(agents[i])


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
   
    
    if random.random() < 0.01:
        carry_on = False
        print("Stopping condition met - explain what this is/why")
   
    for i in range(num_of_agents):
        matplotlib.pyplot.scatter(agents[i]._x,agents[i]._y)
    #print(agents[i]._x, agents[i]._y)


def gen_function(b = [0]):
    a = 0
    global carry_on #Not actually needed as we're not assigning, but clearer
    while (a < 50) & (carry_on) :
        yield a			# Returns control and waits next call.
        a = a + 1


#animation = matplotlib.animation.FuncAnimation(fig, update, interval=1, repeat=False, frames=num_of_iterations)
animation = matplotlib.animation.FuncAnimation(fig, update, frames=gen_function, repeat=False)
matplotlib.pyplot.show()
print ("End")
    </code>
  </pre>
</figure>


<figure>
  <figcaption>Agents module:</figcaption>
  <pre>
    <code contenteditable spellcheck="false">
import random
class Agent():
    def __init__ (self, environment, neighbourhood, agents):
        self.environment = environment
        self.store = 0
        #making the labels "self._x" and "self._y", assigning them the value "random.randint(0,99)":
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


    def move(self): 
        if random.random() < 0.5:
            self._y = (self._y + 1) % 300
        else:
            self._y = (self._y - 1) % 300
            
        if random.random() < 0.5:
            self._x = (self._x + 1) % 300
        else:
            self._x = (self._x - 1) % 300


    def share_with_neighbours(self, neighbourhood):
            for agent in self.agents:
                dist = self.distance_between(agent) 
                if dist <= neighbourhood:
                    sum = self.store + agent.store
                    ave = sum /2
                    self.store = ave
                    agent.store = ave
                    print("sharing " + str(dist) + " " + str(ave))


    def distance_between(self, agent):
            return (((self._x - agent._x)**2) + ((self._y - agent._y)**2))**0.5
    </code>
  </pre>
</figure>

[Return to the homepage](https://davidosh96.github.io/index.html)
