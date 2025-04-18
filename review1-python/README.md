# Review 1 Python

## Beurteiltes Projekt

|       | Bitte ausfüllen |
|-------|-----------------|
| Review von  | (uhlersan)           |
| Review durch  |   (rueegmau)         |
| Datum Review, von/bis |  25.03.25, 16:40 -16:50   |

## Review

| Thema                                                                      | Skala | Mängel* | Verbesserungsmöglichkeiten* |
|----------------------------------------------------------------------------|-------|--------|----------------------------|
| Datenquelle klar definiert (Projekt 2: zusätzlich Abgrenzung zu Projekt 1) | 2  | Datenquelle ist klar definiert und vom vorherigen Projekt abgegrenzt.    | Es könnten weitere Datensätze ergänzt werden, um aussagekräftigere Ergebnisse zu erhalten (z. B. via Scrapy).  | 
| Scraping automatisiert                                                     | 0  | Aktuell ist das Scraping noch nicht automatisiert.   | Scraping automatisieren, z. B. mit Scrapy oder Requests + BeautifulSoup.                |
| Datensatz vorhanden                                                        | 1  | Nur ein kleiner Test-Datensatz (10 Einträge) vorhanden  | Umfang des Datensatzes erhöhen, um bessere Modellleistung zu ermöglichen.                     |
| Erstellung Datensatz automatisiert, Verwendung Datenbank                   | 1  | Die Automatisierung und Integration in eine Datenbank fehlt bisher.  | MongoDB wie in der Vorlesung einsetzen, z. B. via pymongo.            |
| Datensatz-Grösse ausreichend, Aufteilung Train/Test, Kennzahlen vorhanden  | 1  | Datensatz ist zu klein, kaum Aufteilung möglich, keine aussagekräftigen Kennzahlen.  | Mehr Daten, Train/Test-Split einführen und Performance-Metriken (z. B. MAE, R²) berechnen.                    |
| Modell vorhanden                                                           | 1  | Modell ist vorhanden, funktioniert jedoch noch nicht gut – zu wenige Features.   | Zusätzliche Features integrieren und andere Modelltypen wie Linear Regression oder Random Forest testen.                    |
| Modell-Versionierung vorhanden (ModelOps)                                  | 0  |Bisher keine Versionierung oder Modell-Management vorhanden. | Modellversionierung analog zur Vorlesung implementieren, z. B. mit MLflow oder manuell in Azure verwalten.                    |
| App: auf lokalem Rechner gestartet und funktional                          | 1  | App wurde erstellt, läuft aber nicht stabil oder ist noch unvollständig.  | Struktur und Logik der App überarbeiten (Beispiel-Repo als Vorlage nehmen).                     |
| App: mehrere unterschiedliche Testcases durch Reviewer ausführbar          | 0  | Noch keine Tests implementiert.   | Unterschiedliche Eingaben als Testfälle definieren und Testskripte ergänzen.               |
| Deployment: Falls bereits vorhanden, funktional und automatisiert          | 0  | Noch kein Deployment umgesetzt.   | Deployment über GitHub Actions automatisieren.                       |
| Code: Git-Repository vorhanden, Arbeiten mit Branches / Commits            | 1  | Git wird genutzt, aber es wurde bisher nur einmal committet.  | Häufiger committen, sinnvolle Commit-Messages nutzen, optional mit Branches arbeiten.                 |
| Code: Dependency Management, Dockerfile, Build funktional                  | 2  | Dockerfile ist vorhanden und funktional. | Dockerfile optimieren, indem nur benötigte Packages installiert werden.                  |

\* wenn fehlend: mögliche Schwierigkeiten und Lösungen besprechen



## Skala

| Skala |                 |
|-------|-----------------|
| 0     | fehlt           |
| 1     | mit Lücken      |
| 2     | alles vorhanden |
| 3     | übertroffen     |

## Hinweise

Der Projekt-Review fliesst nicht in die Beurteilung der Leistungsnachweise ein, soll aber dem Studierenden dazu dienen, bis zur Abgabe noch Verbesserungsmöglichkeiten zu erkennen. Der Review *des fremden Projektes* muss als Teil des *eigenen* Lernjournals abgegeben werden.

