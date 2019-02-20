#include "stdafx.h"
#include <iostream>
#include <string>
#include <ctime>
#include <stdlib.h>
//chrono für Zeitanzeige
#include <chrono>
//conio für press enter
#include <conio.h>
//folgende für highscore 
#include <fstream> //für speichern in Datei
#include <vector> 
#include <algorithm> //für sort
#include <sstream> //stringstream
#include <iomanip> //für setfill

using namespace std;
char brett[10][10];
char anzeigeBrett[10][10];
//vordeklarieren der Funktion für logischere Anordnung
void init(char initVal);
void bombe(int anz);
int bombenAnzahl();
int markierung();
int aufdecken(int xCord, int yCord);
int markierung(int xCord, int yCord);
int auswahl();
int spielerscore(int aufruf);
int check(int bombenAnzahl);
double zeitzähler(int first);
time_t start, ende;
int main();

void banner() {
	cout << R"(

   $$\      $$\ $$\                      $$$$$$\                                                                  
   $$$\    $$$ |\__|                    $$  __$$\                                                                
   $$$$\  $$$$ |$$\ $$$$$$$\   $$$$$$\  $$ /  \__|$$\  $$\  $$\  $$$$$$\   $$$$$$\   $$$$$$\   $$$$$$\   $$$$$$\ 
   $$\$$\$$ $$ |$$ |$$  __$$\ $$  __$$\ \$$$$$$\  $$ | $$ | $$ |$$  __$$\ $$  __$$\ $$  __$$\ $$  __$$\ $$  __$$\ 
   $$ \$$$  $$ |$$ |$$ |  $$ |$$$$$$$$ | \____$$\ $$ | $$ | $$ |$$$$$$$$ |$$$$$$$$ |$$ /  $$ |$$$$$$$$ |$$ |  \__|
   $$ |\$  /$$ |$$ |$$ |  $$ |$$   ____|$$\   $$ |$$ | $$ | $$ |$$   ____|$$   ____|$$ |  $$ |$$   ____|$$ |      
   $$ | \_/ $$ |$$ |$$ |  $$ |\$$$$$$$\ \$$$$$$  |\$$$$$\$$$$  |\$$$$$$$\ \$$$$$$$\ $$$$$$$  |\$$$$$$$\ $$ |      
   \__|     \__|\__|\__|  \__| \_______| \______/  \_____\____/  \_______| \_______|$$  ____/  \_______|\__|      
                                                                                    $$ |                          
                                                                                    $$ |                          
                                                                                    \__|                                                                                                                   
	)" << '\n';

}

void highscoreBanner() {
	cout << R"(

  $$\   $$\ $$\           $$\              $$$$$$\   $$$$$$\   $$$$$$\  $$$$$$$\  $$$$$$$$\ 
  $$ |  $$ |\__|          $$ |            $$  __$$\ $$  __$$\ $$  __$$\ $$  __$$\ $$  _____|
  $$ |  $$ |$$\  $$$$$$\  $$$$$$$\        $$ /  \__|$$ /  \__|$$ /  $$ |$$ |  $$ |$$ |      
  $$$$$$$$ |$$ |$$  __$$\ $$  __$$\       \$$$$$$\  $$ |      $$ |  $$ |$$$$$$$  |$$$$$\    
  $$  __$$ |$$ |$$ /  $$ |$$ |  $$ |       \____$$\ $$ |      $$ |  $$ |$$  __$$< $$  __|   
  $$ |  $$ |$$ |$$ |  $$ |$$ |  $$ |      $$\   $$ |$$ |  $$\ $$ |  $$ |$$ |  $$ |$$ |      
  $$ |  $$ |$$ |\$$$$$$$ |$$ |  $$ |      \$$$$$$  |\$$$$$$  | $$$$$$  |$$ |  $$ |$$$$$$$$\ 
  \__|  \__|\__| \____$$ |\__|  \__|       \______/  \______/  \______/ \__|  \__|\________|
                $$\   $$ |                                                                  
                \$$$$$$  |                                                                  
                 \______/                                                                   
                                                                                                        
	)" << '\n';

}

//clear 
void clear() {
	//schiebt 50 Felder nach unten
	//cout << string(50, '\n');

	//windows spezifisch
	system("cls");
}

void weiter() 
{
	//
	cout << "Press Enter to Continue..." <<endl << flush;
	_getch();
}

//Bombenanzahl definieren
int bombenAnzahl() {
	int defAnzahl = 0;
	while (defAnzahl <= 5) {
		cout << "Wieviele Bomben sollen gelegt werden?" << endl;
		cin >> defAnzahl;
		if (defAnzahl <= 5) { cout << "Bombenanzahl muss ueber 5 sein!" << endl; }
	}
	// Bei über 50 Bomben wird die Anzahl der Bomben von der maximal Anzahl abgezogen 
	if (defAnzahl > 50) {
		//übergibt an init dass alle Felder erstmal als Bomben deklariert werden, da Bomben anzahl über 50
		//die Bombenanzahl wird an func. bombe übergeben 
		init('X');
		bombe(100 - defAnzahl);
	}
	else
	{
		init(48);
		//die Bombenanzahl wird an func. bombe übergeben 
		bombe(defAnzahl);
	}
	return defAnzahl;
}


// initialisieren ob brett 0 oder X gefüllt ist, je nachdem über oder unter 50 Bomben
void init(char initVal) {
	for (int a = 0; a < 10; a++)
	{
		for (int b = 0; b < 10; b++) {
			brett[a][b] = initVal;
			anzeigeBrett[a][b] = 35;
		}
	}
}

// setzt die Bomben
void bombe(int anz) {
	srand(time(NULL));
	int counta = 0;

	for(int a = 0; a < 10; a++)
	{
		for (int b = 0; b < anz; b++) {
			while (counta < anz) {
				int rnd1 = rand() % 10 + 0;
				int rnd2 = rand() % 10 + 0;
				// wenn über fünfzig Bomben werden alle Felder auf X gesetzt, logische abfrage ob Arrayfeld 0 0 auf 5 ist
				if (brett[0][0] == 'X'){
					//Alle Felder sind erstmal Bomben und freie Felder werden gesetzt
					if (brett[rnd1][rnd2] == 'X') {
						brett[rnd1][rnd2] = 48;
						counta++;
					}
				}
				else
				{
					if (brett[rnd1][rnd2] == 48) {
						brett[rnd1][rnd2] = 'X';
						counta++;
					}
				}
			}
		}


	}
}

//setz die Zahlen um das X
int markierung(){
	
	for (int a = 0; a < 10; a++)
	{
		
		for (int b = 0; b < 10; b++) {
			if (brett[a][b] == 'X')
			{
				if (brett[a][b+1] != 'X' && b+1 <= 9)
				{
					brett[a][b+1]++;
				}
				if (brett[a][b-1] != 'X' && b-1 >= 0)
				{
					brett[a][b-1]++;
				}
				if (brett[a+1][b] != 'X')
				{
					brett[a+1][b]++;
				}
				if (brett[a-1][b] != 'X')
				{
					brett[a-1][b]++;
				}
				if (brett[a-1][b+1] != 'X' && b+1 <= 9)
				{
					brett[a-1][b+1]++;
				}
				if (brett[a-1][b-1] != 'X' && b-1 >= 0)
				{
					brett[a-1][b-1]++;
				}
				if (brett[a+1][b+1] != 'X' && b+1 <= 9)
				{
					brett[a+1][b+1]++;
				}
				if (brett[a+1][b-1] != 'X' && b-1 >= 0)
				{
					brett[a+1][b-1]++;
				}
			}
		}
	}

	return 0;
}

int auswahl() {
	int xCord = 0;
	int yCord = 0;
	int funktionsWahl;
	char oeffnenAbfrage;

	cout << "Waehlen!" << endl;
	cout << "Eingabe X Koordinate:";
	cin >> xCord;
	cout << "Eingabe y Koordinate:";
	cin >> yCord;

	cout <<endl << "Was moechtest du tun?" << endl << "Aufdecken: Druecke 1" << endl << "Markieren: Druecke 2" << endl;
	cin >> funktionsWahl;
	cout << endl;
	//prüfen ob feld schon ausgewählt ist
	if (anzeigeBrett[xCord][yCord] == 35 || anzeigeBrett[xCord][yCord] == 63) {

		if (funktionsWahl == 1)
		{
			if (anzeigeBrett[xCord][yCord] == 63)
			{
				cout << "Das Feld ist markiert Wirklich oeffnen?(J|N)" << endl;
				cin >> oeffnenAbfrage;
				if (oeffnenAbfrage == 'j' || oeffnenAbfrage == 'J')
				{
					aufdecken(xCord, yCord);
				}
			};
			if (anzeigeBrett[xCord][yCord] != 63)
			{
				aufdecken(xCord, yCord);
			};

		}
		if (funktionsWahl == 2)
		{
			markierung(xCord, yCord);
		}
	}
	else
	{
		cout << "Das Feld ist bereits geoeffnet" <<endl;
		auswahl();
	}
	

	return 0;
}

//rekursives aufdecken; geht jeweils jede möglichkeit durch kopiert ind spielbrett.
int aufdecken(int xCord, int yCord) {
	if (brett[xCord][yCord] == 'X') {
		anzeigeBrett[xCord][yCord] = brett[xCord][yCord];
	}

	if (brett[xCord][yCord] > 48 && brett[xCord][yCord] < 88) {
		anzeigeBrett[xCord][yCord] = brett[xCord][yCord];
	}

	if (brett[xCord][yCord] == 48) {

		anzeigeBrett[xCord][yCord] = brett[xCord][yCord];

		if (xCord + 1 <= 9 && brett[xCord + 1][yCord] < 88 && anzeigeBrett[xCord + 1][yCord] == 35) {
			aufdecken(xCord + 1, yCord);
		}
		if (xCord - 1 >= 0 && brett[xCord - 1][yCord] < 88 && anzeigeBrett[xCord - 1][yCord] == 35) {
			aufdecken(xCord - 1, yCord);
		}
		if (yCord + 1 <= 9 && brett[xCord][yCord + 1] < 88 && anzeigeBrett[xCord][yCord + 1] == 35) {
			aufdecken(xCord, yCord + 1);
		}

		if (yCord - 1 >= 0 && brett[xCord][yCord - 1] < 88 && anzeigeBrett[xCord][yCord - 1] == 35) {
			aufdecken(xCord, yCord - 1);
		}

		if (xCord - 1 >= 0 && yCord - 1 >= 0 && brett[xCord - 1][yCord - 1] < 88 && anzeigeBrett[xCord - 1][yCord - 1] == 35) {
			aufdecken(xCord - 1, yCord - 1);
		}

		if (xCord - 1 > -1 && yCord + 1 < 10 && brett[xCord - 1][yCord + 1] < 88 && anzeigeBrett[xCord - 1][yCord + 1] == 35) {
			aufdecken(xCord - 1, yCord + 1);
		}
		if (xCord + 1 < 10 && yCord - 1 > -1 && brett[xCord + 1][yCord - 1] < 88 && anzeigeBrett[xCord + 1][yCord - 1] == 35) {
			aufdecken(xCord + 1, yCord - 1);
		}
		if (xCord + 1 < 10 && yCord + 1 < 10 && brett[xCord + 1][yCord + 1] < 88 && anzeigeBrett[xCord + 1][yCord + 1] == 35) {
			aufdecken(xCord + 1, yCord + 1);
		}
	}


	return 0;
}

int markierung(int xCord, int yCord) {
	anzeigeBrett[xCord][yCord] = 63;

	return 0;
}

int anzeige(int last = 0) {
	int cordix = 0;
	int cordiy = 0;
	for (int a = 0; a < 10; a++)
	{
		if (cordiy == 0) {
			cout << "	";
			for (cordiy = 0; cordiy < 10; cordiy++) {
				//koordinaten ausgabe y
				cout << "  " << cordiy << "  ";

			}
			cout << endl << endl << endl<<endl;
		}
		//koordinaten ausgabe x an for schleife gebunden der den zähler erhöht
		cout << cordix << "	";

		for (int b = 0; b < 10; b++) {
			if (last == 1) {
				cout << "  " << brett[a][b] << "  ";
			}
			else {
				cout << "  " << anzeigeBrett[a][b] << "  ";
			}
		}
		cordix++;
		cout << endl << endl;

	}
	return 0;
}

//prüft ob alles gelößt wurde
int check(int bombenAnzahl) {
	int winCount = 0;
	
	//Schleife geht alle Felder durch
	for (int a = 0; a < 10; a++)
	{
		for (int b = 0; b < 10; b++) {
			
			if (anzeigeBrett[a][b] == 'X')
			{
				cout << endl << "Du hast Verloren" << endl << endl;
				return 1;
			}
			if (anzeigeBrett[a][b] != 35)
			{
				winCount++;
			}
			//prüftmarkierung
			if (anzeigeBrett[a][b] == 63 && brett[a][b] == 'X')
			{
				winCount++;
			}
		}
	}
	if (winCount == 100 - bombenAnzahl) { 
		cout << endl << "Du hast Gewonnen" << endl;
		return 2; 
	}
	
	return 0;
}

double zeitzähler(int first) {
	
	//erster aufruf in mainteil zum abrufen der Starzeit
	if (first == 1)
	{
		time(&start);
	}
	///ende und errechnung der Enzeit
	if (first == 2)
	{
		time(&ende);
		double dif = difftime(ende, start);
		cout << "Spielzeit: " << dif << " Sekunden" << endl << endl;
	}
	//wird für highscore in spielscore aufgerufen
	if (first == 3)
	{
		double dif = difftime(ende, start);
		return dif;
	}
	return 0;
}

int spielerscore(int gewonnen) {
	//nur fragen wenn gewonnen
	if (gewonnen == 2)
	{
	string name;
	char speichern;
	cout << endl << "Gut gemacht!!" << endl;
	cout << endl << "Highscore Speichern?(J|N)" << endl;
	cin >> speichern;

	//speichern in datei
	if (speichern == 'j' || speichern == 'J') 
	{
		//zeit aus zeitzähler funktion die drei holt sich den wert aus if abfrage von zeitzähler
		double saveTime = zeitzähler(3);

		ofstream outfile;
		//ios = append
		outfile.open("highscore.dat", ios_base::app);
		cout << endl << "Name eingeben:" << endl;
		cin >> name;
		//stringstream für das anhängen einer null wenn kleiner 10
		stringstream ss;
		ss << setfill('0') << setw(2) << saveTime;
		//output in datei 
		outfile << ss.str()<< "|Sekunden|" << name << endl;
		outfile.close();
	}
	}
	return 0;
}

//Highscore anzeigen mit sortier algorythmus
int highscore()
{
	cout << endl << "Highscore:" << endl<< endl;
	//declariert den vector
	vector<string> sV;
	//holt den inhalt aus highscore.dat
	ifstream infile("highscore.dat");
	//deklaiert word
	string word = "";

	while (infile >> word) {
		sV.push_back(word);
	}
	//sortiert
	sort(sV.begin(), sV.end());
	//gibt aus
	for (int i = 0; i < sV.size(); i++)
		cout << sV[i] << endl;
	return 0;
}

int nochmal() {
	char auswahl;
	cout << endl << "Nochmal Spielen?(J|N)" << endl;
	cin >> auswahl;
	if (auswahl == 'j' || auswahl == 'J') 
	{
		//clear für neustart
		clear();
		//recursives öffnen des main teils
		main();
	}
	return 0;
}



//*	##########################################################################################################################														
int main()
{
	banner();
	weiter();
	//muss für 2. while schleife auf 0 gesetzt werden
	int lost_win = 0;
	//Abfrage wieviele Bomben gelegt werden sollen
	int bombenAnzahlInt = bombenAnzahl();

	cout << endl;
	//setzt marikierungen um die bombe
	markierung();
	clear();
	//Beginn Zeitzähler
	zeitzähler(1);
		

	//schleife die beendet wird, wenn alle freien felder gefunden wurden oder Bombe erwischt
	while (lost_win == 0) {
		lost_win = check(bombenAnzahlInt);
		//if da sonst abfrage erscheint auch bei verloren oder gewonnen
		if (lost_win == 0)
		{
			zeitzähler(2);
			anzeige();
			auswahl();
			clear();
		}
	}

	//ende Zeitzähler
	zeitzähler(2);
	//nochmalige anzeige des Spielfelds für vergleich
	anzeige(1);
	weiter();
	clear();
	spielerscore(lost_win);
	clear();
	highscoreBanner();
	highscore();

	//abfrage nochmal spielen
	nochmal();	
}
