---
order: 80
---

# Netiquette

Die Anzahl Meshtastic Nodes in der Schweiz erhöht sich Woche für Woche und damit wächst auch die Ausbreitung des
Meshes. Theoretisch ist es mittlerweile möglich, Nachrichten vom Bodensee bis an den Genfersee zu schicken. Auf dem
Primären `Medium Fast` Kanal werden aber auch Positions-, Device- und Telemetriedaten versendet, die zu immer mehr
Datenkollisionen führen und das “Mesh” unnötig belasten. Hier einige Tipps zur Geräteeinstellung, um das Mesh zu
entlasten.

---

## Device
### Device Role
||| `Device role` - Fall A:
Ihr habt Zugang zum Mesh über einen benachbarten, gut gelegenen Node (z.B. auf einem Berggipfel):
- stellt euren Node auf `Client_Mute`
||| `Device role` - Fall B:
Ihr habt selbst einen gut gelegenen Node, von dem andere profitieren, weil diese sonst keinen Zugang hätten:
- stellt euren Node auf `Client`

Solltet Ihr mehrere Nodes zuhause haben, stellt bitte gegebenenfalls nur den Haupt-Node auf `Client`, die
anderen auf `Client_Mute`. der Node in eurem Auto, das bei euch vor dem Haus steht, sollte im Modus
`Client_Mute` sein.

Router, Repeater **nur für Nodes** an topographisch sinnvollen Positionen wie Berggipfel oder Hochhäuser mit
freier Sicht.

Das Mesh wird nicht besser nur weil zusätzliche Nodes dazukommen. Die Nodes benötigen auch die die
passende Rollen und Positionen. Siehe: https://www.youtube.com/watch?v=htjwtnjQkkE
|||

### Node Info
| <!-- -->    | <!-- -->    |
|-------------|-------------|
| `NodeInfo broadcast interval`         | 10800 Sekunden (3h)        |

!!! Was steckt in den NodeInfo-Aussendungen ?
- Long- und Short-Name
- Node-Typ (z.B. LILYGO_TBEAM, HELTEC usw.)
- Rolle (z.B. Client_Mute, Router usw.)
!!!

Die Standard Einstellung ist 3h (10'800 Sekunden).
Unsere Smartphones merken sich in der Nodeliste diese Information für jeden. Es ist darum nicht nötig weniger als 3h in den
Settings einzustellen.

### Rebroadcast
| <!-- -->    | <!-- -->    |
|-------------|-------------|
| `Rebroadcast mode`         | ALL|

In der Schweiz/EU gilt eine gesetzliche Grenze von 10% Sendezeit pro Stunde und Gerät. Sollte die “Airtime” eurer Node
zu hoch sein, es also knapp werden mit den 10% Sendezeit, könnt ihr versuchsweise den “Rebroadcast Mode” auf “Local
only” stellen. Dadurch werden von eurer Node nur noch Nachrichten weitergegeben, die eurem Primary oder Sekundary
Kanal entsprechen.

## Position
| <!-- -->    | <!-- -->    |
|-------------|-------------|
| `Broadcast intervall`         | 21600 Sekunden (6h)|
| `Smart position`         | OFF |

!!! Was steckt in den Positions-Aussendungen?
- Länge- und Breiten-Angabe und falls gewählt auch die:
- Höhe,
- Uhrzeit,
- Anzahl der empfangenen Satelliten,
- Geschwindigkeit über Grund
!!!

Unsere Empfehlung ist die Position nur alle 6h (21'600 Sekunden) auszusenden.

Natürlich könnt Ihr auch mal eine andere Zeit einstellen, wenn ihr unterwegs seid, am Wandern oder Bergfunken. Wenn ihr
aber euren Node fix montiert habt, dann sind 6h ausreichend. Unsere Smartphones merken sich ja auf der Karte wo jeder ist.

!!!danger 
Bitte **schaltet unbedingt die «Smart-Position» Funktion aus**. Ansonsten sendet euer Node alle 2-3 Minuten eure
Position und müllt das ganze Mesh zu.
!!!

## Telemetrie
### Device Metrics
| <!-- -->    | <!-- -->    |
|-------------|-------------|
| `Device Metrics Interval`         | 259200 Sekunden (72h)* |

-> Android-User: lasst den Wert nicht auf 0 stehen. Sonst wird der Standard-Intervall von 30min benutzt.

!!! Was steckt in den DeviceTelemetrie-Aussendungen ?
- Uhrzeit
- Batterie-Spannung
- „Channel_Utilization“: wie sehr der Kanal bei euch belegt ist (in %)
- „Air_Util_Tx“: wie oft euer Node sendet (in %)
- „Uptime_Seconds“: Wie lange ihr schon online seid
!!!

Diese Information kann interessant sein, wenn ihr einen Remote Node (z.B. irgendwo auf dem Berg) betreibt und den
Zustand überwachen wollt.

!!!danger
Steht aber der Node bei euch zuhause auf dem Fensterbrett, liegt im Auto, oder er steckt in eurer Tasche, dann ist
es recht sinnbefreit diese Information ständig ins Netz zu senden. Ihr seht ja euren Batterielevel mittels Bluetooth
oder WLAN auf eurem Smartphone. Die anderen User im Mesh interessieren sich sicher recht wenig für den Ladezustand
eures Nodes.
!!!

Unsere Empfehlung ist daher die DeviceTelemetrie auf das Maximum einzustellen: 72h (= 259'200 Sekunden)

### Sensor Metrics
| <!-- -->    | <!-- -->    |
|-------------|-------------|
| `Sensor Metrics Interval`         | Alles auf OFF |

!!! Was steckt in den EnvironmentTelemetrie-Aussendungen ?
- Uhrzeit
- Temperatur, Luftdruck, Luftfeuchtigkeit usw. (falls diese Sensoren angeschlossen sind)
!!!

Das kann spannend sein, falls richtig gemacht und nicht ständig ausgesandt.
Falls keine Sensoren verbaut, stellt im App alle Sensoren auf «OFF»

-> Falls ihr Sensoren verbaut habt, stellt die Intervall-Zeit bitte möglichst lange ein z.B. 3'600 Sekunden (1h)

### Power Metrics
| <!-- -->    | <!-- -->    |
|-------------|-------------|
| `Sensor Metrics Interval`         |  OFF |

!!! Was steckt in den PowerTelemetrie-Aussendungen ?
- Strom und Spannungswerte
!!!

Das hat nichts mit dem Batterie-Level eurer Node zu tun.
Hierbei handelt es sich um externe Sensoren zur Strom- und Spannung-Messung.

## Lora
| <!-- -->    | <!-- -->    |
|-------------|-------------|
| `Hop limit`         |  **5** <br> Die Mesh Struktur ist nicht für die Größe des Netzes ausgelegt, die wir mittlerweile haben. Darum sollte das Hop limit nicht über 5 liegen.|
| `Override Duty Cycle` | **disabled** <br> In der Schweiz/EU gilt eine gesetzliche Grenze von 10% Sendezeit pro Stunde und Gerät |
| `Ignore MQTT` | **ON** (Das heisst: das „Ignorieren“ ist aktiviert) <br> MQTT nur für spezifische Anwendungen verwenden und Upload zu LongFast **unbedingt ausschalten**.|

## Firmware
!!!danger
Bitte aktualisiert eure Firmware regelmässig
!!!

Das geht mit dem Web-Flasher wirklich kinderleicht und ist in 3 Minuten erledigt.
Die Software wird stetig weiterentwickelt und die Mesh Struktur dadurch immer effizienter !

→ Den Web-Flasher findet ihr hier: https://meshtastic.org/docs/getting-started/flashing-firmware/esp32/web-flasher/


## Fragen?
Bei Fragen wendet Euch bitte an:

- Forum Mesh Schweiz: https://forum.mesh-schweiz.ch
- Meshtastic Schweiz Facebook Gruppe: https://www.facebook.com/groups/771317178261325/
- GitHub Meshtastic Schweiz: https://github.com/orgs/meshtastic/discussions/24

## Netiquette Autoren
!!! Disclaimer
Die Netiquette wurde **nicht** durch Mesh Schweiz verfasst, sondern durch verschiedene versierte Personen. Hier der [Link](https://drive.google.com/file/d/14Wd3UXRfnrliED6sUjJXb7UYsQ3iZCbp/edit) zum Origial der Netiquette.
!!!



