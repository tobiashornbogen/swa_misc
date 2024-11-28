# SWA Diagramme
Beim Code aufräumen ist mir aufgefallen, dass es wichtig wäre ein gemeinsames Verständnis uns insbesondere eine single source of truth zu haben, was unsere Architektur angeht. Weil Squeak und Git habe ich deshalb jetzt ein neues Repository aufgemacht, in dem eine .puml file liegt. Das ist eine plantUML file. Das ist ein sehr populäres Format für UML-Diagramme. Ihr könnt euch beispielsweise in VS Code eine Extension holen, mit der ihr das immer previewn oder exporten könnt etc. Ich würde vorschlagen, zu jedem Commit, der die Architektur anpasst, neue Methoden hinzufügt etc. das Diagramm anzupassen und hier ebenfalls einen commit zu machen, weil das es wesentlich leichter macht, die aktuelle Architektur zu verstehen, Refactorings zu planen, Stellen festzustellen, die man verbessern könnte usw.

Wie macht ihr das so grob?

1. Repository clonen und Ordner in VS Code öffnen (muss nicht, aber hat hilfreiche utilities)
2. PlantUML extension installieren (einfach das höchstgeratete)
3. PlantUML Installationsschritten folgen, die in der Beschreibung sind
4. Änderungen können in der .puml Datei gemacht werden und mit `cmd + shift + p` oder dem entsprechenden Windows / Linux Äquivalent für VS Code die Kommand Palette öffnen und nach Plant UML Preview für die eigene Datei suchen und ausführen (oder `opt d` bzw. `alt d` auf Windows. Dann habt ihr ein schönes Preview
5. Es müsste in der Command Palette auch eine Export Option geben, kann man nutzen, muss aber nicht immer
6. Dann die Änderungen committen und paralle zur PR im SWA Repo eine PR öffnen, damit immer alles up to date ist

![alt text](/out/diagram/diagram.svg)
