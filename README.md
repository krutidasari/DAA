# DAA
prims
#include<stdio.h>
int a, b, u, v, n, i, j, ne = 1;
int visited[10] = {0}, min, mincost = 0, cost[10][10];

void main() {
  printf("Prim's Algorithm");
  printf("\nEnter the number of nodes:");
  scanf("%d", & n);
  printf("\nEnter the adjacency matrix:\n");
  for (i = 1; i <= n; i++) {
    for (j = 1; j <= n; j++) {
      scanf("%d", & cost[i][j]);
      if (cost[i][j] == 0)
        cost[i][j] = 999;
    }
  }
  visited[1] = 1;
  printf("\n");
  while (ne < n) {
    for (i = 1, min = 999; i <= n; i++) {
      for (j = 1; j <= n; j++) {
        if (cost[i][j] < min) {
          if (visited[i] != 0) {
            min = cost[i][j];
            a = u = i;
            b = v = j;
          }
        }
      }
    }
    if (visited[u] == 0 || visited[v] == 0) {
      printf("\nEdge %d:(%d %d), Cost = %d", ne++, a, b, min);
      mincost += min;
      visited[b] = 1;
    }
    cost[a][b] = cost[b][a] = 999;
  }
  printf("\n\nMinimum cost=%d", mincost);
}


krushkals#include <stdlib.h>
#include <stdio.h>
int cycle(int a,int parent[]){
    while(parent[a]) a=parent[a];
    return a;
}
void kruskal(int n,int arr[][n]){
    int parent[n],itr=1,cost=0;
    while(itr<n){
        int min=99999,a,b,c,d;
        for(int i=0;i<n;i++){
            parent[i]=0;
            for(int j=0;j<n;j++){
                if(arr[i][j]<min){
                    min=arr[i][j];
                    a=c=i;b=d=j;
                }
            }
        }
        c=cycle(c,parent);
        d=cycle(d,parent);
        if(c!=d){
            parent[c]=d;
            printf("%d - %d  %d\n",b,a,min);
            cost+=min;
            itr++;
        }
        arr[a][b]=arr[b][a]=99999;
    }
    printf("total cost:%d\n",cost);
}
int main(){
    int n=5;
    int arr[5][5]={ { 0, 2, 0, 6, 0 },
                    { 2, 0, 3, 8, 5 },
                    { 0, 3, 0, 0, 7 },
                    { 6, 8, 0, 0, 9 },
                    { 0, 5, 7, 9, 0 } };
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            if(arr[i][j]==0) arr[i][j]=99999;
        }
    }
    kruskal(n,arr);
    return 0;
}


djistras
Dijkstra's Algorithm in C

#include <stdio.h>
#define INFINITY 9999
#define MAX 10

void Dijkstra(int Graph[MAX][MAX], int n, int start);

void Dijkstra(int Graph[MAX][MAX], int n, int start) {
  int cost[MAX][MAX], distance[MAX], pred[MAX];
  int visited[MAX], count, mindistance, nextnode, i, j;

  // Creating cost matrix
  for (i = 0; i < n; i++)
    for (j = 0; j < n; j++)
      if (Graph[i][j] == 0)
        cost[i][j] = INFINITY;
      else
        cost[i][j] = Graph[i][j];

  for (i = 0; i < n; i++) {
    distance[i] = cost[start][i];
    pred[i] = start;
    visited[i] = 0;
  }

  distance[start] = 0;
  visited[start] = 1;
  count = 1;

  while (count < n - 1) {
    mindistance = INFINITY;

    for (i = 0; i < n; i++)
      if (distance[i] < mindistance && !visited[i]) {
        mindistance = distance[i];
        nextnode = i;
      }

    visited[nextnode] = 1;
    for (i = 0; i < n; i++)
      if (!visited[i])
        if (mindistance + cost[nextnode][i] < distance[i]) {
          distance[i] = mindistance + cost[nextnode][i];
          pred[i] = nextnode;
        }
    count++;
  }

  // Printing the distance
  for (i = 0; i < n; i++)
    if (i != start) {
      printf("\nDistance from source to %d: %d", i, distance[i]);
    }
}
int main() {
  int Graph[MAX][MAX], i, j, n, u;
  n = 7;

  Graph[0][0] = 0;
  Graph[0][1] = 0;
  Graph[0][2] = 1;
  Graph[0][3] = 2;
  Graph[0][4] = 0;
  Graph[0][5] = 0;
  Graph[0][6] = 0;

  Graph[1][0] = 0;
  Graph[1][1] = 0;
  Graph[1][2] = 2;
  Graph[1][3] = 0;
  Graph[1][4] = 0;
  Graph[1][5] = 3;
  Graph[1][6] = 0;

  Graph[2][0] = 1;
  Graph[2][1] = 2;
  Graph[2][2] = 0;
  Graph[2][3] = 1;
  Graph[2][4] = 3;
  Graph[2][5] = 0;
  Graph[2][6] = 0;

  Graph[3][0] = 2;
  Graph[3][1] = 0;
  Graph[3][2] = 1;
  Graph[3][3] = 0;
  Graph[3][4] = 0;
  Graph[3][5] = 0;
  Graph[3][6] = 1;

  Graph[4][0] = 0;
  Graph[4][1] = 0;
  Graph[4][2] = 3;
  Graph[4][3] = 0;
  Graph[4][4] = 0;
  Graph[4][5] = 2;
  Graph[4][6] = 0;

  Graph[5][0] = 0;
  Graph[5][1] = 3;
  Graph[5][2] = 0;
  Graph[5][3] = 0;
  Graph[5][4] = 2;
  Graph[5][5] = 0;
  Graph[5][6] = 1;

  Graph[6][0] = 0;
  Graph[6][1] = 0;
  Graph[6][2] = 0;
  Graph[6][3] = 1;
  Graph[6][4] = 0;
  Graph[6][5] = 1;
  Graph[6][6] = 0;

  u = 0;
  Dijkstra(Graph, n, u);

  return 0;
}
