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
- Qualitätsmerkmale
  - Wartbarkeit: Leicht anpassbar an neue Anforderungen.
  - Skalierbarkeit: Kann wachsen und größere Lasten bewältigen.
  - Sicherheit: Schutz vor Angriffen und Datenverlust.
  - Performance: Effiziente Nutzung von Ressourcen.

### Warum ist eine gute Software-Architektur wichtig?

- Erleichtert die Entwicklung durch klare Strukturen.
- Verbessert Wartung & Erweiterbarkeit, da Änderungen gezielt vorgenommen werden können.
- Erhöht Zuverlässigkeit & Stabilität, indem Fehlerquellen minimiert werden.
- Unterstützt Skalierung für größere Nutzerzahlen oder höhere Lasten.

Fazit
Eine durchdachte Software-Architektur ist entscheidend für den Erfolg eines Softwareprojekts. Sie sorgt für eine effiziente Entwicklung, erleichtert die Wartung und stellt sicher, dass das System langfristig leistungsfähig und anpassbar bleibt.



Die Architektur besteht aus mehreren Schichten, die in drei Hauptbereiche unterteilt sind: **Frontend**, **Backend** und **Qualitätssicherung**. Die Kommunikation zwischen diesen Komponenten erfolgt über eine **Web API**.

---

## Backend

Das Backend ist in drei Hauptmodule unterteilt:

### Web API (Blauer Block)

- Enthält **Controllers** und **Models**.
- Dient als Schnittstelle zwischen Frontend und Backend-Logik.
- Ist für die Verarbeitung der Anfragen und das Bereitstellen der Daten zuständig.

### Common Modul (Gelber Block)

- Enthält:
  - **Contracts** – Definiert Schnittstellen für die Kommunikation.
  - **Modules** – Enthält wiederverwendbare Module.

### Logic Modul (Orangefarbener Block)

- Enthält:
  - **Contracts** – Definiert Geschäftslogik-Schnittstellen.
  - **DataContext** – Datenbankzugriff und ORM (Object-Relational Mapping).
  - **Entities** – Datenmodelle für die Anwendung.

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
