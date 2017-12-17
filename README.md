# RasPiWorkshop2017
Raspberry Pi Workshop im Rahmen der StartApp-Tagung im Medienzentrum München des JFF - Jugend Film Fernsehen e. V.<br>

![Alt text](Slides/Overview.png?raw=true "Title")

## Einrichtung des Raspberry Pi
Es gibt viele Linux-Distributionen, die für unterschiedliche Aufgaben genutzt werden können (z.B. RasPi als Spielkonsole, Mediacenter oder Wetterstation) - wir benutzen aber das Standardsystem Raspbian. Dieses enthält alles, was wir brauchen: einen Desktop und Tools zum Entwickeln von Software. Um das Betriebssystem zu installieren, laden wir den Installations-Wizard NOOBS von der Raspberry Pi-Webseite herunter https://www.raspberrypi.org/downloads/noobs/

Das Ganze ist sehr einfach: Paket entpacken, auf die SD-Karte kopieren, RasPi mit SD-Karte starten und den Anweisungen auf dem Bildschirm folgen. Eine detaillierte Anleitung für NOOBS gibt's hier: https://www.raspberrypi.org/learning/software-guide/

Für Eltern ist die Distribution KANO interessant: http://developers.kano.me/downloads/ - dieses Betriebssystem ist speziell für Kinder ausgelegt und vermittelt Programmierkenntnisse auf spielerische Art und Weise. Für die Arbeit an Schulen oder in Workshops empfehle ich aber das schlichtere und weniger verspielte Raspbian.


## Entwickeln mit Scratch 2.0
Scratch ist eine Entwicklungsumgebung speziell für Programmier-Anfänger. Es lassen sich damit Programme mithilfe von fertigen Bausteinen zusammensetzen und ausführen.

Auf dem Raspberry Pi gibt es ein Addon für die Nutzung der GPIO-Leiste, das wir unter dem Punkt "Mehr Blöcke"/"Erweiterung hinzufügen" aktivieren, um neue Bauteile zu erhalten.
https://www.raspberrypi.org/blog/scratch-2-raspberry-pi/

## Eingabegeräte, Buttons, Sensoren
Um einen Sensor auszulesen benötigen wir zwei Dinge: ein stabiles Signal und eine Schnittstelle zu unserem Programm. Die Schnittstelle ist die GPIO-Leiste unseres RasPis. Der Knackpunkt ist das "stabile Signal"...

Die einfachste Möglichkeit, einen Button über die GPIO-Leiste des Raspberry Pi auszulesen, ist die Verwendung des internen Pullup-Widerstandes. 
![Alt text](Slides/Button.png?raw=true "Title")
