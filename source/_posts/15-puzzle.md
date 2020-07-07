---
title: 15-puzzle
tags: [Algorithm, AI, Searching, A*, IDS, Iterative Deepening Search, DFS, 15-puzzle]
date: 2018-09-08 22:19:31
categories: Algorithm Problem
description: Solving 15-puzzle Problem by IDS, DFS and A* Search
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fv34t6hyuaj212w0m8e83.jpg" alt="Mayer, Merkel, & Ottmann: lithographers James Albert Wales: artist - Library of Congress" title="Mayer, Merkel, & Ottmann: lithographers James Albert Wales: artist - Library of Congress" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## A* Searching
```python
# Title: 15-puzzle by A*
# Author: YF
# Time: 9/8/2018

import numpy as np
import time

class State:
    # Initiate new state
    def __init__(self, state, directionFlag=None, parent=None, depth=1):
        # state is a (4,4) array to storage the state        
        self.state = state
        # record the possible directions to generate the sub-states
        self.direction = ['up', 'down', 'right', 'left']
        if directionFlag:
            self.direction.remove(directionFlag)  
        # Initialization
        self.parent = parent
        self.symbol = ' '
        self.answer = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, State.symbol]])
        self.depth = depth
        # calculate the num of tiles which are not in the correct position
        # h
        num = 0
        for i in range(len(state)):
            for j in range(len(state)):
                if self.state[i, j] != ' 'and self.state[i, j] != self.answer[i, j]:
                    num += 1
        # calculate the state's cost 
        # f
        self.cost = num + self.depth
    # print the search path
    def showPath(self):
        for i in range(4):
            for j in range(4):
                if self.state[i, j] == ' ':
                    print(self.state[i, j], end='   ')
                elif int(self.state[i, j])>9:
                    print(self.state[i, j], end='  ')
                else:
                    print(self.state[i, j], end='   ')
            print("\n")
        return
    # FInd the position of the empty 
    def getEmptyPos(self):
        postion = np.where(self.state == self.symbol)
        return postion
    # expand notes
    def expandStates(self):
        if not self.direction:
            return []
        subStates = []
        # the maximum of the x,y
        row, col = self.getEmptyPos()
        if 'left' in self.direction and col > 0:    
        #it can move to left place
            s = self.state.copy()
            temp = s.copy()
            s[row, col] = s[row, col-1]
            s[row, col-1] = temp[row, col]
            news = State(s, directionFlag='right', parent=self, depth=self.depth+1)
            subStates.append(news)
        if 'up' in self.direction and row > 0:    
        #it can move to upper place
            s = self.state.copy()
            temp = s.copy()
            s[row, col] = s[row-1, col]
            s[row-1, col] = temp[row, col]
            news = State(s, directionFlag='down', parent=self, depth=self.depth+1)
            subStates.append(news)
        if 'down' in self.direction and row < 3:
            #it can move to down place   
            s = self.state.copy()
            temp = s.copy()
            s[row, col] = s[row+1, col]
            s[row+1, col] = temp[row, col]
            news = State(s, directionFlag='up', parent=self, depth=self.depth+1)
            subStates.append(news)
        if self.direction.count('right') and col < 3:
            #it can move to right place    
            s = self.state.copy()
            temp = s.copy()
            s[row, col] = s[row, col+1]
            s[row, col+1] = temp[row, col]
            news = State(s, directionFlag='left', parent=self, depth=self.depth+1)
            subStates.append(news)
        return subStates
    
    def AStar(self):
        # generate a empty frontierList
        frontierList = []
        # generate a empty exploredList                 
        exploredList = []
        # append the origin state to the frontierList                
        frontierList.append(self)
        amount = 1
        # denote the steps it travels         
        while len(frontierList) > 0:     # start the loop
            n = frontierList.pop(0)
            exploredList.append(n)
            subStates = n.expandStates()
            # Add the number of new nodes expanded
            amount += len(subStates)
            path = []
            for s in subStates:
                if (s.state == s.answer).all():
                    while s.parent:
                        path.append(s.parent)
                        s = s.parent
                    path.reverse()
                    return path, amount
            frontierList.extend(subStates)
            # sort the frontierList in terms of the cost f
            frontierList.sort(key=lambda x: x.cost)  
        else:
            return None, None

if __name__ == '__main__':    
    # the symbol representing the empty place
    emptySite = ' '
    # you can change the symbol at here              
    State.symbol = emptySite
    # set the origin state of the puzzle
    # First test state
    # originState = State(np.array([[1, 2, 7, 3], [5, 6 , 11, 4], [9, 10, 15, 8], [13, 14, 12, emptySite]]))
    # Second test state
    originState = State(np.array([[5, 1, 7, 3], [9, 2, 11, 4], [13, 6, 15, 8], [emptySite, 10, 14, 12]]))  
    State.answer = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12],[13, 14, 15, State.symbol]])       
    s1 = State(state=originState.state)
    start = time.perf_counter_ns()      # searchiing start time
    path, amount = s1.AStar()
    if path:                        # if find the solution
        end = time.perf_counter_ns()        # searching end time 
        steps = 0
        for node in path:
            print("Step: ", steps)
            # print the path from the origin to final state         
            node.showPath()
            steps += 1
        # print the goal state
        print("Step: ", steps)
        for i in range(4):
            for j in range(4):
                if State.answer[i, j] == ' ':
                    print(State.answer[i, j], end='   ')
                elif int(State.answer[i, j])>9:
                    print(State.answer[i, j], end='  ')
                else:
                    print(State.answer[i, j], end='   ')
            print("\n")
        
        print("Total steps is: ", steps)
        print("The number of notes expended: ", amount)
    print("CPU execution time is", (int(end)- int(start))/1000000, "ms")
```

## DFS
```
LOADING...
```

## IDS
```python
# Title: 15-puzzle by IDS
# Author: YF
# Time: 9/9/2018

import numpy as np
import time


class State:
    # Initiate new state
    def __init__(self, state, directionFlag=None, parent=None, depth=1):
        # state is a (4,4) array to storage the state        
        self.state = state
        # record the possible directions to generate the sub-states
        self.direction = ['up', 'down', 'right', 'left']
        if directionFlag:
            self.direction.remove(directionFlag)  
        # Initialization
        self.parent = parent
        self.symbol = ' '
        self.answer = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, State.symbol]])
        self.depth = depth
        # calculate the num of tiles which are not in the correct position
        # h
        num = 0
        for i in range(len(state)):
            for j in range(len(state)):
                if self.state[i, j] != ' 'and self.state[i, j] != self.answer[i, j]:
                    num += 1
        # calculate the state's cost 
        # f
        self.cost = num + self.depth
    # print the search path
    def showPath(self):
        for i in range(4):
            for j in range(4):
                if self.state[i, j] == ' ':
                    print(self.state[i, j], end='   ')
                elif int(self.state[i, j])>9:
                    print(self.state[i, j], end='  ')
                else:
                    print(self.state[i, j], end='   ')
            print("\n")
        return
    # FInd the position of the empty 
    def getEmptyPos(self):
        postion = np.where(self.state == self.symbol)
        return postion
    # expand notes
    def expandStates(self):
        if not self.direction:
            return []
        subStates = []
        # the maximum of the x,y
        row, col = self.getEmptyPos()
        if 'left' in self.direction and col > 0:    
        #it can move to left place
            s = self.state.copy()
            temp = s.copy()
            s[row, col] = s[row, col-1]
            s[row, col-1] = temp[row, col]
            news = State(s, directionFlag='right', parent=self, depth=self.depth+1)
            subStates.append(news)
        if 'up' in self.direction and row > 0:    
        #it can move to upper place
            s = self.state.copy()
            temp = s.copy()
            s[row, col] = s[row-1, col]
            s[row-1, col] = temp[row, col]
            news = State(s, directionFlag='down', parent=self, depth=self.depth+1)
            subStates.append(news)
        if 'down' in self.direction and row < 3:
            #it can move to down place   
            s = self.state.copy()
            temp = s.copy()
            s[row, col] = s[row+1, col]
            s[row+1, col] = temp[row, col]
            news = State(s, directionFlag='up', parent=self, depth=self.depth+1)
            subStates.append(news)
        if self.direction.count('right') and col < 3:
            #it can move to right place    
            s = self.state.copy()
            temp = s.copy()
            s[row, col] = s[row, col+1]
            s[row, col+1] = temp[row, col]
            news = State(s, directionFlag='left', parent=self, depth=self.depth+1)
            subStates.append(news)
        return subStates
    
    def IDS(self):
        for depth in range(10000):
            path, flag = self.DLS(depth)
            if flag != -1:
                return path, flag
        return None, None

    def DLS(self, depth):
        # the amount is used to record how many notes expanded 
        global amount
        amount += 1
        # Goal test
        if (self.state == self.answer).all():
            s = self
            path = []
            # When s is not the root note
            while s.parent:
                path.append(s.parent)
                s = s.parent
            path.reverse()
            return path, 1

        if depth == 0:
            return None, -1
        # cutoff => cutoff occurred?
        cutoff = False
        # Get all possible sub notes
        subStates = self.expandStates()
        for s in subStates:
            # DLS
            result, flag = s.DLS(depth-1)
            # cutoff occurred?
            if flag == -1:  # cutoff occurred
                cutoff = True
            else:
                if result != None:
                    return result, flag
        if cutoff:
            return None, -1

            
if __name__ == '__main__':    
    # the symbol representing the empty place
    emptySite = ' '
    # you can change the symbol at here              
    State.symbol = emptySite
    # set the origin state of the puzzle
    # First test state
    originState = State(np.array([[1, 2, 7, 3], [5, 6 , 11, 4], [9, 10, 15, 8], [13, 14, 12, emptySite]]))
    # Second test state
    # originState = State(np.array([[5, 1, 7, 3], [9, 2, 11, 4], [13, 6, 15, 8], [emptySite, 10, 14, 12]]))  
    State.answer = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12],[13, 14, 15, State.symbol]])       
    s1 = State(state=originState.state)
    start = time.perf_counter_ns()      # searchiing start time
    global amount
    amount = 0
    path, flag = s1.IDS()
    end = time.perf_counter_ns()        # searching end time 
    if path:                        # if find the solution
        steps = 0
        for node in path:
            print("Step: ", steps)
            # print the path from the origin to final state         
            node.showPath()
            steps += 1
        # print the goal state
        print("Step: ", steps)
        for i in range(4):
            for j in range(4):
                if State.answer[i, j] == ' ':
                    print(State.answer[i, j], end='   ')
                elif int(State.answer[i, j])>9:
                    print(State.answer[i, j], end='  ')
                else:
                    print(State.answer[i, j], end='   ')
            print("\n")
        
        print("Total steps is: ", steps)
        print("The number of notes expended: ", amount)
    print("CPU execution time is", (int(end)- int(start))/1000000, "ms")
    ```

<hr />