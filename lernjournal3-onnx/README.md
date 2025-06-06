# Lernjournal 3 ONNX

## Übersicht

| | Bitte ausfüllen |
| -------- | ------- |
| ONNX Modell für Analyse (Netron) | https://github.com/onnx/models/blob/main/Computer_Vision/efficientnet_b0_Opset16_timm/efficientnet_b0_Opset16.onnx |
| onnx-image-classification Fork (EfficientNet-Lite) | https://github.com/onnx/models/tree/main/validated/vision/classification/efficientnet-lite4/model |
| onnx-image-classification Fork Repo | https://github.com/mauricerueegg/onnx-image-classification.git |

## Dokumentation ONNX Analyse

Ziel dieses Lernjournals war es, die ONNX Runtime zu verstehen, ein eigenes ONNX-Modell einzubinden, es mit dem Tool Netron zu analysieren und die Inferenz in einer Webapplikation umzusetzen.

📘 Dokumentation ONNX Analyse

Ziel dieses Lernjournals war es, die ONNX Runtime zu verstehen, ein eigenes ONNX-Modell einzubinden, es mit dem Tool Netron zu analysieren und die Inferenz in einer Webapplikation umzusetzen.

🧠 Verwendetes Modell

Das verwendete Modell ist EfficientNet-Lite4 (und alternativ EfficientNet-B0 OpSet16). Beide Modelle basieren auf der EfficientNet-Architektur, die besonders effizient in der Klassifikation ist und in vielen mobilen sowie embedded ML-Anwendungen genutzt wird.

Modellgrössen:
	•	EfficientNet-B0: kleineres Modell, schneller, weniger genau.
	•	EfficientNet-Lite4: grösser, benötigt mehr Ressourcen, liefert aber eine bessere Genauigkeit.

🔍 Analyse mit Netron

Die Netzwerkstruktur wurde mit Netron analysiert.
	•	Die Architektur zeigt typische CNN-Schichten wie Conv, BatchNormalization, Clip, Transpose.
	•	Die Eingabegröße beträgt: 1x224x224x3 (RGB-Bild).
	•	Beispielhafte Layer:
	•	Conv (3x3) mit 32 Filtern
	•	Strides 2x2 zur Reduktion der Auflösung
	•	Clip Layer zur Aktivierungsbegrenzung (ReLU6)
	•	BatchNorm zur Stabilisierung der Lernrate


efficientnet-lite4-11.onnx
![alt text](<images/Bildschirmfoto 2025-05-04 um 09.28.27.png>)

efficientnet_b0_OpSet16.onnx
![alt text](<images/Bildschirmfoto 2025-05-04 um 09.28.59.png>)

## Dokumentation onnx-image-classification

Die vorhandene Web-Applikation onnx-image-classification wurde geforkt und angepasst. Das ONNX-Modell wurde im Flask-Backend eingebunden und über eine einfache Web-Oberfläche ansprechbar gemacht.

🔄 Modell-Austausch

Im Backend wurde die ONNX-Datei durch ein anderes Modell ersetzt:

<pre>
```python
ort_session = onnxruntime.InferenceSession("efficientnet-lite4-11.onnx")
```
</pre>

![alt text](<images/Bildschirmfoto 2025-05-04 um 09.07.42.png>)

🔁 Vergleichsweise wurde auch efficientnet_b0_OpSet16.onnx getestet:

<pre>
```python
ort_session = onnxruntime.InferenceSession("efficientnet_b0_OpSet16.onnx")
```
</pre>

![alt text](<images/Bildschirmfoto 2025-05-04 um 09.09.33.png>)

🖼️ Bildanalyse-Vergleich

Bild: Matterhorn (JPEG)


Mit EfficientNet-Lite4:
	•	lakeside: 0.0131
	•	valley: 0.0125
	•	mountain tent: 0.0002

![alt text](<images/Bildschirmfoto 2025-05-04 um 09.08.44.png>)


Mit EfficientNet-B0:
	•	alp: 0.9733
	•	lakeside: 0.0131
	•	valley: 0.0125

![alt text](<images/Bildschirmfoto 2025-05-04 um 09.50.15.png>)


🔍 Interpretation
	•	EfficientNet-B0 erkennt die Klasse “alp” mit sehr hoher Wahrscheinlichkeit (97.33%), was dem Bildinhalt des Matterhorns sehr gut entspricht.
	•	EfficientNet-Lite4 erkennt “alp” nicht unter den Top-Klassen. Stattdessen zeigt es eine gleichmäßigere Verteilung auf mehrere ähnliche Klassen wie “lakeside” und “valley”.

⸻

💡 Fazit
	•	Das kleinere Modell EfficientNet-B0 liefert eine klare, dominante Vorhersage mit hoher Konfidenz, ist jedoch möglicherweise weniger differenziert in der Bewertung.
	•	Das grössere Modell EfficientNet-Lite4 zeigt zwar keine eindeutige Hauptklasse, kann jedoch subtilere Klassen mit niedriger Wahrscheinlichkeit berücksichtigen – was auf eine feinere Auswertung und ein differenzierteres Modellverhalten hindeuten könnte.

➡️ EfficientNet-B0 eignet sich gut für schnelle und einfache Klassifikationen mit klaren Ergebnissen.
➡️ EfficientNet-Lite4 bietet potenziell präzisere, aber auch komplexere Ergebnisse, was in Anwendungen mit höherem Qualitätsanspruch nützlich sein kann.