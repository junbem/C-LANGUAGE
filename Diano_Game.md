```c
#include <stdio.h>
#include <stdbool.h>
#include <windows.h>
#include <conio.h>
#include <time.h>
#define DINO_BOTTOM_Y 12
#define TREE_BOTTOM_Y 20
#define TREE_BOTTOM_X 45
//콘솔 창의 크기와 제목을 지정하는 함수
void SetConsoleView()
{
    system("mode con:cols=100 lines=25");
    system("title Google Dinosaurs. By BlockDMask");
}
// 게임 시작화면 만들어주기
void GameStartTitle()
{
    int x = 18;
    int y = 8;
    GotoXY(x, y + 1);
    printf("========== Dino Game ==========");
    GotoXY(x-16, y +14);
    printf("z를 누르면 시작, q를 누르면 종료");
    while (true) {
        char key = GetKeyDown();
        if (key == 'z')
        {
            break;
        }
        if (key == 'q') {
            exit(1);
        }
        Sleep(60);
    }
}

//커서의 위치를 x, y로 이동하는 함수
void GotoXY(int x, int y)
{
    COORD Pos;
    Pos.X = 2 * x;
    Pos.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), Pos);
}
//키보드의 입력을 받고, 입력된 키의 값을 반환하는 함수
int GetKeyDown()
{
    if (_kbhit() != 0)
    {
        return _getch();
    }
    return 0;
}
// 공룡 형상화하기
void DrawDino(int dinoY)
{
    GotoXY(0, dinoY);
    static bool legFlag = true;
    printf("        $$$$$$$ \n");
    printf("       $$ $$$$$$\n");
    printf("       $$$$$$$$$\n");
    printf("$      $$$      \n");
    printf("$$     $$$$$$$  \n");
    printf("$$$   $$$$$     \n");
    printf(" $$  $$$$$$$$$$ \n");
    printf(" $$$$$$$$$$$    \n");
    printf("  $$$$$$$$$$    \n");
    printf("    $$$$$$$$    \n");
    printf("     $$$$$$     \n");
    if (legFlag)
    {
        printf("     $    $$$    \n");
        printf("     $$          ");
        legFlag = false;
    }
    else
    {
        printf("     $$$  $     \n");
        printf("          $$    ");
        legFlag = true;
    }
}
//장애물 나무 3개 형상화하기
void DrawTree(int treeX, int tree_num)
    if (tree_num == 1)
    {
        GotoXY(treeX, TREE_BOTTOM_Y);
        printf("$$$$");
        GotoXY(treeX, TREE_BOTTOM_Y + 1);
        printf(" $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 2);
        printf(" $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 3);
        printf(" $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 4);
        printf(" $$ ");
    }
  else if (tree_num == 2)
    {
        GotoXY(treeX, TREE_BOTTOM_Y);
        printf("$$$$$$$$$$$");
        GotoXY(treeX, TREE_BOTTOM_Y + 1);
        printf(" $$     $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 2);
        printf(" $$     $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 3);
        printf(" $$     $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 4);
        printf(" $$     $$ ");
    }
  else if (tree_num == 3)
    {
        GotoXY(treeX, TREE_BOTTOM_Y-2);
        printf("$$$$");
        GotoXY(treeX, TREE_BOTTOM_Y - 1);
        printf(" $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y);
        printf(" $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 1);
        printf(" $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 2);
        printf(" $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 3);
        printf(" $$ ");
        GotoXY(treeX, TREE_BOTTOM_Y + 4);
        printf(" $$ ");
    }
}
// 공룡의 점프 기능 
void Jump(int* dinoY, int gravity) {
    char key = GetKeyDown();
    if (key == 'z')
    {
        *dinoY -= gravity;
    }
    else if (key == 'x')
    {
        *dinoY += gravity;
    }
}
// 충돌 했을 때 게임오버 화면을 출력하기
void DrawGameOver(const int score)
{
    system("cls");
    int x = 18;
    int y = 8;
    GotoXY(x, y);
    printf("===========================");
    GotoXY(x, y + 1);
    printf("======G A M E O V E R======");
    GotoXY(x, y + 2);
    printf("===========================");
    GotoXY(x, y + 5);
    printf("SCORE : %d", score);

    printf("\n\n\n\n\n\n\n\n\n");
    system("pause");
}
//충돌 했으면 true, 아니면 false
bool isCollision(const int treeX, const int dinoY)
{
    //트리의 X가 공룡의 몸체 쪽에 있을 때 
   //공룡의 높이가 충분하지 않다면 충돌로 처리
    GotoXY(0, 0);
    printf(＂treeX : %d, dinoY : %d＂, treeX, dinoY); 
// 이런식으로 적절한 X, Y를 찾습니다.
    if (treeX <= 8 && treeX >= 4 &&
        dinoY > 8)
    {
        return true;
    }
    return false;
}
int main()
{
    SetConsoleView();
    GameStartTitle(); // 위에서 만든 함수 출력
     while (true)        //게임 루프
      {
        //게임 시작 시 초기화 
        bool isJumping = false;
        bool isBottom = true;
        const int gravity = 3;
        int speed = 1;
        int dinoY = DINO_BOTTOM_Y;
        int treeX = TREE_BOTTOM_X;
        int tree_num = 1;
        srand(time(NULL));
        int score = 0;
        clock_t start, curr;    //점수, 변수 초기화
        start = clock();        //시작시간 초기화
        while (true)    // 한 판에 대한 루프
        {
            if (isCollision(treeX, dinoY))
                break;
            jump(&dinoY, gravity);
            // 배경 움직이게 하기 
            treeX -= speed;
            if (treeX <= 0)
            {
                treeX = TREE_BOTTOM_X;
                tree_num = rand() % 3 + 1;
            }
            if (score >= 10)
            {
                speed = (int)score / 5;
            }
            // 5초마다 속도가 증가한다
            if (dinoY <= 3)
            {
                isJumping = false;
            }
            GotoXY(22, 0);  // 공룡 그리기
            printf("Score : %d ", score);   //장애물 그리기
            curr = clock();            // 현재 시간 받아오기
           if (((curr - start) / CLOCKS_PER_SEC) >= 1) // 1초가 넘었을때
           {
                score++; // 스코어 증가
                start = clock();    // 시작시간 초기화
            }
            Sleep(60);
            system("cls");    //clear

            // 점수 출력을 1초마다 해주는것이 아니라 항상 출력해주면서, 1초가 지났을 때 증가한다.
            GotoXY(22, 0); // 커서를 가운데 위쪽으로 옮긴다.
                               // 콘솔창이 cols=100이니까 2*x이므로 22 정도 넣어준다.
            printf("Score : %d ", score);    //?점수출력
        }

        // 게임 오버 화면 출력
        DrawGameOver(score);
    }
    return 0;
}
```

오픈 소스 코드입니다.
사용 후 피드백해줄 내용은 댓글을 통해 받겠습니다.


            












