---


---

<h1 id="readme---roberta-klassifizierungsmodell">README - RoBERTa Klassifizierungsmodell</h1>
<h2 id="übersicht">1. Übersicht</h2>
<p>Dieses Projekt implementiert ein Textklassifizierungsmodell mit <strong>RoBERTa base</strong>. Der Code ist in zwei Hauptteile unterteilt:</p>
<ul>
<li>
<p><strong>Training</strong>: Fine-Tuning von RoBERTa mit einem benutzerdefinierten Datensatz.</p>
</li>
<li>
<p><strong>Vorhersage</strong>: Verwendung des trainierten Modells zur Vorhersage von Labels für neue Daten.</p>
</li>
</ul>
<p>Die Ausgabedatei wird immer als <code>test_with_label.csv</code> generiert und enthält die Vorhersagen für die Eingabedaten.</p>
<h2 id="anforderungen">2. Anforderungen</h2>
<p>Stellen Sie sicher, dass die folgenden Bibliotheken installiert sind:</p>
<ul>
<li>
<p><code>torch</code></p>
</li>
<li>
<p><code>transformers</code></p>
</li>
<li>
<p><code>sklearn</code></p>
</li>
<li>
<p><code>pandas</code></p>
</li>
</ul>
<p>Die erforderlichen Bibliotheken können mit folgendem Befehl installiert werden:</p>
<pre><code>pip install torch transformers scikit-learn pandas
</code></pre>
<h2 id="ausführung-des-codes">3. Ausführung des Codes</h2>
<h3 id="training">3.1 Training</h3>
<ol>
<li>
<p>Stellen Sie sicher, dass sich Ihre Trainingsdatei (<code>train.csv</code>) im selben Verzeichnis wie der Code befindet.</p>
</li>
<li>
<p>Führen Sie das Trainingsskript aus:</p>
<pre><code>python RoBERTa_training.py
</code></pre>
</li>
<li>
<p>Das Skript speichert das beste Modell als <code>best_roberta_model.pth</code> und zeigt die gesamte Trainingszeit an.</p>
</li>
</ol>
<h3 id="vorhersage">3.2 Vorhersage</h3>
<ol>
<li>
<p>Stellen Sie sicher, dass sich Ihre Testdatei (<code>test_no_labels.csv</code>) im selben Verzeichnis wie der Code befindet.</p>
</li>
<li>
<p>Führen Sie das Vorhersageskript aus:</p>
<pre><code>python roberta_predicting.py
</code></pre>
</li>
<li>
<p>Das Skript generiert eine Datei namens <code>test_with_label.csv</code>, die die vorhergesagten Labels enthält.</p>
</li>
</ol>
<h2 id="reproduzierbarkeit">4. Reproduzierbarkeit</h2>
<p>Um konsistente Ergebnisse sicherzustellen, wird in beiden Skripten ein fester Zufalls-Seed gesetzt:</p>
<pre><code>import random
import numpy as np
import torch

random.seed(42)
np.random.seed(42)
torch.manual_seed(42)
if torch.cuda.is_available():
    torch.cuda.manual_seed_all(42)
</code></pre>
<h2 id="ausgabeformat">5. Ausgabeformat</h2>
<p>Die Ausgabedatei <code>test_with_label.csv</code> hat folgendes Format:</p>

<table>
<thead>
<tr>
<th>id</th>
<th>text</th>
<th>label</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>Beispieltext zur Vorhersage.</td>
<td>0</td>
</tr>
<tr>
<td>2</td>
<td>Ein weiterer Beispieltext.</td>
<td>1</td>
</tr>
</tbody>
</table><h2 id="wichtige-parameter">6. Wichtige Parameter</h2>
<ul>
<li>
<p><strong>Modell</strong>: <code>roberta-base</code></p>
</li>
<li>
<p><strong>Lernrate</strong>: <code>2e-5</code></p>
</li>
<li>
<p><strong>Batch-Größe</strong>: <code>64</code></p>
</li>
<li>
<p><strong>Maximale Sequenzlänge</strong>: <code>128</code></p>
</li>
<li>
<p><strong>Anzahl der Epochen</strong>: <code>30</code></p>
</li>
<li>
<p><strong>Early Stopping Geduld</strong>: <code>5</code> Epochen</p>
</li>
</ul>
<h2 id="kontakt">7. Kontakt</h2>
<p>Bei Fragen zu diesem Projekt wenden Sie sich bitte an <a href="mailto:rodrigocastilla27@gmail.com">rodrigocastilla27@gmail.com</a></p>

