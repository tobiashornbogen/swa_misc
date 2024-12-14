# Ideen für das Refactoring

## Separation von Logik und UI

Wir haben ja zwischendurch darüber diskutiert, inwieweit die Trennung von Play Mode und Game Manager notwendig ist, ob man das in zwei Klassen packen kann/soll/muss etc. Aktuell haben Klassen wie zum Beispiel `EP_Board`, `EP_PlayMode` und `EP_GameWindow` sehr viele Verantwortlichkeiten (entgegen des Single Responsibility Principle), da sie gleichzeitig UI, Logik und Eingaben handeln. Bei einem potenziellen Refactoring könnte man diese nach dem Model View Controller pattern separieren. Das heißt man würde beispielsweise wieder PlayMode haben (was nur die UI managed) und parallel dazu den Game Manager, der dann die Level lädt und in dem Wave Manager und Level Manager etc. leben.

## Dependency Injection

An vielen Stellen unseres Codes werden Referenzen auf andere Objekte benötigt, damit jeder alle Objekte kennt, mit dener er kommunizieren muss. Dadurch sind allerdings beispielsweise solche Dinge passiert: `way := self owner owner way.`. Eine Lösung dafür wäre an diesen Stellen stattdessen dependency injection zu verwenden. Der Begriff hört sich kompllizierer an, als er ist. Es geht im übrigen einfach darum, Instanzvariablen, die andere Objekte sind nicht von Hand zu rekonstruieren, sondern bei der Initialisierung zu übergeben. Zum Beispiel würde man bei der Initialiserung von Enemy (aus dem der Code oben kommt) way als Parameter übergeben und sich das so sparen. Ist eigentlich vor allem aus Gründen der Testbarkeit populär, aber ig die werden es gut finden und denke, um solche Konstruktionen zu vermeiden, könnte es allgemein sinnvoll sein.

## Factory / Builder Patterns

Wir hatten ja schon ein paar Mal besprochen, dass an einigen Stellen Builder patterns eine Möglichkeit wären, den Code zu verbessern. Zum Beispiel in `EP_Board` muss die Initialiserung in einer klaren Reihenfolge stattfinden. Für Board wäre vielleicht sogar schon ein Builder angebracht, ansonsten könnte man an einigen Stellen, wie zum Beispiel Enemies vermutlich gut eine Factory benutzen.

## Event Driven Architecture (Observer Pattern)

Eine Art Publish Subscribe (also in SWA Terminologie Observer pattern) könnte einige Stellen vielliecht ein bisschen erleichtern. Zum Beispiel war ja eins der Probleme, die am Anfang beim Design der Tower Range ein Problem waren, dass es schwierig ist Referenzen von Enemies auf Towers und umgekehrt zu behalten. Das könnte man vereinfachen, in dem man an verschiedenen Stellen ein Observer Pattern benutzt. Stellen an denen ich mir das vorstellen könnte, sind zum Beispiel die folgenden:

- Enemy Tod (wenn ein Enemy stirbt könnte man einfach eine Nachrich senden und dann hören da die entsprechenden Manager und Board etc. drauf und reagieren entsprechend)
- Stage completed (also, wenn eine Stage fertig ist und irgendwelche Dinge passieren sollen)
  Allgemein wäre das eine Option bei asynchronen Ereignissen, die irgendwann passieren können, wie die eben beschriebenen.

## Singleton für globalen Game State

kein Plan inwieweit das in Tills kommender PR abgedeckt ist, aber NotAGameManager oder so sollten ein Interface für den globalen GameState darstellen, also alle Sachen, wie Geld, Leben, das aktuelle Level, die man immer aus einer Single Source of Truth lesen sollte.
