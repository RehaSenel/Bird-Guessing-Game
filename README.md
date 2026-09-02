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

Zun¨æchst mit `find_taxonomy()` die Taxonomie `Aves` gesucht. Anschließen werden mit `get_species()` die verfügbaren Vogelarten abgerufen.

Dann für jede Vogelart werden mit `get_occurences()` Beobachtungen mit Bildmaterial gesucht. Dabe werden unter anderem `StillImage` und Dabei werden unter anderem `StillImage` und `PRESENT` als Filter verwendet.

Weitere Informationen zur API finden Sie auf der folgende Website:

- [techdocs.gbif.org/en/openapi](https://techdocs.gbif.org/en/openapi/)

### Spiel

Das Spiel besteh sich aus zwei Modi.

#### 1. Lernmodus

`play_learning()` wählt zufällig eine Vogelart aus und zeigt bis zu drei Bilder dieser Art. Für jedes Bild werden vier mögliche wissenschafliche Namen angezeigt.

Die richtige Antwort wird sofot überprüft. Nach der anzeige der Bilder können die bereits gelernten Vogelarten gespeichert werden.

#### 2. Testmodus

`play()` verwendet die zuvor gelernten Vogelarten.

Zu jedem zufällig ausgewählten Bild werden vier möglicher Antworten angezeigt. Der Spieler verfügt über drei Leben und erh¨ælt für richtige Antworten Punkte.

### Mögliche Verbesserungen

#### Genauere Filterung der Bilddaten

Aktuelle Filterung entfernt bereits viele ungeeignete Bilder anhand von Metadaten und Bildquellen. Trotzdem kann es vorkommen, dass nach der Filterun noch Bilder enthalten sind, die keine geeignete Vogelaufnahmen darstellen, beispielsweise, Knochen, Skelette oder andere nicht-repräsentative Darstellungen.

Eine weitere einschränkung ist die Auswahl der Daten über den API-Parameter `limit`. Eine Erhöhung des Limits fürht nicht automatisch zu einer entsprechend größeren Anzahl an unterschiedlichen Vogelarten. Beispielsweise wurden bei einem Limit von 200 nur 48 verschiedene Einträge erhalten, während ein Limit von 1000 die Anzahlt nur auf etwas mehr als 55 erhöhte.

Eine mögliche Verbesserung wäre daher eine gezieltere Auswahl der Vogelarten sowie eine weitergehende automatische Bildprüfung oder eine zusätzliche manuelle Kontrolle der vorbereiten Bilddaten.

#### Verbesserte Auswahl der Antwortmöglichkeiten

Im aktuellen Testmodus werden die drei falschen Antworten zufällig aus den gelernten Vogelarten ausgewählt. Dadurch sind die Antwortmöglichkeiten nicht immer optimal ausgewogen.

eine mögliche Verbesserung wäre, zwei Antworten zufällig auszuwählen und zusätlich eine Antwort gezierlt aus den bereits gelernten Vogelarten zu bestimmen. Dadurch könnten die Fragen kontrolliert und die Ergebnisse der Tests aussagekräftiger werden.
