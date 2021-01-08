---
title: "Day1. Data Types"
permalink: /challenges/30daysofcode/day1-data-types
last_modified_at: 2021-01-08T19:10:58+09:00
redirect_from:
  - /theme-setup/
---


## Difficulty

Easy

## Task

Complete the code in the editor below. The variables `i`, `d`, and `s` are already declared and initialized for you.     

You must:

1. Declare 3 variables: one of type `int`, one of type `double`, and one of type `String`.    

2. Read 3 lines of input from stdin (according to the sequence given in the Input Format section below) and initialize your 3 variables.    

3. Use the `+` operator to perform the following operations:    
    - Print the sum of `i` plus your int variable on a new line.   
    - Print the sum of `d` plus your double variable to a scale of one decimal place on a new line.    
    - Concatenate `s` with the string you read as input and print the result on a new line.    

> ***Note:***    
> If you are using a language that doesn't support using `+` for string concatenation (e.g.: C), you can just print one variable immediately following the other on the same line.     
> The string provided in your editor must be printed first, immediately followed by the string you read as input.

### Input Format

The first line contains an integer that you must sum with `i`.    
The second line contains a double that you must sum with `d`.    
The third line contains a string that you must concatenate with `s`.    

### Output Format

Print the sum of both integers on the first line, the sum of both doubles (scaled to  decimal place) on the second line, and then the two concatenated strings on the third line.

### Sample Input
```
12
4.0
is the best place to learn and practice coding!
```

### Sample Output
```
16
8.0
HackerRank is the best place to learn and practice coding!
```

## Solution (Java8)

이미 만들어져 있는 main method를 채우는 문제


```java
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {
	
    public static void main(String[] args) {
        /* 사전에 미리 작성되어 있는 코드 */
        int i = 4;
        double d = 4.0;
        String s = "HackerRank ";
		
        Scanner scan = new Scanner(System.in);

        /* 구현한 task */
        int nextIntValue = Integer.parseInt(scan.nextLine());
        double nextDoubleValue = Double.parseDouble(scan.nextLine());
        String nextStrValue = scan.nextLine();
        
        System.out.println(String.format("%d", i + nextIntValue));
        System.out.println(String.format("%.1f", d + nextDoubleValue));
        System.out.println(s + nextStrValue);

        scan.close();
    }
}
```