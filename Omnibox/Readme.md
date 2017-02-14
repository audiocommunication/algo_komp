## Omnibox Visual
Erste Itteration der "verschachtelten Quader" die durch LFOs moduliert werden.
Im Gegensatz zur demonstrierten Version im Seminar in Pd statt Max/MSP realisiert.

## Omnibox Sound
Empfängt via OSC eine Liste aus Noten der Form /Notes/(i)(i)(i)(i)(i)(i)(i)(i)(i)(i)(i)
Mit (i) = Integer.
Die erste Position kann zur weiteren Verarbeitung einen Index enthalten. Die zehn folgenden Integer sind als MIDI-Noten gedacht und laufen danach in ein mtof (MIDI-to-Frequency) Objekt in der Klangsynthese.
Weiter können via OSC mit /LFO1/, /LFO2/ und /LFO3/ drei Floats empfangen werden, welche primär dazu gedacht sind den Hallanteil (Freezeverb) und die Skala (falls in Verwendung) zu modifizieren.

Nicht alle Elemente des Patches sind von mir ursprünglich geschrieben. Der Freezeverb ist aus einem älteren Projekt. Suche die Referenz noch raus.
