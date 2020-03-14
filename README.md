# migongzuoye
This is a migong
#include<stdio.h>
#define M 10 

struct P
{
    int x; 
    int y; 
};

int m[M][M],n,z = 10000; 

struct P b;
struct P d[4]={{0,1},{1,0},{0,-1},{-1,0}};

void Try(struct P c,int t)
{
    int i;
    struct P q;                                                
	// 下一个位置 
    for(i=0;i<=3;i++)                                         
	// 动方向,依次为东南西北;依次试探下左上右四个方向
    {
        q.x=c.x+d[i].x;
        q.y=c.y+d[i].y;

        if(m[q.x][q.y] == 0)                           
		// 是通路
        {
            m[q.x][q.y]=++t;
            if(q.x != b.x || q.y != b.y)            
			// 没到终点
                Try(q,t);                          
				// 试探下一点(递归调用)
            else
                z = z>t?t:z; 
            m[q.x][q.y]=0;                       
			// 恢复为通路，试探下一条路
            t--;
        }
    }
        return;
}

int main(void)
{
    struct P h;                             
	//起点
    int i,j;
    while(scanf("%d",&n)!=EOF)
        for(i=0;i<n;i++)
            for(j=0;j<n;j++)
                scanf("%d",*(m+i)+j);  
				//二维数组的指针调用
      
    h.x = 1,h.y=1;
    b.x = n-2,b.y= n-2;
    m[h.x][h.y]=2;
    Try(h,0);                      
	// 由第一步起点试探起
    if(z == 10000)
        printf("No solution");
    else
        printf("%d",z);
    return 0;
}
