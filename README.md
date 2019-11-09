# 1-1. 리스트

 리스트는 데이터가 저장되어 있는 노드들이 포인더를 통하여 선형적으로 연결된 형태의 자료구조를 말한다. 리스트는 컴퓨팅에서 가장 근본이 되는 자료구조로써 스택, 큐, 배열과의 연관성 등에 활용된다. 배열에 비해서 리스트의 장점은 리스트를 구서아는 요소들이 기억장소에 연속적인 순서로 할당되어 있을 필요 없이 각각 독립적으로 존재할 수 있으므로 손쉽게 추가 및 제거될 수 있다느 것이고, 또한 이러한 작업이 리스트의 전체 구조에 영향을 주지 않는다는 점이다. 반면에, 리스트를 구성하는 노드들이 포인터를 통하여 상호 연결되어 있으므로 노드들의 추가/삭제 시 포인터의 상호 연결관계를 관리해야 하는 단점이 있다. 또한, 노드들을 검색할 때 무작위로 접근하지 못하고 처음부터 순서대로 포인터를 따라가며 탐색해야 하는 비효율성이 존재하다. 

# 1-2. 리스트의 종류 

 # Singly Linked List
 
 노드안에 링크가 1개이고 단방향으로 진행하는 리스트
 
 # Doubly Linked List

 노드안에 링크가 2개이고 양방향으로 진행할 수 있는 리스트
 
 # Circular Linked List

 마지막 노드가 첫번째 노드를 가르켜서 계속 회전할 수 있게 만들어진 리스트
 
 # 1-3. 예시코드
#include <stdio.h>
#include <stdlib.h>
typedef struct list {
 int d;
 struct list* p;
} LIST;
LIST* root = NULL;
LIST* last = NULL;
int main(void){
 LIST* r = (LIST*)malloc(sizeof(LIST));
 r->d = 35;
 r->p = NULL; 
 root = r;
 last = r;
 
 r = (LIST*)malloc(sizeof(LIST));
 last->p = r;
 r->d = 40;
 r->p = NULL;
 last = r;
 
 r = (LIST*)malloc(sizeof(LIST));
 last->p = r;
 r->d = 45;
 r->p = NULL;
 last = r;
 
 while(root){
  printf("%d\n", root->d);
  root = root->p;
 }
}

함수를 이용할 때

#include <stdio.h>
#include <stdlib.h>
typedef struct list {
 int d;
 struct list* p;
} LIST;
LIST* root = NULL;
LIST* last = NULL;
void AddList(int a){
 LIST* r = (LIST*)malloc(sizeof(LIST));
 r->d = a;
 r->p = NULL;
 if(root==NULL) root = r;
 else           last->p = r;
 last = r;
}
int main(void){
 AddList(35);
 AddList(40);
 AddList(45);
 while(root){
  printf("%d\n", root->d);
  root = root->p;
 }
}

# 2-1. 트리

![캡처](https://user-images.githubusercontent.com/50951220/68526272-5ac4c000-031d-11ea-987d-06f21e20b2cb.PNG)

 트리는 대용량의 자료를 다룰 때 효과적이다.(자료의 삽입, 삭제, 검색이 빠르다.)

# 2-2. 트리의 종류

 # 2진트리(Binary Tree)

 2진트리는 차수의 개수가 2개 이하인 트리를 말한다. 차수는 얼마든지 늘릴 수 있지만, 기본적으로 2진트리를 많이 사용한다.

 # Ternary Tree

 노드에 차일드가 3개씩 붙는 트리를 말한다. 

 # 트리의 순회 

트리의 순회는 재귀 방식을 사용한다. printf의 위치에 따라 3가지의 출력순서가 있다.

![캡처2](https://user-images.githubusercontent.com/50951220/68526420-1cc89b80-031f-11ea-8cdf-dff11ae6bf11.PNG)

# 2-3. 예시코드
	
#include <stdlib.h>               
typedef struct Tree {
    struct Tr *l, *r;
    int d;
} T;
void print(T* p){
   printf("%d\n", p->d);
   if(p->l) print(p->l);
   if(p->r) print(p->r);    
}
T* mem(){
 T* p=(T*)malloc(sizeof(T));
 p->l=p->r=NULL;
 return(p);
}
int main(void){
    T *r, *r1, *r2, *l1;
    l1= (T*)mem(); l1->d=3; 
    r2= (T*)mem(); r2->d=8; 
    r1= (T*)mem(); r1->d=7; r1->r=r2;
    r= (T*)mem(); r->d=5; r->l=l1;  r->r=r1;
    print(r);
}

# 3-1. 그래프 

 그래프는 실제 세계의 현상이나 사물을 정점(Vertex)와 간선(Edge)으로 표현을 하기 위해 사용한다.
그래프는 간단한 실생활에서 적용할 수 있고, 많은 알고리즘에 이용될 수 있다. 그래프는 최단거리 알고리즘(다익스트라, 벨만포드), 네트워크 플로우, 최소 스패닝 트리, DFS, BFS 등등에 이용된다. 

# 3-2. 그래프의 종류와 구현

 # 유향 그래프(Directed Graph) 
 ![캡처3](https://user-images.githubusercontent.com/50951220/68526641-9c576a00-0321-11ea-9159-c8d48a01cda7.PNG)
 
 정점 간의 간선이 방향이 존재할 경우
 # 무향 그래프(Undirected Graph)
 ![캡처4](https://user-images.githubusercontent.com/50951220/68526668-ca3cae80-0321-11ea-916b-ddeeeb37b1de.PNG)

 정점 간의 간선이 방향이 없을 경우
 
 # 3-3. 예시코드
 
#include <stdio.h>
#include <stdlib.h>
#include <memory.h>
typedef struct{
    int vn; 
    int **matrix;
} Graph;
Graph *NewGraph(int max_vertex);
void DeleteGraph(Graph *graph);
void AddEdge(Graph *graph, int start, int goal);
void ViewGraph(Graph *graph);
void ViewIndegree(Graph *g);
void ViewOutdegree(Graph *g);
int main(void)
{       
    Graph *graph;
    graph = NewGraph(6);
    AddEdge(graph, 0, 1);
    AddEdge(graph, 3, 1);
    AddEdge(graph, 2, 4);
    AddEdge(graph, 4, 2);
    ViewGraph(graph);
    ViewIndegree(graph); 
    ViewOutdegree(graph);  
    DeleteGraph(graph);
    return 0;   
}
Graph *NewGraph(int max_vertex)
{
    int i = 0;
    Graph *graph = (Graph *)malloc(sizeof(Graph));
    graph->vn = max_vertex;
    graph->matrix = (int **)malloc(sizeof(int *)*max_vertex);
    for (i = 0; i < max_vertex; i++)
    {
        graph->matrix[i] = (int *)malloc(sizeof(int)*max_vertex);
        memset(graph->matrix[i], 0, sizeof(int)*max_vertex);
    }
    return graph;
}
void DeleteGraph(Graph *graph)
{
    int i = 0;
    for (i = 0; i < graph->vn; i++)
    {
        free(graph->matrix[i])
    }
    free(graph->matrix);
    free(graph);
}
void AddEdge(Graph *graph, int start, int goal)
{
    graph->matrix[start][goal] = 1;
}
void ViewGraph(Graph *graph)
{
    int i =0;
    int j =0;
    for(i=0;i<graph->vn;i++)
    {
        printf("%d 에서 갈 수 있는 정점:",i);
        for(j=0;j<graph->vn;j++)
        {
            if(graph->matrix[i][j])
            {
                printf("%d ",j);
            }
        }
        printf("\n");
    }
}
void ViewIndegree(Graph *g)
{
    int i, j;
    int degree;
    printf("In-degree\n");
    for (i = 0; i < g->vn; i++)
    {
        degree = 0;
        for (j = 0; j < g->vn; j++)
        {
            if (g->matrix[j][i])
            {
                degree++;
            }
        }
        printf("%d ", degree);
    }
    printf("\n");
}
void ViewOutdegree(Graph *g)
{
    int i, j;
    int degree;
    printf("Out-degree\n");
    for (i = 0; i < g->vn; i++)
    {
        degree = 0;
        for (j = 0; j < g->vn; j++)
        {
            if (g->matrix[i][j])
            {
                degree++;
            }
        }
        printf("%d ", degree);
    }
    printf("\n");
}




 
