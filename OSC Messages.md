OSC Messages
============

Dieser Text ist mit [Markdown](https://de.wikipedia.org/wiki/Markdown) formatiert.
Markdown ist ein einfach Textauszeichungsprache.
[Markdown Cheatsheet.](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


|      Name      | Sound | Kanäle | OSC In | OSC Out | Video Out |
|:--------------:|:-----:|:------:|:------:|:-------:|:---------:|
| Omnibox (Bild) |   x   |   0    |   4    |    0    |     ✓     |
| Omnibox (Ton)  |   ✓   |   2    |   1    |    0    |     x     |
|      Cell      |   ✓   |  1-2   |  4-∞   |   4-∞   |     x     |
|     Marble     |   x   |        |   1    |    9    |     x     |



Parameter Konvention
====================

 * `/gruppenName/param1 float`


Omnibox
=======

Wir horchen auf OSC Messages im folgenden Format:

### Bild

 * `/size f f f`     (x,y,z: Ausdehnung der geometrischen Figuren von 0. bis 1.)
 * `/rota f    `     (alpha: Freiheitsgrad der geometrischen Figuren von 0. bis 360.)
 * `/move f f f`     (x,y,z: Verschiebt die geometrischen Figuren anteilig vom Zentrum weg, Werte: 0. bis 1.)
 * `/color f f f`    (r,g,b: Coloriert die geometrischen Figuren, Werte: 0. bis 1.)

### Ton

 * `/notes i i i i i i i i i i i `(index + 11 Noten: Integers, die als MIDI-Noten interpretiert werden. Treiben die Klangsynthese an.)



Cell
====

Cellular Sequencer as a Service (CSaaS).

Der zelluläre Automat besitzt eine beliebige Anzahl an Spuren.
Der Default besteht aus 4 Spuren, die als Rythmusgruppe zu verstehen sind (Kick, Snare, Hi-Hat und Percussion).
Die Standartbelegung wird von uns als Ton augegeben, kann aber auch von jedem als OSC empfangen werden.
Die Messages sind als Bang/Note-On zu verstehen.
Der gesendete `float` Wert ist daher immer `1.0`.

### OSC Out

Wir senden folgende OSC Messages:

 * `cell/note/kick f` -> Bang (Note-On) der ersten Spur (f immer 1.0)
 * `cell/note/snare f` -> Bang (Note-On) der zweiten Spur (f immer 1.0)
 * `cell/note/hat f` -> Bang (Note-On) der dritten Spur (f immer 1.0)
 * `cell/note/perc f` -> Bang (Note-On) der vierte Spur (f immer 1.0)

Note-Off Messages sind nicht vorgesehen, können bei Bedarf aber implementiert werden.

Wenn eine eigene Sequenz definiert wurde (siehe OSC In) ist diese unter dem selbst definierten Namen erreichbar.

 * `cell/note/lustigerBeispielName f` -> Bang für die vorher selbst definierte Sequenz `lustigerBeispielName`

### OSC In

Wir empfangen folgende OSC Messages:

Die Sequenzen der einzelnen Spuren können überschrieben werden.
Hierbei kann eine beliebige Anzahl an `float` Werten an die entsprechende Spur gesendet werden.
Ein `float` Wert von `0.0` entspricht dabei einem ausgeschaltetem Sequenzelement und `1.0` einem eingeschaltetem.
Beispiel: `0.0 1.0 1.0 0.0 1.0`

 * `cell/sequ/kick f f ... f` -> Neue Sequenz für die erste Spur
 * `cell/sequ/snare f f ... f` -> Neue Sequenz für die zweite Spur
 * `cell/sequ/hat f f ... f` -> Neue Sequenz für die dritte Spur
 * `cell/sequ/perc f f ... f` -> Neue Sequenz für die vierte Spur

Es können auch neue Spuren definiert werden. Dafür muss eine Sequenz an einen noch nicht vergebenen Namen geschickt werden.
Die Sequenz ist danach unter diesem Name erreichbar.

 * `cell/sequ/lustigerBeispielName f f ... f` -> Definiert eine neue Sequenz

Marble
======

Kugelspiel - "Marble"

Das Kugelspiel ist ein, über einen Motor bewegliches, Spielbrett auf dem sich drei Holzkugeln in den Farben Rot, Grün, Blau (RGB) zufällig bewegen. Die jeweilige Farbe wird mittels Colortracking per Webcam erfasst und somit die Position der jeweiligen Farbkugel ermittelt. Es werden X-Position, Y-Position und der Abstand der Kugeln zueinander in Form von OSC-Daten gesendet. Zusätzlich kann zur Geschwingigkeitsregulierung des Motors ("Wippgeschwindigkeit") eine OSC-Nachricht empfangen werden.

Unsere Daten können z.B. sehr gut für Modulations(effekte) verwendet und weiterverarbeitet werden. Alle Ausgabewerte sind auf die Range 0.0 bis 1.0 normiert.

### OSC Out

Wir senden folgende OSC Messages:

 * `marble/ballR/xCoordinate f` -> Range 0.0 bis 1.0
 * `marble/ballR/yCoordinate f` -> Range 0.0 bis 1.0
 * `marble/ballG/xCoordinate f` -> Range 0.0 bis 1.0
 * `marble/ballG/yCoordinate f` -> Range 0.0 bis 1.0
 * `marble/ballB/xCoordinate f` -> Range 0.0 bis 1.0
 * `marble/ballB/yCoordinate f` -> Range 0.0 bis 1.0
 * `marble/distanceRG f` -> Range 0.0 bis 1.0
 * `marble/distanceGB f` -> Range 0.0 bis 1.0
 * `marble/distanceBR f` -> Range 0.0 bis 1.0 

### OSC In

Wir empfangen folgende OSC Messages:

Zur Steuerung des Motors. Hier ist VORSICHT geboten! Da die Steuerung und Berechnung des Motorgeschwindigkeit/ Beschleunigung über einen Arduino erfolgt, kann es zu "Verschlucken" und holperigen Artefakten des Motors führen. Deswegen ist hier eine gute Absprache nötig, sodass nicht zu viele OSC-Nachrichten gesendet werden.

 * `marble/motorspeed f` -> Range 0.0 bis 1.0

