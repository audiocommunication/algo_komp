OSC Messages
============

Dieser Text ist mit [Markdown](https://de.wikipedia.org/wiki/Markdown) formatiert.
Markdown ist ein einfach Textauszeichungsprache.
[Markdown Cheatsheet.](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


|      Name       | Sound | Kanäle | Midi In | Midi Out | Video Out |
|:---------------:|:-----:|:------:|:-------:|:--------:|:---------:|
| BeispielGruppe1 |   ✓   |   5    |    2    |    4     |     x     |
| BeispielGruppe2 |   x   |   2    |    0    |    2     |     ✓     |
|                 |       |        |         |          |           |
|                 |       |        |         |          |           |
|                 |       |        |         |          |           |


Parameter Konvention
====================

* `/gruppenName/param1 float`


BeispielGruppe1
===============

Wir senden folgende OSC Messages

### Synth1

 * `/BeispielGruppe1/synth1/volume` -> Lautstärke des ersten Synth
 * `/BeispielGruppe1/synth1/note` -> Ton des ersten Synth

### Drums

 * `/BeispielGruppe1/drums/noteOn` -> Schickt eine 1 wenn die Drum angeschlagen wird
