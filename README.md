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

## Layer via QGIS hochladen
