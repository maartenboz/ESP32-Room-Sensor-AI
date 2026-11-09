# Original project prompt

The following is the original Dutch user brief that started the KiCad experiment. Formatting has been preserved as Markdown; transport metadata and later approval/publication messages are not part of this prompt.

---

# Opdracht: Ontwerp een complete ESP32 Room Sensor PCB met KiCad

## 1. Doel van de opdracht

Ik wil dat je zelfstandig een volledig werkende PCB ontwerpt in KiCad.

Het ontwerp wordt een **ESP32 Room Sensor & Control Board**: een compacte PCB waarmee ik de temperatuur en relatieve luchtvochtigheid van mijn kamer kan meten. Daarnaast bevat het bord verschillende programmeerbare gebruikersinterfaces.

Dit project dient tegelijkertijd als uitgebreide praktijktest van jouw mogelijkheden om zelfstandig met KiCad te werken via mijn lokale MCP-server.

**Belangrijk:**
- Gebruik actief de MCP-server `KiCad-agentic`.
- Maak gebruik van alle relevante beschikbare KiCad-skills.
- Gebruik de MCP-tools daadwerkelijk voor het lezen, ontwerpen, aanpassen en controleren van het project.
- Werk zoveel mogelijk zelfstandig.
- Maak zelf verantwoorde engineeringkeuzes op basis van datasheets, application notes en best practices.
- Beperk je niet tot het tekenen van een schema: het eindresultaat moet een volledig ontworpen, gerouteerde en gecontroleerde PCB zijn.
- Gebruik geen fictieve onderdelen, footprints of onbevestigde elektrische aansluitingen.

Ik voer deze opdracht eerst uit in **Plan Mode**. Onderzoek daarom eerst het project, de technische mogelijkheden en de benodigde ontwerpstappen. Maak een volledig uitvoeringsplan voordat je wijzigingen aanbrengt.

Na goedkeuring van het plan moet je het ontwerp zelfstandig kunnen uitvoeren.

## 2. Bestaand KiCad-project

Ik heb een bestaand KiCad-project met de naam:

`KiCad_MCP_Test`

Dit project is momenteel geopend in KiCad.

In het project is eerder een kleine test uitgevoerd, waarbij twee componenten zijn geplaatst. Deze testcomponenten hoeven niet behouden te blijven.

### Instructies

1. Controleer of de MCP-server `KiCad-agentic` beschikbaar is en correct communiceert met KiCad.
2. Controleer welke KiCad MCP-tools en skills beschikbaar zijn.
3. Inspecteer het bestaande project.
4. Onderzoek welke schematic-, PCB- en projectbestanden aanwezig zijn.
5. Controleer of het schema en de PCB via MCP kunnen worden gelezen en gewijzigd.
6. Bepaal hoe je de oude testcomponenten en eventuele overige testobjecten veilig kunt verwijderen.
7. Gebruik het bestaande project als basis voor het nieuwe ontwerp.

Maak geen nieuw project als dat niet noodzakelijk is.

Het bestaande project mag tijdens de uitvoeringsfase volledig opnieuw worden ingericht.

**Tijdens Plan Mode mag je het project uitsluitend inspecteren. Verwijder of wijzig nog niets.**

## 3. Functionele eisen

Het ontwerp moet minimaal de volgende functies bevatten.

### 3.1 ESP32-microcontroller

Gebruik een geschikte ESP32-module als centrale microcontroller.

Je mag zelf bepalen welke ESP32-variant het meest geschikt is.

Selectiecriteria:
- Geïntegreerde WiFi en bij voorkeur Bluetooth.
- Voldoende GPIO-pinnen.
- Minimaal twee geschikte ADC-ingangen.
- Ondersteuning voor programmeren en communicatie via USB-C.
- Goede beschikbaarheid en documentatie.
- Geschikt voor een compact PCB-ontwerp.
- Bij voorkeur een ESP32-module met geïntegreerde PCB-antenne.

Onderzoek welke ESP32 het beste past bij deze toepassing.

Gebruik bij voorkeur een module met geïntegreerde flash, RF-componenten en antenne, zodat het ontwerp niet onnodig complex wordt.

Houd rekening met GPIO-beperkingen, strapping-pinnen, bootconfiguratie en ADC-functionaliteit.

### 3.2 Temperatuur- en luchtvochtigheidssensor

Het bord moet de volgende omgevingswaarden kunnen meten:

- Temperatuur in °C.
- Relatieve luchtvochtigheid in %RH.

Selecteer hiervoor een geschikte digitale SMD-sensor.

Een mogelijke kandidaat is de Sensirion SHT40, maar je mag een beter alternatief selecteren.

Eisen:
- Communicatie via I²C.
- Geschikt voor 3,3 V.
- Goede nauwkeurigheid.
- Compact SMD-component.
- Goede softwareondersteuning voor ESP32.

Besteed extra aandacht aan de PCB-layout rond deze sensor.

Plaats de sensor zodanig dat:
- Warmte van de ESP32 en spanningsregelaar de meting zo weinig mogelijk beïnvloedt.
- De sensor goed wordt blootgesteld aan de omgevingslucht.
- Warmtegeleiding via koper zoveel mogelijk wordt beperkt indien nodig.
- De sensor niet direct naast warmteproducerende componenten staat.

Volg hiervoor de aanbevelingen uit de datasheet en eventuele application notes.

### 3.3 Twee programmeerbare gebruikersknoppen

Plaats twee SMD-drukknoppen:

- USER_BTN1
- USER_BTN2

Beide knoppen worden aangesloten op afzonderlijke GPIO-pinnen van de ESP32.

Eisen:
- Momentary pushbutton.
- Logische active-low configuratie.
- Correcte pull-upweerstanden indien nodig.
- Geschikte GPIO-pinnen zonder ongewenste bootproblemen.
- Eenvoudig met de hand bedienbaar.
- Goed bereikbaar op de PCB.

De knoppen moeten later vrij programmeerbaar zijn.

### 3.4 Twee 10 kΩ-potentiometers

Plaats twee SMD-potentiometers van 10 kΩ:

- POT1
- POT2

Elke potentiometer moet worden aangesloten op een afzonderlijke ADC-ingang van de ESP32.

Aansluiting:
- Eén uiteinde aan 3,3 V.
- Eén uiteinde aan GND.
- Wiper naar de ADC-ingang.

Eisen:
- Beide potentiometers onafhankelijk uitleesbaar.
- Bij voorkeur geschikte ADC1-pinnen, zodat WiFi-functionaliteit geen problemen veroorzaakt.
- Zorg voor een stabiele ADC-meting.
- Onderzoek of een RC-filter op de ADC-ingangen zinvol is.
- Bescherm de ingangen waar nodig.

Kies bij voorkeur SMD-potentiometers die eenvoudig met de hand verstelbaar zijn.

Wanneer geschikte handmatig verstelbare SMD-modellen niet beschikbaar zijn, mogen SMD-trimpotentiometers worden gebruikt.

Onderbouw je keuze.

### 3.5 Twee programmeerbare gebruikers-LEDs

Plaats twee SMD-LEDs:

- USER_LED1
- USER_LED2

Elke LED wordt aangesloten op een afzonderlijke GPIO-pin.

Eisen:
- Onafhankelijk programmeerbaar.
- Geschikte voorschakelweerstanden.
- Geschikte LED-stroom.
- Geen ongewenste beïnvloeding van strapping-pinnen.
- Duidelijk zichtbaar.

Je mag zelf geschikte LED-kleuren kiezen.

### 3.6 Reset- en bootknoppen

Plaats twee extra SMD-drukknoppen:

- RESET
- BOOT

De RESET-knop moet de ESP32 correct resetten.

De BOOT-knop moet handmatig toegang geven tot de juiste firmware-downloadmodus.

Gebruik de aanbevolen schakelingen uit de officiële Espressif-documentatie.

Controleer:
- EN/reset-circuit.
- Pull-up- en pull-downweerstanden.
- Eventuele RC-vertragingen.
- Bootstrapping.
- Effect op andere aangesloten componenten.

### 3.7 USB-C-aansluiting

Plaats één USB-C-connector.

Deze moet gebruikt kunnen worden voor:

1. Voeding van het bord.
2. Programmeren van de ESP32.
3. Seriële communicatie tussen ESP32 en computer.

USB-C moet functioneren als USB 2.0-device.

Onderzoek welke oplossing het meest geschikt is:

**Optie A: Native USB**

Gebruik de geïntegreerde USB-functionaliteit van een geschikte ESP32.

**Optie B: USB-naar-UART**

Gebruik een afzonderlijke USB-naar-UART-bridge, bijvoorbeeld een geschikte CP210x- of FTDI-chip.

Mijn voorkeur gaat uit naar een oplossing die betrouwbaar werkt met gangbare ESP32-ontwikkelomgevingen.

#### Automatisch programmeren

Ik wil bij voorkeur firmware kunnen uploaden zonder handmatig BOOT en RESET te bedienen.

Wanneer je een USB-UART-bridge gebruikt, implementeer dan indien mogelijk automatische download-/resetbesturing via DTR/RTS volgens de aanbevolen Espressif-schakeling.

De BOOT- en RESET-knoppen moeten wel aanwezig blijven.

#### USB-C-aandachtspunten

Houd rekening met:
- Correcte CC1- en CC2-pull-downweerstanden.
- USB D+ en D−.
- ESD-bescherming.
- VBUS en GND.
- Eventuele beveiliging tegen overstroom.
- Correcte aansluiting van de connectorbehuizing.
- Geschikte ontkoppelcondensatoren.
- USB-signaalintegriteit.
- Betrouwbare footprint en mechanische bevestiging.

### 3.8 USB RX- en TX-activiteits-LEDs

Ik wil twee extra SMD-LEDs:

- USB_RX_LED
- USB_TX_LED

Deze moeten activiteit van de communicatieverbinding aangeven.

Onderzoek hoe dit het betrouwbaarst kan worden geïmplementeerd.

Bij een USB-UART-bridge gaat mijn voorkeur uit naar echte hardwarematige TX/RX-activiteitsindicatie, bijvoorbeeld met daarvoor bedoelde uitgangspinnen.

Bij gebruik van native USB moet je expliciet onderzoeken hoe RX/TX-activiteit kan worden weergegeven, bijvoorbeeld via firmware.

**Belangrijk:** Ga er niet automatisch vanuit dat native USB afzonderlijke RX- en TX-signalen heeft waarop direct LEDs kunnen worden aangesloten.

Kies een technisch correcte implementatie en leg de consequenties uit.

### 3.9 Power-indicatie

Plaats één SMD-LED:

- PWR_LED

Deze moet aangeven dat de interne 3,3V-voeding aanwezig is.

Gebruik een passende voorschakelweerstand en beperk het stroomverbruik.

## 4. Voedingsontwerp

Ontwerp zelfstandig een geschikte voeding voor het bord.

### Ingang

USB-C 5 V.

### Uitgang

Een stabiele 3,3V-voedingsrail voor de ESP32, sensor en overige componenten.

### Eisen

- Geschikt voor de piekstromen van de ESP32 tijdens WiFi-activiteit.
- Laag genoeg spanningsverlies.
- Voldoende uitgangsstroom.
- Correcte condensatoren volgens de datasheet.
- Goede ontkoppeling bij alle IC's.
- Geschikte bescherming van USB-voeding.
- Thermisch verantwoord ontwerp.

Je mag zelf kiezen tussen een LDO en een schakelende spanningsregelaar.

Onderbouw je keuze op basis van:
- Maximale belasting.
- Verwacht stroomverbruik.
- Rendement.
- Warmteontwikkeling.
- Complexiteit.
- Beschikbare PCB-ruimte.

Gebruik een betrouwbare, gangbare SMD-spanningsregelaar.

## 5. Componentselectie en libraries

Je bent verantwoordelijk voor de volledige componentselectie.

Gebruik bij voorkeur componenten van bekende fabrikanten.

Voor elk belangrijk component moet je:

1. Een geschikt onderdeelnummer selecteren.
2. De officiële datasheet raadplegen.
3. Controleren of het onderdeel aan de eisen voldoet.
4. Een correct KiCad-symbool gebruiken.
5. Een correcte KiCad-footprint gebruiken.
6. Controleren of symboolpinnen en footprintpads correct overeenkomen.

### Ontbrekende componenten

Wanneer een component niet in de standaard KiCad-libraries voorkomt:

- Zoek eerst naar een geschikte officiële library.
- Onderzoek of een betrouwbare externe library beschikbaar is.
- Download en installeer deze indien nodig tijdens de uitvoeringsfase.
- Maak anders zelf een correct symbool en footprint op basis van de datasheet.

Gebruik bij voorkeur projectlokale libraries, zodat het project overdraagbaar blijft.

Download geen bestanden van onbetrouwbare bronnen.

**Alle elektronische componenten moeten SMD zijn.**

Gebruik geen THT-componenten.

De mechanische montagegaten zijn uiteraard uitgezonderd.

Let erop dat ook de USB-C-connector daadwerkelijk geschikt is voor volledige SMD-montage.

## 6. Schematic design

Maak een volledig, overzichtelijk elektrisch schema.

Deel het schema logisch in.

Bijvoorbeeld:

1. USB-C & USB Interface
2. Power Supply
3. ESP32 & Boot Configuration
4. Temperature & Humidity Sensor
5. User Buttons
6. Potentiometers & ADC
7. Status LEDs

Je mag hiervoor meerdere schematic sheets gebruiken als dat overzichtelijker is.

### Schema-eisen

- Duidelijke netnamen.
- Logische signaalrichting.
- Correcte componentwaarden.
- Overzichtelijke plaatsing.
- Consistente naamgeving.
- Correcte power symbols.
- Duidelijke annotaties.
- Relevante ontwerpnotities.

Maak een GPIO-toewijzingstabel waarin staat welke ESP32-pin welke functie krijgt.

Controleer dat alle toegewezen pinnen daadwerkelijk geschikt zijn voor hun functie.

Voer een volledige ERC-controle uit.

Het uiteindelijke schema moet vrij zijn van onverklaarde ERC-fouten.

## 7. PCB-specificaties

### 7.1 Afmetingen en vorm

De PCB moet:
- Rechthoekig zijn.
- Maximaal 200 × 100 mm groot zijn.
- Afgeronde hoeken hebben.
- Vier montagegaten hebben.

Ik geef de voorkeur aan een aanzienlijk kleiner bord als dat praktisch mogelijk is.

Kies zelf logische afmetingen op basis van de componenten en benodigde ruimte.

Gebruik een afrondingsradius van ongeveer 3–5 mm, tenzij een andere waarde beter uitkomt.

### 7.2 Montagegaten

Plaats in alle vier de hoeken een montagegat.

Specificaties:
- Geschikt voor M3-montage.
- Nominale gatdiameter 3 mm; kies indien noodzakelijk een passende speling en onderbouw dit.
- Non-plated through holes (NPTH).
- Geen onnodig koper rond de gaten.
- Voldoende mechanische afstand tot de PCB-rand.
- Symmetrische positionering.

### 7.3 Layer stackup

Kies zelf het geschikte aantal koperlagen.

Bij voorkeur:
- 2 lagen als dit zonder kwaliteitsverlies mogelijk is.
- 4 lagen als dit een duidelijk betere oplossing oplevert.

Maak een logische stackup met geschikte GND-referentievlakken en voedingsdistributie.

Onderbouw de keuze.

#### Copper layer numbering

Ik wil dat iedere koperlaag een eigen laagnummer krijgt.

Plaats hiervoor een kleine koperen tekstmarkering op elke koperlaag:

- L1 op de bovenste koperlaag.
- L2 op de tweede koperlaag.
- L3 op de derde koperlaag, indien aanwezig.
- L4 op de onderste koperlaag, indien aanwezig.

Gebruik de daadwerkelijke KiCad-koperlagen.

Zorg dat de markeringen correct worden geïmplementeerd en geen ongewenste verbindingen, shorts of DRC-fouten veroorzaken.

### 7.4 PCB-naam

Plaats de volgende tekst duidelijk op de silkscreen:

**ESP32 ROOM SENSOR**

Voeg eventueel een kleinere versieaanduiding toe:

**REV 1.0**

Maak de tekst goed leesbaar en plaats deze op een logische plek.

## 8. Component placement

De componenten moeten logisch, overzichtelijk en professioneel worden geplaatst.

Ik wil niet dat je de componenten willekeurig verdeelt.

Houd rekening met de volgende richtlijnen.

### USB-C
- Plaats aan een PCB-rand.
- Zorg dat een USB-C-kabel eenvoudig kan worden aangesloten.
- Houd rekening met de mechanische afmetingen van de connector.

### ESP32
- Plaats logisch ten opzichte van USB, voeding en overige componenten.
- Respecteer de antenne-keepout van de fabrikant.
- Plaats geen koper of componenten in verboden antennegebieden.
- Houd de antenne bij voorkeur aan een buitenrand van de PCB.

### Temperatuur-/luchtvochtigheidssensor
- Plaats op een geschikte plek voor nauwkeurige omgevingsmetingen.
- Bij voorkeur aan een rand.
- Niet direct naast de ESP32, voeding of andere warmtebronnen.

### Gebruikersknoppen
- Plaats naast elkaar.
- Houd voldoende afstand voor bediening.
- Zorg voor duidelijke silkscreen-labels.

### Potentiometers
- Plaats logisch naast elkaar.
- Zorg dat ze bereikbaar en verstelbaar blijven.
- Vermijd mechanische conflicten met andere componenten.

### LEDs
- Plaats USER_LED1 en USER_LED2 op een logische plek.
- Plaats USB_RX_LED en USB_TX_LED bij elkaar, bij voorkeur nabij de USB-interface.
- Plaats PWR_LED op een duidelijk zichtbare plek.

### BOOT en RESET
- Plaats naast elkaar of op een andere logische locatie.
- Maak duidelijk welke knop welke functie heeft.
- Voorkom verwarring met de programmeerbare gebruikersknoppen.

### Passieve componenten
- Plaats ontkoppelcondensatoren zo dicht mogelijk bij de relevante voedingspinnen.
- Houd kritische stroomlussen kort.
- Plaats pull-upweerstanden en filters logisch bij hun schakeling.

## 9. PCB-routing

Route het volledige bord.

### Vereisten

- Alle noodzakelijke elektrische verbindingen moeten gerouteerd zijn.
- Geen resterende unrouted nets.
- Geen onbedoelde kortsluitingen.
- Correcte spoorbreedtes voor de betreffende stromen.
- Geschikte via-afmetingen.
- Correcte clearance-regels.
- Logische GND-polygons.
- Goede voedingsdistributie.
- Geen onnodig lange signaalsporen.
- Vermijd onnodige via's.
- Zorg voor een goede retourstroomroute.

### USB

Houd rekening met USB 2.0-routingrichtlijnen.

Gebruik waar van toepassing:
- Korte D+/D−-verbindingen.
- Geschikte differentiële routing.
- Een ononderbroken referentievlak.
- Correcte plaatsing van ESD-componenten.

### Sensor

Voorkom dat warmteproducerende componenten en grote koperoppervlakken de nauwkeurigheid van de temperatuursensor onnodig beïnvloeden.

### ESP32

Volg de officiële Espressif PCB Design Guidelines voor:
- Voeding.
- Ontkoppeling.
- Grounding.
- RF-antenne.
- GPIO-routing.

## 10. Silkscreen en afwerking

Maak het bord overzichtelijk en professioneel.

Plaats duidelijke silkscreen-labels voor:

- USB-C
- BOOT
- RESET
- BTN1
- BTN2
- POT1
- POT2
- LED1
- LED2
- RX
- TX
- PWR

Voeg daarnaast toe:
- PCB-naam.
- Revisienummer.
- Duidelijke componentreferenties waar praktisch.
- Pin-1-markeringen waar nodig.
- Eventueel plus/min-indicaties bij relevante aansluitingen.

Zorg dat de silkscreen niet over pads of andere ongewenste locaties loopt.

## 11. Ontwerpcontrole

Controleer het ontwerp grondig.

### Schematic

Voer ERC uit en los alle relevante fouten op.

### PCB

Voer DRC uit en los alle relevante fouten op.

Controleer onder andere:
- Clearance.
- Unconnected items.
- Track widths.
- Via sizes.
- Copper zones.
- Silkscreen.
- Board outline.
- Component overlaps.
- Afstand tussen koper en montagegaten.
- Antenne-keepout.

Controleer ook of de PCB daadwerkelijk overeenkomt met het schema.

### Mechanische controle

Controleer:
- Afmetingen.
- Afgeronde hoeken.
- Montagegaten.
- Toegankelijkheid van knoppen en potmeters.
- Toegankelijkheid van de USB-C-connector.
- Eventuele componenten die buiten de board outline uitsteken.

Gebruik indien mogelijk ook KiCad's 3D Viewer om het ontwerp te beoordelen.

## 12. Verwachte eindresultaten

Na uitvoering verwacht ik minimaal:

1. Een compleet KiCad-schema.
2. Een volledig geplaatste PCB.
3. Een volledig gerouteerde PCB.
4. Een correcte board outline.
5. Volledig ingestelde koperlagen en ground planes.
6. Alle gevraagde silkscreen-markeringen.
7. Een succesvolle ERC-controle.
8. Een succesvolle DRC-controle.
9. Een componentenlijst (BOM) met fabrikant en onderdeelnummer.
10. Een overzicht van alle ESP32 GPIO-toewijzingen.
11. Een korte technische toelichting op belangrijke ontwerpkeuzes.

Sla alles op in het bestaande KiCad-project `KiCad_MCP_Test`.

Zorg ervoor dat de bestanden opnieuw in KiCad geopend en bewerkt kunnen worden.

Maak geen onnodige tijdelijke bestanden in de projectmap.

## 13. Werkwijze en zelfstandigheid

Ik wil je zelfstandigheid testen.

Daarom gelden de volgende uitgangspunten:

- Raadpleeg zelfstandig datasheets en documentatie.
- Selecteer zelfstandig geschikte componenten.
- Kies zelfstandig footprints.
- Kies zelfstandig componentwaarden.
- Neem zelfstandig beslissingen over de stackup.
- Bepaal zelfstandig de GPIO-toewijzing.
- Maak zelfstandig de layout.
- Route zelfstandig alle verbindingen.
- Controleer zelfstandig je eigen werk.
- Los fouten zoveel mogelijk zelfstandig op.

Als je tegen een probleem aanloopt, onderzoek dan eerst zelf mogelijke oplossingen.

Wanneer een MCP-tool iets niet ondersteunt, onderzoek dan of een andere beschikbare tool, KiCad-skill of officiële KiCad-interface gebruikt kan worden.

Gebruik geen onbetrouwbare workarounds die het project kunnen beschadigen.

Doe geen aannames over succesvolle toolacties: controleer daadwerkelijk of de wijziging is uitgevoerd.

Rapporteer duidelijk welke taken via MCP zijn uitgevoerd en welke eventueel via andere middelen.

Vraag alleen om mijn input wanneer een fundamentele ontwerpkeuze niet verantwoord zelfstandig genomen kan worden.

## 14. Instructies voor Plan Mode

**Je bevindt je momenteel in Plan Mode.**

Ik wil dat je nu eerst een grondig uitvoeringsplan maakt.

Voer nog geen wijzigingen aan het KiCad-project uit. Download of installeer ook nog geen onderdelen of libraries.

Je mag wel read-only MCP-tools gebruiken om het project en de mogelijkheden van de KiCad-verbinding te onderzoeken.

### Stap 1 — Verken de omgeving

Onderzoek:
- Of `KiCad-agentic` bereikbaar is.
- Welke MCP-functionaliteit beschikbaar is.
- Welke KiCad-skills beschikbaar zijn.
- Wat de huidige projectstatus is.
- Welke projectbestanden aanwezig zijn.
- Welke KiCad-onderdelen eventueel ontbreken.
- Of schema-, PCB- en DRC/ERC-functionaliteit via de beschikbare tools kan worden uitgevoerd.

### Stap 2 — Technisch ontwerpvoorstel

Geef een concreet voorstel voor:
- De ESP32-variant.
- De temperatuur-/luchtvochtigheidssensor.
- De USB-architectuur.
- De USB-naar-UART-chip, indien nodig.
- De voedingsregelaar.
- De potentiometers.
- De knoppen.
- De LEDs.
- De ESD- en beveiligingscomponenten.
- De overige noodzakelijke passieve componenten.

Vermeld belangrijke fabrikantonderdeelnummers en motiveer de keuzes.

### Stap 3 — Elektrische architectuur

Maak een overzicht van:
- De belangrijkste functionele blokken.
- De onderlinge elektrische verbindingen.
- De voedingsstructuur.
- De GPIO-toewijzing.
- De USB-programmeerarchitectuur.
- De verwachte stroombehoefte.

### Stap 4 — PCB-ontwerpvoorstel

Geef een voorstel voor:
- PCB-afmetingen.
- Aantal koperlagen.
- Stackup.
- Globale componentplaatsing.
- Positie van de montagegaten.
- Antenne-keepout.
- Plaatsing van de temperatuursensor.
- Routingstrategie.
- Design rules.

### Stap 5 — Concreet uitvoeringsplan

Maak een stapsgewijs plan waarmee je het project vervolgens volledig kunt uitvoeren.

Verdeel dit bijvoorbeeld in:

1. Project voorbereiden.
2. Componenten en libraries voorbereiden.
3. Schematic opbouwen.
4. ERC uitvoeren.
5. PCB configureren.
6. Componenten plaatsen.
7. Copper zones en routing.
8. Silkscreen en mechanische afwerking.
9. DRC uitvoeren.
10. Eindcontrole en documentatie.

Geef per stap aan:
- Wat je gaat uitvoeren.
- Welke MCP-tools of skills je daarvoor verwacht te gebruiken.
- Wat het verwachte resultaat is.
- Hoe je controleert of de stap succesvol is.

### Stap 6 — Haalbaarheidsanalyse

Dit is nadrukkelijk ook een test van de MCP-server.

Onderzoek daarom kritisch welke onderdelen van de opdracht daadwerkelijk geautomatiseerd kunnen worden.

Maak onderscheid tussen:
- Functionaliteit die je hebt bevestigd met een werkende MCP-tool.
- Functionaliteit die waarschijnlijk mogelijk is, maar nog niet is getest.
- Functionaliteit waarvoor een aanvullende tool of alternatieve aanpak nodig is.
- Functionaliteit die mogelijk handmatig moet worden uitgevoerd.

Claim niet dat een functie beschikbaar is als je dit niet hebt kunnen verifiëren.

### Stap 7 — Definitief plan presenteren

Presenteer uiteindelijk één samenhangend en concreet uitvoeringsplan.

Benoem eventuele technische risico's, openstaande keuzes en beperkingen van de MCP-server.

Mijn doel is dat ik dit plan kan goedkeuren en je daarna met zo min mogelijk verdere instructies zelfstandig de volledige PCB kan laten ontwerpen.

**Begin nu met het onderzoeken van de KiCad-omgeving en stel vervolgens het uitvoeringsplan op. Wijzig het project nog niet.**

---

Later, after the read-only plan was approved, the user explicitly requested implementation of that plan. Repository publication and this provenance update were separate follow-up requests.
