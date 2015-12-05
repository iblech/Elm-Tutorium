[Zur�ck](Pendulum.md)

---

# Dritte Aufgabe

Setze [dieses Verhalten](http://jvoigtlaender.github.io/Elm-Tutorium/examples/Movement.html) um.
Es sollen also in Reaktion auf Mausbewegungen immer genau die Kreise rot sein, die n�her am gemeinsamen Mittelpunkt sind als der Mauszeiger (und die anderen gr�n).

Hinweise:
* Das Modul [`Mouse`](http://package.elm-lang.org/packages/elm-lang/core/latest/Mouse) enth�lt ein Signal `position : Signal (Int, Int)`.
* Das Modul [`Color`](http://package.elm-lang.org/packages/elm-lang/core/latest/Color) enth�lt `red`, `green`, etc.
* Au�erdem kann statt wie bisher `defaultLine : LineStyle` nun `solid : Color -> LineStyle` verwendet werden.
* Die Koordinatensysteme f�r `Mouse.position` und f�r das Malen innerhalb eines `collage`-Aufrufs unterscheiden sich. Zum Herausfinden der Details dazu eignet sich wieder [`Debug.watch`](http://package.elm-lang.org/packages/elm-lang/core/latest/Debug#watch).

---

[Weiter](Counting.md)

