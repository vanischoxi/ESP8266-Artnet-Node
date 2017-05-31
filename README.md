## ArtNet Node based on ESP8266  ##

Die erste Verson basierte auf einem arduino mit dem Funkmodul nrf24L01.
Vorteil ist ein geringer Stromverbrauch sowie eine properit�re Funkverbindung, die nicht so leicht geknackt werden kann.
F�r die Show werden 20 Module gebraucht. Der Aufwand f�r die Verdrahtung f�r das Funkmodul war mir einfach zu hoch.

Der folgende Ansatz basiert nun auf dem ESP8266. Die Hardware ist nun wesentlich schneller aufgebaut, da ich nur noch die Treiberstufe f�r die LED-Stripes hinzuf�gen muss. Das Modul hat nun einen Web-Server und s�mtliche Einstellungen k�nnen hier�ber vorgenommen werden. Weiterhin l�sst sich die Firmware einfach �ber OTA (Over The Air) aktualisieren. Weiterhin schicken die Module Nachrichten an einen Node-Server. �ber diesen Server kann man sehen, ob die Module alle Daten empfangen. F�r mich sehr beruhigend, da unmittelbar vor der Show eine gewisse Hektik ausbricht und man keine Zeit alle 20 Module zu pr�fen.



Node Server
F�r den Node Server gibt es Web-Interface, um den Status zu kontrollieren.



Web-Interface
Das Web-Interface basiert auf dieser Vorlage http://www.john-lassen.de/en/projects/esp-8266-arduino-ide-webconfig



DMX Settings

Die Module sind alle identisch aufgebaut � also keine Schalter oder DIP-Switches um eine Kodierung vorzunehmen.
Hier kann man die Rolle des Moduls bestimmen bzw. welche DMX-Kan�le verwendet werden.



Der DMX Kanal wird nicht direkt bestimmt, sondern man w�hlt hier z.B. den Fahrer aus.
Das Modul ermittelt dann selber den Kanal und generiert eine Namen f�r das Modul.
Dieser Name ist nachher auf dem node-Server und WLAN-Router sichtbar.



Gamma-Korrektur

�ber die Gamma-Korrektur l�sst sich die Helligkeit reduzieren.

DMX output

Das DMX-Paket wird dann �ber  Serial1 ausgegeben. Somit kann man beliebige Ger�te mit DMX-Eingang anbinden.

LED Pin

Ich habe mit mehreren Modulen experimentiert (NodeLUA, ESP12E) und unterschiedlichen Layouts.
Hier kann man die Zuordnung der LED Treiber zum PWM Pin ausw�hlen, so dass das Layout flexibel ist.



DMX-Sender

Backstage oder bei Proben, m�chte ich in der Lage sein die Module zu testen.
Jedes Modul kann eine Testsequenz per Multicast schicken.
Somit kann ich z.B. einen Fahrer ausw�hlen und sehen, ob dessen drei Module aktiv sind.



 

Hardware

Grunds�tzlich verwende ich ein NodeLua-Modul, welches auf dem ESP12E basiert.

Die erste Programmierung kann �ber USB erfolgen
Ein Spannungsregler ist bereits integriert
Achtung: es gibt Module, die f�r Vin nur 5V statt 12V haben
Die Treiberstufe befindet sich auf einer Platine, die auf der Unterseite verl�tet wird.
Damit ist das Modul kompakt und schnell aufgebaut.

Als Treiber verwende ich den IRLR7843 mit der Bauform D-PAK. Diese SMD Bauform ist klein (aber nicht zu klein) und l�sst sich gut auf eine Lochrasterplatine verl�ten.
Wichtig sind der R DS (on) von 3.3m Ohm und V GS (th) von 1,5-2,3V, da der ESP mit 3,3V arbeitet.

 

