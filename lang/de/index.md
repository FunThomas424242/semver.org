---
layout: default
title: Semantische Versionsnumerierung 2.0.0
---

Semantische Versionsnumerierung 2.0.0
=====================================

Zusammenfassung
---------------

Hat man eine Versionsnummer in der Form MAJOR.MINOR.PATCH, dann erhöht man

1. die Hauptversionsnummer MAJOR, wenn man Änderungen vornimmt, die wahrscheinlich zu Inkompatibilitäten führen,
1. die Nebenversionsnummer MINOR, wenn man Änderungen oder Erweiterungen vornimmt und dabei abwärtskompatibel bleibt,
1. die Patchnummer, wenn man lediglich Fehler korrigiert, ohne die Kompatibilität zu beeinträchtigen.

Zusätzliche Kennzeichnungen für Vorabversionen und Build-Informationen können ergänzend zum Format HAUPT.NEBEN.PATCH verwendet werden.

Einführung
----------

In der Welt der Softwareverwaltung gibt es eine böse Falle, nämlich die
„Hölle der Abhängigkeiten“. Je umfangreicher ein System wird und je mehr
Pakete man in seine Software integriert, desto wahrscheinlicher ist es,
dass man sich eines Tages verzweifelt in dieser Hölle wiederfindet.

Bei Systemen mit vielen Abhängigkeiten kann die Herausgabe eines neuen
Pakets schnell zum Alptraum werden. Sind die Abhängigkeiten zu eng
festgelegt, besteht die Gefahr einer Versionsblockade (nämlich dann,
wenn es nicht möglich ist, ein Paket zu aktualisieren, ohne auch
sämtliche abhängigen Pakete mit zu aktualisieren). Sind die
Abhängigkeiten dagegen zu unscharf festgelegt, wird man sich
unweigerlich in einem Durcheinander von Versionen verlieren (wenn man
die Kompatibilität mit zukünftigen Versionen großzügiger festlegt als es
gut wäre). Die Hölle der Abhängigkeiten hat man erreicht, wenn eine
Versionsblockade oder die Kombination der vorliegenden Versionen eine
einfache und sichere Aktualisierung des Projekts unmöglich macht.

Als Lösung für dieses Problem schlage ich ein paar simple Regeln vor,
welche festlegen, wie Versionsnummern einer Software vergeben und erhöht
werden sollten. Diese Regeln basieren auf gängigen und verbreiteten
Verfahren, die sowohl in proprietärer als auch quelloffener Software
verwendet werden, gehen aber auch darüber hinaus.

Damit dieses System funktioniert, muss man zunächst eine Schnittstelle
(API) definieren und veröffentlichen. Das kann in einer förmlichen
Dokumentation geschehen oder auch implizit durch den Code selbst.
Unabhängig davon ist es wichtig, dass diese Schnittstelle klar und
präzise beschrieben ist. Ist sie einmal festgelegt, markiert man
Änderungen mit festgelegten Erhöhungen der Versionsnummer. Betrachten
wir eine Versionsnummer der Form X.Y.Z (MAJOR.MINOR.PATCH):
Fehlerkorrekturen, die die Schnittstelle nicht betreffen, erhöhen die
Patchnummer; abwärtskompatible Änderungen oder Erweiterungen der
Schnittstelle erhöhen die Nebenversionsnummer; Änderungen der
Schnittstelle, die nicht mehr voll abwärtskompatibel sind, erhöhen die
Hauptversionsnummer.

Ich nenne dieses System „semantische Versionsnumerierung“ (Semantic
Versioning). Mit diesem System vermittelt die Versionsnummer und die
Art, wie sie fortgezählt wird, eine Bedeutung für den damit
beschriebenen Code und den Umfang der Änderungen von einer Version zur
nächsten.


Spezifikation der semantischen Versionsnumerierung (SemVer)

Die Schlüsselworte *MUSS*, *DARF NICHT*, *NOTWENDIG*, *SOLL*, *SOLL
NICHT*, *SOLLTE*, *SOLLTE NICHT*, *EMPFOHLEN*, *KANN* und *OPTIONAL*
sind in diesem Dokument so zu interpretieren wie in [RFC 2119](http://tools.ietf.org/html/rfc2119) beschrieben.

1. Software, die semantische Versionsnumerierung nutzt, MUSS eine
öffentliche Schnittstelle (API) deklarieren. Diese Schnittstelle
kann im Code selbst festgelegt sein, oder als förmliche
Dokumentation existieren. In jedem Fall sollte sie präzise und
leicht verständlich sein.
1. Eine reguläre Versionsnummer MUSS die Form X.Y.Z haben, wobei X, Y,
und Z nicht-negative Ganzzahlen sind, die keine führenden Nullen
aufweisen DÜRFEN. X ist die Hauptversion, Y die Nebenversion, und Z
die Patch-Version. Jedes Element MUSS numerisch hochzählen.
Beispiel: 1.9.0 -> 1.10.0 -> 1.11.0
1. Der Inhalt eines Pakets mit einer Versionsnummer DARF NICHT mehr
verändert werden, wenn es einmal veröffentlicht ist. Jegliche
Änderungen MÜSSEN als neue Version herausgegeben werden.

1. Die Hauptversionsnummer 0 (0.y.z) ist für den Beginn der Entwicklung
vorgesehen. Alle Eigenschaften können sich noch jederzeit ändern.
Die öffentliche Schnittstelle sollte noch nicht als stabil
betrachtet werden.

1. Version 1.0.0 definiert die öffentliche Schnittstelle (API). Wie die
Versionsnummer nach dieser Veröffentlichung fortgezählt wird, hängt
von dieser öffentlichen Schnittstelle ab und davon, wie sie
verändert wird.

1. Die Patchnummer Z (x.y.Z mit x>0) MUSS erhöht werden, wenn
ausschließlich abwärtskompatible Korrekturen eingeführt werden. Eine
Fehlerkorrektur ist definiert als interne Änderung, die ein
fehlerhaftes Verhalten beseitigt.

1. Die Nebenversionsnummer Y (x.Y.z mit x>0) MUSS erhöht werden, sobald
neue, abwärtskompatible Funktionen der öffentlichen Schnittstelle
eingeführt werden. Sie MUSS auch erhöht werden, wenn irgendeine
Funktion der Schnittstelle abgekündigt wird. Sie KANN erhöht werden,
wenn wesentliche neue Funktionen oder Verbesserungen im Innern des
Codes eingeführt werden. Das KANN auch Änderungen der Patchnummer
einschließen. Die Patchnummer MUSS auf 0 zurückgesetzt werden, wenn
die Nebenversionsnummer erhöht wird.

1. Die Hauptversionsnummer X (X.y.z mit X>0) MUSS erhöht werden, wenn
die Schnittstelle in einer Weise geändert wird, die nicht mehr
abwärtskompatibel ist. Das KANN Änderungen an der Nebenversions– und
Patchnummer einschließen. Patch– und Nebenversionsnummer MÜSSEN auf
0 zurückgesetzt werden, wenn die Hauptversionsnummer erhöht wird.

1. Eine inoffizielle Vorabversion KANN kenntlich gemacht werden, indem
ein Bindestrich und eine Folge von Bezeichnern, die durch einen
Punkt getrennt sind, an die Versionsnummer angehängt werden. Diese
Bezeichner MÜSSEN ausschließlich aus Buchstaben, Ziffern und
Bindestrichen bestehen [0-9A-Za-z-]. Bezeichner DÜRFEN NICHT leer
sein. Numerische Bezeichner DÜRFEN NICHT mit Nullen beginnen.
Vorabversionen haben eine niedrigere Rangfolge als die entsprechende
reguläre Version. Eine Vorab-Versionsnummer zeigt an, dass diese
Version noch nicht stabil ist und die Regeln der Versionsnumerierung
noch nicht unbedingt einhält.
*Beispiele:* 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0 0.3.7, 1.0.0 x.7.z.92

1. Metadaten zur Übersetzung KÖNNEN kenntlich gemacht werden, indem ein
Pluszeichen und eine Folge von Bezeichnern, die durch einen Punkt
getrennt sind, an die Versionsnummer angehängt werden. Diese
Bezeichner MÜSSEN ausschließlich aus Buchstaben, Ziffern und
Bindestrichen bestehen [0-9A-Za-z-]. Bezeichner DÜRFEN NICHT leer
sein. Metadaten zur Übersetzung SOLLTEN bei der Bestimmung der
Rangfolge von Versionen ignoriert werden. Folglich gelten zwei
Versionen, die sich nur in den Metadaten unterscheiden, als
gleichwertig im Hinblick auf die Reihenfolge.
*Beispiele:* 1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85

1. Die Rangfolge gibt an, wie Versionen zueinander sortiert werden. Zur
Bestimmung der Rangfolge MUSS die Versionsnummer nach Hauptversion,
Nebenversion, Patch und Vorab-Bezeichnern getrennt betrachtet werden
(Metadaten gehen nicht in die Betrachtung ein). Die Rangfolge wird
durch den ersten Unterschied bestimmt, der beim Lesen von links nach
rechts auftritt. Hauptversion, Nebenversion und Patch werden immer
numerisch betrachtet.
*Beispiel:* 1.0.0 < 2.0.0 < 2.1.0 < 2.1.1
Wenn Hauptversion, Nebenversion und Patch identisch sind, hat eine
Vorabversion eine niedrigere Rangfolge als eine reguläre Version.
*Beispiel:* 1.0.0-alpha < 1.0.0
Die Rangfolge von Vorabversionen mit denselben Hauptversionen,
Nebenversionen und Patchnummern MUSS bestimmt werden, indem jeder
Bezeichner zwischen den Punkten von links nach rechts vergleichen
wird, bis ein Unterschied auftritt. Dabei werden Bezeichner, die nur
aus Ziffern bestehen, numerisch verglichen, und Bezeichner, die
Buchstaben oder Bindestriche enthalten, in der Reihenfolge ihrer
ASCII-Codes. Numerische Bezeichner haben eine niedrigere Rangfolge
als nichtnumerische. Eine größere Anzahl von Bezeichnern hat eine
höhere Rangfolge als eine kleinere, wenn alle vorangegangenen
Bezeichner gleich sind.
*Beispiel:* 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta <
1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.


Wozu ist semantische Versionsnumerierung gut?
---------------------------------------------

Der Gedanke ist nicht neu, schon gar nicht revolutionär. Wahrscheinlich
verwenden Sie sogar schon etwas, das dem ziemlich nahe kommt. Aber
„ziemlich nahe“ ist nicht gut genug. Wenn man sich nicht gewissenhaft an
irgendeine formale Spezifikation hält, sind Versionsnummern letztendlich
unbrauchbar, um Abhängigkeiten zu beherrschen. Wenn man den
beschriebenen Ideen einen Namen gibt und sie klar beschreibt, wird es
leicht, den Nutzern Ihrer Software Ihre Absichten mitzuteilen. Sobald
diese Absichten klar sind, kann man Abhängigkeiten flexibel (aber nicht
zu flexibel) handhaben.

Ein einfaches Beispiel soll zeigen, wie die Hölle der Abhängigkeiten
durch den Einsatz semantischer Versionsnumerierung der Vergangenheit
angehört. Betrachten wir eine Bibliothek namens „Feuerwehrauto“. Sie
erfordert ein semantisch numeriertes Paket namens „Leiter“. Zum
Zeitpunkt, da „Feuerwehrauto“ erzeugt wird, liegt „Leiter“ in der
Version 3.1.0 vor. Da „Feuerwehrauto“ Funktionen verwendet, die erst mit
Version 3.1.0 von „Leiter“ eingeführt wurden, kann man mit gutem
Gewissen festlegen, dass „Leiter“ in Version 3.1.0 oder höher, aber
niedriger als 4.0.0 erforderlich ist. Wenn nun „Leiter“ in Version 3.1.1
oder 3.2.0 verfügbar ist, kann man sie in das Paketverwaltungssystem
einpflegen und sicher sein, dass sie mit der vorhandenen, davon
abhängigen Software kompatibel ist.

Als verantwortungsbewusster Entwickler möchte man natürlich
sicherstellen, dass jedes Update wie beschrieben funktioniert. Die Welt
da draußen ist aber chaotisch; dagegen können wir nichts tun, wir müssen
also auf der Hut sein. Man kann aber auf eine semantische
Versionsnumerierung setzen und damit seine Pakete auf eine vernünftige
Art veröffentlichen und aktualisieren, ohne jedes mal auch die
abhängigen Pakete aktualisieren zu müssen und sich so Zeit und Ärger
ersparen.

Wenn sich das alles erstrebenswert anhört, müssen Sie nur anfangen, die
semantische Versionsnumerierung zu nutzen, indem Sie einfach behaupten,
dies zu tun und dann die vorgeschlagenen Regeln einhalten. Setzen Sie in
Ihrer README-Datei einen Link zur Website http://www.semver.org/ oder
auf dieses Dokument, sodass auch andere die Regeln kennenlernen und
davon profitieren können.

FAQ
---

### Wie sollte ich in der Frühphase der Entwicklung, solange ich Version 0.Y.Z habe, mit Änderungen verfahren?

Das Einfachste ist, wenn Sie ihre Entwicklung mit 0.1.0 beginnen und für
jede noch nicht stabile Version, die Sie herausgeben, die
Nebenversionsnummer erhöhen.

### Woher weiß ich, wann ich Version 1.0.0 erklären soll?

Wenn Ihre Software bereits produktiv genutzt wird, sollte sie
wahrscheinlich schon in der Version 1.0.0 vorliegen. Wenn Sie eine
stabile Schnittstelle haben, auf die sich die Anwender schon verlassen,
sollten Sie mindestens bei 1.0.0 sein. Wenn Sie sehr um
Abwärtskompatibilität besorgt sind, sollten Sie wohl ebenfalls schon bei
Version 1.0.0 sein.

### Hemmt das nicht eine rasche Entwicklung und schnelle Aktualisierungen?

Die Hauptversionsnummer 0 ist gleichbedeutend mit rascher Entwicklung.
Wenn Sie die Schnittstelle täglich ändern, sollten Sie entweder noch
Version 0.y.z haben, oder an einem separaten Entwicklungszweig arbeiten,
der auf die nächsthöhere Hauptversionsnummer abzielt.

### Wenn schon die kleinste nicht abwärtskompatible Änderung eine Erhöhung der Hauptversionsnummer bedeutet, lande ich dann nicht ganz schnell bei Version 42.0.0?

Das ist eine Frage von verantwortungsvoller Entwicklung und Weitsicht.
Nicht abwärtskompatible Änderungen an Software mit vielen Abhängigkeiten
sollten nicht leichtfertig durchgeführt werden. Der Aufwand für eine
Aktualisierung kann erheblich sein. Wenn Sie für die Veröffentlichung
von nicht abwärtskompatiblen Änderungen die Hauptversionsnummer erhöhen
müssen, sollten Sie die Tragweite Ihrer Änderungen und das Verhältnis
von Aufwand zum Nutzen bedenken.

### Die Dokumentation der Schnittstelle ist zuviel Arbeit!

Es liegt in Ihrer Verantwortung als professioneller Entwickler, die
Software, die von anderen benutzt werden soll, sorgfältig zu
dokumentieren. Software in all ihrer Komplexität zu beherrschen ist ein
äußerst wichtiger Beitrag, um ein Projekt effizient zu halten, und das
ist schwierig, wenn niemand weiß, wie Ihre Software zu nutzen ist oder
welche Methoden man sicher verwenden darf. Langfristig kann semantische
Versionsnumerierung und das Beharren auf klar definierten Schnittstellen
dafür sorgen, dass alles reibungslos läuft.

### Was mache ich, wenn ich versehentlich eine nicht abwärtskompatible Änderung nur mit einer Änderung der Nebenversionsnummer veröffentlicht habe?

Sobald Sie merken, dass Sie gegen die Spezifikation der semantischen
VersionsNumerierung verstoßen haben, beheben Sie das Problem und geben
Sie eine neue Nebenversion heraus, die den Irrtum korrigiert und die
Abwärtskompatibilität wiederherstellt. Selbst in diesem Fall ist es
nicht akzeptabel, einmal herausgegebene Versionen zu modifizieren. Wenn
es Ihnen angemessen erscheint, dokumentieren Sie die fehlerhafte Version
und informieren Sie Ihre Nutzer über das Problem, so dass sie von der
fehlerhaften Version wissen.

### Was soll ich tun, wenn ich interne Abhängigkeiten aktualisiere, ohne dass die Schnittstelle davon betroffen ist?

Das sollte man als kompatibel betrachten, da es die öffentlich
dokumentierte Schnittstelle nicht betrifft. Der Autor einer Software,
die ausdrücklich dieselben Abhängigkeiten hat, wie Ihr Paket, wird jeden
Konflikt feststellen, sofern er eine eigene Spezifikation für
Abhängigkeiten nutzt. Die Entscheidung, ob eine Änderung nur ein Patch
oder eine Änderung im Sinne der Nebenversionsnummer ist, hängt davon ab,
ob Sie die Abhängigkeiten wegen einer Fehlerkorrektur oder wegen der
Einführung zusätzlicher Funktionalität geändert haben. Ich würde das
Ergänzen von weiterem Programmcode normalerweise als letzteres
einschätzen, so dass offensichtlich die Nebenversionsnummer erhöht
werden sollte.

### Was ist, wenn ich versehentlich die Schnittstelle in einer Weise geändert habe, die nicht zur Änderung der Versionsnummer passt (z.B. wenn der Code fälschlicherweise eine wesentliche Änderung in einem Patch-Release einführt)?

Das liegt in Ihrem Ermessen. Wenn Sie ein großes Publikum haben, das von
einer Änderung zurück zu dem, was die Versionsnummer widerspiegelt,
erheblich betroffen ist, dann ist es möglicherweise das Beste, wenn Sie
eine neue Hauptversion veröffentlichen, auch wenn die Korrektur genau
genommen nur als Patch einzuordnen wäre. Vergessen Sie nicht, dass es
bei der semantischen VersionsNumerierung vor allem darum geht, der
Versionsnummer und ihrer Änderung eine Bedeutung zu geben. Wenn
Änderungen für Ihre Nutzer wichtig sind, nutzen Sie die Versionsnummer,
um diese Information zu vermitteln.

### Wie soll ich verfahren, wenn Funktionen wegfallen?

Eine existierende Funktionalität aufzugeben, ist in der
Softwareentwicklung ein völlig normaler Vorgang; er ist im Interesse des
Fortschritts oft notwendig. Wenn Sie einen Teil der definierten
Schnittstelle sterben lassen möchten, sollten Sie zwei Dinge tun: (1)
Aktualisieren Sie Ihre Dokumentation, um Ihre Nutzer über die
Abkündigung zu informieren, (2) Veröffentlichen Sie eine neue
Nebenversion, in der Sie die Abschaffung bereits deutlich machen. Bevor
Sie die Funktionalität in einer neuen Hauptversion komplett abschaffen,
sollten Sie mindestens eine Nebenversion mit dem Hinweis auf die
Abschaffung herausgeben, damit sich Ihre Nutzer ohne Schwierigkeiten auf
die neue Schnittstelle umstellen können.

### Limitiert SemVer die Länge der Versionsangabe?

Nein, aber handeln Sie überlegt. Eine 255 Zeichen lange Versionsangabe
ist vermutlich vollkommen überdimensioniert. Einzelne Systeme könnten
auch ihrerseits eine Grenze setzen.


Über den Artikel
----------------

Die Spezifikation für semantische Versionsnumerierung wurde von [Tom
Preston-Werner](http://tom.preston-werner.com) verfasst, Erfinder der
Gravatars und Mitbegründer von GitHub.

Wenn Sie diesen Artikel im Original kommentieren möchten, eröffnen Sie
bitte ein Ticket auf github <https://github.com/mojombo/semver/issues>.
Das Original <http://semver.org/> wurde unter der Creative
Commons-Lizenz CC BY 3.0 <http://creativecommons.org/licenses/by/3.0/>
veröffentlicht.

Die Übersetzung ins Deutsche stammt von Martin Kunkel selfhtml@kennst.net
<mailto:selfhtml@kennst.net>. Sie steht ebenfalls unter der Creative
Commons Lizenz CC BY 3.0 DE
<http://creativecommons.org/licenses/by/3.0/de/>.


Über die Lizenz
---------------

Die essentiellen Punkte dieser Lizenz sind

* *Sie dürfen:*
  ** das Werk bzw. den Inhalt vervielfältigen, verbreiten und  öffentlich zugänglich machen
  ** Abwandlungen und Bearbeitungen des Werkes bzw. Inhaltes anfertigen
* *Zu den folgenden Bedingungen:*
  ** Namensnennung — Sie müssen den Namen des Autors/Rechteinhabers in der von ihm festgelegten Weise nennen.
  ** Weitergabe unter gleichen Bedingungen — Wenn Sie das lizenzierte  Werk bzw. den lizenzierten Inhalt bearbeiten, abwandeln oder in
     anderer Weise erkennbar als Grundlage für eigenes Schaffen
     verwenden, dürfen Sie die daraufhin neu entstandenen Werke bzw.
     Inhalte nur unter Verwendung von Lizenzbedingungen weitergeben,
     die mit denen dieses Lizenzvertrages identisch, vergleichbar
     oder kompatibel sind.
* *Gewünschte Namensnennung:*
  ** „*Quelle: Martin Kunkel, SELFHTML*“, ohne Anführungszeichen, dabei ist auf diesen Artikel zu verlinken.
  ** Die Adresse zu diesem Artikel lautet:
     http://blog.selfhtml.org/2013/11/08/semantische-versionsnumerierung-2-0-0/

* Veröffentlicht in: Softwareentwicklung
    <https://blog.selfhtml.org/c/softwareentwicklung/>
