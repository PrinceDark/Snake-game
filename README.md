/*# Snake-game
Simple snake game created with cpp language 
And only works on pc effectively */





#include <iostream>
#include<cstdlib>
#include<stdlib.h>
#include<conio.h>
#include<unistd.h>
using namespace std;
bool gameover;
const int width=20;
const int height=20;
int x,y,scorex,scorey,points;
int tailx[100],taily[100],n;
enum eDirecton {STOP=0,LEFT,RIGHT,UP,DOWN};
eDirecton dir;
char p;

//Here the setup for game is done ie. to give starting input
void Setup()
{
    gameover=false;
    dir=STOP;
    x=width/2;
    y=height/2;
    scorex=rand()%width;
    scorey=rand()%height;
    points=0;
}
//Here the drawing the border and fruit and snake is done
void Draw()
{int i,j,k;
 system("cls");
    for(i=0;i<width+2;i++)
       cout<<"#";
       cout<<endl;
     for(i=0;i<height;i++)
     {
         for(j=0;j<width;j++)
           {

                if(j==0)
                        {cout<<"#";}
              if(i==y&&j==x)
                     cout<<"O";
        else if(i==scorey&&j==scorex)
                       cout<<"x";
                      else
                      {
                             bool print=false;
                           for(k=0;k<n;k++)
                           {

                               if(tailx[k]==j&&taily[k]==i)
                               {

                                cout<<"o";
                               print=true;
                               }
                           }
                           if(!print)
                          cout<<" ";
                    }
                if(j==width-1)
                       {cout<<"#";}

            }
            cout<<endl;
     }

       for(i=0;i<width+2;i++)
       cout<<"#";
       cout<<endl;
       cout<<"points Obtained:"<<points<<endl;

}
//Here the  control of snake is done
void Input()
{
    if(_kbhit())
     switch(_getch())
    {case 'a':
        dir=LEFT;
        break;
    case 'd':
        dir=RIGHT;
        break;
     case 'w':
        dir=UP;
        break;
     case 's':
        dir=DOWN;
        break;
     case 'x':
        gameover=true;
        break;}
}
//Here every logic for tail increase or movement is done
void Logic()
{int prex,prex2,prey,prey2,i;
    prex=tailx[0];
    prey=taily[0];
    tailx[0]=x;
    taily[0]=y;
   for(i=1;i< n;i++)
    {
        prex2=tailx[i];
    prey2=taily[i];
    tailx[i]=prex;
    taily[i]=prey;
    prex=prex2;
    prey=prey2;
    }
    switch(dir)
    {
    case LEFT:
        x--;
        break;
    case RIGHT:
        x++;
        break;
    case UP:
        y--;
        break;
    case DOWN:
        y++;
        break;
    default:
        break;
    }
    //for classic section use this code
    if(x>width||y>height||y<0||x<0)
        gameover=true;
     //for moving through wall use this code
/*
                if(x>width)
                    x=0;
                  if(x<0)
                   x=width-1;
            if(y>height)
                    y=0;
                  if(y<0)
                   y=height-1;
*/
     for(int i=0;i<n;i++)
     {if (tailx[i]==x&&taily[i]==y)
        gameover=true;}
    if(x==scorex&&y==scorey)
     {
    points+=10;
     scorex=rand()%width;
    scorey=rand()%height;
    n++;
    }
}
int main()
{    again:
    Setup();

    while(!gameover)
    {
        Draw();
        Input();
        Logic();
        usleep(90000);     //For slowing down reaction time
    }
    cout<<"Do you want to PLAY AGAIN:"<<"(Y/N)"<<endl;
    cin>>p;
    if(p=='y')
    {
        goto again;
    }
    return 0;
}


