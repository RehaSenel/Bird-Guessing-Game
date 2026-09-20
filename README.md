# Vogelarten-Ratespiel

Python projekt zum Lernen und Erkennen von Vogelarten anhand von Bildern. Die Daten werden über die GBIF API abgerufen, anschließend bereinigt und für das Spiel vorbereitet.

## Verwendete Bibliotheken

```python
import requests
import random
from PIL import Image
from io import BytesIO
import matplotlib.pyplot as plt
import time
```

### GBIF API

GBIF API wird als Datenquelle verwendet.

Zun¨æchst mit `find_taxonomy()` die Taxonomie `Aves` gesucht. Anschließen werden mit `get_species()` die verfügbaren Vogelarten abgerufen. Nach der Datenbereinigung stehen aktuell 188 verschiedene Vogelarten für das Spiel zur Verfügung.

Dann für jede Vogelart werden mit `get_occurences()` Beobachtungen mit Bildmaterial gesucht. Dabe werden unter anderem `StillImage` und Dabei werden unter anderem `StillImage` und `PRESENT` als Filter verwendet.

Weitere Informationen zur API finden Sie auf der folgende Website:

- [techdocs.gbif.org/en/openapi](https://techdocs.gbif.org/en/openapi/)


### Datenbereinigung

Die abgerufenen Bilddaten werden anhand verschiedener Metadaten überprüft. Ungeeignete Aufnahmen, beispielsweise Skelette, Präparate, Diagramme oder andere nicht-repräsentative Darstellungen, werden dabei herausgefiltert. Dadurch werden die für das Spiel verwendeten Bilddaten gezielter vorbereitet.


### Spiel

Das Spiel besteh sich aus zwei Modi.

#### 1. Lernmodus

`play_learning()` wählt zufällig eine Vogelart aus und zeigt bis zu drei Bilder dieser Art. Für jedes Bild werden vier mögliche wissenschafliche Namen angezeigt.

Die richtige Antwort wird sofot überprüft. Nach der anzeige der Bilder können die bereits gelernten Vogelarten gespeichert werden.

#### 2. Testmodus

`play()` verwendet die zuvor gelernten Vogelarten. Der Testmodus kann gestartet werden, sobald mindestens fünf Vogelarten gelernt wurden.

Zu jedem zufällig ausgewählten Bild werden vier möglicher Antworten angezeigt. Der Spieler verfügt über drei Leben und erh¨ælt für richtige Antworten Punkte.
