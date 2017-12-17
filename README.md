# RasPiWorkshop2017
<p>Raspberry Pi Workshop im Rahmen der StartApp-Tagung im Medienzentrum München des JFF - Jugend Film Fernsehen e. V.</p>

![Alt text](Slides/Overview.png?raw=true "Overview")

In der Game-Jam-Phase dieses Workshops haben wir eine Quiz-Show entwickelt. Jede Gruppe hat eine Teil-Aufgabe übernommen und am Ende konnten wir unser kleines Quiz vor Publikum veranstalten. Die Scratch-Vorlagen und Ergebnisse der Gruppen werden hier demnächst veröffentlicht.

In diesem Dokument werden während des Workshops angesprochene Themen aufgegriffen und vertieft. 

## Einrichtung des Raspberry Pi
Es gibt viele Linux-Distributionen, die für unterschiedliche Aufgaben genutzt werden können (z.B. RasPi als Spielkonsole, Mediacenter oder Wetterstation) - wir benutzen aber das Standardsystem Raspbian. Dieses enthält alles, was wir brauchen: einen Desktop und Tools zum Entwickeln von Software. Um das Betriebssystem zu installieren, laden wir den Installations-Wizard NOOBS von der Raspberry Pi-Webseite herunter https://www.raspberrypi.org/downloads/noobs/

Das Ganze ist sehr einfach: Paket entpacken, auf die SD-Karte kopieren, RasPi mit SD-Karte starten und den Anweisungen auf dem Bildschirm folgen. Eine detaillierte Anleitung für NOOBS gibt's hier: https://www.raspberrypi.org/learning/software-guide/

Für Eltern ist die Distribution KANO interessant: http://developers.kano.me/downloads/ - dieses Betriebssystem ist speziell für Kinder ausgelegt und vermittelt Programmierkenntnisse auf spielerische Art und Weise. Für die Arbeit an Schulen oder in Workshops empfehle ich aber das schlichtere und weniger verspielte Raspbian.

## Entwickeln mit Scratch 2.0
Scratch ist eine Entwicklungsumgebung speziell für Programmier-Anfänger. Es lassen sich damit Programme mithilfe von fertigen Bausteinen zusammensetzen und ausführen.

Auf dem Raspberry Pi gibt es ein Addon für die Nutzung der GPIO-Leiste, das wir unter dem Punkt "Mehr Blöcke"/"Erweiterung hinzufügen" aktivieren, um neue Bauteile zu erhalten.
https://www.raspberrypi.org/blog/scratch-2-raspberry-pi/

## Physical Computing: Eingabegeräte, Buttons, Sensoren, Aktoren

### USB-Peripherie
Da der Raspberry Pi über mehrere USB-Anschlüsse verfügt, kann man dort nahezu jede PC-Peripherie anschließen: Maus, Tastatur, Gamepad, mit nachinstallierbaren Treibern sogar Webcams und Drucker. Da der [MakeyMakey](https://www.makeymakey.com/) sich einfach als Tastatur anmeldet, kann man auch damit direkt loslegen.

### GPIO (General Purpose Input Output)
Um einen Sensor, z.B. einen Button, auszulesen benötigen wir zwei Dinge: ein stabiles Signal und eine Schnittstelle zu unserem Programm. Die Schnittstelle ist die GPIO-Leiste unseres RasPis. ACHTUNG: es darf niemals eine Spannung höher als 3,3 Volt an einen der GPIO-Pins angelegt werden, da sonst der SoC beschädigt wird! Das ist besonders wichtig zu wissen, weil zwei der Pins 5 Volt liefern. Es gibt also Pins, mit denen sich der RasPi selbst zerstören kann!
![Alt text](Slides/Raspipins.png?raw=true "Raspberry Pi GPIO pins")

Der eigentliche Knackpunkt ist aber das "stabile Signal" - um ein solches zu erhalten, reicht es nicht aus, einen "Stromkreis" zu schließen oder zu öffnen. Da auf einer Microcontroller-Platine und in ihrer Umgebung etliche - natürliche und selbst verursachte - elektromagnetische Felder (EMF) auf den GPIO einwirken, ist eine besondere Schaltung nötig: der Pullup-Widerstand. Ohne ihn hängt immer einer der Zustände (gedrückt, nicht gedrückt) "in der Luft". Dann fungiert der Pin als eine Art Antenne, die EMF-Schwingungen der näheren Umgebung an den GPIO-Pin leitet. Dadurch entstehen Fluktuationen an der Signal-Leitung, die wir (in diesem Fall) nicht haben wollen. Ein Pullup-Widerstand "zieht" das Signal auf eine hohe Spannung, entsprechend können wir an dem Pin ein HIGH auslesen, solange der Button NICHT gedrückt wurde. Drückt man den Button, wird der Pin direkt mit Ground verbunden: am Pin wird 0 Volt (LOW) ausgelesen.

##### Verbindung zwischen 3,3V und Pin mit einem 10k Ohm-Widerstand, Button zwischen Pin und Ground:
![Alt text](Slides/Pullup1.png?raw=true "Pullup 1")

Netterweise hat der RasPi einen internen Pullup-Widerstand. Für kleinere Experimente und Prototypen kann dieser ruhig genutzt werden, um "schnell mal eben" einen Button an einen RasPi zu bauen. 

##### Buttons zwischen Pin und Ground:
![Alt text](Slides/Pullup2.png?raw=true "Pullup 2")

Für Projekte, die dauerhaft in Betrieb und möglichst wartungsfrei sein sollen, empfehle ich aber, für jeden Button externe Pullup-Schaltungen zu löten. Zusätzlich sollte eine Schutzdiode zwischen Pin und 3,3V eingesetzt werden, die schädliche Spannungen vom Pin wegführen. Falls es hierzu Fragen geben sollte, kann ich das Thema gerne noch ausweiten ;)

### Sensor-Module
Viele Sensoren gibt es als fertige Module auf kleinen Platinen, die man direkt mit Microcontrollern verbinden kann, ohne sich über deren Stromversorgung oder nötige Schutzschaltungen Gedanken machen zu müssen. Neben Buttons gibt es Licht-, Hitze- und Lage-Sensoren. Es gibt Luftdruck-, Abstand- und Magnetfeld-Sensoren. Die meisten davon benötigen nur eine Verbindung mit der Stromversorgung (+/-) und eine Datenleitung zu einem Pin. Viele Sensoren funktionieren auch sowohl mit 3,3-Volt- als auch mit 5-Volt-Logik und können daher mit RasPis und Arduinos eingesetzt werden. Beim Kauf sollte man aber trotzdem darauf achten, dass die Module kompatibel mit dem Raspberry Pi sind.

### Aktoren
Auch für den Output gibt es viel zu entdecken: LEDs, Motoren/Servos, Sound. Mit Relais-Modulen lassen sich andere Geräte an- und ausschalten, Motoren mit einer Unwucht vibrieren wie ein Handy, mit Infrarot-LEDs kann man den Sender im Fernseher ändern oder ein Lautsprecher piepst wie R2D2.
