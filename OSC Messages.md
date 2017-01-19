OSC Messages
============

Dieser Text ist mit [Markdown](https://de.wikipedia.org/wiki/Markdown) formatiert.
Markdown ist ein einfach Textauszeichungsprache.
[Markdown Cheatsheet.](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


|      Name       | Sound | Kanäle | OSC In | OSC Out | Video Out |
|:---------------:|:-----:|:------:|:------:|:-------:|:---------:|
| Omnibox (Bild)  |   x   |   0    |    4   |    0    |     ✓     |
| Omnibox (Ton)   |   ✓   |   2    |    1   |    0    |     x     |
|                 |       |        |        |         |           |


Parameter Konvention
====================

 * `/gruppenName/param1 float`


Omnibox
===============

Wir horchen auf OSC Messages im folgenden Format:

### Bild

 * `/size f f f`     (x,y,z: Ausdehnung der geometrischen Figuren von 0. bis 1.)
 * `/rota f    `     (alpha: Freiheitsgrad der geometrischen Figuren von 0. bis 360.)
 * `/move f f f`     (x,y,z: Verschiebt die geometrischen Figuren anteilig vom Zentrum weg, Werte: 0. bis 1.)
 * `/color f f f`    (r,g,b: Coloriert die geometrischen Figuren, Werte: 0. bis 1.)

### Ton

 * `/notes i i i i i i i i i i i `(index + 11 Noten: Integers, die als MIDI-Noten interpretiert werden. Treiben die Klangsynthese an.)
 
