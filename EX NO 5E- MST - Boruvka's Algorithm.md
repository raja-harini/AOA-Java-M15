
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 09/11/2025
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1. Start the program.
2. Initialize each vertex as its own component and repeatedly find the cheapest outgoing edge for every component.
3. For all components, add their cheapest edges to the MST, performing unions to merge components and accumulate total weight.
4. Repeat the process until only one component remains, ensuring all chosen edges connect different components. 
5. End the program.   

## Program:
```
/*
Program to implement Reverse a String
Developed by: HARINI R
Register Number: 212223100010 
*/

import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    
    static int boruvkaMST(int V, List<Edge> edges) {
        //Type your code here
        parent = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;
        int numTrees = V;                
        int MSTweight = 0;
        List<Edge> mstEdges = new ArrayList<>();
        while (numTrees > 1) 
        {
            int[] cheapest = new int[V];
            Arrays.fill(cheapest, -1);
            for (int i = 0; i < edges.size(); i++) 
            {
                Edge e = edges.get(i);
                int setU = find(e.src);
                int setV = find(e.dest);
                if (setU == setV) continue; 
                if (cheapest[setU] == -1 || edges.get(cheapest[setU]).weight > e.weight) 
                {
                    cheapest[setU] = i;
                }
                if (cheapest[setV] == -1 || edges.get(cheapest[setV]).weight > e.weight) 
                {
                    cheapest[setV] = i;
                }
            }
            boolean anyUnion = false;
            for (int i = 0; i < V; i++) 
            {
                int edgeIndex = cheapest[i];
                if (edgeIndex != -1) 
                {
                    Edge e = edges.get(edgeIndex);
                    int setU = find(e.src);
                    int setV = find(e.dest);
                    if (setU == setV) continue; 
                    union(setU, setV);
                    MSTweight += e.weight;
                    mstEdges.add(e);
                    numTrees--;
                    anyUnion = true;
                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                }
            }
            if (!anyUnion) 
            {
                System.err.println("Graph is disconnected — MST does not exist for all vertices.");
                return -1;
            }
        }
        return MSTweight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s; dest = d; weight = w;
    }
}
```

## Output:

![alt text](5e.png)

## Result:
The program successfully implemented and the expected output is verified.
