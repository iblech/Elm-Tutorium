[Zur�ck](Movement.md)

---

# Vierte Aufgabe

Folgendes Programm ([`Counting.elm`](../src/task04/Counting.elm)):

```elm
import Graphics.Element exposing (..)
import Mouse

main : Signal Element
main = Signal.map show (Signal.foldp (\_ c -> c + 1) 0 Mouse.clicks)
```

zeigt einen Z�hler, der bei `0` startet und mit jedem Mausklick um `1` erh�ht wird.

Benutzt werden dabei:

```elm
Mouse.clicks : Signal ()

Signal.foldp : (a -> b -> b) -> b -> Signal a -> Signal b
```

Wegen des Typs `Signal ()` ist von `Mouse.clicks` nur der Aspekt "diskret eintretende Ereignisse" relevant, denn "�nderungen des Werts" sind im Typ `()` ja gar nicht m�glich.
Die Funktion `Signal.foldp` wiederum reagiert auf jedes Ereignis in ihrem Eingangssignal (jeweils einen Wert des Typs `a` tragend) durch Aktualisierung eines aktuellen Zustands (von Typ `b`, zu Beginn initialisiert durch einen entsprechenden Startwert) und gibt diesen dann in ihrem Ausgabesignal wieder.
Stellt man sich ein Signal also als eine Liste von nacheinander eintreffenden Werten vor, dann entspricht `Signal.foldp f` etwa `scanl (flip f)` in Haskell.

Ziel ist nun, das Verhalten des Programms so zu �ndern, dass der Z�hler mit jedem Mausklick weiterhin um `1` erh�ht wird, falls der Mauszeiger maximal `100` Pixel von der linken oberen Ecke (wo der Z�hler angezeigt wird) entfernt ist, andernfalls um `1` verringert.

Hinweis:
* Das Modul [`Signal`](http://package.elm-lang.org/packages/elm-lang/core/latest/Signal) enth�lt interessante Funktionen, die mehr als ein Eingabesignal haben.

---

[Weiter](Stamping.md)

