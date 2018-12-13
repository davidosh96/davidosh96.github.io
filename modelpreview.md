---
title: Assessment 1 - Model preview
---
[Return to the homepage](https://davidosh96.github.io/index.html)

The code used to display/embed model on this page was adapted from code found [here](https://websemantics.uk/articles/displaying-code-in-web-pages/).

<figure>
  <figcaption>Your code title</figcaption>
  <pre>
    <code contenteditable spellcheck="false">
      <!-- your code here -->
    </code>
  </pre>
</figure>

<figure>
  <figcaption>Agent framework preview:</figcaption>
  <pre>
    <code contenteditable spellcheck="false">
      
import random
class Agent():
    def __init__ (self, environment, neighbourhood, agents):
#defining the agents and environment:        
        self.environment = environment
        self.store = 0
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
            return (((self._x - agent._x)**2) + ((self._y - agent._y)**2))**0.5>
    </code>
  </pre>
</figure>

[Return to the homepage](https://davidosh96.github.io/index.html)
