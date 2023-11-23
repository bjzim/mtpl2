# Datenquelle
Unter [https://www.openml.org/d/41214](https://www.openml.org/d/41214) und [https://www.openml.org/d/41215](https://www.openml.org/d/41215) liegen zwei Datensätze eines französischen Automobilversicherers. 

Diese beinhalten Risikomerkmale und Schadeninformationen zu Kraftfahrt-Haftpflicht-Versicherungsverträgen. 

**Hinweis: Der Datensatz steht im .arff Format zur Verfügung. Mit Hilfe folgender Code-Zeile können die Daten in Python einlesen und zu einem Pandas Dataframe konvertieren:**

    import pandas as pd
    import arff
    data_freq = arff.load('freMTPL2freq.arff')
    df_freq = pd.DataFrame(data_freq, columns=["idpol", "claimNb", "exposure", "area", "vehpower",
    "vehage","drivage", "bonusmalus", "vehbrand", "vehgas", "density", "region"])
    data_sev = arff.load('freMTPL2sev.arff')
    df_sev = pd.DataFrame(data_sev, columns=["idpol", "claimamount"])


# Ziel

Die Aufgabe besteht in der Modellierung der zu erwartenden Schadenhöhe pro Versicherungsnehmer und Jahr anhand der Risikomerkmale der Kunden. Dieser Wert ist Basis für die Berechnung eines fairen Versicherungsbeitrags.

# Arbeitsschritte

**1 Explorative Datenanalyse:**  
Machen Sie sich mit dem Datensatz vertraut. Identifizieren Sie dabei mögliche Probleme sowie grundlegende statistische Zusammenhänge, welche für die anschließende Modellierung wichtig sein könnten.

**2 Feature Engineering:**  
Bereiten Sie, soweit für ihre Modellierung nötig, die Variablen geeignet auf.

**3 Modellvergleich:**  
Entscheiden Sie sich für ein geeignetes Modell anhand einer dafür geeigneten Metrik. Erläutern Sie wie Sie dabei vorgehen und begründen Sie ihre Entscheidung.

**4 Modellbuilding:**  
Trainieren Sie unter Berücksichtigung der vorangegangenen Schritte das von Ihnen gewählte Modell zur Vorhersage der erwarteten Schadenhöhe pro Kunde und Jahr. Ihr Ziel ist es, einen möglichst fairen Versicherungsbeitrag pro Jahr für einzelne Kunden anhand der Ihnen zu Verfügung stehenden Merkmale zu bestimmen. Wählen Sie mindestens eine geeignete Metrik, um die Güte des finalen Modells zu beurteilen. Zeigen Sie, welche Variablen und Zusammenhänge für Ihr finales Modell relevant sind. Überlegen Sie sich (ohne dies umzusetzen) wie Sie Ihr Modell weiter optimieren könnten.


# Datensatzbeschreibung

freMTPL2freq:

**idpol**: ID des Vertrags  
**claimnb**: Anzahl Schäden im Versicherungszeitraum  
**exposure**: Länge des Versicherungszeitraums (in Jahren) [Komponente der abhängigen
Variable]  
**area**: Area-Code des Versicherungsnehmers [unabhängige Variable]  
**vehpower**: Leistung des versicherten Kfz [unabhängige Variable]  
**vehage**: Alter des versicherten Kfz [unabhängige Variable]  
**drivage**: Alter des Versicherungsnehmers [unabhängige Variable]  
**bonusmalus**: Schadenfreiheitsrabatt (französische Entsprechung der Schadenfreiheitsklasse) [unabhängige Variable]  
**vehbrand**: Marke des versicherten Kfz [unabhängige Variable]  
**vehgas**: Antrieb des versicherten Kfz [unabhängige Variable]  
**density**: Anzahl der Einwohner pro km2 im Wohnort des Versicherungsnehmers [unabhängige Variable]  
**region**: Region des Versicherungsnehmers [unabhängige Variable]  


freMTPL2sev:

**idpol**: ID des Vertrags  
**claimamount**: Höhe der einzelnen Schadenaufwände (mehrere Einträge pro Vertrag, falls im
Zeitraum mehrere Schäden vorhanden waren.) [Komponente der abhängigen Variable.]  
    

Die abhängige Variable ist definiert als ${\Large \frac{ClaimAmount}{Exposure}}$.

# Projektphasen

**1 Explorative Datenanalyse:**  
Machen Sie sich mit dem Datensatz vertraut. Identifizieren Sie dabei mögliche Probleme sowie grundlegende statistische Zusammenhänge, welche für die anschließende Modellierung wichtig sein könnten.

**2 Feature Engineering:**  
Bereiten Sie, soweit für ihre Modellierung nötig, die Variablen geeignet auf.

**3 Modellvergleich:**  
Entscheiden Sie sich für ein geeignetes Modell anhand einer dafür geeigneten Metrik. Erläutern Sie wie Sie dabei vorgehen und begründen Sie ihre Entscheidung.

**4 Modellbuilding:**  
Trainieren Sie unter Berücksichtigung der vorangegangenen Schritte das von Ihnen gewählte Modell zur Vorhersage der erwarteten Schadenhöhe pro Kunde und Jahr. Ihr Ziel ist es, einen möglichst fairen Versicherungsbeitrag pro Jahr für einzelne Kunden anhand der Ihnen zu Verfügung stehenden Merkmale zu bestimmen. Wählen Sie mindestens eine geeignete Metrik, um die Güte des finalen Modells zu beurteilen. Zeigen Sie, welche Variablen und Zusammenhänge für Ihr finales Modell relevant sind. Überlegen Sie sich (ohne dies umzusetzen) wie Sie Ihr Modell weiter optimieren könnten.


# Requirements and Environment

Requirements:
- pyenv with Python: 3.11.3

Environment: 

For installing the virtual environment you can either use the Makefile and run `make setup` or install it manually with the following commands: 

```Bash
pyenv local 3.11.3
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

# Usage

In order to train the model and store test data in the data folder and the model in models run:

```bash
#activate env
source .venv/bin/activate

python example_files/train.py  
```

In order to test that predict works on a test set you created run:

```bash
python example_files/predict.py models/linear_regression_model.sav data/X_test.csv data/y_test.csv
```

# Limitations

Development libraries are part of the production environment, normally these would be separate as the production code should be as slim as possible.


