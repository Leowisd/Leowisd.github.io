---
title: Leetcode353-designSnakeGame
categories: leetcode
tags: [Design, Queue, Amazon, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-05 22:11:07
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Design a Snake game that is played on a device with screen size = width x height. Play the game online if you are not familiar with the game.

The snake is initially positioned at the top left corner (0,0) with length = 1 unit.

You are given a list of food's positions in row-column order. When a snake eats the food, its length and the game's score both increase by 1.

Each food appears one by one on the screen. For example, the second food will not appear until the first food was eaten by the snake.

When a food does appear on the screen, it is guaranteed that it will not appear on a block occupied by the snake.

## Example
```
Given width = 3, height = 2, and food = [[1,2],[0,1]].

Snake snake = new Snake(width, height, food);

Initially the snake appears at position (0,0) and the food at (1,2).

|S| | |
| | |F|

snake.move("R"); -> Returns 0

| |S| |
| | |F|

snake.move("D"); -> Returns 0

| | | |
| |S|F|

snake.move("R"); -> Returns 1 (Snake eats the first food and right after that, the second food appears at (0,1) )

| |F| |
| |S|S|

snake.move("U"); -> Returns 1

| |F|S|
| | |S|

snake.move("L"); -> Returns 2 (Snake eats the second food)

| |S|S|
| | |S|

snake.move("U"); -> Returns -1 (Game over because snake collides with border)
```

## Solution
```java
// if use row*width + col = the number of coordinate
class SnakeGame {

    /** Initialize your data structure here.
        @param width - screen width
        @param height - screen height 
        @param food - A list of food positions
        E.g food = [[1,1], [1,0]] means the first food is positioned at [1,1], the second is at [1,0]. */
    int[][] food;
    LinkedList<int[]> snack;
    HashSet<int[]> set;
    int n,m;
    int nf;
    
    public SnakeGame(int width, int height, int[][] food) {
        snack = new LinkedList<>();
        snack.offer(new int[]{0,0});
        
        set = new HashSet<>();
        set.add(new int[]{0,0});
        
        this.food = food;
        n = height;
        m = width;
        nf = 0;
    }
    
    /** Moves the snake.
        @param direction - 'U' = Up, 'L' = Left, 'R' = Right, 'D' = Down 
        @return The game's score after the move. Return -1 if game over. 
        Game over when snake crosses the screen boundary or bites its body. */
    public int move(String direction) {
        int[] head = new int[]{snack.peek()[0], snack.peek()[1]};
        int x=head[0],y=head[1];
        switch (direction){
            case "U":
                x--;
                break;
            case "L":
                y--;
                break;
            case "R":
                y++;
                break;
            case "D":
                x++;
                break;
        }
        
        if (x >= n || x < 0 || y >= m || y < 0) return -1;
        for (int i = 1; i < snack.size()-1; i++){
            if (x == snack.get(i)[0] && y == snack.get(i)[1]) return -1;
        }
        
        snack.addFirst(new int[]{x,y});
        if (food.length > nf && x == food[nf][0] && y == food[nf][1]){
            return ++nf;  
        }
        snack.pollLast();        
        return nf;
        
    }
}

/**
 * Your SnakeGame object will be instantiated and called as such:
 * SnakeGame obj = new SnakeGame(width, height, food);
 * int param_1 = obj.move(direction);
 */
```

<hr />