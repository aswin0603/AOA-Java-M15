
# EX 5D Flower Planting.
## DATE: 15-11-2025
## AIM:
To write a Java program to for given constraints.
You are given n gardens, labelled from 1 to n.

You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe  garden xi and garden yi.

You want to plant one flower in each garden, and there are exactly 4 types of flowers labelled as 1, 2, 3, and 4.

Your goal is to plant flowers such that:

No two connected gardens (i.e., connected via a path) have the same flower type.

Return any valid flower assignment as an array where:

answer[i] is the flower type planted in the (i+1) ᵗʰ garden

It is guaranteed that:

No garden is connected to more than 3 other gardens

A valid flower assignment always exists

<img width="177" height="292" alt="image" src="https://github.com/user-attachments/assets/36aa40cb-1cdd-4746-b1a6-fc51ce6e96aa" />

## Algorithm
1. Create a list for each garden to store all directly connected (neighboring) gardens using the given paths.
2. Prepare an array result of size n to store the flower type (1–4) assigned to each garden.
3. For every garden i, create a boolean array used[5] to track flower types already used by its neighbors.
4. For each neighbor of garden i, mark its assigned flower type as used if it already has one.
5. From flower types 1 to 4, assign the first unused flower type to garden i and continue until all gardens are assigned.

## Program:
```java
import java.util.*;

public class GardenFlowerPlanner {

    public static int[] assignFlowers(int n, int[][] paths) {
        @SuppressWarnings("unchecked")
        List < Integer > [] adj = new ArrayList[n];

        for (int i = 0; i < n; i++) {
            adj[i] = new ArrayList < > ();
        }

        for (int[] path: paths) {
            int a = path[0] - 1;
            int b = path[1] - 1;
            adj[a].add(b);
            adj[b].add(a);
        }

        int[] result = new int[n];

        for (int i = 0; i < n; i++) {
            boolean[] used = new boolean[5]; 
            for (int neighbor: adj[i]) {
                int flower = result[neighbor];
                if (flower != 0) {
                    used[flower] = true;
                }
            }

            for (int flower = 1; flower <= 4; flower++) {
                if (!used[flower]) {
                    result[i] = flower;
                    break;
                }
            }
        }

        return result;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); // number of gardens
        int m = sc.nextInt(); // number of paths

        int[][] paths = new int[m][2];
        for (int i = 0; i < m; i++) {
            paths[i][0] = sc.nextInt();
            paths[i][1] = sc.nextInt();
        }

        int[] result = assignFlowers(n, paths);

        for (int flower: result) {
            System.out.print(flower + " ");
        }
        System.out.println();
    }
}
```

## Output:
<img width="349" height="384" alt="image" src="https://github.com/user-attachments/assets/d345ea65-588b-4c74-a4b1-8a51605787a0" />



## Result:
The program successfully implemented and the expected output is verified.

```
Developed by: ASWIN B
Register Number:  212224110007
```
