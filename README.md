# SHORTEST-PATH
This shortest path project implements algorithms to find the minimum distance paths between nodes in a graph, a core concept in graph and optimization. it demonstrates practical applications like route planning in networks representing roads, computers, social connections 

import java.util.Scanner;
public class ShortestPath {
    static final int INF = 9999;
    public static void dijkstra(int[][] graph, int n, int source) {
        int[] distance = new int[n];
        boolean[] visited = new boolean[n];
        
        // Initialize distances
        for (int i=0;i<n;i++) {
            distance[i] = INF;
            visited[i] = false;
        }
        distance[source] = 0;

        // Main algorithm
        for (int count = 0; count < n - 1; count++) {
            int u = -1;
            int min = INF;

            // Find minimum distance vertex
            for (int i=0;i<n;i++) {
                if (!visited[i] && distance[i] < min) {
                    min = distance[i];
                    u = i;
                }
            }
            visited[u] = true;
            
            // Update distances
            for (int v=0;v<n;v++) {
                if (!visited[v] && graph[u][v] != 0 &&
                        distance[u] + graph[u][v] < distance[v]) {
                    distance[v] = distance[u] + graph[u][v];
                }
            }
        }
        System.out.println("Vertex\tDistance from Source");
        for (int i=0;i<n;i++) {
            System.out.println(i + "\t\t" + distance[i]);
        }
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of vertices: ");
        int n = sc.nextInt();
        int[][] graph = new int[n][n];
        System.out.println("Enter adjacency matrix : ");
        for (int i=0;i<n;i++)
            for (int j=0;j<n;j++)
                graph[i][j] = sc.nextInt();
        System.out.print("Enter source vertex: ");
        int source = sc.nextInt();
        dijkstra(graph,n,source);
        sc.close();
    }
}
