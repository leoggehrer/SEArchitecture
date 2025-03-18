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

Um die beschriebene Architektur in die Praxis umzusetzen, betrachten wir ein einfaches Beispielprojekt namens **ContactManager**. Dieses Projekt verwaltet Kontakte und verwendet die vorgestellte Architektur. Die Umsetzung erfolgt in einer Schritt für Schritt Anleitung. Bevor mit der Umsetzung begonnen wird - [hier](https://github.com/leoggehrer/SEArchitecture/blob/main/contactmanager.md) die Aufgabenstellung.

## Schritt für Schritt Umsetzung

### Erstellung der `Solution` 'ContactManager'

| Schritt      | Aktion | Note |
|--------------|--------|------|
| **1**        | Erstellen Sie eine `Solution` mit dem Namen **ContactManager** erstellt. | Verwenden Sie VS2022, VSCode oder Rider |

### Erstellung der `Bibliothek` 'ContactManager.Common'

| Schritt      | Aktion | Note |
|--------------|--------|------|
| **1**        | Fügen Sie der `Solution` eine Bibliothek mit dem Namen **ContactManager.Common** hinzu. | **Achtung:** Core-Bibliothek |
| **1.1**      | Löschen Sie die Klasse `Class1`. | |
| **2**        | Installieren Sie die folgenden 'NuGet'-Packages. | |
| **2.1**      | 'NuGet'-Packages für das Laden der **AppSetting**. | |
| **2.1.1**    | Microsoft.Extensions.Configuration | |
| **2.1.2**    | Microsoft.Extensions.Configuration.Json | |
| **2.1.3**    | Microsoft.Extensions.Configuration.EnviromentVariables | |
| **3**        | Erstellen Sie einen Ordner mit dem Name **Contracts**. | Hier werden die Schnittstellen gesammelt. |
| **3.1**      | Erstellen Sie eine Schnittstelle mit dem Namen `IIdentifiable`. | |
| **3.1.A**    | Definieren Sie die Eigenschaften von `IIdentifiable`. | `Id` |
| **3.2**      | Erstellen Sie eine Schnittstelle mit dem Namen `IContact`. | |
| **3.2.A**    | Definieren Sie die Eigenschaften von `IContact`. | siehe Aufgabenstellung |
| **3.2.B**    | Implementieren Sie die Methode `CopyProperties(IContact other)` von `IContact`. | Kopiert alle Eigenschaften. |
| **3.3**      | Erstellen Sie eine Schnittstelle mit dem Namen `ISettings`. |  |
| **3.3.A**    | Definieren Sie den Indexer in `ISettings`. | `string? this[string key] { get; }` |
| **4**        | Erstellen Sie einen Ordner mit dem Name **Modules**. | Hier werden zusätzliche Komponenten implementiert. |
| **4.1**      | Erstellen Sie einen Unterordner mit dem Name **Configuration**. | In diesem Abschnitt ist die Komponente `AppSettings`. |
| **4.2**      | Erstellen Sie die Klasse `AppSettings` im Ordner **Configuration**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithCommon/blob/master/ContactManager.Common/Modules/Configuration/AppSettings.cs). |

> **HINWEIS:** Die **Solution** muss übersetzbar sein!

Die fertige Lösung finden Sie [hier](https://github.com/leoggehrer/ContactManagerWithCommon).

### Erstellung des `Bibliothek` 'ContactManager.Logic'

| Schritt      | Aktion | Note |
|--------------|--------|------|
| **1**        | Fügen Sie der `Solution` eine Bibliothek mit dem Namen **ContactManager.Logic** hinzu. | **Achtung:** Core-Bibliothek |
| **1.1**      | Löschen Sie die Klasse `Class1`. | |
| **1.2**      | Verbinden Sie das Projekt **ContactManager.Logic** mit dem Projekt **ContactManager.Common**. | |
| **2**        | Installieren Sie die folgenden 'NuGet'-Packages. | |
| **2.1**      | 'NuGet'-Packages für das Verwenden des **EntityFrameworkCore**. | |
| **2.1.1**    | Microsoft.EntityFrameworkCore | Basis für den **EF** |
| **2.1.2**    | Microsoft.EntityFrameworkCore.Sqlite | Verwendung von **Sqlite** als Datenbank |
| **2.1.3**    | Microsoft.EntityFrameworkCore.SqlServer | Verwendung von **SQL Server** als Datenbank |
| **3**        | Erstellen Sie einen Ordner mit dem Name **Entities**. | Hier werden die Entitäten implementiert. |
| **3.1**      | Erstellen Sie die Klasse `EntityObject` im Ordner **Entities**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithLogic/blob/master/ContactManager.Logic/Entities/EntityObject.cs). |
| **3.2**      | Erstellen Sie die Klasse `Contact` im Ordner **Entities**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithLogic/blob/master/ContactManager.Logic/Entities/Contact.cs). |
| **4**        | Erstellen Sie einen Ordner mit dem Name **Contracts**. | Hier werden die Schnittstellen gesammelt. |
| **4.1**      | Erstellen Sie eine Schnittstelle mit dem Namen `IContext`. |  |
| **4.2**      | Definieren Sie die Eigenschaften und Methoden von `IContext`. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithLogic/blob/master/ContactManager.Logic/Contracts/IContext.cs). |
| **5**        | Erstellen Sie einen Ordner mit dem Name **DataContext**. | Hier befindet sich der Datenzugriff. |
| **5.1**      | Erstellen Sie die Klasse `ContactContext` im Ordner **DataContext**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithLogic/blob/master/ContactManager.Logic/DataContext/ContactContext.cs). |
| **5.2**      | Erstellen Sie die Klasse `Factory` im Ordner **DataContext**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithLogic/blob/master/ContactManager.Logic/DataContext/Factory.cs). |

> **HINWEIS:** Die **Solution** muss übersetzbar sein!

Die fertige Lösung finden Sie [hier](https://github.com/leoggehrer/ContactManagerWithLogic).

### Erstellung der `Logic.UnitTests` 'ContactManager.Logic.UnitTests'

Dieses Kapitel folgt zu einem späteren Zeitpunkt!

### Erstellung des `WebServers` 'ContactManager.WebApi'

| Schritt      | Aktion | Note |
|--------------|--------|------|
| **1**        | Fügen Sie der `Solution` ein **ASP.NET Core Web App** Projekt mit dem Namen **ContactManager.WebApi** hinzu. |  |
| **1.1**      | Verbinden Sie das Projekt **ContactManager.WebApi** mit dem Projekt **ContactManager.Logic**. | |
| **2**        | Installieren Sie die folgenden 'NuGet'-Packages. | |
| **2.1**      | 'NuGet'-Packages für das Verwenden des **Dynamic Linq**. | |
| **2.1.1**    | System.Linq.Dynamic.Core | String to Linq |
| **2.2**      | 'NuGet'-Packages für die Verwendung von **PATCH**. | |
| **2.2.1**    | Microsoft.AspNetCore.JsonPatch |  |
| **2.2.2**    | Microsoft.AspNetCore.Mvc.NewtonsoftJson |  |
| **3**        | Löschen Sie die Dateien `WeatherForecast` und `WeatherForecastController`. |  |
| **4**        | Anpassen der **AppSettings**. |  |
| **4.1**      | Anpassen von `appsettings.json`. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithWebApi/blob/master/ContactManager.WebApi/appsettings.json). |
| **4.2**      | Anpassen von `appsettings.Development.json`. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithWebApi/blob/master/ContactManager.WebApi/appsettings.Development.json). |
| **5**        | Erstellen Sie einen Ordner mit dem Name **Models**. |  |
| **5.1**      | Erstellen Sie die Klasse `UserData` im Ordner **Models**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithWebApi/blob/master/ContactManager.WebApi/Models/UserData.cs). |
| **5.2**      | Erstellen Sie die Klasse `ModelObject` im Ordner **Models**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithWebApi/blob/master/ContactManager.WebApi/Models/ModelObject.cs). |
| **5.3**      | Erstellen Sie die Klasse `Contact` im Ordner **Models**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithWebApi/blob/master/ContactManager.WebApi/Models/Contact.cs). |
| **6**        | Erstellen von **Controllers**. |  |
| **6.1**      | Erstellen Sie die Klasse `SystemController` im Ordner **Controllers**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithWebApi/blob/master/ContactManager.WebApi/Controllers/SystemController.cs). |
| **6.2**      | Erstellen Sie die Klasse `ContactsController` im Ordner **Controllers**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithWebApi/blob/master/ContactManager.WebApi/Controllers/ContactsController.cs). |

> **HINWEIS:** Die **Solution** muss übersetzbar sein!

Die fertige Lösung finden Sie [hier](https://github.com/leoggehrer/ContactManagerWithWebApi).

### Erstellung der `MVVM-App` 'ContactManager.MVVMApp'

| Schritt      | Aktion | Note |
|--------------|--------|------|
| **1**        | Fügen Sie der `Solution` ein **Avalonia.NET MVVM App** Projekt mit dem Namen **ContactManager.MVVMApp** hinzu. |  |
| **1.1**      | Verbinden Sie das Projekt **ContactManager.MVVMApp** mit dem Projekt **ContactManager.Common**. | |
| **2**        | Erstellen und Anpassen der **AppSettings**. |  |
| **2.1**      | Erstellen der Datei `appsettings.json`. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithMVVMApp/blob/master/ContactManager.MVVMApp/appsettings.json). |
| **2.2**      | Erstellen der Datei `appsettings.Development.json`. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithMVVMApp/blob/master/ContactManager.MVVMApp/appsettings.Development.json). |
| **3**        | Erstellen Sie einen Ordner mit dem Name **Models**. |  |
| **3.1**      | Erstellen Sie die Klasse `ModelObject` im Ordner **Models**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithMVVMApp/blob/master/ContactManager.MVVMApp/Models/ModelObject.cs). |
| **3.2**      | Erstellen Sie die Klasse `Contact` im Ordner **Models**. | Siehe [hier](https://github.com/leoggehrer/ContactManagerWithMVVMApp/blob/master/ContactManager.MVVMApp/Models/Contact.cs). |

> **HINWEIS:** Die **Solution** muss übersetzbar sein!

Die fertige Lösung finden Sie [hier](https://github.com/leoggehrer/ContactManagerWithMVVMApp).

## Fazit

Das **ContactManager**-Projekt zeigt, wie die vorgestellte Architektur mit DotNet (C#) umgesetzt werden kann. Die klare Trennung der Schichten und die Verwendung von Schnittstellen erleichtern die Wartung und Erweiterung des Systems. Die Web API ermöglicht die Kommunikation zwischen Frontend und Backend, während die Geschäftslogik und Datenzugriffsschicht im Logic-Modul gekapselt sind.
