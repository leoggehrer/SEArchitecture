# Umsetzung der Architektur mit DotNet (C#)

## Infrastruktur  
  
Zur Umsetzung des Projektes wird DotNetCore (8.0 und höher) als Framework, die Programmiersprache CSharp (C#) und die Entwicklungsumgebung Visual Studio 2022 Community verwendet. Alle Komponenten können kostenlos aus dem Internet heruntergeladen werden.  
  
In diese Dokumentation werden unterschiedliche Begriffe verwendet. In der nachfolgenden Tabelle werden die wichtigsten Begriffe zusammengefasst und erlaeutert:  

|Begriff|Bedeutung|Synonym(e)|
|---|---|---|
|**Solution**|Ist eine Zusammenstellung von verschiedenen Teilprojekten zu einer Gesamtlösung.|Gesamtlösung, Lösung, Projekt|
|**Domain Solution**|Damit ist eine Gesamtlösung gemeint, welches fuer einen bestimmten Problembereich eine Lösung darstellt.|Problemlösung, Projekt|
|**Teilprojekt**|Ist die Zusammenfassung von Klassen und/oder Algorithmen, welches eine logische Einheit fuer die Lösungen bestimmter Teilprobleme bildet.|Teillösung, Projekteinheit, Projekt|
|**Projekttyp**|Unter Projekttyp wird die physikalische Beschaffenheit eines Projektes bezeichnet. Es gibt zwei grundlegende Typen von Projekten: <br>  - Ein wiederverwendbares Projekt (z.B.: eine Bibliothek) und <br>  - ein ausfuehrbares Projekt (z.B.: eine Konsolenanwendung, WepApi, AspMvc usw.). <br>**Als Regel gilt:**<br> Alle Programme und Algorithmen werden in den *wiederverwendbaren Projekten* implementiert. Die ausfuehrbaren Einheiten dienen nur als Startprojekte und leiten die Anfragen an die *wiederverwendbaren Komponenten* weiter.|Bibliothekstyp, Consolentyp|
|**Library oder Bibliothek**|Kennzeichnet einen *wiederverwendbaren Projekttyp*.|Bibliothek|
|**Console**|Kennzeichnet einen *ausfuehrbaren Projekttyp*. Dieser Typ startet eine Konsole fuer die Programmausfuehrung.|Konsole|
|**Host**|Dieser Typ kennzeichnet ein *ausfuehrbares Projekt*, welches zum Starten den IIS verwendet oder im Modus `selfhosting` gestartet werden kann.|Web-Application |
|**Abhaengigkeit**|Die Abhaengikeit beschreibt die Beziehungen von Projekten untereinander. Benötigt ein *Projekt A* Funktionalitaeten aus einem *Projekt B*, so wird eine Projektreferenz vom *Projekt B* in *Projekt A* benötigt.|Projektreferenz, Referenz, Dependency, Projektverweis|

## Das Beispiel

Um die beschriebene Architektur in die Praxis umzusetzen, betrachten wir ein einfaches Beispielprojekt namens **ContactManager**. Dieses Projekt verwaltet Kontakte und verwendet die vorgestellte Architektur. Die Umsetzung erfolgt in einer Schritt für Schritt Anleitung. Bevor mit der Umsetzung begonnen wird - hier die Aufgabenstellung.










Das **ContactManager**-Projekt zeigt, wie die vorgestellte Architektur mit DotNet (C#) umgesetzt werden kann. Die klare Trennung der Schichten und die Verwendung von Schnittstellen erleichtern die Wartung und Erweiterung des Systems. Die Web API ermöglicht die Kommunikation zwischen Frontend und Backend, während die Geschäftslogik und Datenzugriffsschicht im Logic-Modul gekapselt sind.
