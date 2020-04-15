
# snake
snake
#include<conio.h>
#include<cstdio>
#include<time.h>
#include<windows.h>
#define SIZE 20
int map[SIZE][SIZE]={0};
void drawMap(int map[][SIZE]);
void food();
void init();
int top_x,top_y,top_num=1,lenshe=1;
void she(int x,int y);
void findxy(int num,int can);
void she(int x,int y,int can)
{
	map[x][y]=can;
}
void move(int cz)
{
	switch(cz)
	{
		case 'w':top_x--;break;
		case 's':top_x++;break;
		case 'a':top_y--;break;
		case 'd':top_y++;break;
	}
	if(map[top_x][top_y]==-1)
	{
		she(top_x,top_y,top_num);
		lenshe++;
		food();
	}
	else
	{
		she(top_x,top_y,top_num);
		findxy(top_num-lenshe,0);
	}
	top_num++;
} 
void findxy(int num,int can)
{
	for(int i=0;i<SIZE;i++)
	for(int j=0;j<SIZE;j++)
	if(map[i][j]==num)
	map[i][j]=can;
}
void food()
{
	map[rand()%SIZE][rand()%SIZE]=-1;
}
void init()
{
	top_x=rand()%SIZE;
	top_y=rand()%SIZE;
	map[top_x][top_y]=top_num++;
}
int main()
{
	srand((int)time(NULL));
	init();
	food();
	drawMap(map);
	while(1)
	{
		move(getche());
		system("cls");
		drawMap(map);
	}
}
void drawMap(int map[][SIZE])
{
	int i,j;
	for(i=0;i<2+SIZE;i++)
	printf("+");
	printf("\n");
	for(i=0;i<SIZE;i++)
	{
		printf("+");
		for(j=0;j<SIZE;j++)
		{
		switch(map[i][j])
		{
			case -1:printf("#");break;
			case 0:printf(" ");break;
			default:printf("*");break;
		}
	    }
	    printf("+\n");
	}
	for(i=0;i<2+SIZE;i++)
	printf("+");
	printf("\n(英文输入法操作)wasd控制移动\n蛇的长度:%d\n",lenshe);
}
