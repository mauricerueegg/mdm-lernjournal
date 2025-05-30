# Lernjournal 2 Container

## Docker Web-Applikation

### Verwendete Docker Images

| | Bitte ausfüllen |
| -------- | ------- |
| Image 1 | Wordpress |
| Image 1 | https://hub.docker.com/repository/docker/mauricerueegg/wordpress |
| Image 2 | MySQL |
| Image 2 | https://hub.docker.com/repository/docker/mauricerueegg/mysql/general |
| Image 3 | MediaWiki |
| Image 3 | https://hub.docker.com/repository/docker/mauricerueegg/mediawiki/general |


### Dokumentation manuelles Deployment

#### 1. MediaWiki-Image herunterladen

Das offizielle MediaWiki-Image in Version 1.42.3 wird mit folgendem Befehl lokal heruntergeladen:

```bash
docker pull mediawiki:1.42.3
```

📷 **Screenshot: `docker pull` erfolgreich ausgeführt**  

![alt text](<images/mediawiki/Bildschirmfoto 2025-04-21 um 07.04.06.png>)

---

#### 2. Container starten

Starte den Container mit Portweiterleitung von `8081` auf `80`:

```bash
docker run --name some-mediawiki -p 8081:80 -d mediawiki:1.42.3
```

📷 **Screenshot: Container erfolgreich gestartet**  

![alt text](<images/mediawiki/Bildschirmfoto 2025-04-21 um 07.04.34.png>)

---

#### 3. Container- und Image-Verwaltung in Docker Desktop

Vergewissere dich, dass:

- Das Image `mediawiki:1.42.3` vorhanden ist
- Der Container `some-mediawiki` läuft und Port 8081 verwendet wird

📷 **Screenshot: MediaWiki-Image sichtbar**  

![alt text](<images/mediawiki/Bildschirmfoto 2025-04-21 um 07.05.07.png>) 

📷 **Screenshot: Container läuft mit Portbindung**  
![alt text](<images/mediawiki/Bildschirmfoto 2025-04-21 um 07.05.16.png>)

---

#### 4. Setup im Browser

Rufe die Anwendung im Browser unter `http://localhost:8081` auf. Die Setup-Seite erscheint automatisch:

📷 **Screenshot: Setup-Seite erkannt `LocalSettings.php not found`**  

![alt text](<images/mediawiki/Bildschirmfoto 2025-04-21 um 07.05.22.png>)

Klicke auf „set up the wiki“, um die Installation zu starten.

---

#### 5. MediaWiki konfigurieren

Wähle die gewünschte Sprache und folge dem Schritt-für-Schritt-Installationsassistenten.

📷 **Screenshot: Sprache auswählen im Setup-Wizard**  

![alt text](<images/mediawiki/Bildschirmfoto 2025-04-21 um 07.05.29.png>)

### Dokumentation Docker-Compose Deployment

#### 1. Manuelle Vorbereitung (Alternative zur `docker-compose.yml`)

```bash
docker run --name local-mysql \
  -e MYSQL_ROOT_PASSWORD=12345 \
  -e MYSQL_DATABASE=wordpress \
  -e MYSQL_USER=wordpress \
  -e MYSQL_PASSWORD=wordpress \
  -v mysql-data:/var/lib/mysql \
  -d mysql:9.1.0
```

📷 **Screenshot: MySQL-Container wird gestartet**  
![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.10.35.png>)

```bash
docker run --name local-wordpress \
  -p 8082:80 \
  -v wordpress-data:/var/www/html \
  -d wordpress:6.7.0-php8.3
```

📷 **Screenshot: WordPress-Container wird gestartet**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.10.47.png>)

---

#### 2. Kontrolle über Docker Desktop

Stelle sicher, dass beide Container korrekt laufen:

📷 **Screenshot: laufende Container**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.11.00.png>)

---

#### 3. Netzwerkverbindung herstellen

Damit sich WordPress mit der Datenbank verbinden kann, müssen beide Container im selben Netzwerk sein:

```bash
docker network create --attachable wordpress-network
docker network connect wordpress-network local-mysql
docker network connect wordpress-network local-wordpress
```

📷 **Screenshot: Netzwerkverbindung zwischen Containern**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.11.47.png>)

---

#### 4. WordPress Setup starten

Rufe im Browser `http://localhost:8082` auf. Gib die Verbindungsdaten zur Datenbank ein:

- DB-Name: `wordpress`
- Benutzername: `wordpress`
- Passwort: `wordpress`
- DB-Host: `local-mysql` (weil im Docker-Netzwerk verbunden)

📷 **Screenshot: WordPress Setup Maske für DB-Verbindung**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.18.01.png>)
---

#### 5. Benutzer- und Website-Einstellungen

Fülle die Felder für Titel, Benutzername, Passwort und E-Mail-Adresse aus:

📷 **Screenshot: WordPress 5-Minuten-Installation**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.19.15.png>)
---

#### 6. Login-Maske und Dashboard

Nach erfolgreicher Einrichtung kannst du dich anmelden:

📷 **Screenshot: Login-Maske**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.19.31.png>)

📷 **Screenshot: WordPress Dashboard**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.19.48.png>)
---

#### 7. Deployment mit Docker Compose

```bash
docker-compose up -d --build
```

📷 **Screenshot: VS Code mit docker-compose.yml + Ausführung**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.29.56.png>)

📷 **Screenshot: Erfolgreiches Deployment mit `up -d --build`**  

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.30.16.png>)

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.30.57.png>)

![alt text](<images/wordpress/Bildschirmfoto 2025-04-21 um 07.31.50.png>)

## Deployment ML-App

???

### Variante und Repository

| Gewähltes Beispiel | Bitte ausfüllen |
| -------- | ------- |
| onnx-sentiment-analysis | Ja |
| onnx-image-classification | Ja |
| Repo URL Fork | https://github.com/mauricerueegg/onnx-sentiment-analysis |
| Repo URL Fork | https://github.com/mauricerueegg/onnx-image-classification |
| Docker Hub URL | https://hub.docker.com/repository/docker/mauricerueegg/onnx-sentiment-analysis |
| Docker Hub URL | https://hub.docker.com/repository/docker/mauricerueegg/onnx-image-classification/general |

### Dokumentation lokales Deployment sentiment-analysis

#### 1. Lokales Docker Image bauen

Das Docker-Image wird lokal mit folgendem Befehl erstellt:

```bash
docker build -t rueegmau/onnx-sentiment-analysis .
```

📷 **Screenshot: Erfolgreicher Build-Prozess**  
![alt text](<images/onnx-sentiment-analysis/Bildschirmfoto 2025-04-25 um 16.19.56.png>)

---

#### 2. Container lokal starten

Starte den Container und mappe den internen Port 5000 auf Port 9000 lokal:

```bash
docker run --name onnx-sentiment-analysis -p 9000:5000 -d rueegmau/onnx-sentiment-analysis
```

📷 **Screenshot: Container-Start mit `docker run`**  
![alt text](<images/onnx-sentiment-analysis/Bildschirmfoto 2025-04-25 um 16.20.14.png>)

---

#### 3. Überprüfung mit Docker Desktop

Nach dem Start ist der Container in Docker Desktop sichtbar:

- CPU- und RAM-Nutzung
- Offen auf Port 9000

📷 **Screenshot: Container in Docker Desktop aktiv**  
![alt text](image.png)

---

#### 4. Applikation im Browser testen

Die Anwendung ist im Browser unter `http://localhost:9000` verfügbar. Es kann ein Text eingegeben werden, der vom RoBERTa-Modell analysiert wird.

📷 **Screenshot: UI im Browser bei Texteingabe**  
![alt text](<images/onnx-sentiment-analysis/Bildschirmfoto 2025-04-25 um 16.20.45.png>)
---

#### 5. Optional: Image in Docker Desktop prüfen

In Docker Desktop ist das Image unter `Images` sichtbar:

📷 **Screenshot: Docker Image unter Images sichtbar**  
![alt text](<images/onnx-sentiment-analysis/Bildschirmfoto 2025-04-25 um 16.21.19.png>)
---

### Dokumentation lokales Deployment image-classification

#### 1. Docker Image lokal bauen

Erstelle das Image auf Basis des `Dockerfile` im aktuellen Verzeichnis:

```bash
docker build -t rueegmau/onnx-image-classification .
```

📷 **Screenshot: Erfolgreicher Docker Build**  
![alt text](<images/onnx-image/Bildschirmfoto 2025-04-25 um 16.28.33.png>)

---

#### 2. Container starten

Starte den Container und mappe Port 5000 auf Port 9000:

```bash
docker run --name onnx-image-classification -p 9000:5000 -d rueegmau/onnx-image-classification
```

📷 **Screenshot: Ausführung des Docker Containers**  

![alt text](<images/onnx-image/Bildschirmfoto 2025-04-25 um 16.28.42.png>)
---

#### 3. Überprüfung in Docker Desktop

Vergewissere dich, dass der Container aktiv ist und auf dem richtigen Port läuft:

📷 **Screenshot: Laufender Container in Docker Desktop**  
![👉 _Siehe Bild: `Bildschirmfoto 2025-04-25 um 16.28.42.png`_](<images/onnx-image/Bildschirmfoto 2025-04-25 um 16.28.51.png>)

---

#### 4. Anwendung im Browser testen

Gehe zu `http://localhost:9000`, lade ein Bild hoch (JPEG, PNG) und lasse es durch das Modell klassifizieren.

📷 **Screenshot: Webanwendung mit klassifiziertem Bild**  

![alt text](<images/onnx-image/Bildschirmfoto 2025-04-25 um 16.28.06.png>)
---

#### 5. Image in Docker Desktop prüfen

Das erzeugte Image kann in Docker Desktop unter „Images“ gefunden werden:

📷 **Screenshot: Lokales Docker-Image sichtbar**  

![alt text](<images/onnx-image/Bildschirmfoto 2025-04-25 um 16.29.01.png>)

---

#### 6. Image auf Docker Hub pushen

Falls du das Image auf Docker Hub veröffentlichen möchtest:

```bash
docker push mauricerueegg/onnx-image-classification:latest
```

📷 **Screenshot: Erfolgreicher Push zu Docker Hub**  

![alt text](<images/onnx-image-dockerhub/Bildschirmfoto 2025-04-26 um 08.22.51.png>) 
![alt text](<images/onnx-image-dockerhub/Bildschirmfoto 2025-04-26 um 08.22.28.png>)

### Dokumentation Deployment Azure Web App

Melde dich in der Azure CLI an, um Zugriff auf deine Subscriptions zu erhalten:

```bash
az login
```

📷 **Screenshot: CLI Login und Subscription Auswahl**  

![alt text](<images/azure/azure_web_app/Bildschirmfoto 2025-04-27 um 20.04.23.png>)

Erstelle eine neue Ressourcengruppe für die App:

```bash
az group create --name sw03-appservice --location switzerlandnorth
```

📷 **Screenshot: Erfolgreiche Erstellung der Ressourcengruppe**  

![alt text](<images/azure/azure_web_app/Bildschirmfoto 2025-04-27 um 20.04.36.png>)

Erstelle einen App Service Plan im Free Tier (Linux):

```bash
az appservice plan create \
  --name onnx-sentiment-analysis \
  --resource-group sw03-appservice \
  --sku F1 \
  --is-linux
```

📷 **Screenshot: Ausgabe bei erfolgreichem Erstellen des Plans**  

![alt text](<images/azure/azure_web_app/Bildschirmfoto 2025-04-27 um 20.04.59.png>)

```bash
az webapp create \
  --resource-group sw03-appservice \
  --plan onnx-sentiment-analysis \
  --name onnx-sentiment-analysis-12345 \
  --runtime "PYTHON:3.9"
```


Navigiere im Azure Portal zur Ressourcengruppe `sw03-appservice` und überprüfe die erfolgreiche Erstellung und den Status der Web App.


📷 **Screenshot: Ressourcengruppe und Web App im Azure Portal**  

![alt text](<images/azure/azure_web_app/Bildschirmfoto 2025-04-27 um 20.03.51.png>)


Im Azure Portal kannst du unter der Web App den Live-Log-Stream aktivieren, um Ausgaben der App zu verfolgen:

📷 **Screenshot: Live-Log-Stream bei Start der App**  

![alt text](<images/azure/azure_web_app/Bildschirmfoto 2025-04-27 um 20.03.14.png>)


### Dokumentation Deployment ACA

#### 1. Azure Container App Environment erstellen

Zuerst ein Container App Environment in der gewünschten Region (hier: `westeurope`) erstellen:

```bash
az containerapp env create \
  --name onnx-image-classification \
  --resource-group rueegmau \
  --location westeurope
```

> ℹ️ Falls kein Log Analytics Workspace existiert, wird automatisch einer erstellt.

📷 **Screenshot: Erstellung des ACA-Environments inkl. Log Analytics**  
![👉 _Siehe Bild: `Bildschirmfoto 2025-04-27 um 21.05.42.png`_](<images/azure/aca/Bildschirmfoto 2025-04-27 um 21.05.42.png>)

---

#### 2. Container App deployen

Danach den eigentlichen Container mit einem eigenen Image deployen. Das Image muss z. B. auf Docker Hub verfügbar sein.

```bash
az containerapp create \
  --name onnx-image-classification \
  --resource-group rueegmau \
  --environment onnx-image-classification \
  --image mauricerueegg/onnx-image-classification:latest \
  --target-port 5000 \
  --ingress external \
  --query properties.configuration.ingress.fqdn
```

📷 **Screenshot: Erfolgreiches Deployment mit Zugriff auf öffentliche URL**  
lernjournal2-container/images/azure/aca/Bildschirmfoto 2025-04-27 um 21.06.00.png
---

#### 3. Anwendung im Browser testen

Nach erfolgreicher Erstellung ist die Webanwendung unter der angegebenen URL erreichbar. Hier kannst du ein Bild im `.jpeg`- oder `.png`-Format hochladen, um es klassifizieren zu lassen.

📷 **Screenshot: UI der ACA-basierten Anwendung**  

![alt text](<images/azure/aca/Bildschirmfoto 2025-04-27 um 21.05.18.png>)


### Dokumentation Deployment ACI

#### 1. Ressourcengruppe erstellen

```bash
az group create --location switzerlandnorth --name mdm-aci
```

📷 **Screenshot: Erstellung der Ressourcengruppe**  
![👉 _Siehe Bild: `Bildschirmfoto 2025-04-29 um 15.44.33.png`_](<images/azure/aci/Bildschirmfoto 2025-04-29 um 16.35.08.png>)

---

#### 2. Container Instanz erstellen

```bash
az container create \
  --resource-group mdm-aci \
  --name onnx-image-classification \
  --image mauricerueegg/onnx-image-classification:latest \
  --dns-name-label onnx-image-classification-mr123 \
  --ports 5000 \
  --os-type Linux \
  --cpu 1 \
  --memory 1.5
```

📷 **Screenshot: Deployment der Container Instanz**  
![alt text](<images/azure/aci/Bildschirmfoto 2025-04-29 um 15.44.20.png>)

---

#### 3. Container testen (via curl oder im Browser)

```bash
curl http://onnx-image-classification-mr123.switzerlandnorth.azurecontainer.io:5000
```

Wenn du eine blockierte Webseite angezeigt bekommst (z. B. von einem Proxy), kannst du alternativ über das öffentliche Internet zugreifen.

📷 **Screenshot: Blockierte Seite via curl**  
![👉 _Siehe Bild: `Bildschirmfoto 2025-04-29 um 16.05.59.png`_](<images/azure/aci/Bildschirmfoto 2025-04-29 um 15.44.33.png>)

---

#### 4. Applikation im Browser aufrufen

Die Applikation ist direkt über die bereitgestellte Domain erreichbar, z. B.:

```
http://onnx-image-classification-mr123.switzerlandnorth.azurecontainer.io:5000
```

📷 **Screenshot: Funktionierende UI über ACI**  
![👉 _Siehe Bild: `Bildschirmfoto 2025-04-29 um 16.35.08.png`_](<images/azure/aci/Bildschirmfoto 2025-04-29 um 16.05.59.png>)