# Lastenboek Planning Tool Applicatie

## 1. Inleiding

### 1.1 Projectcontext
Dit lastenboek beschrijft de functionele en niet-functionele requirements voor een planning tool applicatie die de verborgen chaos van scheduling in grote commerciële organisaties moet oplossen. De tool moet zorgen voor verhoogde productiviteit, betere kwaliteit, kostenbesparing en gestroomlijnde communicatie.

### 1.2 Doelstellingen
- Volledig overzicht van scheduling en taaktoewijzing
- Data-driven besluitvorming mogelijk maken
- Maximaal 10% verlies aan productiviteit
- Centrale communicatie en notificaties
- Proactief beheer van afwezigheden

### 1.3 Scope
De applicatie ondersteunt drie hoofdrollen (Manager, Supervisor, Werknemer) en omvat vijf kerncomponenten: Task Overview, Plant Details, Notifications, Master Data Management, en Holiday/Illness Management.

---

## 2. Use Case Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    PLANNING TOOL SYSTEEM                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌─────────┐                                                     │
│  │ Manager │                                                     │
│  └────┬────┘                                                     │
│       │                                                          │
│       ├──► UC01: Teams en werknemers beheren                    │
│       ├──► UC02: Taken toewijzen en beheren                     │
│       ├──► UC03: Verlof goedkeuren/afwijzen                     │
│       ├──► UC04: Centraal planningsbord gebruiken               │
│       ├──► UC05: Vestigingen beheren (CRUD)                     │
│       ├──► UC06: Taken beheren (CRUD)                           │
│       ├──► UC07: Werknemers beheren (CRUD)                      │
│       ├──► UC08: Dashboard met KPI's bekijken                   │
│       ├──► UC09: Plant details bekijken                         │
│       ├──► UC10: Notificaties bekijken                          │
│       ├──► UC11: Takenplanning per werknemer bekijken           │
│       ├──► UC12: Taken herplannen bij afwezigheid               │
│       ├──► UC14: Eigen planning bekijken                        │ 
│       └──► UC16: Taken overzicht bekijken        				     │ 
│                                                                   │
│  ┌───────────┐                                                   │
│  │ Supervisor│                                                   │
│  └─────┬─────┘                                                   │
│        │                                                          │
│        	├──► UC04: Centraal planningsbord gebruiken               │
│        ├──► UC09: Plant details bekijken                         │
│        ├──► UC08: Dashboard met KPI's bekijken                   │
│        ├──► UC13: Teamplanning bekijken                          │
│        ├──► UC14: Eigen planning bekijken                        │
│        ├──► UC15: Taken van team filteren/zoeken                │
│        ├──► UC10: Notificaties bekijken                          │
│        ├──► UC05: Vestigingen beheren (CRUD)                     │
│        ├──► UC06: Taken beheren (CRUD)                           │
│        ├──► UC07: Werknemers beheren (CRUD)                      │ 
│        └──► UC16: Taken overzicht bekijken                        │
│                                                                   │
│  ┌──────────┐                                                    │
│  │Werknemer │                                                    │
│  └────┬─────┘                                                    │
│       │                                                          │
│       ├──► UC14: Eigen planning bekijken                         │
│       ├──► UC16: Taken overzicht bekijken                        │
│       ├──► UC17: Eigen taken filteren/zoeken                           │
│       ├──► UC18: Taak markeren als voltooid                      │
│       ├──► UC19: Afwezigheid melden (ziekte)                     │
│       ├──► UC20: Verlof aanvragen                                │
│       ├──► UC21: Afwezigheden opvolgen en beheren                │
│       ├──► UC10: Notificaties bekijken                           │
│       └──► UC22: Chatbot raadplegen over taken (extra)          │
│                                                                   │
│  ┌─────────┐                                                     │
│  │ Systeem │ (automatisch)                                       │
│  └────┬────┘                                                     │
│       │                                                          │
│       ├──► UC23: Taken auto-dealloceren bij afwezigheid         │
│       ├──► UC24: Notificatie versturen bij planningswijziging   │
│       ├──► UC25: Notificatie versturen bij ziekte               │
│       └──► UC26: KPI's automatisch berekenen                    │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

## 3. Functionele Requirements (Use Cases)

### UC01: Een manager kan supervisors en werknemers aan teams toewijzen en beheren

**Primaire actor:** Manager

**Stakeholders:** 
- Manager: wil teams samenstellen en wijzigen
- Supervisors: willen weten welk team ze beheren
- Werknemers: willen weten tot welk team ze behoren
- Organisatie: wil duidelijke teamstructuur

**Precondities:**
- Manager is ingelogd en geauthenticeerd
- Vestigingen zijn aangemaakt in het systeem
- Werknemers en supervisors zijn aangemaakt in het systeem

**Postcondities:**
- Teamsamenstelling is opgeslagen in het systeem
- Werknemers en supervisors zijn gekoppeld aan teams
- Wijzigingen zijn zichtbaar in het planningsoverzicht

**Normaal verloop:**
1. Manager navigeert naar de teambeheerpagina
2. Systeem toont overzicht van bestaande teams en beschikbare werknemers
3. Manager selecteert een vestiging
4. Manager creëert een nieuw team of selecteert bestaand team
5. Manager wijst een supervisor toe aan het team
6. Manager selecteert werknemers om aan het team toe te voegen
7. Manager bevestigt de teamsamenstelling
8. Systeem valideert de teamsamenstelling (DR_TEAM_01, DR_TEAM_02)
9. Systeem bewaart de wijzigingen
10. Systeem toont bevestiging van succesvolle opslag
11. Systeem stuurt notificatie naar toegevoegde teamleden

**Alternatieve verlopen:**
- 8a. Supervisor is al toegewezen aan ander team:
  - Systeem toont waarschuwing
  - Manager kan supervisor verplaatsen of actie annuleren
- 8b. Werknemer heeft actieve taken in ander team:
  - Systeem toont waarschuwing met openstaande taken
  - Manager moet eerst taken herplannen of transfer bevestigen
- 6a. Manager verwijdert werknemer uit team:
  - Systeem controleert op toegewezen taken
  - Systeem dealloceert toekomstige taken of vraagt bevestiging
- 4a. Manager wijzigt teamnaam of teamdetails:
  - Systeem update teamgegevens
  - Historische data blijft behouden

**Domeinspecifieke regels:**

**DR_TEAM_01**: Een supervisor kan maximaal toegewezen worden aan één team tegelijkertijd.

**DR_TEAM_02**: Een werknemer kan lid zijn van meerdere teams, maar moet een primair team hebben voor rapportagedoeleinden.

**DR_TEAM_03**: Een team moet minimaal 1 supervisor en 1 werknemer bevatten om actief te kunnen zijn.

**Op te klaren punten:**
- Moeten werknemers notificatie krijgen bij teamwijziging?
- Kunnen teams cross-vestiging zijn of zijn ze vestigingspecifiek?
- Wat gebeurt er met teamhistoriek bij ontbinding van een team?
- Maximaal aantal werknemers per team?

---

### UC02: Een manager kan teamleden aan taken toewijzen en eigen taken beheren

**Primaire actor:** Manager

**Stakeholders:**
- Manager: wil taken efficiënt toewijzen
- Werknemers: willen duidelijke taakopdrachten
- Klanten: willen tijdige oplevering
- Organisatie: wil optimale capaciteitsbenutting

**Precondities:**
- Manager is ingelogd en geauthenticeerd
- Taken zijn aangemaakt in het systeem
- Werknemers zijn beschikbaar en niet op verlof/ziek
- Teams zijn samengesteld

**Postcondities:**
- Taken zijn toegewezen aan werknemers
- Werknemers zien nieuwe taken in hun overzicht
- Planningstool reflecteert de wijzigingen
- Capaciteit per werknemer is bijgewerkt

**Normaal verloop:**
1. Manager navigeert naar het centrale planningsbord
2. Systeem toont overzicht van niet-toegewezen taken en beschikbare werknemers
3. Manager selecteert een taak uit de lijst
4. Systeem toont taakdetails (geschatte duur, prioriteit, deadline, vereiste competenties)
5. Manager selecteert een werknemer of team
6. Systeem toont beschikbaarheid en huidige werkbelasting van geselecteerde werknemer(s)
7. Manager bevestigt toewijzing en plant start- en einddatum
8. Systeem valideert de toewijzing (DR_TASK_01, DR_TASK_02, DR_TASK_03)
9. Systeem bewaart de taaktoewijzing
10. Systeem update capaciteitsplanning
11. Systeem stuurt notificatie naar werknemer
12. Systeem toont bevestiging van succesvolle toewijzing

**Alternatieve verlopen:**
- 8a. Werknemer heeft onvoldoende capaciteit:
  - Systeem toont waarschuwing met overcapaciteit percentage
  - Manager kan andere werknemer kiezen of toewijzing forceren met reden
- 8b. Werknemer mist vereiste competentie:
  - Systeem toont waarschuwing
  - Manager kan toewijzing bevestigen met training indicatie
- 3a. Manager wijzigt bestaande taaktoewijzing:
  - Systeem controleert voortgang van de taak
  - Bij gedeeltelijke voltooiing: systeem vraagt bevestiging
  - Beide werknemers (oud en nieuw) ontvangen notificatie
- 5a. Manager wijst taak toe aan zichzelf:
  - Systeem behandelt manager als werknemer voor deze taak
  - Taak verschijnt in manager's eigen takenoverzicht
- 2a. Manager zoekt/filtert taken:
  - Systeem biedt filters: vestiging, prioriteit, status, deadline, niet-toegewezen
  - Systeem toont gefilterde resultaten

**Domeinspecifieke regels:**

**DR_TASK_01**: Een taak kan aan maximaal één werknemer tegelijk toegewezen worden.

**DR_TASK_02**: De geplande capaciteit van een werknemer mag niet meer dan 110% bedragen (met waarschuwing tussen 90-110%).

**DR_TASK_03**: Taken met hoge prioriteit moeten binnen 24 uur toegewezen worden aan een werknemer.

**DR_TASK_04**: Een taak die al gestart is (status = "in progress") kan alleen herplanend worden met bevestiging en reden.

**Op te klaren punten:**
- Moeten taken automatisch voorgestelde werknemers tonen op basis van competenties en capaciteit?
- Wat is de maximum lookahead periode voor taakplanning?
- Kunnen taken gesplitst worden over meerdere werknemers?
- Moet er een audit trail zijn van alle taakmutaties?

---

### UC20: Een werknemer kan een afwezigheid melden en zijn afwezigheden opvolgen en beheren

**Primaire actor:** Werknemer

**Stakeholders:**
- Werknemer: wil afwezigheid correct registreren
- Manager: wil tijdig geïnformeerd worden voor herplanning
- Team: wordt beïnvloed door afwezigheid
- HR: moet afwezigheden bijhouden

**Precondities:**
- Werknemer is ingelogd en geauthenticeerd
- Werknemer heeft een actieve arbeidsrelatie
- Werknemer heeft mogelijk toegewezen taken

**Postcondities:**
- Afwezigheid is geregistreerd in het systeem
- Bij ziekte: manager ontvangt onmiddellijke notificatie
- Bij verlof: aanvraag wacht op goedkeuring
- Toegewezen taken in afwezigheidsperiode krijgen status "niet toegewezen"
- Werknemer ziet afwezigheid in persoonlijk overzicht

**Normaal verloop:**
1. Werknemer navigeert naar afwezigheidsbeheer
2. Systeem toont overzicht van geplande en historische afwezigheden
3. Werknemer selecteert "nieuwe afwezigheid melden"
4. Systeem vraagt type afwezigheid: ziekte of verlof
5. Werknemer selecteert type afwezigheid
6. Systeem toont formulier voor afwezigheidsdetails
7. Werknemer vult in: startdatum, einddatum (indien gekend), reden (optioneel voor verlof)
8. Systeem toont overzicht van taken die beïnvloed worden door deze afwezigheid
9. Werknemer bevestigt de afwezigheidsmelding
10. Systeem valideert de afwezigheid (DR_ABSENCE_01, DR_ABSENCE_02)
11. Systeem registreert de afwezigheid
12. **Bij ziekte:** Systeem voert UC23 uit (taken auto-dealloceren) en UC25 (notificatie naar manager)
13. **Bij verlof:** Systeem creëert verlofaanvraag met status "in behandeling"
14. Systeem toont bevestiging
15. Systeem update beschikbaarheidsplanning

**Alternatieve verlopen:**
- 10a. Overlappende afwezigheid gedetecteerd:
  - Systeem toont waarschuwing met bestaande afwezigheid
  - Werknemer kan datums aanpassen of bevestigen
- 8a. Geen beïnvloede taken:
  - Systeem toont "Geen taken gepland in deze periode"
  - Workflow gaat verder naar stap 9
- 2a. Werknemer wijzigt bestaande afwezigheid:
  - Bij ziekte: werknemer kan einddatum bijwerken (verlengen/verkorten)
  - Bij verlof: alleen mogelijk indien status = "in behandeling" of "goedgekeurd" met herbevestiging manager
  - Systeem hervalideert beïnvloede taken
- 2b. Werknemer annuleert afwezigheid:
  - Systeem vraagt bevestiging
  - Bij verlof: mogelijk tot 24u voor startdatum
  - Bij ziekte: alleen toekomstige afwezigheden
  - Systeem herstelt taken NIET automatisch (manager moet hertoewijzen)
- 7a. Werknemer vult geen einddatum in (bij ziekte):
  - Systeem accepteert open-ended ziekte
  - Manager krijgt reminder om status op te volgen
  - Werknemer moet later terugkeer melden

**Domeinspecifieke regels:**

**DR_ABSENCE_01**: Ziektemelding moet minimaal de startdatum bevatten; einddatum is optioneel.

**DR_ABSENCE_02**: Verlofaanvraag moet minimaal 5 werkdagen op voorhand ingediend worden, tenzij uitzonderlijke omstandigheden.

**DR_ABSENCE_03**: Overlappende afwezigheidsperiodes voor dezelfde werknemer zijn niet toegestaan.

**DR_ABSENCE_04**: Bij afwezigheid worden alle taken in de afwezigheidsperiode automatisch gedealloceerd (status = "niet toegewezen").

**DR_ABSENCE_05**: Een afwezigheid kan enkel geannuleerd worden minimum 24 uur voor aanvang, behalve bij ziekte.

**Op te klaren punten:**
- Moet de werknemer documentatie kunnen uploaden (bijv. doktersattest)?
- Hoe lang blijven historische afwezigheden zichtbaar?
- Kunnen werknemers zien hoeveel verlofdagen ze nog hebben?
- Moet er een optie zijn voor deeltijdse afwezigheid (halve dagen)?
- Wat gebeurt er met taken die al gestart zijn bij ziektemelding?

---

### UC13: Een supervisor kan de planning van zijn team en zijn eigen planning bekijken

**Primaire actor:** Supervisor

**Stakeholders:**
- Supervisor: wil teamoverzicht en eigen planning
- Teamleden: hun planning wordt gecontroleerd
- Manager: verwacht dat supervisor team monitort
- Organisatie: wil dat supervisors teams efficiënt begeleiden

**Precondities:**
- Supervisor is ingelogd en geauthenticeerd
- Supervisor is toegewezen aan minimaal één team
- Team heeft werknemers en eventueel toegewezen taken

**Postcondities:**
- Supervisor heeft actueel overzicht van teamplanning en eigen planning
- Geen data wordt gewijzigd (read-only functie)

**Normaal verloop:**
1. Supervisor navigeert naar planningsoverzicht
2. Systeem toont standaardweergave met twee secties: "Mijn Planning" en "Team Planning"
3. Systeem toont supervisor's eigen toegewezen taken met status, deadline en prioriteit
4. Systeem toont planning van alle teamleden met hun taken
5. Supervisor selecteert een weergavemodus (dag, week, maand)
6. Systeem past de weergave aan met geselecteerde tijdsperiode
7. Systeem visualiseert:
   - Toegewezen taken per werknemer (kleurgecodeerd naar status)
   - Capaciteitsbenutting per werknemer (percentage)
   - Deadlines en prioriteiten
   - Afwezigheden (verlof, ziekte)
8. Supervisor kan individuele taken selecteren voor detailweergave
9. Systeem toont taakdetails in popup of sidepanel
10. Supervisor kan filters toepassen (werknemer, status, vestiging, prioriteit)
11. Systeem toont gefilterde resultaten

**Alternatieve verlopen:**
- 2a. Supervisor beheert meerdere teams:
  - Systeem toont teamkiezer dropdown
  - Supervisor selecteert team
  - Systeem toont planning van geselecteerd team
- 7a. Een of meerdere werknemers hebben overcapaciteit (>90%):
  - Systeem markeert deze werknemers visueel (bijv. rode markering)
  - Supervisor ziet waarschuwingsindicator
- 7b. Er zijn niet-toegewezen taken in het team:
  - Systeem toont aparte sectie "Niet-toegewezen taken"
  - Supervisor ziet aantal niet-toegewezen taken
  - Supervisor kan manager notificeren (optioneel)
- 3a. Supervisor heeft geen eigen taken:
  - Systeem toont boodschap "Geen taken momenteel toegewezen"
- 10a. Supervisor exporteert planning:
  - Systeem biedt export functie (PDF, Excel)
  - Systeem genereert rapport met huidige weergave
- 8a. Supervisor zoekt specifieke taak:
  - Systeem biedt zoekfunctie
  - Supervisor voert taaknaam of ID in
  - Systeem highlight de taak in de planning

**Domeinspecifieke regels:**

**DR_PLANNING_01**: Supervisor kan enkel planning zien van teams waaraan hij/zij is toegewezen.

**DR_PLANNING_02**: Historische planning is toegankelijk tot 3 maanden terug.

**DR_PLANNING_03**: Toekomstige planning is zichtbaar tot maximaal 6 maanden vooruit.

**DR_PLANNING_04**: Capaciteitsbenutting wordt berekend als: (som geschatte uren toegewezen taken / beschikbare uren) × 100%.

**Op te klaren punten:**
- Moet supervisor notificaties kunnen activeren voor specifieke events (bijv. overcapaciteit)?
- Kunnen supervisors commentaar toevoegen aan taken (read-only context)?
- Moet er real-time synchronisatie zijn of periodieke refresh?
- Welke kleuren/statussen worden gebruikt voor visuele codering?
- Kan supervisor aanbevelingen doen aan manager voor hertoewijzing?

---

### UC14: Een werknemer kan zijn eigen planning bekijken

**Primaire actor:** Werknemer

**Stakeholders:**
- Werknemer: wil eigen taken en planning kennen
- Manager/Supervisor: verwacht dat werknemer planning volgt
- Team: wordt beïnvloed door werknemer's uitvoering
- Organisatie: wil dat werknemers hun prioriteiten kennen

**Precondities:**
- Werknemer is ingelogd en geauthenticeerd
- Werknemer heeft mogelijk toegewezen taken

**Postcondities:**
- Werknemer heeft actueel overzicht van eigen planning
- Geen data wordt gewijzigd (read-only functie)
- Werknemer is op de hoogte van prioriteiten en deadlines

**Normaal verloop:**
1. Werknemer navigeert naar "Mijn Planning"
2. Systeem toont overzicht van toegewezen taken
3. Systeem visualiseert taken in kalenderweergave (dag, week of maand)
4. Voor elke taak toont systeem:
   - Taaknaam en beschrijving
   - Status (niet gestart, in uitvoering, voltooid)
   - Prioriteit (laag, normaal, hoog, urgent)
   - Geschatte duur
   - Deadline
   - Vestiging/locatie
   - Toegewezen datum
5. Werknemer selecteert een weergavemodus (dag, week, maand)
6. Systeem past weergave aan
7. Werknemer kan individuele taak selecteren voor meer details
8. Systeem toont uitgebreide taakdetails
9. Systeem toont ook geplande afwezigheden (verlof, ziekte) in de planning
10. Werknemer ziet totale werkbelasting (percentage capaciteit)

**Alternatieve verlopen:**
- 2a. Werknemer heeft geen toegewezen taken:
  - Systeem toont boodschap "Geen taken momenteel toegewezen"
  - Systeem suggereert contact met supervisor
- 10a. Werknemer heeft overcapaciteit (>100%):
  - Systeem toont waarschuwingsbericht
  - Systeem suggereert contact met manager/supervisor
- 7a. Werknemer filtert taken:
  - Systeem biedt filters: status, prioriteit, vestiging, deadline
  - Systeem toont gefilterde resultaten
- 7b. Werknemer zoekt specifieke taak:
  - Werknemer voert zoekterm in
  - Systeem toont matchende taken
- 5a. Werknemer wisselt tussen kalender- en lijstweergave:
  - Systeem biedt toggle tussen weergavemodi
  - Systeem bewaart voorkeur voor toekomstige sessies
- 8a. Werknemer bekijkt taakhistoriek:
  - Systeem toont eerdere updates aan de taak
  - Systeem toont wie wijzigingen heeft aangebracht
- 2b. Werknemer ziet toekomstige taken:
  - Systeem toont taken die nog niet gestart zijn met startdatum in toekomst
  - Taken zijn visueel onderscheiden van huidige taken

**Domeinspecifieke regels:**

**DR_PLANNING_05**: Werknemer kan enkel eigen toegewezen taken zien, niet die van collega's.

**DR_PLANNING_06**: Taken met deadline binnen 48 uur worden visueel gemarkeerd als urgent.

**DR_PLANNING_07**: Voltooide taken blijven zichtbaar in de planning gedurende 30 dagen.

**DR_PLANNING_08**: Werknemer ziet alleen taken toegewezen vanaf vandaag tot 3 maanden vooruit.

**Op te klaren punten:**
- Moet de werknemer kunnen zien wie de taak heeft toegewezen?
- Kunnen werknemers notities/commentaar zien die aan taken gekoppeld zijn?
- Moet er synchronisatie zijn met externe kalenders (Google Calendar, Outlook)?
- Kunnen werknemers de volgorde van taken aanpassen (prioriteit suggereren)?
- Moet de planning print/exporteerbaar zijn?

---

### UC04: Een manager heeft een centraal bord om taken en werkuren te plannen voor werknemers

**Primaire actor:** Manager

**Stakeholders:**
- Manager: wil efficiënt en visueel plannen
- Werknemers: ontvangen planning en taaktoewijzingen
- Supervisors: zien resultaat van planning in hun teams
- Organisatie: wil optimale capaciteitsbenutting en <10% verlies

**Precondities:**
- Manager is ingelogd en geauthenticeerd
- Vestigingen, teams, werknemers en taken zijn aangemaakt in systeem
- Werknemers hebben beschikbaarheid en capaciteitsinformatie

**Postcondities:**
- Taken zijn visueel gepland en toegewezen aan werknemers
- Planning is opgeslagen en zichtbaar voor betrokken werknemers
- Capaciteitsbenutting is geoptimaliseerd
- Werknemers ontvangen notificaties van nieuwe/gewijzigde toewijzingen

**Normaal verloop:**
1. Manager navigeert naar centraal planningsbord
2. Systeem toont visueel dashboard met:
   - Tijdslijn (weken/maanden weergave)
   - Werknemers (rijen per werknemer)
   - Taken (visuele blokken op tijdslijn)
   - Niet-toegewezen taken (aparte sectie/zijbalk)
   - Afwezigheden (verlof, ziekte) gemarkeerd op tijdslijn
3. Manager selecteert weergavefilters (vestiging, team, periode)
4. Systeem toont gefilterde planning
5. Manager selecteert niet-toegewezen taak uit de lijst
6. Systeem toont taakdetails en suggesties voor geschikte werknemers (op basis van capaciteit, competenties)
7. Manager draagt taak via drag-and-drop naar werknemer en tijdslot
8. Systeem valideert toewijzing real-time (DR_TASK_02, DR_PLANNING_09)
9. Systeem visualiseert capaciteitsimpact met kleurcode:
   - Groen: <70% capaciteit
   - Oranje: 70-90% capaciteit
   - Rood: >90% capaciteit
10. Manager bevestigt toewijzing
11. Systeem bewaart toewijzing
12. Systeem update visuele planning
13. Systeem stuurt notificatie naar werknemer (UC24)
14. Manager kan proces herhalen voor volgende taken

**Alternatieve verlopen:**
- 8a. Werknemer heeft conflicterende afwezigheid:
  - Systeem blokkeert toewijzing
  - Systeem toont waarschuwing met afwezigheidsdetails
  - Manager kiest andere werknemer of ander tijdslot
- 8b. Werknemer heeft overcapaciteit bij toewijzing:
  - Systeem toont waarschuwing met overcapaciteitspercentage
  - Manager kan forceren met reden of andere werknemer kiezen
- 7a. Manager past bestaande toewijzing aan:
  - Manager selecteert bestaande taak op tijdslijn
  - Manager draagt taak naar andere werknemer of ander tijdslot
  - Systeem vraagt bevestiging
  - Oude en nieuwe werknemer ontvangen notificatie
- 7b. Manager verwijdert toewijzing:
  - Manager selecteert taak en kiest "dealloceren"
  - Systeem plaatst taak terug in niet-toegewezen lijst
  - Werknemer ontvangt notificatie
- 5a. Manager creëert nieuwe taak direct vanuit planningsbord:
  - Manager klikt "Nieuwe taak"
  - Systeem toont quick-create formulier
  - Manager kan direct toewijzen aan werknemer
- 2a. Manager gebruikt bulkoperaties:
  - Manager selecteert meerdere taken (multi-select)
  - Manager wijst alle taken toe aan team/werknemer
  - Systeem valideert alle toewijzingen
  - Systeem toont samenvattend rapport
- 2b. Manager bekijkt capaciteitsoverzicht:
  - Systeem toont aggregaat statistieken per team/vestiging
  - Manager ziet gem. capaciteitsbenutting, overbelaste werknemers, beschikbare capaciteit
- 7c. Manager kopieert planning van vorige week/maand:
  - Manager selecteert "planning kopiëren"
  - Systeem dupliceert toewijzingen naar nieuwe periode
  - Systeem valideert en toont conflicten
  - Manager past aan waar nodig

**Domeinspecifieke regels:**

**DR_PLANNING_09**: Het planningsbord gebruikt real-time validatie bij elke drag-and-drop actie.

**DR_PLANNING_10**: Kleurcodering voor capaciteit: Groen (<70%), Oranje (70-90%), Rood (>90%).

**DR_PLANNING_11**: Taken kunnen niet toegewezen worden aan werknemers die afwezig zijn in die periode.

**DR_PLANNING_12**: Het systeem suggereert automatisch de top 3 meest geschikte werknemers op basis van: beschikbare capaciteit, vereiste competenties, vestiging, eerdere ervaring met soortgelijke taken.

**DR_PLANNING_13**: Wijzigingen in het planningsbord worden automatisch opgeslagen na bevestiging (auto-save).

**Op te klaren punten:**
- Moet het systeem waarschuwen wanneer totale teamcapaciteit <90% is (onderbenutting)?
- Kunnen managers "wat-als" scenario's simuleren zonder op te slaan?
- Moet er een undo/redo functie zijn voor planningswijzigingen?
- Kunnen meerdere managers gelijktijdig plannen (collaborative editing)?
- Welke granulariteit heeft de tijdslijn (uur, dag, week)?
- Moet het systeem automatische suggesties geven voor optimale planning (AI-assisted)?

---

### UC24: Een werknemer ontvangt een melding bij updates in hun planning. Bij afwezigheid wordt de manager automatisch verwittigd

**Primaire actor:** Systeem (automatisch proces)

**Stakeholders:**
- Werknemer: wil tijdig op de hoogte zijn van planningswijzigingen
- Manager: moet weten wanneer werknemers afwezig zijn
- Organisatie: wil effectieve communicatie en snelle reactie

**Precondities:**
- Notificatiesysteem is actief
- Gebruikers hebben notificatievoorkeuren ingesteld
- Er vindt een trigger event plaats (taakwijziging, afwezigheid)

**Postcondities:**
- Betrokken gebruikers ontvangen notificatie
- Notificatie is gelogd in het systeem
- Gebruikers kunnen notificatie bekijken en actie ondernemen

**Normaal verloop:**

**Scenario A: Planningswijziging voor werknemer**
1. Systeem detecteert planningswijziging (nieuwe taak, taakwijziging, deallocatie)
2. Systeem identificeert betrokken werknemer(s)
3. Systeem controleert notificatievoorkeuren van werknemer
4. Systeem creëert notificatiebericht met:
   - Type wijziging (nieuwe taak, gewijzigde taak, verwijderde taak)
   - Taakdetails (naam, deadline, prioriteit)
   - Wie de wijziging heeft aangebracht
   - Tijdstip van wijziging
5. Systeem verstuurt notificatie via geactiveerde kanalen (in-app, email, push)
6. Systeem markeert notificatie als "ongelezen" voor werknemer
7. Systeem logt notificatie met timestamp
8. Werknemer ontvangt notificatie
9. Werknemer opent applicatie en ziet notificatie in notificatiepaneel
10. Werknemer klikt op notificatie
11. Systeem navigeert naar relevante taak/planning
12. Systeem markeert notificatie als "gelezen"

**Scenario B: Afwezigheidsmelding voor manager**
1. Systeem detecteert afwezigheidsmelding (ziekte of goedgekeurd verlof)
2. Systeem identificeert manager van de afwezige werknemer
3. Systeem voert UC23 uit (taken auto-dealloceren)
4. Systeem creëert notificatiebericht voor manager met:
   - Type afwezigheid (ziekte, verlof)
   - Werknemer naam
   - Startdatum en einddatum (indien bekend)
   - Lijst van gedealloceerde taken
   - Urgentie indicator (indien taken met hoge prioriteit betrokken zijn)
5. Systeem verstuurt notificatie via geactiveerde kanalen
6. Systeem markeert notificatie als "urgent" indien taken met deadline <3 dagen betrokken zijn
7. Systeem logt notificatie
8. Manager ontvangt notificatie
9. Manager opent applicatie
10. Manager klikt op notificatie
11. Systeem navigeert naar planningsbord met gedealloceerde taken gemarkeerd
12. Manager kan direct herplanning starten (UC04, UC12)

**Alternatieve verlopen:**
- 3a. Werknemer heeft notificaties uitgeschakeld:
  - Systeem slaat notificatie op in notificatiepaneel
  - Systeem verstuurt geen externe notificatie
  - Werknemer ziet notificatie bij volgende login
- 8a. Meerdere managers zijn verantwoordelijk:
  - Systeem identificeert alle relevante managers
  - Systeem verstuurt notificatie naar alle managers
- 5a. Email delivery faalt:
  - Systeem probeert opnieuw (max 3 pogingen)
  - Systeem logt error
  - In-app notificatie blijft beschikbaar
- 4a. Massale planningswijziging (bijv. bulk toewijzing):
  - Systeem groepeert notificaties
  - Systeem verstuurt één samengestelde notificatie
  - Notificatie bevat samenvatting van alle wijzigingen
- 6a. Urgente notificatie (deadline <24u):
  - Systeem markeert notificatie als "urgent" met visuele indicator
  - Systeem verstuurt push notificatie ongeacht voorkeuren
- Scenario C: Notificatie bij voltooide taak:
  - Werknemer markeert taak als voltooid (UC18)
  - Systeem notificeert manager/supervisor
  - Notificatie bevat taakdetails en voltooiingsdatum

**Domeinspecifieke regels:**

**DR_NOTIFICATION_01**: Notificaties worden binnen 30 seconden na trigger event verstuurd.

**DR_NOTIFICATION_02**: Urgente notificaties (afwezigheid, deadline <24u) worden altijd verstuurd, ongeacht gebruikersvoorkeuren.

**DR_NOTIFICATION_03**: Notificaties blijven 90 dagen bewaard in het systeem.

**DR_NOTIFICATION_04**: Gebruikers kunnen notificatievoorkeuren instellen per type event (taak, afwezigheid, deadlines).

**DR_NOTIFICATION_05**: Bij afwezigheid wordt enkel de directe manager genotificeerd, niet het volledige team.

**DR_NOTIFICATION_06**: Gegroepeerde notificaties worden verstuurd bij >5 individuele events binnen 1 uur.

**Op te klaren punten:**
- Moeten werknemers real-time push notificaties ontvangen of batch (einde dag)?
- Kunnen gebruikers notificatiekanalen per event type configureren?
- Moet er een escalatiemechanisme zijn indien manager niet reageert op urgente afwezigheid?
- Kunnen gebruikers notificaties snoozen/uitstellen?
- Moet er een dashboard zijn met notificatiestatistieken?
- Worden teamleden ook genotificeerd bij collega-afwezigheid?

---

## 4. Niet-Functionele Requirements (NFR's)

### NFR 1: Gebruiksvriendelijkheid - Leercurve

**Categorie NFR:** Usability - Learnability (ISO 25010)

**Indicator:** Tijd die een nieuwe gebruiker nodig heeft om basistaken uit te voeren zonder hulp

**Meetvoorschrift:**
- Selecteer 10 representatieve gebruikers (3 managers, 3 supervisors, 4 werknemers) zonder voorafgaande kennis van het systeem
- Geef korte introductiepresentatie van 15 minuten over hoofdfunctionaliteiten
- Laat gebruikers 5 typische taken uitvoeren zonder hulp:
  1. Inloggen en eigen dashboard bekijken
  2. Eigen planning raadplegen (werknemer/supervisor)
  3. Taak markeren als voltooid (werknemer)
  4. Afwezigheid melden (werknemer)
  5. Taak toewijzen aan werknemer (manager/supervisor)
- Meet de tijd vanaf start opdracht tot succesvolle afronding
- Registreer aantal fouten/misstappen per taak
- Bereken gemiddelde voltooiingstijd en foutpercentage

**Norm:** 
- Minimaal 80% van de nieuwe gebruikers moet alle 5 basistaken succesvol uitvoeren binnen 30 minuten na de introductiepresentatie
- Maximaal 2 fouten per taak gemiddeld
- Succespercentage (taak correct afgerond) moet >90% zijn

---

### NFR 2: Performance - Responstijd

**Categorie NFR:** Performance Efficiency - Time Behaviour (ISO 25010)

**Indicator:** Responstijd van het systeem bij gebruikersinteracties

**Meetvoorschrift:**
- Meet de responstijd voor kritieke gebruikersacties gedurende testperiode van 5 werkdagen
- Test onder realistische load: 100 gelijktijdige gebruikers
- Kritieke acties om te meten:
  1. Laden van planningsbord met 50 werknemers en 200 taken
  2. Toewijzen van taak aan werknemer (drag-and-drop)
  3. Opslaan van nieuwe afwezigheid
  4. Laden van dashboard met KPI's en grafieken
  5. Zoeken/filteren van taken (resultaatset van 100 taken)
- Meet tijd tussen gebruikersactie en volledige weergave resultaat
- Registreer 95e percentiel responstijd voor elke actie
- Test op verschillende tijdstippen (piekuren vs. rustige uren)

**Norm:**
- 95% van alle acties moet responstijd hebben van <2 seconden
- Planningsbord laden: <3 seconden
- Dashboard laden met grafieken: <4 seconden
- Drag-and-drop taaktoewijzing: <1 seconde (visuele feedback onmiddellijk, opslaan asynchroon)
- Zoeken/filteren: <1,5 seconde
- Geen enkele actie mag >10 seconden duren

---

### NFR 3: Betrouwbaarheid - Databehoud

**Categorie NFR:** Reliability - Fault Tolerance (ISO 25010)

**Indicator:** Percentage gegevensverlies bij systeemfalen of onverwachte gebeurtenissen

**Meetvoorschrift:**
- Simuleer verschillende failure scenarios gedurende testperiode:
  1. Onverwacht afsluiten van browser tijdens taaktoewijzing (10x)
  2. Netwerk-onderbreking tijdens opslaan van planning (10x)
  3. Gelijktijdige wijziging van dezelfde taak door 2 managers (conflict test, 10x)
  4. Server restart tijdens actieve gebruikerssessies (5x)
  5. Database verbinding verlies tijdens transactie (10x)
- Voor elk scenario:
  - Voer actie uit tot 50% voortgang
  - Introduceer failure
  - Herstel systeem
  - Controleer of gegevens correct opgeslagen/hersteld zijn
- Bereken percentage scenarios waarbij:
  - Geen gegevensverlies optrad (correct opgeslagen of volledig teruggezet)
  - Gedeeltelijk gegevensverlies (incomplete data)
  - Volledig gegevensverlies
- Test ook auto-save functionaliteit: wijziging moet binnen X seconden bewaard worden

**Norm:**
- 99% van transacties moet correct afgehandeld worden (geen gegevensverlies of volledige rollback)
- Bij falen tijdens transactie: systeem moet automatisch rollback uitvoeren (atomicity)
- Auto-save functionaliteit moet wijzigingen binnen 5 seconden bewaren
- Gelijktijdige wijzigingen: systeem moet conflict detecteren en gebruiker waarschuwen (laatste schrijver wint, met notificatie)
- Na systeemfalen moet gebruiker kunnen doorgaan zonder gegevensverlies binnen 2 minuten na herstel

---

### NFR 4: Bruikbaarheid - Efficiëntie van gebruik

**Categorie NFR:** Usability - Operability (ISO 25010)

**Indicator:** Aantal klikken/acties nodig om veelgebruikte taken uit te voeren

**Meetvoorschrift:**
- Identificeer 8 meest uitgevoerde taken op basis van use cases:
  1. Taak toewijzen aan werknemer (vanaf centraal bord)
  2. Eigen planning raadplegen als werknemer
  3. Taak markeren als voltooid
  4. Afwezigheid (ziekte) melden
  5. Verlof aanvragen
  6. Dashboard met KPI's bekijken
  7. Notificaties bekijken en openen
  8. Werknemer toevoegen aan team
- Voor elke taak:
  - Documenteer optimale workflow (kortste pad)
  - Tel aantal klikken/interacties vanaf homepage tot succesvolle afronding
  - Tel aantal schermovergangen
  - Meet tijd tot voltooiing door ervaren gebruiker
- Voer uit met 5 ervaren gebruikers per rol (manager, supervisor, werknemer)
- Bereken gemiddelde voor elke taak

**Norm:**
- Geen enkele veelgebruikte taak mag meer dan 5 klikken vereisen
- Specifieke normen per taak:
  - Taak toewijzen (drag-and-drop): 2 acties (selecteer + drop)
  - Eigen planning bekijken: 1 klik
  - Taak markeren als voltooid: 2 klikken
  - Ziekte melden: 3 klikken (navigeer > selecteer type > bevestig)
  - Dashboard bekijken: 1 klik
  - Notificatie openen: 1 klik
- Gemiddelde voltooiingstijd voor ervaren gebruiker per taak: <15 seconden (exclusief denktijd)
- Minimaal 90% van functionaliteiten toegankelijk binnen 2 klikken vanaf homepage

---

### NFR 5: Onderhoudbaarheid - Aanpasbaarheid

**Categorie NFR:** Maintainability - Modifiability (ISO 25010)

**Indicator:** Tijd en effort nodig om wijzigingen door te voeren in het systeem

**Meetvoorschrift:**
- Definieer 5 representatieve wijzigingsscenario's van verschillende complexiteit:
  1. **Klein**: Toevoegen van nieuw veld aan taakformulier (bijv. "Locatie notitie")
  2. **Klein**: Wijzigen van kleurcode voor capaciteitsvisualisatie
  3. **Gemiddeld**: Toevoegen van nieuwe notificatietype (bijv. "taak bijna verlopen")
  4. **Gemiddeld**: Aanpassen van autorisatielogica (nieuwe rol toevoegen)
  5. **Groot**: Toevoegen van nieuwe KPI in dashboard (inclusief backend berekening en visualisatie)
- Voor elk scenario:
  - Laat ontwikkelaar wijziging doorvoeren (zonder voorkennis van specifieke code)
  - Meet tijd vanaf start analyse tot deployment in test-omgeving
  - Tel aantal bestanden dat gewijzigd moet worden
  - Tel aantal regressiefouten na wijziging (via geautomatiseerde tests)
- Bereken gemiddelde effort per complexiteitscategorie
- Herhaal met 3 verschillende ontwikkelaars voor betrouwbaarheid

**Norm:**
- Kleine wijzigingen: <4 uur ontwikkeltijd, max 3 bestanden aangepast
- Gemiddelde wijzigingen: <2 werkdagen, max 8 bestanden aangepast
- Grote wijzigingen: <5 werkdagen, max 15 bestanden aangepast
- Code coverage van geautomatiseerde tests: >75%
- Regressiefouten na wijziging: 0 (alle tests moeten slagen)
- Modulaire architectuur: elke component (Task, Planning, Notification, Master Data, Absence) moet onafhankelijk aanpasbaar zijn
- Documentatie: elke component moet gedocumenteerde interfaces hebben (API specs)
- Gemiddelde tijd voor nieuwe ontwikkelaar om productief te worden: <3 werkdagen

---

## 5. Aanvullende Opmerkingen

### 5.1 Scope beperkingen POC
Dit lastenboek beschrijft de volledige scope van het systeem. Voor de Proof of Concept (POC) worden prioriteiten gesteld op basis van:
- Kernfunctionaliteiten die de grootste business impact hebben
- Components die de waardepropositie demonstreren
- Use cases die essentieel zijn voor minimale viable product (MVP)

### 5.2 Agile benadering
Conform agile principes zullen:
- Use cases incrementeel verfijnd worden tijdens ontwikkeling
- NFR's continu gemonitord worden met testautomatisering
- Stakeholder feedback verwerkt worden in iteraties
- Requirements bijgesteld worden op basis van POC learnings

### 5.3 Technische architectuur
De technische architectuur is niet gespecificeerd in dit lastenboek en blijft de verantwoordelijkheid van het ontwikkelteam, met de eis dat NFR's behaald worden.

### 5.4 Integraties
Toekomstige integraties met externe systemen (HR-systeem, ERP, externe kalenders) zijn out-of-scope voor POC maar moeten architecturaal voorzien worden (NFR5 - Modifiability).

---

## 6. Goedkeuring

| Rol | Naam | Handtekening | Datum |
|-----|------|--------------|-------|
| Product Owner | | | |
| Lead Consultant | | | |
| Technical Lead | | | |

---

**Document versie:** 1.0  
**Laatste wijziging:** [datum]  
**Status:** Draft - ter review
