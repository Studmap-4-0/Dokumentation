# Dokumentation Studmap 4.0 Testumgebung

## Willkommen

Danke, dass Du Dich bereit erklärt hast, die Studmap 4.0 Testumgebung zu testen und Dein Feedback abzuegeben.
Dieser Prototyp dient als Proof of Concept für ein Geodatenportal für Foschung und Lehre am Fachbereich 14 Geowissenschaften der Universität Münster.
Der Prototyp ist, wenn Du erfolgreich mit dem VPN verbunden bist unter http://192.168.198.24:8080/geoserver/web/ zu erreichen.

## LayerVorschau

Im Menü lässt sich links unter Daten die Layer-Vorschau aufrufen. Sie lässt sich auch direkt mit folgendem Link aufrufen: http://192.168.198.24:8080/geoserver/web/wicket/bookmarkable/org.geoserver.web.demo.MapPreviewPage
Hier findet sich eine durchsuchbare Übersicht über die als Layer publizierten Daten. 
In der Spalte "Gängige Formate" lässt sich jeweils mit dem OpenLayers Link eine rudimentäre Kartenansicht des Layer aufrufen. In der Spalte "Alle Formate" stehen weitere Formate in einem Dropdown-Menü zur Ansicht bzw. zum Download bereit.

Für die Nutzung der Layer-Vorschau muss man nicht im Portal angemeldet sein.

## Web Processing Service

Auf den vorhandenen Daten lassen sich auch verschiedene Berechnungen als Web Processing Service durchführen.
Hierfür wählst Du im linken Menü Demo und dann im Hauptteil der Seite den WPS Request-Builder aus.
Als Beispiel wird unten die Berechnung des Vegetationsindex NDVI erläutert.
### NDVI

Um den NDVI anhand des vorhandenen Beispieldatensatze zu berechnen müssen im WPS Request-Builder folgende Schritte durchgeführt werden.

1. Im Dropdown-Menü unter "Prozess auswählen" die Option "ras:jiffle" wählen.
2. Unter den Prozessparametern folgendes auswählen bzw. eingeben
3. Unter Source "Raster(s)" im linken Dropdwon Menü erst "RASTER_LAYER" auswählen und dann im rechten Dropdown Menü "Sentil2:sentinel_rgbnir" auswählen.
4. In das Textfeld unter "script" dann folgendes kopieren: `nir = src[3]; vir = src[2]; dest = (nir - vir) / (nir + vir);`
5. Dann unten links auf "Prozess ausführen" klicken
6. Es öffnet sich ein Popup mit dem Text "Lade ........"
7. Nach einger Zeit stratet der Download des Ergebnisses.
8. Wenn der Download fertig ist, kann das Popup geschlossen werden

## Daten in QGIS als Layer einbinden

Da das Studmap 4.0 Portal seine Daten als OGC-konforme Web Map Services, Web Map Tile Services und Web Feature Services anbietet. Dementsprechend lassen sich die Daten auch in jeder Desktop-GIS Software, die diese Standards unterstützen nutzen. Erläutrt wird die nötige Vorgehensweise anhand der Open Source Desktop GIS Software [QGIS](https://qgis.org/de/site/forusers/download.html)

QGIS zeigt einen links einen Browser mit den möglichen Datenquellen an, hier kann das Portal an zwei einbinden.

1. Rechtsklick auf WMS/WMTS und dann "Neue Verbindung" bzw. "New Connection" wählen. Dort dann einen Namen deiner Wahl und due URL http://192.168.198.24:8080/geoserver/ows eintragen. Im Browser stehen danach alle WM(T)S Layer die das Portal anbieten zur Verfügung.
2. Rechtsklick auf WMS/WMTS und dann "Neue Verbindung" bzw. "New Connection" wählen. Dort dann einen Namen deiner Wahl und due URL http://192.168.198.24:8080/geoserver/ows?service=WFS&acceptversions=2.0.0&request=GetCapabilities eintragen. Im Browser stehen danach alle WFS Layer die das Portal anbieten zur Verfügung. (Stand zu Zeitpunkt der Dokumentationserstellung: 0)

Die entsprechenden Daten stehen dann zur Arbeit in QGIS zur Verfügung und lassen sich zum Beispiel einfach per Drag&Drop ins aktuelle Projekt einbinden.
Je nach Datentyp und Verwendungszweck ist die Darbietungsform die das Portal über die Web Services anbietet nicht ideal. Hier kann der Download der Daten über die Layerpreview (s.o.) abhilfe schaffen.

## Layer via QGIS hochladen

Es ist auch möglich mit QGIS Daten für das Portal hochzuladen. Hierfür benötigst du Deine Zugangsdaten.
Es muss das QGIS Plugion [GeoCat Bridge](https://geocat.github.io/qgis-bridge-plugin/latest/index.html) installiert werden.
Hierfür den Reiter Plugins auswählen. Dann links "All" bzw. "Alle" auswählen und GeoCat Bridge suchen und auswählen und unten rechts auf die Schaltfläöche "Install Plugin" bzw "Plugin installieren" klicken.

In der Toolbar erscheint dann ein Symbol "Publish", mit dem sich das Plugin dann einrichten und nutzen lässt.
Es muss der Reiter "Servers"ausgwählt werden und dort dann auf "New Server"geklickt und Geoserver ausgewählt werden.
Der Name des Servers ist frei wählbar.
Die URL muss http://192.168.198.24:8080/geoserver/web/ lauten.
Als Storage sollte "File-based Storage" gewählt werden.
Bei den Credentials müssen Deine Zugangsdaten für den Geosevereingegen werden. Hierfür musst Du auf das grüne Plus Klicken um sie hinzuzufügen. Gib einen Namen Deiner Wahl an, wähle Basic Authentification und gebe Deine Zugangsdaten bei Username und password ein. Eventuell verlangt QGIS ein Masterpassword von dir, um deine Credentials zu verwalten, dies kannst Du beliebig wählen.
Mit Test Connection lassen sich die Einstellungen dann überprüfen.

Um die Daten zu publizieren müssen diese als Layer im aktuellen Projekt vorhanden sein. Das Projekt muss auch gespeichert sein. Wähle hierfür am besten einen eindeutigen Namen.
Wähle dann im Menü des Plugins den Reiter Publish. Setze Haken bei den Layern, die du hochladen möchtest und gebe ihnen Rechts einen Titel.
Unten wählst du dann bei Data Server den gerade angelegten Server aus und klickst auf Publish. Die Daten werden dann hochgeladen und stehen im Portal zur Verfügung.

Nicht immer sogrt die Darstellungsart, die das Portal selbst wählt, für eine passende Darstellung in der Layer Preview oder den per Download oder Web Services verfügbaren Daten.
Hier kann durch das Hochladen eines passenden mit QGIS erstellen Stils Abhilfe geschaffen werden. 
Hierzu wird in QGIS die Symbologie des Layers entsprechend angepasst (Rechtsklick auf den Layer unten links, dann "Eigenschaften" bzw. "Properties" und dann "Symbologie" bzw. "Symbology"). Dort kann der Stzil dann auch exportiert werden. Im selben Menü wählt man unten "Stil" bzw. "Style" dann "Stil speichern" bzw. "Save Style" und dann als SLD Style speichern.
Um den Stil im Potral hochzuladen meldet euch unter http://192.168.198.24:8080/geoserver/web/ an.
Wählt links unter "Daten" "Stile" aus und klikct auf "Hinzufügen eines neuen Stils".
Wählt einen passenden Namen und ladet eure gerade erzeugte Stildatei hoch. Prüft mit der Schaltfläche "Validieren" auf Fehler und speichert den Stil dann mit der entsprechenden Schaltfläche.
Wechselt dann links unter "Daten" zu "Layer" und klickt auf den Layer, dem ihr den Stil hinzufügen wollt.
Klikct dann auf den Reiter "Publizierung" unter "WMS-Einstellungen" kann in einem Dropdown Menü der gerade hochgeladene Stil als Standardstil gesetzt werden.
Achtung: Einige Stil-Einstellungen können mit der Berechnung von Indices via WPS kollidieren und die Ergebnisse verfälschen. Im Zweifel kann vor der Berechnung einfach der Standardstil auf Raster gesetzt werden.
