# 3D-Modelle und Dateistände

Die bereitgestellten Modelle gehören zu den überlieferten Unterlagen des Erstsemesterprojekts. Enes Türksever hat nach eigener Angabe an ihrer Gestaltung mitgewirkt. Die Modelle werden hier als Teil einer Teamleistung gezeigt.

## Bereinigung

Die beiden 3MF-Dateien wurden als schlanke Standard-3MF neu verpackt. Dabei wurden die vollständigen ursprünglichen Mesh-Daten und die Einheit Millimeter beibehalten. Entfernt wurden Slicer-Einstellungen, Vorschaubilder, interne Kennungen, persönliche Quelldateipfade und die Platzierung auf der Druckplatte. Es wurden keine Formdetails ergänzt.

| Modell | Eckpunkte | Dreiecke |
| --- | ---: | ---: |
| Bumper mit Stoßer | 3514 | 7040 |
| ESP-Platte | 5048 | 10112 |

Die zusätzlichen gleichnamigen STL-Dateien wurden aus diesen Netzen erzeugt. Die Geometrie ist dabei auf das Gleitkommaformat einer binären STL gerundet. STL speichert keine verbindliche Einheit; hier sind die Koordinaten als Millimeter zu interpretieren.

Die separat bereitgestellte Datei `bumper-mit-stosser-original.stl` ist ein weiterer überlieferter Modellstand. Ihr Geometrieinhalt wurde unverändert übernommen; nur der frei beschreibbare Dateikopf wurde neutralisiert. Sie ist nicht automatisch identisch mit dem Bumper-Netz der 3MF-Datei.

## Vor einem Druck

Die Dateien enthalten keine zugesicherten Druckprofile. Insbesondere die ESP-Platte muss gegebenenfalls im Slicer gedreht und auf die Druckfläche gelegt werden. Maße, Montagepunkte, Druckraum und Material sind vor dem Druck am eigenen Aufbau zu kontrollieren.
