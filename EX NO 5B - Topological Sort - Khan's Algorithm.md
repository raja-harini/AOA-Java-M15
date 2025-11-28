
# EX 5B Topological Sort - Khan's Algorithm
## DATE: 06/11/2025
## AIM:
To write a Java program to for given constraints.
Problem Description:
A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.

Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b.

Implement a program to find a valid task execution order using topological sort.

Input Format:

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

Output Format:

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

## Algorithm
1. Start the program.
2. Build a directed graph and maintain an indegree array by recording all dependency edges.
3. Push all tasks with indegree 0 into a queue and repeatedly remove a task, append it to the order, and decrease indegree of its neighbors.
4. Continue until the queue empties; if all tasks are processed, return the order, otherwise report that scheduling is impossible. 
5. End the program.  

## Program:
```
/*
Program to implement Reverse a String
Developed by: HARINI R
Register Number: 212223100010
*/

import java.util.*;

public class prog {

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
        int[] indeg = new int[n];

        for (int[] dep : dependencies) {
            int a = dep[0];
            int b = dep[1];
            adj.get(b).add(a);
            indeg[a]++;
        }

        Deque<Integer> q = new ArrayDeque<>();
        for (int i = 0; i < n; i++)
            if (indeg[i] == 0)
                q.add(i);

        List<Integer> order = new ArrayList<>(n);
        while (!q.isEmpty()) {
            int u = q.remove();
            order.add(u);
            for (int v : adj.get(u)) {
                indeg[v]--;
                if (indeg[v] == 0) q.add(v);
            }
        }

        if (order.size() == n) return order;
        return null;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int m = sc.nextInt();

        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt();
            dependencies[i][1] = sc.nextInt();
        }

        List<Integer> result = findTaskOrder(n, dependencies);

        if (result == null) {
            System.out.println("Release cannot be scheduled");
        } else {
            for (int task : result) {
                System.out.print(task + " ");
            }
            System.out.println();
        }

        sc.close();
    }
}
```

## Output:

![alt text](5b.png)

## Result:
The program successfully implemented and the expected output is verified.
