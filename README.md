# Minesweeper
This is a Minesweeper in C++
With a fixed Size.
The Minesweeper was made for a shool Project.




Abgabeanforderung „Minesweeper“

Ein Konsolenprogramm „Minesweeper“ soll erstellt werden.
Die folgende Tabelle stellt die Anforderungen den entsprechenden Noten gegenüber

Ungenügend	- keine Abgabe
oder Abgabe erfolgt aber alles „geklaut“
oder: Keine Frage zur Abgabe kann beantwortet werden

mangelhaft	- Abgabe erfolgt, aber nicht kompilierbar.
- Abgabe erfolgt, kompilierbar, aber mit Mängeln gegenüber Anforderungskatalog „Ausreichend“
- Abgabe erfolgt, kompilierbar, Anforderungskatalog „Ausreichend“ (oder besser) aber keine Frage konnte korrekt beantwortet werden

ausreichend
	Grundanforderung:
- Das Spielfeld soll 10x10 Felder gross sein.
- es soll mit (genau)10 zufällig gesetzten Bomben gefüllt sein.
- es ist spielbar: also Eingabe der Koordinaten kann verarbeitet werden, und das Spielfeld wird neu gezeichnet,
- Das Programm ist kompilierbar, absturzfrei
- Die Fragen können inhaltlich evtl. mit kleinen Hilfen beantwortet werden

befriedigend	Grundanforderung wie bei „ausreichend“ plus zusätzlich:
- Die Zahlen sind korrekt gesetzt
- Bei einer „0“ werden zumindest alle 8 umliegenden Felder geöffnet ( auch wenn es dann nicht rekursiv weitergeht)
- Es wird mit Funktionen gearbeitet (also nicht: der ganze Text steht in einer main () Funktion)
- Alle Fragen können zu diesem Programm beantwortet werden

gut	Anforderungen wie bei „befriedigend“ plus zusätzlich:
- rekursives Öffnen wenn ein Feld mit einer „0“ gewählt wird.
- korrektes Erkennen der Gewinnsituation mit Programmende,
- Sie benutzen keine globalen Variablen (ausser den Feldern)
- Sie können auch ohne Fragen frei auf die wesentlichen Stellen des Programms hinweisen



sehr gut	Sie haben die Anforderungen im Sinne der Note „gut“ erfüllt und haben ein bedeutendes Zusatzfeature erarbeitet (Übererfüllung)  z.B : man kann bei ihnen die Bomben „markieren“ und wenn man alle 10 gefunden hat ist ebenfalls das Spielende erreicht.

Oder: Sie sehen eine dynamische Möglichkeit vor, die Spielfeldgröße und die Bombenzahl vor Spielbeginn eingeben zu können

Oder: Sie können den Spielernamen und die Zeit die benötigt wurde abspeichern – zumindest solange das Programm nicht beendet wird können dann Spieler „gegeneinander“ spielen,

oder Sie arbeiten mit Farben: 1 blau, 2 grün, 3 rot...

oder …(es muss ein erkennbarer Mehrwert erarbeitet werden)
