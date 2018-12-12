<figure>
  <figcaption>Your code title</figcaption>
  <pre>
    <code>
      <!-- import random
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
print ("End") -->
    </code>
  </pre>
</figure>
