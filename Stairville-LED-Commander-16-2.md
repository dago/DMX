# Stairville LED Commander 16/2

Verbesserungsvorschläge:
* Ausschließen von Kanälen bei "Full On". Dies ist wichtig, da sonst z.B. bei gemappetem Strobe die Scheinwerfer Blitzen
  statt gleichmäßig zu leuchten.
  Idee: Während des "Patch/Clear" Modus auf einem Kanal 3 Sekunden drücken von "Full On" nimmt den Kanal rein bzw. raus
  bei "Full On", Anzeige durch "F" neben dem Kanal (also analog zum Master-Mode)
* Werte setzen für AUX1 und AUX2. Zurzeit gibt es bei AUX1 und AUX2 nur die Werte 0 und 255. Der Wert bei eingeschaltetem
  AUX sollte sich setzen lassen um z.B. den Ausstoß der Nebelmaschine zu kontrollieren. Bedienung im Patch-Modus über
  die Value-Tasten neben dem Display zur Änderung des Wertes.
* Mappen das Joysticks ermöglichen. Der Joystick reagiert auf Druck wie ein Taster. Es wäre schön, wen der genau wie die Flash-
  Tasten gemappt werden könnte
* Chases parallel laufen lassen. Wenn der ein Chase-Knopf 3 Sekunden gedrückt wird dann läuft der Chase parallel zu
  den anderen. Dies ist nützlich, wenn man Chases modular gestaltet und dann überlagern möchte (ähnlich wie es bereits
  mit Scenes + Chases in Kombination möglich ist)

Fehler im Handbuch:
* "Einstellungen Speicher" speichert nicht die Einstellung des Fixture-Kanals, sondern alle Einstellungen unter dem
  Namen des Fixture-Kanals

Fragen:
* Wozu ist der Modus, das wenn man auf PAN oder TILT drückt, die Leuchtdioden darüber blinken?
  -> Sperren einer Richtung

Cheat Sheet:

Scenes *addieren* Werte

* Lauflicht abspielen: CHASE x
* Lauflicht programmieren
* Programmschritt bei Lauflicht einfügen
* Programmschritt bei Lauflicht löschen
* Lauflicht löschen: Programmiermodus PROGRAM|RECORD [3 Sek] -> TAP|DEL + SCENE x -> PROGRAM|RECORD [3 Sek] 
* Szene programmieren
* Szene abspielen: SCENE x
* Szene löschen: Programmiermodus PROGRAM|RECORD [3 Sek] -> TAP|DEL + CHASE x -> PROGRAM|RECORD [3 Sek] 
* Fader umbenennen:
* Einstellungen speichern: [MODE] + [Pfeil hoch] [2 Sek] -> FIXTURE x speichert als "led-commander16-2/FILEx.PRO"
  eine 1025 Blöcke große Datei (524800 Bytes)
* Einstellungen laden: [MODE] + [Pfeil runter] [2 Sek] -> LEDs der FIXTURE x-Tasten für gefunden Konfiguration leuchten,
  FIXTURE x lädt die entsprechende Konfiguration
* Werkseinstellungen: Ausschalten -> PROGRAM|RECORD + TAP|DEL + PATCH|CLEAR gedrückt halten -> Einschalten

Full On setzt alle zugeordneten Kanäle auf 255

Eingabeelemente für Fixtures sind:
* einer der 8 Schieberegler
* Pan (x-Achse) und Tilt (y-Achse) des Joysticks
* AUX1 und AUX2

Bedeutung:
* Ein **Fixture** ist eine Zuordnung von einem Eingabeelement zu einem DMX-Kanal. Also in etwa so:

DMX CH1 <--[Fixture x]-- Fader (1-8) [+Max durch Master]
DMX CH2 <--[Fixture y]-- Fader (1-8) [+Max durch Master]
DMX CH3 <-- Unbelegt
DMX CH4 <-- AUX1
DMX CH4 <-- AUX2

* Einem Eingabeelement können beliebig viele DMX-Kanäle innerhalb eines Fixtures zugeordnet werden.
* Jeder DMX-Kanal kann genau einem Fixture zugeordnet oder unbelegt sein

Gerätekanäle zuordnen:
* Einschalten: PATCH | CLEAR für 3 Sekunden drücken
* DMX-Kanal auswählen: SPEED * 20 + FADE
* Kanal deaktivieren: Kein Fixture auswählen + beliebige Flash-Taste
* Fader auf Kanal zuweisen: einen Fixture von 1-16 auswählen und dann einen Fader über die zugehötige Flashtaste
* AUX1 oder AUX2 auf Kanal zuweisen: AUX1 oder AUX2 drücken (unabhängig vom gewählten Fixture)
* Ausschalten: PATCH | CLEAR für 3 Sekunden drücken

Master-Mode für Fixtures:
Einige Geräte haben einen eigenen DMX-Kanal zum Dimmen der Helligkeit, in diesem Fall kann der Dimmer-Fader
einfach auf diesen DMX-Kanal gelegt werden. Ist kein Dimmer-Kanal vorhanden kann man die Werte von bestimmten
Kanälen linear durch den Dimmer-Fader reduzieren. Dies ist etwa für die Kanäle Rot, Grün und Blau sinnvoll, da
dann durch Absenken der Komponentenhelligkeiten ein Dimmereffekt erzeugt wird.
Der Master-Mode wird einmal für den gesamten Fixture aktiviert und dann nochmal pro Kanal.

Testdateien:
* FILE1.PRO Werkseinstellung
* FILE2.PRO Alles unassigned
* FILE3.PRO DMX1 -> Fixture 1 -> Function-Fader
* FILE4.PRO DMX1 -> Fixture 1 -> Function-Fader + Master für Fixture
* FILE5.PRO DMX1 -> Fixture 1 -> Function-Fader + Master für Fixture und Function-Fader
* FILE6.PRO wie FILE5.PRO + SCENE 1 mit FUNCTION FIXTURE1 = 255
* FILE7.PRO Werkseinstellung, 1-20 gewiped
 * DMX1 -> Fixture 1 -> Fader 8 (Dimmer)
 * DMX2 -> Fixture 1 -> Fader 7 (Strobe)
 * DMX3 -> Fixture 1 -> Fader 2 (Red)
 * DMX4 -> Fixture 1 -> Fader 3 (Green)
 * DMX5 -> Fixture 1 -> Fader 4 (Blue)
 * DMX6 -> Fixture 1 -> Fader 1 (Function)
 * DMX11 -> Fixture 2 -> Fader 8 (Dimmer)
 * DMX12 -> Fixture 2 -> Fader 7 (Strobe)
 * DMX13 -> Fixture 2 -> Fader 2 (Red)
 * DMX14 -> Fixture 2 -> Fader 3 (Green)
 * DMX15 -> Fixture 2 -> Fader 4 (Blue)
 * DMX16 -> Fixture 2 -> Fader 1 (Function)

```
diff FILE1.PRO.od FILE2.PRO.od|less
8073,8084c8073,8074
< 1325520 3200 0000 0001 0203 0405 06a2 0809 0a0b
< 1325540 0c0d 0e0f 10a2 1213 1415 1617 1819 1aa2
< 1325560 1c1d 1e1f 2021 2223 24a2 2627 2829 2a2b
< 1325600 2c2d 2ea2 3031 3233 3435 3637 38a2 3a3b
< 1325620 3c3d 3e3f 4041 42a2 4445 4647 4849 4a4b
< 1325640 4ca2 4e4f 5051 5253 5455 56a2 5859 5a5b
< 1325660 5c5d 5e5f 60a2 6263 6465 6667 6869 6aa2
< 1325700 6c6d 6e6f 7071 7273 74a2 7677 7879 7a7b
< 1325720 7c7d 7ea2 8081 8283 8485 8687 88a2 8a8b
< 1325740 8c8d 8e8f 9091 92a2 9495 9697 9899 9a9b
< 1325760 9ca2 9e9f a2a2 a2a2 a2a2 a2a2 a2a2 a2a2
< 1326000 a2a2 a2a2 a2a2 a2a2 a2a2 a2a2 a2a2 a2a2
---
> 1325520 3200 0000 a2a2 a2a2 a2a2 a2a2 a2a2 a2a2
> 1325540 a2a2 a2a2 a2a2 a2a2 a2a2 a2a2 a2a2 a2a2
8095c8085
< 1524600 0000 0000 0000 0000 004b 0164 6401 0101
---
> 1524600 0000 0000 0000 0000 004b 0100 0001 0101

diff FILE2.PRO.od FILE3.PRO.od 
8073c8073
< 1325520 3200 0000 a2a2 a2a2 a2a2 a2a2 a2a2 a2a2
---
> 1325520 3200 0000 00a2 a2a2 a2a2 a2a2 a2a2 a2a2
8085c8085
< 1524600 0000 0000 0000 0000 004b 0100 0001 0101
---
> 1524600 0000 0000 0000 0000 004b 0100 0000 0101

diff FILE3.PRO.od FILE4.PRO.od 
8085c8085
< 1524600 0000 0000 0000 0000 004b 0100 0000 0101
---
> 1524600 0000 0000 0000 0000 004b 0100 0001 0101

diff FILE4.PRO.od FILE5.PRO.od 
8086c8086
< 1524620 0101 0101 0101 0101 0101 0101 0100 0101
---
> 1524620 0101 0101 0101 0101 0101 0101 0101 0101

diff FILE5.PRO.od FILE6.PRO.od 
4c4,5
< 0001000 ffff ffff ffff ffff ffff ffff ffff ffff
---
> 0001000 ff00 0000 0000 0000 0000 0000 0000 0000
> 0001020 0000 0000 0000 0000 0000 0000 0000 0000
6,7c7,8
< 0001240 0000 0000 0000 0000 0000 0000 0000 0000
< 0001260 0000 0000 0000 0000 ffff ffff ffff ffff
---
> 0001240 0100 0000 0000 0000 0000 0000 0000 0000
> 0001260 0000 0000 0100 0100 ffff ffff ffff ffff

```
