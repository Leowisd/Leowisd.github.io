---
title: Leetcode588-designInMemoryFileSystem
categories: leetcode
tags: [Design, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-05 17:43:40
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Design an in-memory file system to simulate the following functions:

ls: Given a path in string format. If it is a file path, return a list that only contains this file's name. If it is a directory path, return the list of file and directory names in this directory. Your output (file and directory names together) should in lexicographic order.

mkdir: Given a directory path that does not exist, you should make a new directory according to the path. If the middle directories in the path don't exist either, you should create them as well. This function has void return type.

addContentToFile: Given a file path and file content in string format. If the file doesn't exist, you need to create that file containing given content. If the file already exists, you need to append given content to original content. This function has void return type.

readContentFromFile: Given a file path, return its content in string format.
## Example
```
Input: 
["FileSystem","ls","mkdir","addContentToFile","ls","readContentFromFile"]
[[],["/"],["/a/b/c"],["/a/b/c/d","hello"],["/"],["/a/b/c/d"]]

Output:
[null,[],null,null,["a"],"hello"]

Explanation:
![](https://assets.leetcode.com/uploads/2018/10/12/filesystem.png)
```

## Solution
```java
class FileSystem {
    HashMap<String, PriorityQueue<String>> dir;
    HashMap<String, String> file;
    public FileSystem() {
        dir = new HashMap<>();
        dir.put("/", new PriorityQueue<String>());
        
        file = new HashMap<>();
        
    }
    
    public List<String> ls(String path) {
        if (file.containsKey(path)){
            String[] tmp = path.split("/");
            List<String> res = new ArrayList<>();
            res.add(tmp[tmp.length-1]);
            return res;
        }
        else {
            if (!dir.containsKey(path)) return null;
            List<String> tmp = new ArrayList<>();
            PriorityQueue<String> pq = new PriorityQueue<>(dir.get(path));
            while (!pq.isEmpty()){
                tmp.add(pq.poll());
            }
            return tmp;
        }
    }
    
    public void mkdir(String path) {
        if (!dir.containsKey(path)){
            dir.put(path, new PriorityQueue<String>());
            String[] tmp = path.split("/");
            String include = "/" + tmp[tmp.length-1];
            int flag = 0;
            for (int i = tmp.length-2; i > 0; i--){
                String pre = path.substring(0, path.length()-include.length());
                if (dir.containsKey(pre)){
                    PriorityQueue<String> pq = new PriorityQueue<>(dir.get(pre));
                    pq.offer(tmp[i+1]);
                    dir.put(pre, pq);
                    flag = 1;
                    break;
                }
                else{
                    // dir.put(pre, new PriorityQueue<String>());
                    PriorityQueue<String> pq = new PriorityQueue<>();
                    pq.offer(tmp[i+1]);
                    dir.put(pre, pq);
                    if (i == 1){
                        PriorityQueue<String> f = dir.get("/");
                        f.offer(tmp[1]);
                        dir.put("/", f);
                        flag = 1;
                    }
                }
                include = "/" + tmp[i] + include;
            }
            if (flag == 0){
                PriorityQueue<String> f = dir.get("/");
                f.offer(tmp[1]);
                dir.put("/", f);      
            }

        }
    }
    
    public void addContentToFile(String filePath, String content) {
        if (file.containsKey(filePath)) file.put(filePath, file.get(filePath)+content);
        else {
            file.put(filePath, content);
            String[] tmp = filePath.split("/");
            String d = filePath.substring(0, filePath.length() - tmp[tmp.length-1].length()-1);
            if (d.equals("")) d = "/";
            if (dir.containsKey(d)){
                PriorityQueue<String> pq = dir.get(d);
                pq.offer(tmp[tmp.length-1]);
                dir.put(d, pq);
            }
        }
    }
    
    public String readContentFromFile(String filePath) {
        if (file.containsKey(filePath)) return file.get(filePath);
        else return null;
    }
}

/**
 * Your FileSystem object will be instantiated and called as such:
 * FileSystem obj = new FileSystem();
 * List<String> param_1 = obj.ls(path);
 * obj.mkdir(path);
 * obj.addContentToFile(filePath,content);
 * String param_4 = obj.readContentFromFile(filePath);
 */
```

<hr />