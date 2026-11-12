# Fahrzeugsoftware

## Grundlage

Der dokumentierte Programmstand stammt aus dem Quellcode-Anhang der Projektdokumentation von 2023/24. Er verwendet **C++ mit der Arduino-Umgebung auf einem ESP32**. RemoteXY übernimmt die Smartphone-Anbindung über Bluetooth Low Energy. Eine Python-Implementierung ist in den bereitgestellten Unterlagen nicht enthalten.

Die Datei im Ordner `src` ist ein überlieferter Dokumentationsstand, keine nachträglich vervollständigte oder am Fahrzeug neu geprüfte Firmware. Der persönliche Bluetooth-Gerätename wurde durch `ESP-RoboCar` ersetzt; die Programmlogik blieb unverändert.

## Ablauf

1. `setup()` initialisiert RemoteXY, die serielle Ausgabe und die Ein- bzw. Ausgänge.
2. `loop()` verarbeitet RemoteXY-Eingaben. Zwei Reglerwerte werden von `-100 … 100` auf `-255 … 255` abgebildet.
3. Beide analogen Liniensensoren werden ausgelesen.
4. Erreicht mindestens ein Sensor den Schwellwert `3000`, ruft das Programm `fahreRueckwaerts()` auf. Nach `700 ms` werden die Motorausgänge auf null gesetzt; anschließend wartet das Programm `2000 ms`.
5. Außerhalb dieser Grenzerkennung steuern Richtung und Betrag der Reglerwerte die beiden Motoren getrennt.
6. Zwei Schaltausgänge werden aus den App-Werten gesetzt; zur Diagnose werden beide Sensorwerte seriell ausgegeben.

Die Grenzreaktion ist damit mehr als ein unmittelbarer Stopp: Der dokumentierte Stand setzt zunächst zurück. Ob dies in jeder späteren Vorführung genauso eingestellt war, lässt sich aus dem Code-Anhang allein nicht ableiten.

## Werte im überlieferten Stand

| Einstellung | Wert im Anhang |
| --- | --- |
| Linker Motor, Richtungsausgänge | `3`, `2` |
| Rechter Motor, Richtungsausgänge | `19`, `18` |
| Sensoranschlüsse | `A0`, `A1` |
| Zusätzliche Schaltausgänge | `11`, `9` |
| Schwellwert der Linienerkennung | `3000` |
| Rückfahrwerte links / rechts | `235` / `255` |
| Serielle Schnittstelle | `9600 Baud` |

Diese Angaben beschreiben den Anhang. Sie sind keine geprüfte Anschlussanleitung für ein beliebiges ESP32-Board. Die proseartige Hardwarebeschreibung und der Code nennen teilweise unterschiedliche Motorpins; die genaue Boardvariante und Bibliotheksversionen sind nicht eindeutig überliefert. Vor einer Inbetriebnahme müssen Pinbelegung, Analog-Eingänge, PWM-Unterstützung und Motortreiber am tatsächlichen Aufbau geprüft werden.

## Fehlende Bestandteile und Grenzen

- In `RemoteXY_CONF` steht nur `// ... Konfigurationsbytes ...`. Die passende App-Oberfläche und ihre erzeugte Konfiguration fehlen.
- Wegen der fehlenden Konfiguration wurde die Datei nicht als unmittelbar nutzbare Firmware ausgewiesen. Die Klammerstruktur des ausgelesenen Codes ist vollständig.
- Die Definitionen des Bluetooth-Gerätenamens und des Zugriffspassworts stehen im Anhang erst nach den Bibliotheks-Includes. Die richtige Reihenfolge muss bei einer Wiederherstellung mit der verwendeten Bibliotheksversion geprüft werden.
- Während der beiden `delay()`-Aufrufe wird `RemoteXY_Handler()` nicht aufgerufen. Eine nicht blockierende Umsetzung wäre für eine Weiterentwicklung sinnvoll.
- Das Feld `verbindungStatus` wird nicht zur Motorfreigabe ausgewertet. Ein ausdrücklicher Stopp bei Verbindungsabbruch ist in diesem Stand nicht implementiert.
- Die Sensoren erfassen Reflexion. Der Schwellwert hängt unter anderem von Oberfläche, Abstand und Beleuchtung ab.

Eine Wiederherstellung sollte die fehlende RemoteXY-Konfiguration ergänzen, die Board- und Anschlussdaten klären und danach Motoren, Sensorik und Verbindungsabbruch separat am Fahrzeug testen. Das wäre eine neue Überarbeitung und ist hier nicht als ursprüngliche Projektleistung ausgegeben.
