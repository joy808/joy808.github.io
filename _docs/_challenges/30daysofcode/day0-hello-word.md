---
title: "Day0. Hello, World"
permalink: /challenges/30daysofcode/day0-hello-word
last_modified_at: 2021-01-06T01:01:03+09:00
redirect_from:
  - /theme-setup/
---


## Difficulty

Easy

## Problem

### Input Format

A single line of text denoting  (the variable whose contents must be printed).

### Output Format

Print Hello, World. on the first line, and the contents of  on the second line.

### Sample Input
```
Welcome to 30 Days of Code!
```
### Sample Output
```
Hello, World. 
Welcome to 30 Days of Code!
```

## Solution (Java8)

```java
import java.io.*;
public class Solution {
  public static void main(String[] args) {
    Scanner scan = new Scanner(System.in);
    String inputString = scan.nextLine();
    scan.close();

    System.out.println("Hello, World.");
    System.out.println(inputString);
  }
}
```