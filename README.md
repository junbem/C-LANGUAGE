# 1-1. 리스트

 리스트는 데이터가 저장되어 있는 노드들이 포인더를 통하여 선형적으로 연결된 형태의 자료구조를 말한다. 리스트는 컴퓨팅에서 가장 근본이 되는 자료구조로써 스택, 큐, 배열과의 연관성 등에 활용된다. 배열에 비해서 리스트의 장점은 리스트를 구서아는 요소들이 기억장소에 연속적인 순서로 할당되어 있을 필요 없이 각각 독립적으로 존재할 수 있으므로 손쉽게 추가 및 제거될 수 있다느 것이고, 또한 이러한 작업이 리스트의 전체 구조에 영향을 주지 않는다는 점이다. 반면에, 리스트를 구성하는 노드들이 포인터를 통하여 상호 연결되어 있으므로 노드들의 추가/삭제 시 포인터의 상호 연결관계를 관리해야 하는 단점이 있다. 또한, 노드들을 검색할 때 무작위로 접근하지 못하고 처음부터 순서대로 포인터를 따라가며 탐색해야 하는 비효율성이 존재하다. 

# 1-2. 리스트의 종류 

Singly Linked List
 
 노드안에 링크가 1개이고 단방향으로 진행하는 리스트
 
Doubly Linked List

 노드안에 링크가 2개이고 양방향으로 진행할 수 있는 리스트
 
Circular Linked List

 마지막 노드가 첫번째 노드를 가르켜서 계속 회전할 수 있게 만들어진 리스트
 
 # 1-3. 예제코드
 
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
