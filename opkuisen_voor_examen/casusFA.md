# Business Case: Planning Tool Applicatie
## De Verborgen Chaos van Scheduling

### Probleemstelling

In grote commerciële organisaties ontstaat er vaak chaos in de planning:

- **Binnenkomende bestellingen** stapelen zich op als uit te voeren taken
- **Werknemers** worden toegewezen aan specifieke taken
- **Taken** worden uitgevoerd volgens planning

### Veelvoorkomende Problemen

#### 🚨 Operationele Uitdagingen
- **Vertragingen**: Taken duren langer dan gepland
- **Vergeten taken**: Geen toewijzing of follow-up van taken
- **Gebrek aan overzicht**: Onduidelijkheid over wie wat doet
- **Verborgen problemen**: Geen zichtbaarheid op knelpunten

#### 💰 Kosten van Verborgen Problemen

| Probleem | Impact |
|----------|--------|
| **Verloren tijd** | Manueel achterhalen van scheduling problemen |
| **Hogere kosten** | Ongeplande downtime door niet-toegewezen werknemers |
| **Verminderde kwaliteit** | Dalende productiviteit, ontevreden klanten, langere levertijden |

### Waarom Een Oplossing Nodig Is

#### 📊 Inzichten Verkrijgen
- **Productiviteitsdoelstelling**: Minimaal 90% productiviteit
- **Maximaal verlies**: Niet meer dan 10%
- **Volledig overzicht**: Van alle scheduling activiteiten

#### 🔄 Verbeterde Communicatie
- **Juiste mensen, juiste moment**: Efficiënte taakverdeling
- **Snelle respons**: Bij ziekte/verlof taken snel herverdelingen
- **Centrale informatie**: Alle data op één platform
- **Visuele weergave**: Duidelijke, overzichtelijke interface

---

## Planning Tool Specificaties

### 🎯 Vereisten
- **Directe toegang**: Alle relevante informatie onmiddellijk beschikbaar
- **Eén platform**: Overzicht van alle vestigingen en werknemers
- **Taakmonitoring**: Geplande/niet-geplande taken, productie voortgang, notificaties

### 📈 Voordelen
- **Data-driven beslissingen** door managers
- **Snellere probleemoplossing** via juiste personeelsinzet
- **Efficiëntere samenwerking**

### 🎁 Value Proposition
- ✅ **Productiviteit verbeteren**
- ✅ **Kwaliteit verbeteren**
- ✅ **Kosten besparen**
- ✅ **Gestroomlijndere uitvoering en communicatie**
- ✅ **Verhoogde werktevredenheid**

---

## Missie
**Een Proof of Concept (POC) ontwikkelen** die een effectieve planning tool applicatie biedt als antwoord op bovenstaande uitdagingen.

---

# Component Overview

## 1. 📋 Task Overview
**Oplossing**: Overzicht van alle activiteiten per locatie

### Core Use Cases
- **Werknemers**:
  - Overzicht van eigen taken
  - Filteren en zoeken van taken
  - Taken markeren als "voltooid"
- **Managers**:
  - Plannen van vestigingen inzien
  - Overzicht taken per werknemer
- **Extra functionaliteit**:
  - Chatbot interactie voor taakvragen

---

## 2. 🏭 Plant Details
**Oplossing**: Datagestuurde inzichten

### Core Use Cases
- **Supervisors**: Vestigingdetails bekijken
- **Dashboard met KPI's**:
  - 📊 Afgewerkte taken per dag
  - 👥 Aantal werknemers per vestiging
  - 📝 Openstaande taken
  - ✅ Voltooide taken per maand
  - 📈 Grafieken: lijn, bar en donut met jaar-op-jaar vergelijking en trendlijnen

---

## 3. 🔔 Notification
**Oplossing**: Inzichten en communicatiemiddelen

### Core Use Cases
- **Managers**: Meldingen bij ziekte werknemers
- **Gebruikers**: Overzicht alle openstaande meldingen
- **Extra functionaliteit**: Meldingen bij planningswijzigingen

---

## 4. 🗂️ Master Data Management
**Oplossing**: Gestructureerde dataflow en minimalisatie human error

### Core Use Cases
**CRUD operaties** voor managers en supervisors:
- 🏢 **Productievestigingen**
- 📋 **Taken**
- 👤 **Werknemers**

> **Kritiek**: Onderlinge koppelingen tussen deze drie entiteiten zijn essentieel voor KPI Dashboard

---

## 5. 🏖️ Define Holiday/Illness
**Oplossing**: Geautomatiseerde afwezigheidsafhandeling

### Core Use Cases
- **Werknemers**:
  - Ziekmelding indienen
  - Verlof aanvragen
- **Automatisering**: 
  - Taken van afwezige werknemers automatisch op "niet toegekend"
- **Managers**:
  - Verlof goedkeuren
  - Visuele planning interface
  - Eenvoudig taken switchen en herplannen

---

## 🎯 Eindresultaat
Een geïntegreerde planning tool die organisaties helpt:
- **Zichtbaarheid** te creëren in scheduling processen
- **Efficiëntie** te verbeteren door geautomatiseerde workflows
- **Kosten** te besparen door optimale resource-allocatie
- **Kwaliteit** te verhogen door betere planning en communicatie