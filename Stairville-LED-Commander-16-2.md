# Stairville LED Commander 16/2

Verbesserungsvorschläge:
* Ausschließen von Kanälen bei "Full On". Dies ist wichtig, da sonst z.B. bei gemappetem Strobe die Scheinwerfer Blitzen
  statt gleichmäßig zu leuchten.
  Idee: Während des "Patch/Clear" Modus auf einem Kanal 3 Sekunden drücken von "Full On" nimmt den Kanal rein bzw. raus
  bei "Full On", Anzeige durch "F" neben dem Kanal
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

