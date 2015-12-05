[Zur�ck](Stamping.md)

---

# Sechste Aufgabe

Wollen wir Bedienelemente wie HTML-Kn�pfe umsetzen, brauchen wir ein neues Konzept.
Bisherige Signalquellen (wie `Time`, `Mouse`) haben keine graphische Repr�sentation, au�erdem existieren sie einfach und immer, ohne erzeugt werden zu m�ssen.
Im Gegensatz dazu muss ein HTML-Knopf zun�chst �berhaupt dargestellt werden, und nur wenn er dargestellt wurde, kann er auch durch den Nutzer bedient werden und somit als Signalquelle fungieren.
Zudem sollte es m�glich sein, abh�ngig vom Programmzustand einen solchen Knopf ein- oder eben auch auszublenden (oder auch mehrere Kn�pfe und andere Bedienelemente).
Folglich w�rde auch die Signalquelle dynamisch entstehen und gegebenenfalls wieder verschwinden.
Dynamisch konfigurierbare Signalgraphen, also quasi `Signal (Signal a)`, werden in Elm jedoch nicht unterst�tzt.

Um mit gegebenenfalls dynamisch erzeugten Bedienelementen umzugehen, wird daher eine Indirektion eingef�hrt.
Daf�r gibt es das Konzept der `Mailbox`.
Eine Mailbox hat eine Adresse und stellt ein Signal bereit:

```elm
type alias Mailbox a = { address : Address a, signal : Signal a }
```

Eine Mailbox wird unter Angabe eines Initialwertes mittels

```elm
Signal.mailbox : a -> Mailbox a
```

erzeugt, ihr k�nnen dann �ber ihre Addresse durch Event-Handler wie `onClick` Werte �bermittelt werden (siehe unten), und �ber das der Mailbox zugeh�rige Signal k�nnen andere Programmteile auf diese Werte reagieren.
Dabei kann eine einzelne Mailbox als Kanal f�r Werte aus verschiedenen Bedienelementen fungieren.

Das folgende Programmfragment zeigt eine typische Nutzung:

```elm
import Html exposing (..)
import Html.Attributes exposing (..)
import Html.Events exposing (..)
import Signal exposing (Address, Mailbox)

type Action = ...

actions : Mailbox Action
actions = Signal.mailbox ...

update : Action -> Int -> Int
update action c = ...

view : Int -> Html
view c = div []
         [ div [] [ text (toString c) ]
         , button [ onClick actions.address ... ] [ text "Zero" ]
         , ...
         ]

main : Signal Html
main = Signal.map view (Signal.foldp update 0 actions.signal)
```

Erkl�rungen:
* Statt graphischer Elemente wie bisher benutzen wir nun Standard-HTML, daher auch `main : Signal Html` statt dem bisherigen `main : Signal Element`.
* HTML wird erzeugt durch Funktionen wie `text : String -> Html` und `div : List Attribute -> List Html -> Html`.
  Analog zu `div` gibt es Funktionen f�r praktisch alle bekannten HTML-Elemente.
  �blicherweise nehmen sie eine Liste von Attributen und eine Liste von HTML-Kindknoten als Eingabe.
  Oft wird eine der beiden Listen leer sein.
* Attribute werden wiederum durch bekannten HTML-Attributen entsprechende Funktionen erzeugt, etwa `autofocus : Bool -> Attribute`, jedoch auch durch Event-Handler wie `onClick : Address a -> a -> Attribute`.
* Der Ausdruck `button [ onClick actions.address ... ] [ text "Zero" ]` erzeugt also einen HTML-Knopf, der mit "Zero" beschriftet ist, und der bei Nutzerklick den Wert `...` an die `actions`-Mailbox �bermittelt.
  (Die beiden Vorkommen der gleichen Typvariable im oben angegebenen Typ von `onClick` sorgen daf�r, dass man nur passend getypte Werte an eine Mailbox senden kann.)
  Jeder Konsument des Signals `actions.signal` wird diesen Wert dann als Eingabe geliefert bekommen.

## Aufgabe

Vervollst�ndige obiges Programmfragment, so dass insgesamt drei Kn�pfe angezeigt werden, beschriftet mit "Zero", "Up", "Down", und dass der ebenfalls angezeigte Z�hler mit jedem Klick auf "Zero" zur�ckgesetzt, jedem Klick auf "Up" erh�ht und jedem Klick auf "Down" verringert wird.

---

[Weiter](Tasks.md)

