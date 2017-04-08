# reversi

//Class_Game.h

#include <iostream>
#include <conio.h>

using namespace std;

class Game
{
private:
	int Size;
	int **pole;
	int game1, game2;
	bool Winers;
	bool hod[8];
	bool prov;
	bool win;
public:
	Game(int);
	bool provHod(int, int, int);
	bool GetWIners();
	void SetWiners(bool);
	void PrintPole();
	void Result();
	void Hod1();
	void II();
	void run();
};

//Class_Game.cpp

#include <iostream>
#include <conio.h>
#include <cstdlib>
#include <ctime>
//#include "Class_Game.h"

using namespace std;

Game::Game(int _size)
{
	Size = _size;
	game1 = 0,game2 = 0;
	pole = new int *[_size];
	 for(int i = 0; i < _size; i++)
		  pole[i] = new int [_size];
	 for(int i(0); i < Size; i++){
		for(int j(0); j < Size; j++){
			pole[i][j] = 0;
		}
	 }
	 pole[2][2] = 1;
	 pole[2][3] = 2;
	 pole[3][2] = 2;
	 pole[3][3] = 1;	
}

bool Game::GetWIners()
{
	return Winers;
}

void Game::SetWiners(bool _Winers)
{
	Winers = _Winers;
}

void Game::PrintPole()
{
	for(int h(0); h < 79;h++)
		cout << "-";
	cout << endl << "\t\t" << "   ";
	for(int h(0); h < Size;h++)
		cout << h << " ";
	cout << endl << "\t\t + ";
	for(int h(0); h < Size;h++)
		cout << "- ";
	cout << "+" << endl;
	for(int i(0); i < Size; i++)
			{
				cout<< "\t\t" << i << "| ";
				for(int j(0); j < Size; j++)
				{
					if(pole[i][j] == 0) cout << "  ";
					if(pole[i][j] == 1) cout << "O ";
					if(pole[i][j] == 2) cout << "X ";
				}
				cout << "|" << endl;
			}
	cout << " \t\t + ";
	for(int h(0); h < Size;h++)
		cout << "- ";
	cout << "+" << endl;
	for(int h(0); h < 79;h++)
		cout << "-";
	cout << endl << endl;
}

bool Game::provHod(int i,int j,int figur)
{
	bool hod1 = false;
	win = false;
	pole[i][j] = figur;
		int counter = 1;
		for(int k(i+1); k < Size; k++)//вниз                                                                  +
		{
			if(pole[i][j] == pole[i+1][j])
			{
				hod[0] = false;
				break;
			}
			if(pole[i+1][j]==0)break;
			if(pole[i][j] == pole[k][j])
			{
				for(int p(1);p <= counter; p++)
					pole[k-p][j] = figur;
				win=true;
				hod[0] = true;
				break;
			}
			else
			{
				counter++;
				hod[0] = false;
			}
		}
		counter = 1;
		for(int k(i-1); k >= 0; k--)//вверх                                                                 +
		{
			if(pole[i][j] == pole[i-1][j])
			{
				hod[1] = false;
				break;
			}
			if(pole[i-1][j]==0)break;
			if(pole[i][j] == pole[k][j])
			{
				for(int p(1);p <= counter; p++)
					pole[k+p][j] = figur;
				win=true;
				hod[1] = true;
				break;
			}
			else
			{
				counter++;
				hod[1] = false;
			}
		}
		counter = 1;
		for(int k(j+1); k < Size; k++)//вправо                                                                 +
		{
			if(pole[i][j] == pole[i][j+1])
			{
				hod[2] = false;
				break;
			}
			if(pole[i][j+1]==0)break;
			if(pole[i][j] == pole[i][k])
			{
				for(int p(1);p <= counter; p++)
					pole[i][k-p] = figur;
				win=true;
				hod[2] = true;
				break;
			}
			else
			{
				counter++;
				hod[2] = false;
			}
		}
		counter = 1;
		for(int k(j-1); k >= 0; k--)//влево                                                                  +
		{
			if(pole[i][j] == pole[i][j-1])
			{
				hod[3] = false;
				break;
			}
			if(pole[i][j-1]==0)break;
			if(pole[i][j] == pole[i][k])
			{
				for(int p(1);p <= counter; p++)
					pole[i][k+p] = figur;
				win=true;
				hod[3] = true;
				break;
			}
			else
			{
				counter++;
				hod[3] = false;
			}
		}
		counter = 1;
		for(int k(i-1), t(j-1); k >= 0 && t >= 0; k--,t--)//диг. вверх влево                                 +
		{
			if(pole[i][j] == pole[i-1][j-1])
			{
				hod[4] = false;
				break;
			}
			if(pole[i-1][j-1]==0)break;
			if(pole[i][j] == pole[k][t])
			{
				for(int p(1);p <= counter; p++)
					pole[k+p][t+p] = figur;
				win=true;
				hod[4] = true;
				break;
			}
			else
			{
				counter++;
				hod[4] = false;
			}
		}
		counter = 1;
		for(int k(i-1), t(j+1); k >= 0 && t < Size; k--, t++)//диг. верх вправо                                +
		{
			if(pole[i][j] == pole[i-1][j+1])
			{
				hod[5] = false;
				break;
			}
			if(pole[i-1][j+1]==0)break;
			if(pole[i][j] == pole[k][t])
			{
				for(int p(1);p <= counter; p++)
					pole[k+p][t-p] = figur;
				win=true;
				hod[5] = true;
				break;
			}
			else
			{
				counter++;
				hod[5] = false;
			}
		}
		counter = 1;
		for(int k(i+1), t(j-1); k < Size && t >= 0; k++, t--)//диг. вниз влево                                   +
		{
			if(pole[i][j] == pole[i+1][j-1])
			{
				hod[6] = false;
				break;
			}
			if(pole[i+1][j-1]==0)break;
			if((k) != 6 && (t) >= 0 && pole[i][j] == pole[k][t])
			{
				for(int p(1);p <= counter; p++)
					pole[k-p][t+p] = figur;
				win=true;
				hod[6] = true;
				break;
			}
			else
			{
				counter++;
				hod[6] = false;
			}
		}
		counter = 1;
		for(int k(i+1), t(j+1); k < Size && t < Size; k++, t++)//диг. вниз вправо                                  +
		{
			if(pole[i][j] == pole[i+1][j+1])
			{
				hod[7] = false;
				break;
			}
			if(pole[i+1][j+1]==0)break;
			if(pole[i][j] == pole[k][t])
			{
				for(int p(1);p <= counter; p++)
					pole[k-p][t-p] = figur;
				win=true;
				hod[7] = true;
				break;
			}
			else
			{
				counter++;
				hod[7] = false;
			}
		}
		
		if(win == false && figur == 2)
		{
			cout << "Сюда ставить нельзя\nповторите ввод: ";
			pole[i][j] = 0;
		}
		if(win == false && figur == 1)
		{
			pole[i][j] = 0;
		}
		if(hod[0] == true||hod[1] == true||hod[2] == true||hod[3] == true||hod[4] == true||hod[5] == true||hod[6] == true||hod[7] == true)
			hod1 = true;
		//else hod1 = false;
		return hod1;
}

void Game::Hod1()
{
	int i,j;
	cout << "Введите ячейку (Х): ";
	bool hod2 = false;
	for(int n(0); n < 8; n++)
		hod[n] = NULL;
	do
	{
		do
		{
			cin >> i >> j;
			if(i < Size && i >= 0 && j < Size && j >= 0) 
				prov = true;
			else
			{
				cout << "Одни из параметров больше или меньше размера поля\nПовторите ввод: ";
				prov = false;
			}
			if(pole[i][j]==1||pole[i][j]==2){
				cout << "Эта ячейка занята!!!\nПовторите ввод: ";
				prov = false;
			}
			
		}
		while(!prov);
		hod2 = provHod(i , j , 2);
	}while(hod2!=true);
}

void Game::II()
{
	int i,j;
	cout << "Ход компьтера, ждите";
	bool hod2 = false;
	for(int n(0); n < 8; n++)
		hod[n] = NULL;
	do
	{
			for(i = 0; i < Size; i++){
				for(j = 0; j < Size; j++)
				{
					if(pole[i][j]==1||pole[i][j]==2)
					{
						prov = false;
					}
					else hod2 = provHod(i , j , 1);
					if(hod2 == true)
						break;
				}
				if(hod2 == true)
					break;
			}
	}while(hod2!=true);
}

void Game::Result()
{
	int counter = 0;
	game1 = 0;
	game2 = 0;
	for(int i(0); i < Size; i++)
	{
		for(int j(0); j < Size; j++)
		{
			if(pole[i][j] == 0)
				counter++;
		}
	}
	for(int i(0); i < Size; i++)
	{
		for(int j(0); j < Size; j++)
		{
			if(pole[i][j] == 1) game2++;
			if(pole[i][j] == 2) game1++;
		}
	}
	if(game1 == 0)
	{
		SetWiners(true);
		cout << "Победил компьютер (О)!!!" << endl;
	}
	if(game2 == 0)
	{
		SetWiners(true);
		cout << "Победил игрок (Х)!!!" << endl;
	}
	if(counter == 0)
	{
		SetWiners(true);
		if(game1 > game2) cout << "Победил игрок (Х)!!!" << endl;
		else cout << "Победил компьютер (О)!!!" << endl;
		if(game1 == game2)
			cout << "Ничья!!!" << endl;
	}
	cout << "+--------------------------------------------------+" << endl;
	cout << "| Игрок (Х): " << game1 << endl; 
	cout << "| Компьтер (О): " << game2 << endl;
	cout << "+--------------------------------------------------+" << endl;
}

void Game::run()
{
	SetWiners(false);
	for( ; ; )
	{
		Result();
		if(GetWIners() == true)
			break;
		PrintPole();
		Hod1();
		system("cls");
		Result();
		if(GetWIners() == true)
			break;
		PrintPole();
		II();
		_sleep(100);
		system("cls");
	}
}

//Main.cpp

#include <iostream>
#include <conio.h>
#include "Class_Game.h"

using namespace std;

const int size = 6;

int main()
{
	setlocale(LC_ALL,"rus");
	Game game(size);
	game.run();
	cout << "Игра окончена";
	_getch();
	return 0;
}
