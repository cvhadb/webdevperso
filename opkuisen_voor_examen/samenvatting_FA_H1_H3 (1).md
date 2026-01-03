# 📑 Samenvatting Use Case Modeling (Functionele Analyse)

## I. De Use Case (UC) Definitie

| Element | Formaat en Doel | Kernregel |
| :--- | :--- | :--- |
| **Titel** | `UCxx : [Actie die gedaan moet worden]` | Moet een duidelijk **doel** beschrijven (e.g., "UC01: Gebruiker inloggen"). |
| **Rol** | `[Rolnaam]` | Beschrijft de algemene rol van de actor (e.g., *Gebruiker*, *Beheerder*); **nooit een jobtitel.** |
| **Stakeholder** | `[Belanghebbende_rolnaam]` | Wie heeft **onrechtstreeks** belang bij de uitvoering van de UC (e.g., *Klant* heeft belang bij *Beheerder* die gegevens verwerkt). |
| **Pre-condities** | Condities die **vervuld moeten zijn** voordat de UC kan starten. | Zonder deze voorwaarden kan de UC **niet** van start gaan (e.g., "De gebruiker moet reeds een account hebben"). |
| **Post-condities**| De verplichte status nadat de UC succesvol is afgerond. | Beschrijf het **eindresultaat** (e.g., "De klantgegevens zijn opgeslagen in de DB"). |
| **Domeinregels (DR)**| Specificeert het strikte kader qua verwachtingen of beperkingen. | Specificeert een limiet of verwachting bij een bepaalde stap (e.g., "Maximaal 10 aanvaarde karakters voor invoer"). |
| **Op te klaren punten** | Zaken die onduidelijk zijn en besproken moeten worden met de opdrachtgever. | Zorgt ervoor dat de specificatie volledig en niet-ambigu is. |

## II. Verloop van de Use Case

### A. Normaal Verloop (NV)

Het **Normaal Verloop** beschrijft het succesvolle, meest gebruikelijke pad (de "happy flow").

1.  Start met het doel van de rol (`[Rolnaam] wil [doel uit titel UC]`).
2.  Beschrijf de interactie beurtelings (`[Rolnaam]` handelt, Systeem reageert).
3.  Spreek steeds vanuit de rolnaam (de actor).
4.  Vermeld steeds wie het onderwerp is (e.g., "Systeem vraagt gebruiker iets").
5.  Vermijd UI-details (zoals "knop," "e-mail," of "scherm").
6.  **Hergebruik:** Gemeenschappelijke acties kunnen als $\ll\text{include}\gg$ UCs opgenomen worden.
7.  **Complexiteit:** Houd het overzichtelijk, **maximaal 10 stappen**.
8.  **Verwijzing naar UC's:** Indien een andere UC nodig is als stap, wordt deze als stap **onderlijnd** aangegeven (e.g., "Gebruiker plaatst bestelling").

### B. Alternatief Verloop (AV)

Het **Alternatief Verloop** beschrijft paden die afwijken van het NV (e.g., fouten of niet-standaard paden).

1.  **Start:** Begin met het nummer van de stap in het NV waar de afwijking zich voordoet. Gebruik een letter (`A`, `B`, `C`, ...) om unieke AV's te onderscheiden (e.g., `3A: Fout wachtwoord ingevoerd`).
2.  **Stappen:** Gebruik genummerde stappen (`1, 2, 3, ...`) voor het verloop van de uitzondering.
3.  **Terugkeer:** Stop de AV steeds met "Ga naar stap X van NV" om aan te geven waar in het Normaal Verloop er opnieuw moet worden gestart (e.g., "Ga naar stap 1 van NV: Toon login scherm").

---

## III. Niet-Functionele Vereisten (NFR)

NFR's specificeren **hoe** goed het systeem de functies moet uitvoeren.

| ISO 25010 Familie | Meest Voorkomende NFR | Voorbeeld van de Norm (Meetvoorschrift) |
| :--- | :--- | :--- |
| **1. Functional Suitability** | **Functionele Volledigheid** | Systeem moet **alle** vereiste belastingtarieven van het huidige boekjaar ondersteunen. |
| **2. Performance Efficiency** | **Time Behaviour (Responstijd)** | Het systeem moet **90%** van de pagina's binnen de **1 seconde** tonen aan de gebruiker. |
| **3. Compatibility** | **Co-existence (Samenwerken)** | De applicatie moet correct naast de huidige virusscanner draaien zonder performance-impact > 5%. |
| **4. Usability** | **Learnability (Leerbaarheid)** | Een nieuwe gebruiker moet **80%** van de kernfuncties foutloos kunnen uitvoeren na een training van 1 uur. |
| **5. Reliability** | **Availability (Beschikbaarheid)** | Het systeem moet **99,9%** van de tijd beschikbaar zijn buiten gepland onderhoud. |
| **6. Security** | **Confidentiality (Vertrouwelijkheid)** | Alle gegevens van klanten (incl. wachtwoorden) moeten **end-to-end** versleuteld worden. |
| **7. Maintainability** | **Testability (Testbaarheid)** | Nieuwe functionaliteiten moeten in minder dan **4 uur** door een geautomatiseerde testsuite gevalideerd kunnen worden. |
| **8. Portability** | **Installability (Installeerbaarheid)** | De mobiele app moet in minder dan **30 seconden** geïnstalleerd kunnen worden via de App Store. |

---

## IV. Use Case Relaties

| Relatie | Kenmerk | Doel en Context | Voorbeelden |
| :--- | :--- | :--- | :--- |
| **$\ll\text{include}\gg$** | **Onvoorwaardelijk gebonden** | Factoriseert gemeenschappelijke, **verplichte** stappen die anders in meerdere UCs zouden moeten staan. | "Log In," "Verify Credentials," "Record Audit Log." |
| **$\ll\text{extend}\gg$** | **Voorwaardelijk gebonden** | Beschrijft optioneel gedrag of stappen die alleen onder **specifieke voorwaarden** (exception points) voorkomen. | "Flag Aanvraag voor Handmatige Review," "Pas Promotiecode Toe," "Toon Foutmelding." |

---