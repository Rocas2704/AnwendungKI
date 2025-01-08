---


---

<h1 id="readme---roberta-klassifizierungsmodell">README - RoBERTa Klassifizierungsmodell</h1>
<h2 id="übersicht">1. Übersicht</h2>
<p>Dieses Projekt implementiert ein Textklassifizierungsmodell mit <strong>RoBERTa base</strong>. Das Modell wird auf einem benutzerdefinierten Datensatz trainiert, und die trainierten Gewichte werden gespeichert, um Vorhersagen auf neuen Daten zu treffen.</p>
<p>Der Code besteht aus zwei Hauptskripten:</p>
<ul>
<li><strong>Training</strong>: Fine-Tuning von RoBERTa auf einem benutzerdefinierten Datensatz.</li>
<li><strong>Vorhersage</strong>: Verwendung des trainierten Modells zur Vorhersage von Labels für neue Daten.</li>
</ul>
<p>Die Ausgabedatei wird immer als <code>test_with_label.csv</code> generiert und enthält die Vorhersagen für die Eingabedaten.</p>
<h2 id="anforderungen">2. Anforderungen</h2>
<p>Stellen Sie sicher, dass die folgenden Bibliotheken installiert sind:</p>
<ul>
<li><code>torch</code></li>
<li><code>transformers</code></li>
<li><code>sklearn</code></li>
<li><code>pandas</code></li>
</ul>
<p>Die erforderlichen Bibliotheken können mit folgendem Befehl installiert werden:</p>
<pre class=" language-bash"><code class="prism  language-bash">pip <span class="token function">install</span> torch transformers scikit-learn pandas
</code></pre>
<h2 id="aufbau-des-datensatzes">3. Aufbau des Datensatzes</h2>
<p>Der Datensatz muss im CSV-Format vorliegen und folgende Spalten enthalten:</p>
<ul>
<li><strong>id</strong>: Eindeutige ID des Textes.</li>
<li><strong>text</strong>: Der zu klassifizierende Text.</li>
<li><strong>label</strong>: Die Klasse des Textes als numerischer Wert.</li>
</ul>
<p>Beispielhafte Zeilen des Datensatzes:</p>

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
<td>Dies ist ein Beispieltext.</td>
<td>0</td>
</tr>
<tr>
<td>2</td>
<td>Ein weiterer Beispieltext.</td>
<td>1</td>
</tr>
</tbody>
</table><h2 id="ausführung-des-codes">4. Ausführung des Codes</h2>
<h3 id="training">4.1 Training</h3>
<ol>
<li>
<p>Stellen Sie sicher, dass sich Ihre Trainingsdatei (<code>train.csv</code>) im selben Verzeichnis wie das Skript befindet.</p>
</li>
<li>
<p>Führen Sie das Trainingsskript aus:</p>
<pre class=" language-bash"><code class="prism  language-bash">python roberta_training_timer.py
</code></pre>
</li>
<li>
<p>Das Skript führt folgende Schritte durch:</p>
<ul>
<li>Laden des Datensatzes und Aufteilen in Trainings- und Validierungsdaten.</li>
<li>Tokenisierung der Texte mit dem RoBERTa-Tokenizer.</li>
<li>Fine-Tuning des vortrainierten RoBERTa-Modells.</li>
<li>Speichern des besten Modells basierend auf dem F1-Score auf dem Validierungsset.</li>
</ul>
</li>
<li>
<p>Das Skript zeigt die folgenden Metriken nach jeder Epoche an:</p>
<ul>
<li><strong>Loss</strong>: Verlustfunktion des Modells.</li>
<li><strong>Val Accuracy</strong>: Genauigkeit auf dem Validierungsset.</li>
<li><strong>Val F1 Score</strong>: F1-Score auf dem Validierungsset.</li>
<li><strong>Val Precision</strong>: Präzision auf dem Validierungsset.</li>
<li><strong>Val Recall</strong>: Recall auf dem Validierungsset.</li>
</ul>
</li>
<li>
<p>Das beste Modell wird als <code>best_roberta_model.pth</code> gespeichert.</p>
</li>
<li>
<p>Am Ende wird die Gesamtdauer des Trainings angezeigt.</p>
</li>
</ol>
<h3 id="vorhersage">4.2 Vorhersage</h3>
<ol>
<li>
<p>Stellen Sie sicher, dass sich Ihre Testdatei (<code>test_no_labels.csv</code>) im selben Verzeichnis wie das Skript befindet.</p>
</li>
<li>
<p>Führen Sie das Vorhersageskript aus:</p>
<pre class=" language-bash"><code class="prism  language-bash">python roberta_predict.py
</code></pre>
</li>
<li>
<p>Das Skript führt folgende Schritte durch:</p>
<ul>
<li>Laden der Testdaten.</li>
<li>Tokenisierung der Texte mit dem RoBERTa-Tokenizer.</li>
<li>Anwenden des trainierten Modells auf die Testdaten.</li>
<li>Generieren einer Datei <code>test_with_label.csv</code>, die die vorhergesagten Labels enthält.</li>
</ul>
</li>
</ol>
<h2 id="reproduzierbarkeit">5. Reproduzierbarkeit</h2>
<p>Um konsistente Ergebnisse sicherzustellen, wird in beiden Skripten ein fester Zufalls-Seed gesetzt:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">import</span> random
<span class="token keyword">import</span> numpy <span class="token keyword">as</span> np
<span class="token keyword">import</span> torch

random<span class="token punctuation">.</span>seed<span class="token punctuation">(</span><span class="token number">42</span><span class="token punctuation">)</span>
np<span class="token punctuation">.</span>random<span class="token punctuation">.</span>seed<span class="token punctuation">(</span><span class="token number">42</span><span class="token punctuation">)</span>
torch<span class="token punctuation">.</span>manual_seed<span class="token punctuation">(</span><span class="token number">42</span><span class="token punctuation">)</span>
<span class="token keyword">if</span> torch<span class="token punctuation">.</span>cuda<span class="token punctuation">.</span>is_available<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
    torch<span class="token punctuation">.</span>cuda<span class="token punctuation">.</span>manual_seed_all<span class="token punctuation">(</span><span class="token number">42</span><span class="token punctuation">)</span>
</code></pre>
<h2 id="ausgabeformat">6. Ausgabeformat</h2>
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
</table><h2 id="wichtige-parameter">7. Wichtige Parameter</h2>
<ul>
<li><strong>Modell</strong>: <code>roberta-base</code></li>
<li><strong>Lernrate</strong>: <code>2e-5</code></li>
<li><strong>Batch-Größe</strong>: <code>64</code></li>
<li><strong>Maximale Sequenzlänge</strong>: <code>128</code></li>
<li><strong>Anzahl der Epochen</strong>: <code>30</code></li>
<li><strong>Early Stopping Geduld</strong>: <code>5</code> Epochen</li>
</ul>
<h2 id="kontakt">8. Kontakt</h2>
<p>Bei Fragen zu diesem Projekt wenden Sie sich bitte an den Autor.</p>

