---
layout: post
title: Welche Dokumentenklasse ist die Richtige
tags: 
- backmatter
- Dokumentenklasse
- frontmatter
- koma
- mainmatter
- part
- scrartcl
- scrbook
- scrreprt
- section
---
Es gibt nicht "die Richtige" Dokumentenklasse, sondern die Wahl ist abhängig davon was man vor hat.

Meine Anforderungen waren:

* Thesis
* Schriftsprache ist Deutsch
* DIN A4

Somit fällt die Wahl schon mal auf die KOMA-Script Klassen, welche alle per Standard auf DIN A4 eingestellt sind. Sehr zu empfehlen ist die Dokumentation zum KOMA-Script, die zu fast allen Fragen eine Antwort vorhält. Nur durch lesen selbiger, konnte ich irgendwelche Konstrukte, die ich über die Jahre in meinen LaTeX Dokumenten verwendet habe, elegant von KOMA-Script erledigen lassen.

Mittels KOMA-Script bekommt man den klassischen Satzspiegel frei Haus. Über dessen Aktualität kann man trefflich streiten und deswegen hat man die Möglichkeit in die Berechnung einzugreifen, worauf ich an geeigneter Stelle noch eingehen werde.

KOMA-Script stellt folgende Klassen bereit:

* scrartcl
* scrreprt
* scrbook
* scrlttr2

Der letzte Punkt ist die neue Briefklasse und kann schon von vornherein für eine Thesis ausgeschlossen werden.

Grundsätzlich sollte man sich nicht von den Namen irreführen lassen. Eine Thesis ist nun etwas mehr als ein Artikel, aber auch etwas weniger als ein Buch. Eigentlich kommt es einem Report am nächsten, da sie ja einen Bericht darstellt. Es spricht aber auch nichts dagegen seine Thesis in scrartcl zu schreiben, wenn man mit der Anzahl der Gliederungsebenen zurechtkommt.

Die Unterschiede zwischen den verschiedenen Klassen liegen im Detail. Erwähnt seien hier folgende nicht ganz unwichtige Sachen (die Liste ist nicht abschließend):

* Die oberste Gliederungsebene bei scrartcl ist \section 
* Die oberste Gliederungsebene bei scrreprt* und scrbook ist \part
* scrreprt kennt keine \frontmatter, \mainmatter und \backmatter Anweisungen; das Verhalten kann jedoch manuell erzeugt werden
* scrreprt kennt die \begin{abstract} Umgebung, welche es bei scrbook nicht gibt
* scrbook erstellt per Default einen zweiseitigen Satz
* neue Kapitel werden bei scrbook immer auf einer rechten Seite gesetzt

Hinweis: Vielfach ist zu lesen, dass die oberste Ebene für scrreprt \chapter sei. Ich habe \part zusammen mit scrreprt ausprobiert und es funktioniert. 

Ich persönlich schwanke zwischen scrreprt und scrbook. Da ich kein \part und auch keinen zweiseitigen Satz brauche, wird es wohl auf scrreprt hinauslaufen.

Weiterführende Links: 

http://www.komascript.de/faqwelcheklasse

{% latex %}
\begin{eqnarray*}
(A\cup B)-(C-A) &=& (A\cup B) \cap (C-A)^c\\
&=& (t\cup r) \cap (ä \cap A^c)^c \\
&=& (A\cup B) \cap (C^c \cup v) \\
&=& q \cup (p\cap C^c) \\
&=& v \cup (p-ü)
\end{eqnarray*}
{% endlatex %}
