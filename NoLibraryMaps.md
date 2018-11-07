```C++
#include <iostream>
#include <conio.h>
using namespace std;
using namespace System;
void Dibujar_mapa(int **mapa)
{
	for (int i = 0; i<25; i++) //largo del mapa
	{
		for (int k = 0; k<80; k++) //ancho del mapa
		{
			if (mapa[i][k] == 1) //si la matriz i k tiene valor 1...
			{
				Console::SetCursorPosition(k, i); //poner el | en posición x, y.
				Console::ForegroundColor = ConsoleColor::Green; //asignar color al 1
				cout << char(219); //dibujar el simbolo █
			}
			if (mapa[i][k] == 2)
			{
				Console::SetCursorPosition(k, i);
				Console::ForegroundColor = ConsoleColor::DarkRed;
				cout << char(219);
			}
			if (mapa[i][k] == 3)
			{
				Console::SetCursorPosition(k, i);
				Console::ForegroundColor = ConsoleColor::Blue;
				cout << char(219);
			}
		}
	}
}
void borrar_personaje(int x, int y)
{
	Console::SetCursorPosition(x, y);
	cout << " ";
}
void dibujar_personaje(int x, int y)
{
	Console::SetCursorPosition(x, y);
	Console::BackgroundColor = ConsoleColor::Blue;
	Console::ForegroundColor = ConsoleColor::Yellow;
	cout << char(1);
}
void dibujarenemigo(int x2, int y2, int **Mapa)
{
	Console::SetCursorPosition(x2, y2);
	if (Mapa[y2][x2] == 3)
	{
		Console::BackgroundColor = ConsoleColor::Blue;
		Console::ForegroundColor = ConsoleColor::DarkMagenta;
		cout << char(1);
	}
	if (Mapa[y2][x2] == 2)
	{
		Console::BackgroundColor = ConsoleColor::DarkRed;
		Console::ForegroundColor = ConsoleColor::DarkMagenta;
		cout << char(1);
	}
	if (Mapa[y2][x2] == 1)
	{
		Console::BackgroundColor = ConsoleColor::Green;
		Console::ForegroundColor = ConsoleColor::DarkMagenta;
		cout << char(1);
	}
}
void borrarenemigo(int x2, int y2)
{
	Console::SetCursorPosition(x2, y2);
	cout << " ";
}
void moverenemigo(int &x2, int &y2, int &ex, int &ey,int **mapa)
{
	if ((x2 + ex) < 0 || (x2 + ex) > 79|| (mapa[y2][x2 + ex] == 2))
		ex = -ex;
	if ((y2 + ey) < 0 || (y2 + ey) > 24|| (mapa[y2][x2 + ex] == 2))
		ey = -ey;
	x2 = x2 + ex;
	y2 = y2 + ey;
	dibujarenemigo(x2, y2,mapa);
	_sleep(60);
	borrarenemigo(x2, y2);
}
void mover_personaje(int &x, int &y, int dx, int dy, int **mapa)
{
	dx = dy = 0;
	if (_kbhit())
	{
		char teclapresionada = _getch();
		teclapresionada = toupper(teclapresionada);
		switch (teclapresionada)
		{
		case 72: dy = -1; dx = 0; break;
		case 80: dy = 1; dx = 0; break;
		case 75: dx = -1; dy = 0; break;
		case 77: dx = 1; dy = 0; break;
		} //switch end
	}//if end
	if(x+dx<0||x+dx>79||(mapa[y][x+dx]==2))
	{
		dx = 0;dy = 0;x = 79;y = 6;
	} //if x end
	if(y+dy<0||y+dy>24|(mapa[y+dy][x]==2))
	{
		dy = 0;dx = 0;x = 69;y = 6;
	} //if y end 
	x = x + dx;
	y = y + dy;
	dibujar_personaje(x, y);
	_sleep(15);
	borrar_personaje(x, y);
}
void controlador(int &xpersonaje, int &ypersonaje, int dx, int dy, int **mapa, int ex, int ey, int &xenemigo, int &yenemigo)
{
	while (1)
	{	mover_personaje(xpersonaje, ypersonaje, dy, dy, mapa);
	moverenemigo(xenemigo, yenemigo, ex, ey,mapa);
	}
}

void menu(int &opcion)
{
	Console::SetCursorPosition(1, 0);
	cout << "ingrese opcion: ";
	cin >> opcion;
}

void main()
{
	Console::SetWindowSize(90, 35);
	Console::CursorVisible = false;
	int **mapa;
	int opcion, xpersonaje, ypersonaje, dx, dy, x, y, xenemigo, yenemigo, ey, ex, x2, y2;
	int x3, y3, ydisparo, xdisparo, disx, disy;
	int xenemigo2, yenemigo2, ey2, ex2, x4, y4;
	mapa = new int*[25];
	for (int i = 0; i<25; i++)
	mapa[i] = new int[80]; //matriz mapa creada
	xpersonaje = 70;
	ypersonaje = 6;
	xenemigo = 9;
	yenemigo = 11;
	disx = 1;
	disy = 0;
	dx = dy = 0;
	x2 = y2 = 10;
	ex = ey = 1;
	do
	{
		menu(opcion);
		Console::Clear();
		if (opcion != 6)
		{
			switch (opcion)
			{
		  	  case 1:
				  Mapa1(mapa); controlador(xpersonaje, ypersonaje, dx, dy, mapa, ex,  ey, xenemigo, yenemigo);dibujar_personaje(x, y);
				  break;
			  case 2:
				  Mapa2(mapa);controlador(xpersonaje, ypersonaje, dx, dy, mapa, ex, ey, xenemigo, yenemigo);dibujar_personaje(x, y);
				  break;
			  case 3:
				  Mapa3(mapa);controlador(xpersonaje, ypersonaje, dx, dy, mapa, ex, ey, xenemigo, yenemigo);dibujar_personaje(x, y); break;
			  case 4:
				  Mapa4(mapa);controlador(xpersonaje, ypersonaje, dx, dy, mapa, ex, ey, xenemigo, yenemigo);dibujar_personaje(x, y); break;
			  case 5:
				  Mapa5(mapa);controlador(xpersonaje, ypersonaje, dx, dy, mapa, ex, ey, xenemigo, yenemigo);dibujar_personaje(x, y); break;
			}
			_getch();
		}
	} while (opcion != 6);
	controlador(xpersonaje, ypersonaje, dx, dy, mapa, ex, ey, xenemigo, yenemigo);
	/*do
	{

	}*/
	for (int i = 0; i < 25; i++)
		delete[]mapa[i];
	delete[]mapa;
}
```
