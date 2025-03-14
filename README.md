# Software-Architektur

Die Software-Architektur beschreibt die grundlegende Struktur eines Softwaresystems. Sie umfasst die Organisation der Komponenten, deren Beziehungen untereinander sowie die Prinzipien, nach denen sie entwickelt und weiterentwickelt werden. Die Architektur dient als Blaupause für die Entwicklung, Wartung und Erweiterung einer Software.

## Hauptbestandteile einer Software-Architektur

- Komponenten
  - Einzelne Bausteine der Software (z. B. Module, Microservices).
  - Erfüllen spezifische Aufgaben und kapseln Funktionalitäten.
- Schnittstellen & Kommunikation
  - Definieren, wie die Komponenten miteinander interagieren.
  - Nutzung von APIs, Datenbanken oder Messaging-Systemen zur Kommunikation.
- Datenflüsse & Speicherung
  - Beschreibt, wie Daten verarbeitet, gespeichert und ausgetauscht werden.
  - Nutzung von Datenbanken, Caches und externen Speichern.
- Architekturstile & Muster
  - Beispiele:
    - Schichtenarchitektur (z. B. Präsentations-, Geschäfts- und Datenhaltungsschicht).
    - Microservices (modulare, unabhängige Services).
    - MVC (Model-View-Controller) für Webanwendungen.
    - MVVM (Model-View-ViewModel) für WPF-Anwendungen
- Qualitätsmerkmale
  - Wartbarkeit: Leicht anpassbar an neue Anforderungen.
  - Skalierbarkeit: Kann wachsen und größere Lasten bewältigen.
  - Sicherheit: Schutz vor Angriffen und Datenverlust.
  - Performance: Effiziente Nutzung von Ressourcen.

### Warum ist eine gute Software-Architektur wichtig?

- Erleichtert die Entwicklung durch eine klare Strukturen.
- Verbessert Wartung & Erweiterbarkeit, da Änderungen gezielt vorgenommen werden können.
- Erhöht Zuverlässigkeit & Stabilität, indem Fehlerquellen minimiert werden.
- Unterstützt Skalierung für größere Nutzerzahlen oder höhere Lasten.

**Zusammenfassung:**

Eine durchdachte Software-Architektur ist entscheidend für den Erfolg eines Softwareprojekts. Sie sorgt für eine effiziente Entwicklung, erleichtert die Wartung und stellt sicher, dass das System langfristig leistungsfähig und anpassbar bleibt.

## Architektur im Unterricht

Im Unterricht wird die Software-Architektur anhand eines praktischen Beispiels vermittelt. Die Studierenden lernen, wie man eine Anwendung in verschiedene Schichten unterteilt und wie diese Schichten miteinander interagieren. Dabei wird besonderer Wert auf die Trennung von Verantwortlichkeiten und die Wiederverwendbarkeit der Komponenten gelegt. Die folgende Abbildung zeigt die verwendete Systemstruktur und bietet einen Überblick über die Komponenten und deren Interaktionen.

![Software-Architektur](/img/systemstructure.png)

Die Architektur besteht aus mehreren Schichten, die in drei Hauptbereiche unterteilt sind: **Frontend**, **Backend** und **Qualitätssicherung**. Die Kommunikation zwischen diesen Komponenten erfolgt über eine **Web API**.

---

### Backend

Das Backend ist in drei Hauptmodule unterteilt:

#### Common Modul (Gelber Block)

Dieses Modul beinhaltet Schnittstellen und allgemeine Komponentne für das gesamte System.

- Enthält:
  - **Contracts** – Beinhaltet Schnittstellen für die Kommunikation, Datenobjekte und Komponenten.
  - **Modules** – Enthält wiederverwendbare Komponenten (z.B.: Konfiguration).

#### Logic Modul (Orangefarbener Block)

In dieser Einheit befindet sich der vollständige Datenzugriff, die gesamte Geschaeftslogik und stellt somit den zentralen Baustein des Systems dar.

- Enthält:
  - **Contracts** – Definiert Geschäftslogik-Schnittstellen.
  - **DataContext** – Datenbankzugriff und ORM (Object-Relational Mapping).
  - **Entities** – Datenmodelle für die Anwendung.

#### Web API (Blauer Block)

Dieses Modul stellt den API (Aplication Programming Interface) Zugriff auf das System über das Netzwerk zur Verfügung. Es dient als Vermittler zwischen der Geschäftslogik und den Klienten. Zusätlich bietet diese API auch die Möglichkeit, dass heterogene Systeme an den **Backend** angebunden werden können.

- Enthält:
  - **Models** - Datenobjekte für die Kommunikation nach außen.
  - **Controllers** - Komponenten zum Empfangen von Abfragen und Aufbereitung der Anfrageergebnissen.

Die **Web API** kommuniziert mit den **Common**- und **Logic**-Modulen, um Geschäftslogik auszuführen und Daten bereitzustellen.

---

## Qualitätssicherung

Die Architektur enthält eine separate **Qualitätssicherungsschicht**, die durch **Unit Tests** (orangefarbene Blöcke) dargestellt wird.

- Die Unit Tests validieren die Funktionalität sowohl des Frontends als auch des Backends.
- Die Tests sind in den Entwicklungsprozess integriert und sichern die Qualität der Module.

---

## Frontend

Das Frontend besteht aus zwei Technologien:

- **TypeScript mit Web-Angular** (lila Block) – Wird für Webanwendungen genutzt.
- **MVVM mit Avalonia** (grüner Block) – Eine Architektur für Desktop-Anwendungen.

Beide Frontend-Technologien kommunizieren über das **Internet** mit der **Web API** im Backend.

---

## Kommunikationsfluss

1. Das **Frontend (Web-Angular oder Avalonia)** sendet Anfragen über das Internet an die **Web API**.
2. Die **Web API** verarbeitet die Anfrage und interagiert mit den **Common**- und **Logic**-Modulen.
3. Die **Logic**-Schicht greift auf den **DataContext** zu, um Daten aus der Datenbank zu laden.
4. Das Ergebnis wird zurück an die **Web API** gesendet und anschließend an das **Frontend** übermittelt.
5. **Unit Tests** prüfen die einzelnen Komponenten, um die Qualität zu gewährleisten.

---

## Fazit

Diese Architektur trennt das System in eine **klare Schichtenstruktur** mit einer **gut definierten API**, einer **modularen Backend-Logik** und **Qualitätssicherung** durch automatisierte Tests. Sie ist sowohl für **Web- als auch Desktop-Anwendungen** ausgelegt.
