---
layout: post
title: Latex ist nicht gleich Latex
tags: 
- latex 
- tex
- thesis
- lua
- lualatex
- pdflatex
---
Wenn man heute LaTeX benutzt, dann nutzt man eigentlich *pdfLaTeX* (in der Literatur findet man auch pdfTeX). Der Grund ist ein ganz einfacher:

LaTeX kann keine PDFs schreiben.

Es erzeugt lediglich DVI oder PostScript Dateien. In den allermeisten Fällen will bzw. muß man seine Thesis als PDF abgeben und müßte sie dann manuell in ein PDF umwandeln. Diesen Schritt übernimmt pdfLaTeX für uns. Darüber hinaus verfeinert pdfLaTeX noch die Darstellung, was sich mikrotypographische Optimierung nennt. Darauf komme ich später noch zurück.

##pdfLaTex

Beginnen wir mit dem ersten Dokument:

{% highlight latex %}
\documentclass{scrartcl}
    \usepackage[utf8]{inputenc}
    \usepackage[T1]{fontenc}
    \usepackage{lmodern}
    \usepackage[ngerman]{babel}
    \title{Minimalbespiel mit pdfLaTex}
    
    \author{Max Mustermann}
    \date{\today}
    
    \begin{document}
    \maketitle
    \section{Einleitung}
    Lorem Ipsum ist ein einfacher Demo-Text für die Print- und Schriftindustrie. Lorem Ipsum ist in der Industrie bereits der Standard Demo-Text seit 1500, als ein unbekannter Schriftsteller eine Hand voll Wörter nahm und diese durcheinander warf um ein Musterbuch zu erstellen. Es hat nicht nur 5 Jahrhunderte überlebt, sondern auch in Spruch in die elektronische Schriftbearbeitung geschafft (bemerke, nahezu unverändert). Bekannt wurde es 1960, mit dem erscheinen von "Letraset", welches Passagen von Lorem Ipsum enthielt, so wie Desktop Software wie "Aldus PageMaker" - ebenfalls mit Lorem Ipsum
\end{document}
{% endhighlight %}

Das Beispiel in eine Datei einfügen und unter dem Namen *pdflatexExample.tex* speichern. Um nun ein PDF zu erhalten, muß im Terminal der Befehl:
`pdflatex pdflatexExample.tex` eingegeben werden.

Es wäre nun keinen Blogpost wert, wenn ich hier nur auf ein einfaches Minimalbeispiel in pdfLaTeX eingehen würde. Der eigentliche Grund des Posts ist die Beschreibung wie man LuaLaTex benutzt, welchen Vorteil das hat und welche Besonderheiten es zu beachten gibt.

##LuaLaTeX
LuaLaTeX ist die Erweiterung von pdfLaTeX und kann somit (fast) alles was pdfLaTeX auch kann. Ein wichtiger Punkt jedoch ist, dass es von Haus aus UTF-8 fähig ist und meiner Meinung nach pdfLaTex vorzuziehen ist. Zum anderen bekommt man durch Luatex die Scriptsprache Lua for free in sein LaTeX Dokument - nicht das ich das bisher vermisst oder gebraucht hätte, aber cool ist es schon ;-)

Das obige Beispiel muß nun etwas verändert werden:

{% highlight latex %}
\documentclass{scrartcl}
    \usepackage{fontspec}
    \usepackage{polyglossia}
    \title{Minimalbespiel mit LuaLaTex}
    
    \author{Max Mustermann}
    \date{\today}
    
    \begin{document}
    \maketitle
    \section{Einleitung}
    Lorem Ipsum ist ein einfacher Demo-Text für die Print- und Schriftindustrie. Lorem Ipsum ist in der Industrie bereits der Standard Demo-Text seit 1500, als ein unbekannter Schriftsteller eine Hand voll Wörter nahm und diese durcheinander warf um ein Musterbuch zu erstellen. Es hat nicht nur 5 Jahrhunderte überlebt, sondern auch in Spruch in die elektronische Schriftbearbeitung geschafft (bemerke, nahezu unverändert). Bekannt wurde es 1960, mit dem erscheinen von "Letraset", welches Passagen von Lorem Ipsum enthielt, so wie Desktop Software wie "Aldus PageMaker" - ebenfalls mit Lorem Ipsum
\end{document}
{% endhighlight %}

Es enfallen die Einbindung der Packages  inputenc, fontenc, lmodern und babel. Anstelle dessen wird fontspec und polyglossia eingebunden. LuaLaTeX erkennt die Kodierung am Dokument - es muß also in UTF-8 abgespeichert werden, damit LuaLaTeX das richtige Charset wählen kann.

Nachdem das Beispiel in der Datei lualatexExample.tex gespeichert wurde, kann es mit dem Kommando `lualatex lualatexExample.tex` kompiliert werden.
