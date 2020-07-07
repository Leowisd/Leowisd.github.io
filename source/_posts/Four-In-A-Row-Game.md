---
title: Four in a row game(2 players)
tags: [AI, Adversarial Search, Minimax, Algorithm, Game]
date: 2018-10-02 22:16:33
categories: Algorithm Problem
description: Implementing a four-in-a-row game by minimax algorithm 
---
<p class="description"></p>

<img src="http://ww1.sinaimg.cn/large/cf684029ly1fvuvfxtokqj212w0m8n96.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

![](http://ww1.sinaimg.cn/large/cf684029ly1fvuvj3ly89j20ig0odta3.jpg)
![](http://ww1.sinaimg.cn/large/cf684029ly1fvuvjegey2j20iq01kwed.jpg)


## Implementation

Using Minimax algorithm with Alpha-Beta pruning to implement player 1 and player 2

#### Class: Grid

At first, we define a class Grid to store state

```python
# To store state
class Grid:
    # Grid Initialization
    def __init__(self, grid = None):
        # A new grid
        self.grid = []
        self.winner = 2
        for i in range(6):
            self.grid.append([0,0,0,0,0,0])
        # Copy a exist grid
        if grid != None:
            for i in range(6):
                for j in range(6):
                    self.grid[i][j] = grid[i][j]
        
    # Check if the game is over, using after one player makes a decision
    def IsOver(self):
        c = 0         # statist the number of pieces
        for i in range(6):
            for j in range(6):
                if self.grid[i][j] != 0:
                    if self.Has4(i,j):
                        if self.GetMove() == 1:
                            print("Player2 is the winner\n")
                            self.winner = -1
                        else:
                            print("Player1 is the winner\n")
                            self.winner = 1
                        return True
                    c += 1
        # if not find the winner
        if c == 36:
            print("Tie between 2 players\n")
            self.winner = 0
            return True
        
        return False
    # Check if the game is over, using during the minimax algorithm
    def IsEnd(self):
        c = 0
        # for each piece, check if it in a four-row
        for i in range(6):
            for j in range(6):
                if self.grid[i][j] != 0:
                    if self.Has4(i, j):
                        return True
                    c += 1
        if c == 36:
            return True
        
        return False
    # Check if there is a four-in-a-row
    def Has4(self, x, y):
        # Check upward
        c = 0
        i = x
        j = y
        move = self.grid[x][y]
        while i >= 0:
            if i-1 >=0:
                i -= 1
                if self.grid[i][j] == move:
                    c += 1
                else: 
                    break
            else:
                break
        if c >= 3:
            return True
        
        # check downward
        c = 0
        i = x
        j = y
        while i <= 5:
            if i+1 <= 5:
                i += 1
                if self.grid[i][j] == move:
                    c += 1
                else:
                    break
            else:
                break
        if c >= 3:
            return True
        # check leftward
        c = 0
        i = x
        j = y
        while j >= 0:
            if j-1 >= 0:
                j -= 1
                if self.grid[i][j] == move:
                    c += 1
                else:
                    break
            else:
                break
        if c >= 3:
            return True
        # check rightward
        c = 0
        i = x
        j = y
        while j <= 5:
            if j+1 <= 5:
                j += 1
                if self.grid[i][j] == move:
                    c += 1
                else:
                    break
            else:
                break
        if c >= 3:
            return True
        # check top-left-line
        c = 0
        i = x
        j = y
        while i>=0 and j>=0:
            if i-1>=0 and j-1>=0:
                i -= 1
                j -= 1
                if self.grid[i][j] == move:
                    c += 1
                else:
                    break
            else:
                break
        if c >= 3:
            return True
        # check top-right-line
        c = 0
        i = x
        j = y
        while i>=0 and j<=5:
            if i-1>=0 and j+1<=5:
                i -= 1
                j += 1
                if self.grid[i][j] == move:
                    c += 1
                else:
                    break
            else:
                break
        if c >= 3:
            return True
        # check down-left-line
        c = 0
        i = x
        j = y
        while i<=5 and j>=0:
            if i+1<=5 and j-1>=0:
                i += 1
                j -= 1
                if self.grid[i][j] == move:
                    c += 1
                else:
                    break
            else:
                break
        if c >= 3:
            return True
        # check down-right-line
        c = 0
        i = x
        j = y
        while i<=5 and j<=5:
            if i+1<=5 and j+1<=5:
                i += 1
                j += 1
                if self.grid[i][j] == move:
                    c += 1
                else:
                    break
            else:
                break
        if c >= 3:
            return True
        
        return False
    # mark one location as one player
    def Mark(self, x, y, value):
        self.grid[x][y] = value

    def GetGrid(self):
        return self.grid       
    # Decide whose turn
    def GetMove(self):
        x = 0
        o = 0
        for i in range(6):
            for j in range(6):
                if self.grid[i][j] == 1:
                    x += 1
                if self.grid[i][j] == -1:
                    o += 1
        if x == o:
            return 1
        return -1
    # print the board
    def PrintBoard(self):
        temp = []
        for i in range(6):
            temp.append([0,0,0,0,0,0])
        for i in range(6):
            for j in range(6):
                temp[i][j] = self.grid[i][j]
        for i in range(6):
            for j in range(6):
                if temp[i][j] == 1:
                    temp[i][j] = 'X'
                elif temp[i][j] == -1:
                    temp[i][j] = 'O'
                elif temp[i][j] ==0:
                    temp[i][j] = '-'
            print(temp[i])
```

#### Class: Position

Define a class Position to store a specific location with utility value

```python
class Position:
    
    def __init__(self, x = None, y = None, value = None):
        self.x = x
        self.y = y
        self.value = value
```

#### Class: Player 1

Player One, using minimax algorithm with Alpha-Beta pruning

Decision=MaxValue(MinValue(H( state )))

H (state) function based on the number of each cutoff notes. For two-side-open-3-in-a-row, if current space is empty, check upwards, leftwards, top-left-wards and top-right-wards four lines in total (because if check downwards, rightwards, down-left-wards or down-right-wards fours lines, it will count repeatedly). For one-side-open-3-in-a-row, if current space is empty, check upwards, leftwards, top-left-wards, top-right-wards, downwards, rightwards, down-left-wards and down-right-wards eight directions in total (it won’t be repeated). For open-2-in-a-row, just like open-3-in-a-row, in 2-side and 1-side two situation.

```python
import random
from Grid import*
from Position import*

class PlayerOne:
    # The number of notes henerated
    NodeNumber = 0
    # To make a decision
    def Decision(self, grid):
        self.NodeNumber = 0
        p = self.MaxValue(grid)
        return p
    # Get the max utility value of current state's successions' states
    def MaxValue(self, grid):
        v = -1000000000
        NextGrid = None
        temp = [[0]*6 for i in range(6)]

        for i in range(6):
            for j in range(6):
                NextGrid = Grid(grid.GetGrid())
                if NextGrid.GetGrid()[i][j] == 0: 
                    # if make decision here  
                    NextGrid.Mark(i, j, NextGrid.GetMove())        
                    self.NodeNumber += 1
                    # is the game over?
                    if NextGrid.IsEnd():
                        return Position(i, j)
                    # Get min value from its successions
                    temp[i][j] = self.MinValue(NextGrid,v)
                    # If the min value bigger than current level's max value
                    if temp[i][j] > v:
                        v = temp[i][j]
        # Get the max value locations
        c = 0
        best = [Position() for i in range(36)]
        for i in range(6):
            for j in range(6):
                if temp[i][j] == v:
                    best[c].x = i
                    best[c].y = j
                    best[c].value = temp[i][j]
                    c += 1
        # Get Random
        RanNum = random.randint(0, c-1)
        # print(best[RanNum].x, best[RanNum].y)
        return Position(best[RanNum].x, best[RanNum].y)
    
    # Get the min value of current state's successions' states
    def MinValue(self, grid, maxUp):
        v = 1000000000
        NextGrid = None
        temp = [[0]*6 for i in range(6)]

        for i in range(6):
            for j in range(6):
                NextGrid = Grid(grid.GetGrid())                  
                if NextGrid.GetGrid()[i][j] == 0:
                    # if make decision here
                    self.NodeNumber += 1     
                    NextGrid.Mark(i, j, NextGrid.GetMove())
                    # is the game over?                 
                    if NextGrid.IsEnd():
                        temp[i][j] = -1000000000
                    else:
                        temp[i][j] = self.GetHValue(NextGrid) # Get heuristic value from its successions
                    # If the min value less than current level's min value
                    if temp[i][j] < v:
                        v = temp[i][j]
                    # Alpha-Beta pruning, if the min value not bigger than the max min-value of the current tree level, pruning 
                    if v <= maxUp:
                        return v

        return v
    # Get heuristic value of current state
    def GetHValue(self, grid):
        h = 0
        m3_2 = 0
        m3_1 = 0
        m2 = 0
        o3_2 = 0
        o3_1 = 0
        o2 = 0
        for i in range(6):
            for j in range(6):
                if grid.GetGrid()[i][j] == 0:
                    m3_2 += self.Three2Open(grid, i, j, grid.GetMove())
                    m3_1 += self.Three1Open(grid, i, j, grid.GetMove())
                    o3_2 += self.Three2Open(grid, i, j, grid.GetMove()*(-1))
                    o3_1 += self.Three1Open(grid, i, j, grid.GetMove()*(-1))
                    m2 += self.TwoOpen(grid, i, j, grid.GetMove())
                    o2 += self.TwoOpen(grid, i, j, grid.GetMove()*(-1))
               
        h = 5 * m3_2 - 10 * o3_2 + 3 * m3_1 - 6 * o3_1 + m2 - o2

        return h
    # count the number of rows with 2 sides open
    def Three2Open(self, grid, x, y, move):
        h = 0
        # check upwards
        c = 0
        i = x
        j = y
        flag = False
        while i>=0:
            if i-1>=0:
                i -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break
            else:
                break
        if c == 3 and flag:
            h += 1

        # check leftwards
        c = 0
        i = x
        j = y
        flag = False 
        while j>=0:
            if j-1>=0:
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag:
            h += 1

        # check top-left-line
        c = 0
        i = x
        j = y
        flag = False 
        while i>=0 and j>=0:
            if i-1>=0 and j-1>=0:
                i -= 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag:
            h += 1

        # check top-right-line
        c = 0
        i = x
        j = y
        flag = False 
        while i>=0 and j<=5:
            if i-1>=0 and j+1<=5:
                i -= 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag:
            h += 1

        return h
    # count the number of rows with 1 side open
    def Three1Open(self, grid, x, y, move):
        h = 0
        # check upwards
        c = 0
        i = x
        j = y
        flag = False
        while i>=0:
            if i-1>=0:
                i -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break
            else:
                break
        if c == 3 and flag == False:
            h += 1
        
        # check downwards
        c = 0
        i = x
        j = y
        flag = False 
        while i<=5:
            if i+1<=5:
                i += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check leftwards
        c = 0
        i = x
        j = y
        flag = False 
        while j>=0:
            if j-1>=0:
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check rightwards
        c = 0
        i = x
        j = y
        flag = False 
        while j<=5:
            if j+1<=5:
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1        

        # check top-left-line
        c = 0
        i = x
        j = y
        flag = False 
        while i>=0 and j>=0:
            if i-1>=0 and j-1>=0:
                i -= 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check top-right-line
        c = 0
        i = x
        j = y
        flag = False 
        while i>=0 and j<=5:
            if i-1>=0 and j+1<=5:
                i -= 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check down-left-line
        c = 0
        i = x
        j = y
        flag = False 
        while i<=5 and j>=0:
            if i+1<=5 and j-1>=0:
                i += 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check down-right-line
        c = 0
        i = x
        j = y
        flag = False 
        while i<=5 and j<=5:
            if i+1<=5 and j+1<=5:
                i += 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        return h
    # count the number of rows with 1/2 sides open
    def TwoOpen(self, grid, x, y, move):
        h = 0
        # check upwards
        c = 0
        i = x
        j = y
        flag = False
        while i>=0:
            if i-1>=0:
                i -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break
            else:
                break
        if c == 2:
            h += 1
        
        # check downwards with 1 open
        c = 0
        i = x
        j = y
        flag = False
        while i<=5:
            if i+1<=5:
                i += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 2 and flag == False:
            h += 1

        # check leftwards
        c = 0
        i = x
        j = y
        flag = False
        while j>=0:
            if j-1>=0:
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c ==2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 2:
            h += 1

        # check rightwards with 1 open
        c = 0
        i = x
        j = y
        flag = False
        while j<=5:
            if j+1<=5:
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag == True
                    break                  
            else:
                break
        if c == 2 and flag == False:
            h += 1        

        # check top-left-line
        c = 0
        i = x
        j = y
        flag = False
        while i>=0 and j>=0:
            if i-1>=0 and j-1>=0:
                i -= 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag == True
                    break                  
            else:
                break
        if c == 2:
            h += 1

        # check top-right-line
        c = 0
        i = x
        j = y
        flag = False
        while i>=0 and j<=5:
            if i-1>=0 and j+1<=5:
                i -= 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag == True
                    break                  
            else:
                break
        if c == 2:
            h += 1

        # check down-left-line with 1 open
        c = 0
        i = x
        j = y
        flag = False
        while i<=5 and j>=0:
            if i+1<=5 and j-1>=0:
                i += 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 2 and flag == False:
            h += 1

        # check down-right-line with 1 open
        c = 0
        i = x
        j = y
        flag = False
        while i<=5 and j<=5:
            if i+1<=5 and j+1<=5:
                i += 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 2 and flag == False:
            h += 1

        return h
```
#### Class: Player 2

Player Two, using minimax algorithm with Alpha-Beta pruning

Decision=MaxValue(MinValue(MaxValue(MinValue(H( state )))))
```python
import random 
from Grid import*
from Position import*

class PlayerTwo:
    # The number of notes henerated
    NodeNumber = 0
    # To make a decision
    def Decision(self, grid):
        self.NodeNumber = 0
        p = self.MaxValue1(grid)
        return p
    # Get the max utility value of current state's successions' states
    def MaxValue1(self, grid):
        v = -1000000000
        NextGrid = None
        temp = [[0]*6 for i in range(6)]

        for i in range(6):
            for j in range(6):
                NextGrid = Grid(grid.GetGrid())
                if NextGrid.GetGrid()[i][j] == 0:
                    # if make decision here  
                    NextGrid.Mark(i, j, NextGrid.GetMove())
                    self.NodeNumber += 1
                    # is the game over?
                    if NextGrid.IsEnd():
                        return Position(i, j)
                    # Get min value from its successions
                    temp[i][j] = self.MinValue1(NextGrid,v)
                    # If the min value bigger than current level's max value
                    if temp[i][j] > v:
                        v = temp[i][j]
        # Get the max value locations
        c = 0
        best = [Position() for i in range(36)]
        for i in range(6):
            for j in range(6):
                if temp[i][j] == v:
                    best[c].x = i
                    best[c].y = j
                    best[c].value = temp[i][j]
                    c += 1
        # Get Random
        RanNum = random.randint(0, c-1)
        # print(best[RanNum].x, best[RanNum].y)
        return Position(best[RanNum].x, best[RanNum].y)
    # Get the min value of current state's successions' states
    def MinValue1(self, grid, maxUp):
        v = 1000000000
        NextGrid = None
        temp = [[0]*6 for i in range(6)]

        for i in range(6):
            for j in range(6):
                NextGrid = Grid(grid.GetGrid())
                if NextGrid.GetGrid()[i][j] == 0:
                    # if make decision here
                    self.NodeNumber += 1
                    NextGrid.Mark(i, j, NextGrid.GetMove())
                    # is the game over?                 
                    if NextGrid.IsEnd():
                        temp[i][j] = -1000000000
                    else:
                        temp[i][j] = self.MaxValue2(NextGrid, v) # Get max value from its successions
                    # If the max value less than current level's min value
                    if temp[i][j] < v:
                        v = temp[i][j]
                    # Alpha-Beta pruning, if the max value not bigger than the max min-value of the current tree level, pruning 
                    if v<=maxUp:
                        return v
        # return utility value
        return v
    # Get the max utility value of current state's successions' states
    def MaxValue2(self, grid, minUp):
        v = -1000000000
        NextGrid = None
        temp = [[0]*6 for i in range(6)]

        for i in range(6):
            for j in range(6):
                NextGrid = Grid(grid.GetGrid())
                if NextGrid.GetGrid()[i][j] == 0:
                    # if make decision here
                    NextGrid.Mark(i, j, NextGrid.GetMove())
                    self.NodeNumber += 1
                    # is the game over?                 
                    if NextGrid.IsEnd():
                        temp[i][j] = 1000000000
                    else:
                        temp[i][j] = self.MinValue2(NextGrid,v) # Get min value from its successions
                    # If the min value bigger than current level's min value
                    if temp[i][j] > v:
                        v = temp[i][j]
                    # Alpha-Beta pruning, if the min value not less than the min max-value of the current tree level, pruning 
                    if v >= minUp:
                        return v
        # return utility value
        return v
    # Get the min utility value of current state's successions' states
    def MinValue2(self, grid, maxUp):
        v = 1000000000
        NextGrid = None
        temp = [[0]*6 for i in range(6)]

        for i in range(6):
            for j in range(6):
                NextGrid = Grid(grid.GetGrid())
                if NextGrid.GetGrid()[i][j] == 0:
                    # if make decision here
                    self.NodeNumber += 1
                    NextGrid.Mark(i, j, NextGrid.GetMove())
                    # is the game over?                 
                    if NextGrid.IsEnd():
                        temp[i][j] = -1000000000 
                    else:
                        temp[i][j] = self.GetHValue(NextGrid) # Get h value from its successions
                    # If the h value less than current level's min value
                    if temp[i][j] < v:
                        v = temp[i][j]
                    # Alpha-Beta pruning, if the h value not bigger than the max min-value of the current tree level, pruning 
                    if v <= maxUp:
                        return v
        # return utility value
        return v
    # Get heuristic value of current state
    def GetHValue(self, grid):
        h = 0
        m3_2 = 0
        m3_1 = 0
        m2 = 0
        o3_2 = 0
        o3_1 = 0
        o2 = 0
        for i in range(6):
            for j in range(6):
                if grid.GetGrid()[i][j] == 0:
                    m3_2 += self.Three2Open(grid, i, j, grid.GetMove())
                    m3_1 += self.Three1Open(grid, i, j, grid.GetMove())
                    o3_2 += self.Three2Open(grid, i, j, grid. GetMove()*(-1))
                    o3_1 += self.Three1Open(grid, i, j, grid.GetMove()*(-1))
                    m2 += self.TwoOpen(grid, i, j, grid.GetMove())
                    o2 += self.TwoOpen(grid, i, j, grid.GetMove()*(-1))
        h = 5 * m3_2 - 10 * o3_2 + 3 * m3_1 - 6 * o3_1 + m2 - o2
        return h
    # count the number of rows with 2 sides open
    def Three2Open(self, grid, x, y, move):
        h = 0
        # check upwards
        c = 0
        i = x
        j = y
        flag = False
        while i>=0:
            if i-1>=0:
                i -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break
            else:
                break
        if c == 3 and flag:
            h += 1

        # check leftwards
        c = 0
        i = x
        j = y
        flag = False 
        while j>=0:
            if j-1>=0:
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag:
            h += 1   

        # check top-left-line
        c = 0
        i = x
        j = y
        flag = False 
        while i>=0 and j>=0:
            if i-1>=0 and j-1>=0:
                i -= 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag:
            h += 1

        # check top-right-line
        c = 0
        i = x
        j = y
        flag = False 
        while i>=0 and j<=5:
            if i-1>=0 and j+1<=5:
                i -= 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag:
            h += 1

        return h
    # count the number of rows with 1 side open
    def Three1Open(self, grid, x, y, move):
        h = 0
        # check upwards
        c = 0
        i = x
        j = y
        flag = False
        while i>=0:
            if i-1>=0:
                i -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break
            else:
                break
        if c == 3 and flag == False:
            h += 1
        
        # check downwards
        c = 0
        i = x
        j = y
        flag = False 
        while i<=5:
            if i+1<=5:
                i += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check leftwards
        c = 0
        i = x
        j = y
        flag = False 
        while j>=0:
            if j-1>=0:
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check rightwards
        c = 0
        i = x
        j = y
        flag = False 
        while j<=5:
            if j+1<=5:
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1        

        # check top-left-line
        c = 0
        i = x
        j = y
        flag = False 
        while i>=0 and j>=0:
            if i-1>=0 and j-1>=0:
                i -= 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check top-right-line
        c = 0
        i = x
        j = y
        flag = False 
        while i>=0 and j<=5:
            if i-1>=0 and j+1<=5:
                i -= 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check down-left-line
        c = 0
        i = x
        j = y
        flag = False 
        while i<=5 and j>=0:
            if i+1<=5 and j-1>=0:
                i += 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        # check down-right-line
        c = 0
        i = x
        j = y
        flag = False 
        while i<=5 and j<=5:
            if i+1<=5 and j+1<=5:
                i += 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 3 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 3 and flag == False:
            h += 1

        return h
    # count the number of rows with 1/2 sides open
    def TwoOpen(self, grid, x, y, move):
        h = 0
        # check upwards
        c = 0
        i = x
        j = y
        flag = False
        while i>=0:
            if i-1>=0:
                i -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break
            else:
                break
        if c == 2:
            h += 1
        
        # check downwards with 1 open
        c = 0
        i = x
        j = y
        flag = False
        while i<=5:
            if i+1<=5:
                i += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 2 and flag == False:
            h += 1

        # check leftwards
        c = 0
        i = x
        j = y
        flag = False
        while j>=0:
            if j-1>=0:
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c ==2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 2:
            h += 1

        # check rightwards with 1 open
        c = 0
        i = x
        j = y
        flag = False
        while j<=5:
            if j+1<=5:
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag == True
                    break                  
            else:
                break
        if c == 2 and flag == False:
            h += 1        

        # check top-left-line
        c = 0
        i = x
        j = y
        flag = False
        while i>=0 and j>=0:
            if i-1>=0 and j-1>=0:
                i -= 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag == True
                    break                  
            else:
                break
        if c == 2:
            h += 1

        # check top-right-line
        c = 0
        i = x
        j = y
        flag = False
        while i>=0 and j<=5:
            if i-1>=0 and j+1<=5:
                i -= 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag == True
                    break                  
            else:
                break
        if c == 2:
            h += 1

        # check down-left-line with 1 open
        c = 0
        i = x
        j = y
        flag = False
        while i<=5 and j>=0:
            if i+1<=5 and j-1>=0:
                i += 1 
                j -= 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 2 and flag == False:
            h += 1

        # check down-right-line with 1 open
        c = 0
        i = x
        j = y
        flag = False
        while i<=5 and j<=5:
            if i+1<=5 and j+1<=5:
                i += 1 
                j += 1
                if grid.GetGrid()[i][j] == move:
                    c += 1
                elif c == 2 and grid.GetGrid()[i][j] == 0:
                    flag = True
                    break                  
            else:
                break
        if c == 2 and flag == False:
            h += 1

        return h
```

#### Class: main 
```python
import time
from PlayerOne import*
from PlayerTwo import*
from Grid import*
from Position import*


play1 = PlayerOne()
play2 = PlayerTwo()
grid = Grid()
p = Position()
# when the game is not over
while grid.IsOver() == 0:
    start = time.perf_counter_ns()
    # player1 makes a decision
    p = play1.Decision(grid)
    end = time.perf_counter_ns()
    # record the decision
    grid.Mark(p.x, p.y, grid.GetMove())
    # print the board
    grid.PrintBoard()
    print("Number of node generated: ", play1.NodeNumber)
    print("Running Time: ", (end-start)/1000000, 'ms')
    # if the game is over
    if grid.IsOver():
        break
    # if the game is not over, player2's turn
    start = time.perf_counter_ns()
    # player2 makes a decision
    p = play2.Decision(grid)
    end = time.perf_counter_ns()
    # record the decision
    grid.Mark(p.x, p.y, grid.GetMove())
    # print the board
    grid.PrintBoard()
    print("Number of node generated: ", play2.NodeNumber)
    print("Running Time: ", (end-start)/1000000, 'ms')
```

## Result

```
-	-	-	-	-	-
-	-	-	-	-	-
-	-	-	-	-	-
-	x	-	-	-	-
-	-	-	-	-	-
-	-	-	-	-	-
Number of node generated:  106
Running Time:  293.659876 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	-	-	-	-
-	x	-	-	-	-
-	-	-	-	-	-
-	-	-	o	-	-
Number of node generated:  74043
Running Time:  259152.273405 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	-	-	-	-
-	x	-	x	-	-
-	-	-	-	-	-
-	-	-	o	-	-
Number of node generated:  574
Running Time:  2125.719408 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	-	-	-	-
-	x	-	x	-	-
-	-	o	-	-	-
-	-	-	o	-	-
Number of node generated:  180340
Running Time:  608766.081878 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	-	-	-	-
-	x	-	x	-	-
-	-	o	-	-	-
-	-	-	o	-	x
Number of node generated:  679
Running Time:  2549.825213 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	-	-	-	-
o	x	-	x	-	-
-	-	o	-	-	-
-	-	-	o	-	x
Number of node generated:  173292
Running Time:  542590.650306 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	-	-	-	-
o	x	-	x	-	-
-	-	o	-	x	-
-	-	-	o	-	x
Number of node generated:  590
Running Time:  1894.320808 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	o	-	-	-
o	x	-	x	-	-
-	-	o	-	x	-
-	-	-	o	-	x
Number of node generated:  90411
Running Time:  243936.519988 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	o	-	-	-
o	x	-	x	-	-
-	-	o	-	x	-
-	-	-	o	x	x
Number of node generated:  670
Running Time:  2081.212216 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	o	-	-	-
o	x	o	x	-	-
-	-	o	-	x	-
-	-	-	o	x	x
Number of node generated:  65546
Running Time:  174985.060459 ms
-	-	-	-	-	-
-	-	-	-	-	-
-	-	o	-	-	-
o	x	o	x	-	-
-	-	o	x	x	-
-	-	-	o	x	x
Number of node generated:  268
Running Time:  648.193449 ms
-	-	-	-	-	-
-	-	o	-	-	-
-	-	o	-	-	-
o	x	o	x	-	-
-	-	o	x	x	-
-	-	-	o	x	x
Number of node generated:  3999
Running Time:  9746.094903 ms
Player 2 is the winner

```

## Discussion

* Alpha-Beta pruning saves a lot of time. Before applying Alpha-Beta pruning, it took about 6 hours to finish a game. After it, only about 30 mins
* It need to be very careful about Python's copy/array initialization. [More details about the problem, please click here](http://yfygoing.com/2018/10/04/CopyInPython/)

<hr />