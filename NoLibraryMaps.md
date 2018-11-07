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
```
