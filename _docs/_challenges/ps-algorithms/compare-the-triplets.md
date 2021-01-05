---
title: "Compare the Triplets"
permalink: /challenges/ps-algorithms/compare-the-triplets
last_modified_at: 2021-01-06T01:27:25+09:00
redirect_from:
  - /theme-setup/
---

## Difficulty

Easy

## Problem

>Alice and Bob each created one problem for HackerRank. A reviewer rates the two challenges, awarding points on a scale from 1 to 100 for three categories: problem clarity, originality, and difficulty.
> 
> The rating for Alice's challenge is the triplet a = (a[0], a[1], a[2]), and the rating for Bob's challenge is the triplet b = (b[0], b[1], b[2]).
> 
> The task is to find their comparison points by comparing a[0] with b[0], a[1] with b[1], and a[2] with b[2].

앨리스와 밥이 각각 HackerRank를 위해 문제를 만들었다.     
리뷰어는 이 두 개의 챌린지(문제)에 대하여 problem clarity, originality, 그리고 difficulty 각 3개 분야 별로 1점에서 100점까지 점수를 부여한다.    

앨리스의 문제에 대한 점수 세 쌍은 `a = (a[0], a[1], a[2])` 이고 밥의 문제에 대한 점수 세 쌍은 `b = (b[0], b[1], b[2])` 이다.   

당신이 작성할 태스크는 점수 세 쌍을 각각 비교하여 앨리스와 밥의 `comparison points` 를 찾을 수 있어야 한다.   

> If a[i] > b[i], then Alice is awarded 1 point.    
> If a[i] < b[i], then Bob is awarded 1 point.    
> If a[i] = b[i], then neither person receives a point.    
> 
> Comparison points is the total points a person earned.

`a[i] > b[i]` 인 경우 앨리스가 1점을 얻는다.    
`a[i] < b[i]` 인 경우 밥이 1점을 얻는다.   
`a[i] = b[i]` 인 경우 둘 모두 점수를 얻을 수 없다.   

`comparison points` 는 각 분야에서 얻은 점수의 총합이다.   

> Given a and b, determine their respective comparison points.

a와 b가 주어지며 이들이 가질 수 있는 각각의 `comparison points`를 구하라.   


### Example

```
a = [1, 2, 3]
b = [3, 2, 1]
```

For elements *0*, Bob is awarded a point because a[0] .
For the equal elements a[1] and b[1], no points are earned.
Finally, for elements 2, a[2] > b[2] so Alice receives a point.
The return array is [1, 1] with Alice's score first and Bob's second.

### Function Description

Complete the function compareTriplets in the editor below.    
compareTriplets has the following parameter(s):

- int a[3]: Alice's challenge rating
- int b[3]: Bob's challenge rating

### Return

- int[2]: Alice's score is in the first position, and Bob's score is in the second.

### Input Format

The first line contains 3 space-separated integers, a[0], a[1], and a[2], the respective values in triplet a.
The second line contains 3 space-separated integers, b[0], b[1], and b[2], the respective values in triplet b.

### Constraints

* 1 ≤ a[i] ≤ 100
* 1 ≤ b[i] ≤ 100

### Sample

#### Sample Input 0
```
5 6 7
3 6 10
```

#### Sample Output 0
```
1 1
```

#### Sample Input 1
```
17 28 30
99 16 8
```

#### Sample Output 1
```
2 1
```


## Solution (Java8)

```java
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;

public class Solution {

    // Complete the compareTriplets function below.
    static List<Integer> compareTriplets(List<Integer> a, List<Integer> b) {
        Integer aScore = 0;
        Integer bScore = 0;
        
        for (int i=0; i<a.size(); i++) {
            int diff = a.get(i) - b.get(i);
            if (diff > 0) {
                ++aScore;
            } else if (diff < 0) {
                ++bScore;
            }
        }
    
        List<Integer> scores = new ArrayList<>();
        scores.add(aScore);
        scores.add(bScore);
        return scores;        
    }

    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        List<Integer> a = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Integer::parseInt)
            .collect(toList());

        List<Integer> b = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Integer::parseInt)
            .collect(toList());

        List<Integer> result = compareTriplets(a, b);

        bufferedWriter.write(
            result.stream()
                .map(Object::toString)
                .collect(joining(" "))
            + "\n"
        );

        bufferedReader.close();
        bufferedWriter.close();
    }
}
```