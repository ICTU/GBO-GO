# Globaal Ontwerp Gemeenschappelijke Bronontsluiting

_ICTU | Juni 2026_

> LET OP: Het project gemeenschappelijke bronontsluiting is in ontwikkeling en de documentatie volgt dit. De huidige versie van dit globaal ontwerp is daarom niet definitief. De status van de documentatie is [hier](https://ictu.github.io/GBO/latest/#reviewproces) te vinden.

## Inleiding

### Globaal ontwerp

In dit globaal ontwerp wordt op hoofdlijnen uiteengezet wat de voorgestelde oplossingsrichting is voor een gemeenschappelijke bronontsluiting en hoe deze ingericht kan worden. Het doel is om input op de voorgestelde oplossingsrichting op te halen en het ontwerp vast te stellen, zodat dit als basis kan dienen voor verdere uitwerking in de volgende documenten:

- Projectstartarchitectuur: kaders en richtlijnen voor het ontwerp en de inrichting van de stelselfuncties.  
- Technisch ontwerp: technisch ontwerp van de benodigde voorzieningen.  
- Technische requirements: de specificaties van de in te richten componenten.  
- Semantiek: informatiemodellen en begrippenkaders van de gegevens die uitgewisseld worden, zowel de gegevens die opgevraagd worden, als gegevens die nodig zijn voor veilige, betrouwbare uitwisseling (zoals GraphQL-schema's, mappings tussen verschillende formaten, toestemmingen, etc.).  

Voor de beschrijving van de doelen van de gemeenschappelijke bronontsluiting wordt verwezen naar het tabblad [Gemeenschappelijke Bronontsluiting](https://ictu.github.io/GBO/). De juridische en organisatorische context worden beschreven op het tabblad [Context](https://ictu.github.io/GBO/latest/context).  

### Uitgangspunten

- Europees interoperabel: Europese afspraken en standaarden (o.a. EIF, eIDAS, OOTS en EUDI) en de Nederlandse invulling hiervan, zoals de NL-Wallet en de Basisinrichting OOTS.  
- Generieke Digitale Infrastructuur (GDI): de verzameling van afspraken(stelsels), standaarden en voorzieningen die alle publieke dienstverleners gebruiken voor hun digitale dienstverlening aan burgers en ondernemers. Deze afspraken, standaarden en voorzieningen zijn verdeeld in 4 domeinen: toegang, interactie, gegevensuitwisseling en infrastructuur.  
- Federatief Datastelsel (FDS): een afsprakenstelsel dat organisaties met een publieke taak hierbij ondersteunt. De gezamenlijke afspraken zijn erop gericht dat overheden werken op basis van dezelfde standaarden, waardoor ze op een uniforme manier met data omgaan.  
NB: Het FDS maakt voor de gegevensuitwisseling gebruik van de GDI-standaarden en zorgt voor aanvullingen op deze GDI-standaarden indien hiervoor nog geen standaarden of afspraken gemaakt zijn. Voorbeelden is bijvoorbeeld: Federatieve Toegangsverlening dat gebaseerd is op AuthZen en als standaard op dit moment is aangeboden bij Forum Standaardisatie.  
- Beleidsgedreven autorisatie (PBAC): PBAC-architectuur voor autorisatie en toegang.  
- Waardengedreven inrichting: De organisatorische en technische inrichting is gebaseerd op publieke waarden en op het principe van een gelijk speelveld bij de rollen en verantwoordelijkheden.  
- Keuzevrijheid: Bronhouders zijn volledig vrij om gebruik te maken van GBO of een alternatief te kiezen. Ook als een bronhouder voor een gegevensstroom een eigen oplossing gebruikt, kan voor de andere GBO gebruikt worden.  


### Leeswijzer

Het globaal ontwerp wordt als volgt uitgewerkt:

- [Hoofdstuk 2](#2-voorgestelde-oplossingsrichting) schetst de voorgestelde oplossingsrichting  
- [Hoofdstuk 3](#3-interactiepatronen) beschrijft de interactiepatronen waar de gemeenschappelijke bronontsluiting invulling aan geeft  
- [Hoofdstuk 4](#4-generieke-functies-en-stelselfuncties) beschrijft de generieke functies die nodig zijn en de stelselfuncties waarmee dit mogelijk wordt  
- [Hoofdstuk 5](#5-te-ontwikkelen-componenten) gaat in op de stelselfuncties die nog ontwikkeld moeten worden  
- [Hoofdstuk 6](#6-impact-op-betrokken-partijen) beschrijft de impact op de betrokken partijen  


## Voorgestelde oplossingsrichting


### Knelpuntenanalyse

Op het tabblad [Gemeenschappelijke Bronontsluiting](https://ictu.github.io/GBO/) worden de voordelen van een gemeenschappelijke bronontsluiting benoemd. Er zitten knelpunten in de huidige informatievoorziening waardoor deze voordelen nog niet bereikt worden:  
- Verschillende gegevensstromen vragen verschillende gegevenssets.  
- Verschillende gegevensstromen hanteren verschillende autorisatiemodellen.  
- Verschillende gegevensstromen gebruiken verschillende protocollen.  
- Verschillende gegevensstromen vallen onder verschillende wet- en regelgeving.  

Om te voorkomen dat overheidsbronnen hier aparte oplossingen voor implementeren, stelt GBO een gemeenschappelijke bronontsluiting voor die:  
- bronhouders eenmalig implementeren en meervoudig gebruiken.  
- door middel van configureren (in plaats van programmeren) gegevens beschikbaar stelt voor EUDI-wallet, OOTS en private dienstverleners.  
- alleen de gegevens beschikbaar stelt die de gegevensvrager mag (en kan) vragen.  
- de toegang tot de gegevens regelt met een configurabele autorisatie en complete audit trail.  
- via gemeenschappelijke oplossingen aansluit op OOTS, attribuutverstrekking en attribuutverificatie.  
- via een gemeenschappelijke toestemmingsvoorziening private dienstverleners toegang geeft tot gegevens die zij mogen opvragen.  


### Oplossingsrichting

Deze paragraaf beschrijft de voorgestelde oplossingsrichting voor GBO. Het onderstaande diagram vormt hiervoor de basis.

<figure>
``` mermaid
--8<-- "diagrammen/gbo_swimlanes_simpel.mmd"
```
<figcaption>Figuur 1: Oplossingsrichting GBO.</figcaption>
</figure>

Voor GBO stellen bronhouders hun gegevens bloot via één API, die voor verschillende gegevensverzoeken gebruikt kan worden. Een nieuw gegevensverzoek kan met configuraties ingesteld worden, in plaats van het moeten inrichten en beheren van een nieuw endpoint.  
Generieke ontsluiting vraagt extra autorisatieregels, die met beleidsregels (eventueel ook federatief) in te stellen moeten zijn. Het koppelvlak moet met een betrouwbare en veilige standaard beschikbaar gesteld worden; zaken als versleuteling, identificatie, authenticatie en logging moeten daarin geborgd zijn. Voor de verschillende gegevensstromen zorgen centrale voorzieningen voor aansluiting op bestaande protocollen en vertrouwensstelsels.  

In de volgende paragrafen worden deze componenten uitgewerkt en wordt toegewerkt naar een invulling daarvan.  

## Interactiepatronen

GBO ondersteunt drie interactiepatronen, elk met eigen actoren, grondslagen en protocollen. De drie interactiepatronen worden in de volgende paragrafen geschetst.

### Patroon A - burger gebruikt EUDI-Wallet

Een burger vraagt een attestatie op bij een overheidsbron als verifieerbare credential (VC) voor opname in zijn EUDI-Wallet. De wallet initieert een OpenID4VCI-ophaalverzoek richting GBO, dat de bron bevraagt en het resultaat retourneert als SD-JWT VC of mdoc (ISO 18013-5). De attestatie is cryptografisch gezegeld en kan daarna door de burger worden gepresenteerd aan dienstverleners via OpenID4VP, zonder verdere tussenkomst van GBO.  
De uitgifte van attestaties kan rechtstreeks door bronhouders uitgevoerd worden, wat resulteert in PubEAA's. De uitgifte kan ook door Qualified Trust Service Providers (QTSP's) uitgevoerd worden, wat resulteert in QEAA's. Juridisch hebben PubEAA's en QEAA's dezelfde betekenis.

GBO ondersteunt functioneel/technisch in dit patroon de rol van PubEAA-uitgevende instantie, maar is zelf geen PubEAA verstrekker. De bronhouder gebruikt deze instantie om zelfstandig attestaties uit te geven.  
Voor uitgifte van attestaties via een QTSP ondersteunt GBO de rol van Authentic Source Interface Provider (ASI-P). Deze ASI-P kan zowel een "verify" dienst (waar aangeleverde attributen geverifieerd worden) als een "retrieve" dienst (waar de QTSP namens de bronhouder attributen ophaalt en kwalificeert) bieden. Voor autorisatie en authenticatie kan gebruik gemaakt worden van een autorisatiedienst die ook door GBO aangeboden wordt.

De Europese Commissie onderzoekt de mogelijkheid om de OOTS common services in te zetten voor de catalogus van regelingen voor de attestering van attributen (Semantic Repository) en de catalogus van leveranciers van attestering van attributen (Data Service Directory). QTSP's en uitgevers van Pub-EAA's moeten van de voorgeschreven catalogi gebruik gaan maken. De bronhouders worden verantwoordelijk voor de juiste configuratie van deze catalogi.  
GBO kan bronhouders ondersteunen door het aanbieden van een gedeelde voorziening voor de semantische mapping tussen het formaat waarin de bronhouder de gegevens ontsluit en het formaat zoals dat door de afnemer verwacht wordt. Of en hoe GBO ondersteuning aan bronhouders biedt bij het vullen van de Data Service Directory is nog in onderzoek.

> **Afstemming lopend:** Over de keuze tussen varianten van PubEAA-uitgifte door overheidsbronnen en QEAA-uitgifte via een QTSP loopt nog afstemming. GBO positioneert alle mogelijke varianten als ondersteund; de governance-keuze wordt extern belegd.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-EUDI-Wallet.mmd"
```
<figcaption>Figuur 2: Interactiepatroon burger deelt gegeven via EUDI-Wallet met dienstverlener.  
NB: een gegeven kan als PubEAA (rechtstreeks van overheidsbron) of QEAA (via QTSP) in de Wallet komen.
</figcaption>
</figure>

### Patroon B - grensoverschrijdend verzoek via OOTS

Nederlandse bronhouders die digitale gegevens leveren voor de uitvoering van een SDG-procedure in andere lidstaten moeten hiervoor op het OOTS aansluiten. Zij kunnen dat doen door aan te sluiten op de Basisinrichting OOTS, gebruik te maken van een sectorale aansluiting op het OOTS (bijvoorbeeld de EMREX-brug) of een eigen aansluiting op het OOTS te ontwikkelen. Stichting RINIS levert de Basisinrichting OOTS in opdracht van het Ministerie van BZK/EZK. Sectorale en eigen aansluitingen zijn buiten scope van dit globaal ontwerp.

Voor bronhouders is het onderdeel OOTS-V van de Basisinrichting OOTS van belang (OOTS-A is voor Nederlandse dienstverleners). De OOTS-V ontvangt bewijsverzoeken van publieke instantie uit andere lidstaten die gericht zijn op bronhouders die op de OOTS-V aangesloten zijn. De OOTS-V analyseert binnenkomende verzoeken, zorgt voor herauthenticatie van de gebruiker, controleert op identiteitsverwisseling, haalt de gegevens bij de bron op en geeft de gebruiker de mogelijkheid om de gegevens voor verzending in te zien. De OOTS-V stuurt de gegevens pas naar de vragende lidstaat zodra de gebruiker daarmee ingestemd heeft.

De interactie tussen de lidstaten vindt conform Europese voorschriften plaats met eDelivery, AS4, eBMS en Regrep. De request-response berichten zijn gespecificeerd in het OOTS Exchange Data Model (OOTS EDM). De OOTS-V past nationale standaarden toe in de interactie met aangesloten bronhouders. Op dit moment is dat Digikoppeling REST API. Zo hoeven bronhouders geen kennis te hebben van de OOTS-afspraken en -standaarden. voor implementatie van de GBO architectuur moet de OOTS-V ook een GraphQL interface gaan bieden.

Aanvullend kan het voorkomen dat bronhouders hun brongegevens om willen of moeten vormen om te voldoen aan de afspraken die daarover tussen de lidstaten zijn gemaakt. De SDG-verordening verplicht semantische omvorming niet, maar stimuleert het wel. Lidstaten mogen gezamenlijk besluiten om gegevens volgens één OOTS-datamodel te leveren. Zo werken lidstaten gezamenlijk aan een uniform bewijs van geboorte.  
GBO biedt een voorziening die de benodigde semantische transformatie - naar de specificatie van de bronhouder - voor de bronhouder kan uitvoeren. De OOTS-V bevraagt in dat geval niet direct de API van de bronhouder, maar de GBO voorziening die in OOTS-datamodelformaat levert.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-OOTS-verzoek.mmd"
```
<figcaption>Figuur 3: Interactiepatroon gegevensverzoek vanuit Europese overheidsorganisatie via OOTS.</figcaption>
</figure>


### Patroon C - gegevensverzoek van private dienstverlener (DvTP)

Een private dienstverlener haalt overheidsgegevens op bij een bronhouder, uitsluitend op basis van een geldige juridische grondslag. In het geval van DvTP is dit een wettelijk vastgestelde toestemming voor het delen van gegevens met private dienstverleners. De burger authenticeert zich met een eIDAS authenticatiemiddel op het vereiste betrouwbaarheidsniveau en geeft geïnformeerde toestemming voor een specifiek doel, een specifieke afnemer en een specifieke set gegevens. GBO registreert de toestemming in een toestemmingenregister, levert een consent-id aan de private dienstverlener, valideert deze op het moment van uitvraag real-time, en zorgt dat het BSN de private dienstverlener nooit bereikt - in de plaats daarvan ontvangt de afnemer een partijspecifiek pseudoniem.

De bronhouder controleert of de private dienstverlener bevoegd is om de gegevens op te vragen, controleert het consent-id en beoordeelt of de gegevensvraag binnen de scope valt. Via het consent-id wordt het BSN van de betrokkene herleid en het antwoord aan de private dienstverlener wordt geleverd als response in het afnemersformaat.

GBO stelt een **centrale toestemmingsvoorziening** voor als kern van dit patroon. Decentrale alternatieven (zoals toestemmingsregistratie per bronhouder) zijn overwogen, maar het centrale model heeft doorslaggevende voordelen:

- **Kostenbesparing:** eenmalig inrichten en beheren is goedkoper dan dat iedere bronhouder dit zelf regelt.
- **Herkenbaarheid voor de burger:** een centrale voorziening biedt de burger telkens dezelfde ervaring, wat herkenning en vertrouwen opbouwt.
- **Inzage voor de burger:** met een centrale voorziening is het aanzienlijk eenvoudiger om de burger inzage te geven in al zijn toestemmingen via een toestemmingsportaal.
- **Eén keer toestemmen:** de burger kan in één handeling toestemming geven voor een set gegevens die mogelijk uit meerdere bronnen afkomstig zijn. Bij decentrale registratie per bron zou de burger voor elke bron apart moeten toestemmen.

Het toestemmingsportaal biedt de burger inzage in alle actieve toestemmingen en de mogelijkheid toestemming in te trekken.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-PP-haalt-gegevens-op.mmd"
```
<figcaption>Figuur 4: Interactiepatroon DvTP (dienstverlener is een private partij).</figcaption>
</figure>


## Generieke functies en stelselfuncties

GBO is opgebouwd uit acht generieke functies die samen de volledige gegevensstromen afdekken, van identiteitsvaststelling en toestemmingsbeheer tot bronontsluiting en beheer. Deze generieke functies zijn technologieneutraal.  
Elke generieke functie wordt ingevuld door een of meer stelselfuncties: concrete afspraken, standaarden en/of voorzieningen. In de paragrafen hieronder zijn de generieke functies uitgewerkt, met de stelselfuncties die GBO in beeld heeft om de functie in te vullen en hun huidige inrichtingsstatus.  

### F1 — Identiteit & Vertrouwen

_Burgers worden geïdentificeerd via het BSN, organisaties worden geïdentificeerd via het (sub)OIN. Om het BSN te verbergen voor afnemers die geen wettelijke grondslag hebben om het BSN te verwerken, wordt dit gegeven gepseudonimiseerd. Als een burger inlogt met een EIDAS middel waar geen BSN aan is gekoppeld, moet het BSN via "identity matching" achterhaald worden.
Burgers authenticeren zich met DigiD of een ander EIDAS middel met een betrouwbaarheidsniveau dat past bij de afgenomen dienst en de op te vragen gegevens. Systemen authenticeren zich met PKIo certificaten. Organisaties mogen enkel deelnemen aan het stelsel als ze voldoen aan de aansluitvoorwaarden._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                                   | **Status**                                                        | **Voornaamste gap / actie**                                              |
| ---------------------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------------ |
| S03 — Burgeridentificatie & Pseudonimisering         | BSNk PP beschikbaar - integratie nodig; Identity Matching nog in onderzoek | Onboarding DvTP-partijen als deelnemer; consent-id-koppeling             |
| S04 — Organisatie-authenticatie & Vertrouwensstelsel | FDS Poortwachter/Marktmeester uitgewerkt als concept; feitelijke beschikbaarheid en GBO-toepassing nog te bepalen | GBO-aansluitvoorwaarden; KvK↔OIN↔eIDAS-koppeling |

### F2 — Toegang & Interactie

_Gegevensvragen worden geautoriseerd met behulp van beleidsregels (PBAC). Als er toestemming (in de betekenis van de AVG) van de burger nodig is, wordt hiervoor een toestemmingsvoorziening gebruikt._

Hiervoor zijn de volgende stelselfuncties nodig:


| **Stelselfunctie**                            | **Status**                         | **Voornaamste gap / actie** |
| --------------------------------------------- | ---------------------------------- | --------------------------- |
| S01 — Toestemmingenregistratie (primair voor DvTP)               | Nog te realiseren ⚠️               | Toestemmingsregister; gebruik als PIP; afhankelijk van benodigde wet- en regelgeving |
| S02 — Toestemmingsportaal (primair voor DvTP) | Nog te realiseren ⚠️               | DvTP; inzage & intrekking; koppeling toestemmingenregister; aansluiting MijnOverheid |
| S05 — Autorisatie (PEP/PDP/PIP)               |  GBO-inrichting nog nodig | PEP/PDP referentie-implementatie per bronhouder; AuthZEN NLGov profiel; Policy Store / PAP (zie S06)  |
| S06 — Beleidsbeheer & -distributie (PAP)      | Nog te ontwerpen ⚠️                | Centrale voorziening voor het beheren en distribueren van policy-bundles naar alle bronhouder-PDP-instanties en de FSC Manager. Policies worden als gesigneerde OCI-bundles beschikbaar gesteld en asynchroon opgehaald door decentrale PDP-instanties. De PAP is het technisch-bestuurlijke gezagspunt van het stelsel: hij bepaalt wat iedere deelnemer mag. Vereist een expliciete governance-afspraak over wie policies mag schrijven, wijzigen en goedkeuren. |

### F3 — Gegevensvoorziening

_Bronhouders ontsluiten hun gegevens via een generieke API. Hiervoor wordt GraphQL voorgesteld: daarmee is hergebruik en dataminimalisatie eenvoudiger te verwezenlijken. Voor bronhouders die geen GraphQL API beschikbaar kunnen stellen, wordt een "GBO-vertaallaag" aangeboden om een bestaand protocol te vertalen naar GraphQL. Verder wordt gebruik gemaakt van de FSC standaard.
Voor aansluiting op OOTS wordt een adapter beschikbaar gesteld waarmee brongegevens omgezet worden naar de gewenste "evidence types". De Basisinrichting OOTS zorgt voor burgerconsent, de omzetting naar het OOTS protocol (AS4/eDelivery) en de aansluiting op de portalen in andere EER-lidstaten._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                              | **Status**                                                       | **Voornaamste gap / actie**                                                            |
| ----------------------------------------------- | ---------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| S07 — Gegevensontsluiting (bronontsluiting-API) | NL API Strategie (met API Design Rules) beschikbaar; Digikoppeling (met FSC) beschikbaar; GraphQL nog niet gestandaardiseerd als API-profiel | Dienstencatalogus; GraphQL positionering in FDS; GBO-vertaallaag                 |
| S08 — OOTS-adapter       | Basisinrichting OOTS beschikbaar                                | Semantische mapping bronformaat <> EDM (Evidence Exchane Data Model) |
| S11 — Attesteringsuitgifte (voor EUDI-wallet)     | Nog te realiseren ⚠️                                             | OpenID4VCI-endpoint; attestatieschema's; signing-infrastructuur; QTSP-verificatie-&retrievedienst   |

### F4 — Semantiek & Eenheid van Taal

_GBO werkt vanuit een gedeeld begrippenkader conform NL-SBB (Nederlandse standaard voor het beschrijven van begrippen). Informatiemodellen worden beoordeeld op toepassing van MIM (Metamodel Informatiemodellering). Verankering van semantiek naar RDF (Resource Description Framework) en/of SKOS (Simple Kowlegde Oranization System). Catalogi worden beschreven conform DCAT-AP NL (NL applicatieprofiel van Data Catalogue Vocabulary). Waar nodig biedt GBO mapping naar gegevensmodellen zoals SDG-EDM (Evidence Data Model) en attestatieschema's._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                  | **Status**                  | **Voornaamste gap / actie**                                                  |
| ----------------------------------- | --------------------------- | ---------------------------------------------------------------------------- |
| S10 — Semantiek & Gegevenscatalogus | Nog te realiseren ⚠️ | GBO-canonieke definities per bronhouder en generiek; begrippenkader conform NL-SBB; toepassing MIM voor informatiemodellen; catalogi vastleggen DCAT-AP NL; mapping tussen GraphQL- en SDG-formaten en attestatieschema's |

### F5 — Gegevenskwaliteit & Validatie

_Omdat GBO gaat over bronontsluiting en (her)gebruik van overheidsgegevens, is de kwaliteit van gegevens cruciaal en moet dit voldoende geborgd worden. De precieze inrichting hiervan moet uitgewerkt worden. RDF-representaties van semantische modellen, validatieprofielen of kwaliteitsmetadata kunnen gevalideerd worden met SHACL (Shapes Constraint Language). Voor niet-RDF-uitwisselformaten zijn aanvullende validatiemechanismen nodig, zoals JSON Schema, GraphQL-schema’s, XML Schema of domeinspecifieke validatieregels. Ten behoeve van herkomstregistratie kan de W3C-standaard PROV-O (PROV Ontolgy) toegepast worden. Datakwaliteitsmeting kan conform het NORA Kwaliteitsraamwerk in combinatie met W3C DQV (Data Quality Vocabulary) ingericht worden. Terugmelding van onjuiste, onvolledige of verouderde gegevens door afnemers aan bronhouders moet als proces worden ingericht._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                  | **Status**                  | **Voornaamste gap / actie**                                                                      |
| ----------------------------------- | --------------------------- | ------------------------------------------------------------------------------------------------ |
| S10 — Semantiek & Gegevenscatalogus | Nog te realiseren ⚠️ | Validatieprofielen (SHACL) per dataset; herkomstregistratie; datakwaliteitsmeting conform NORA Kwaliteitsraamwerk en W3C DQV; feedbackproces richting bronhouders |

### F6 — Grondslag & Beleid

_Als de grondslag voor een gegevensverzoek toestemming is, moet de bronhouder deze kunnen verifiëren. Daarvoor biedt GBO een centraal Toestemmingenregister. Als een andere grondslag gebruikt wordt, moet dit vanuit policies gecontroleerd kunnen worden. Ook andere voorwaarden die gelden bij gegevensverzoeken worden in policies vastgelegd en via de PEP/PDP/PIP-keten gecontroleerd._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                       | **Status**                                                     | **Voornaamste gap / actie** |
| ---------------------------------------- | -------------------------------------------------------------- | --------------------------- |
| S01 — Toestemmingenregistratie           | Nog te realiseren ⚠️                                           | Zie F2                      |
| S05 — Autorisatie (PEP/PDP/PIP)          | OPA/Rego implementatie bij iWlz als inspiratie; GBO-inrichting nog nodig | Zie F2                      |
| S06 — Beleidsbeheer & -distributie (PAP) | Nog te ontwerpen ⚠️                                            | Zie F2                      |

### F7 — Orkestratie & Integratie

_Als een gegevensverzoek meerdere services met afhankelijkheden moet doorlopen is procesorkestratie vereist. Vooralsnog is dit voor de huidige use cases van GBO niet relevant. Voor integratie met bronnen is de gegevensontsluiting nodig, en voor aansluiting op het OOTS intermediair platform is een OOTS-adapter nodig._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                              | **Status**                                                       | **Voornaamste gap / actie** |
| ----------------------------------------------- | ---------------------------------------------------------------- | --------------------------- |
| S07 — Gegevensontsluiting (bronontsluiting-API) | Zie F3 | Zie F3                      |
| S08 — OOTS-adapter        | Zie F3                                | Zie F3                      |

### F8 — Beheer & Continuïteit

_Dit Globaal Ontwerp gaat nog niet diep in op beheer en continuïteit - dit zal in volgende stappen uitgewerkt worden. Het is wel te voorzien dat hiervoor stelselfuncties nodig zijn; de meest voor de hand liggende worden hier genoemd._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                     | **Status**                                   | **Voornaamste gap / actie**                                                |
| -------------------------------------- | -------------------------------------------- | -------------------------------------------------------------------------- |
| S09 — Logging, Audit & Traceerbaarheid | FSC Logging en Logboek Dataverwerking (LDV) beschikbaar; GBO-invulling nodig | Centraal auditlog; herleidbaarheidsprofiel; koppeling aan autorisatieketen |

---

### Overzicht: stelselfuncties en generieke functies

De onderstaande tabel geeft een totaaloverzicht van alle stelselfuncties met hun relatie naar de generieke functies.

| **Stelselfunctie**                                   | **Generieke functie(s)** | **Status**                                                       |
| ---------------------------------------------------- | ------------------------ | ---------------------------------------------------------------- |
| S01 — Toestemmingenregistratie                       | F2, F6                   | Nog te realiseren ⚠️                                             |
| S02 — Toestemmingsportaal (Burger Interactie)        | F2                       | Nog te realiseren ⚠️                                             |
| S03 — Burgeridentificatie & Pseudonimisering         | F1                       | BSNk PP beschikbaar; integratie nodig                            |
| S04 — Organisatie-authenticatie & Vertrouwensstelsel | F1                       | FDS Poortwachter/Marktmeester uitgewerkt als concept; GBO-toepassing nog te bepalen |
| S05 — Autorisatie (PEP/PDP/PIP)                      | F2, F6                   | GBO-inrichting nog nodig                               |
| S06 — Beleidsbeheer & -distributie (PAP)             | F2, F6                   | Nog te ontwerpen ⚠️                                              |
| S07 — Gegevensontsluiting (bronontsluiting-API)      | F3, F7                   | Nederlandse API Strategie beschikbaar; Digikoppeling (met FSC) beschikbaar; GraphQL nog niet gestandaardiseerd als API profiel |
| S08 — OOTS-adapter (Grensoverschrijdend)             | F3, F7                   | OOTS-basisinrichting beschikbaar                                |
| S09 — Logging, Audit & Traceerbaarheid               | F8                       | LDV beschikbaar; GBO-invulling nodig                     |
| S10 — Semantiek & Gegevenscatalogus                  | F4, F5                   | DCAT-AP NL verplicht in FDS                                      |
| S11 — Attesteringsuitgifte (PubEAA / QEAA)          | F3                       | Nog te realiseren ⚠️                                             |

_Legenda: ⚠️ = nog te realiseren als nieuwe GBO-voorziening._

## Te ontwikkelen componenten

### Overzichtsplaat oplossing

De oplossingsrichting die in het tweede hoofdstuk voorgesteld werd, kan nu ingevuld worden. In de onderstaande figuur zijn in het overzicht de componenten benoemd die invulling kunnen geven aan de vereiste functies.

<figure>
``` mermaid
--8<-- "diagrammen/gbo_swimlanes.mmd"
```
<figcaption>Figuur 5: De oplossingsrichting met de gekozen componenten.<br />Toelichting: groen = generieke decentrale bronontsluiting (NB: PAP is wel centraal); lichtbruin = centrale voorzieningen t.b.v. aansluiting (optioneel - de bronhouder kan in deze gegevensstroom een alternatieve keuze maken); donkerbruin = centrale voorzieningen (verplicht als gegevens in deze gegevensstroom uitgewisseld worden); grijs = bestaande voorzieningen waarop aangesloten wordt.</figcaption>
</figure>

In de volgende paragrafen wordt aangegeven welke componenten hergebruikt kunnen worden en waar aanpassingen/aanvullingen nodig zijn om de gemeenschappelijke bronontsluiting mogelijk te maken.

### Bouwstenen die hergebruikt worden

GBO gebruikt het Federatief Datastelsel (FDS) als basisafsprakenstelsel en bouwt daar zoveel mogelijk op voort. FDS biedt al een aantal cruciale bouwstenen: FSC als standaard voor koppelingen, FTV als standaard voor autorisatie, LDV voor logging en verantwoording, DCAT-AP NL voor datacatalogisering en de in ontwikkeling zijnde stelselfuncties Poortwachter en Marktmeester voor onboarding en nalevingsbeheer.

De oplossingsrichting gaat uit van hergebruik van de volgende bouwstenen:

**FSC (Federated Service Connectivity).** Binnenlands koppelnetwerk dat mTLS-gebaseerde verbindingen tussen GBO, bronhouders en private dienstverleners verzorgt. Elke deelnemer beheert een eigen FSC Inway (bronhouder) en/of Outway (afnemer). FSC is beschikbaar als open referentie-implementatie en is de standaard voor binnenlands dataverkeer in het FDS.

**LDV (Logboek Dataverwerking).** Voor logging en verantwoording wordt de LDV standaard toegepast. Door gebruik te maken van deze standaard kunnen dataverwerkingen van verschillende bronnen en afnemers aan elkaar gekoppeld worden.

**GraphQL.** Voorgesteld bevragingsprotocol voor selectieve gegevensuitvraag op de bronontsluiting-API, naast REST als huidige standaard. Toegestane gegevensverzoeken zijn vooraf geregistreerd in de dienstencatalogus en afdwingbaar door het PDP-beleid. Bronhouders die geen eigen GraphQL-implementatie realiseren kunnen gebruik maken van GBO-tooling voor vertaling naar GraphQL. Formele standaardisatie als FDS-datadienst-type verloopt via Digikoppeling en Forum Standaardisatie.

**OAuth 2.0 / OpenID Connect.** Autorisatieprotocol voor de uitgifte van toestemmingstokens na succesvolle burgeridentificatie (DigiD of ander eIDAS-middel), als deze nodig is. Indien het authenticatiemiddel geen BSN bevat, dan zal deze via **Identity Matching** achterhaald moeten worden.

**AuthZEN.** Gestandaardiseerde koppelinterface (OpenID Foundation, draft) tussen de PEP en de PDP. Maakt de autorisatieketen protocolonafhankelijk en vervangbaar per component.

**ODRL (Open Digital Rights Language).** W3C-standaard voor machineleesbare beleidsrepresentatie. Ingezet als beschrijvingstaal voor beleidsregels in de PAP (zie §4.1), aansluitend op de toepassing in FDS en DCAT-AP NL.

**BSNk PP (Polymorf Pseudonimiseringsstelsel).** In productie bij Logius. Verplicht voor alle DvTP-uitvragen: zet het BSN om naar een partijspecifiek, onomkeerbaar pseudoniem vóór enige verstrekking aan een private dienstverlener.

**OpenID4VCI / OpenID4VP.** OpenID-protocollen voor respectievelijk de uitgifte (GBO → wallet) en de presentatie (wallet → dienstverlener) van verifieerbare credentials. Vormt het technische fundament van het EUDI-Wallet-patroon en mogelijke andere toepassingen van VC's.

**SD-JWT VC / mdoc (ISO 18013-5).** Attestatieformaten voor de EUDI-Wallet, conform het ARF. SD-JWT VC is het standaardformaat voor online presentatie; mdoc ondersteunt ook offline (proximity) scenario's.

**AS4 / eDelivery (via OOTS-basisinrichting).** EU-transportprotocol voor het OOTS-berichtenverkeer. GBO communiceert via REST/JSON met de OOTS-basisinrichting; de AS4-laag is volledig bij de OOTS-basisinrichting belegd.


Voor de toepassingen die in beeld zijn is echter meer nodig. In dit hoofdstuk wordt per onderwerp beschreven wat er nog ontbreekt, en wat er dus afgesproken of ontwikkeld moet worden.

### GraphQL als selectief bevragingsmechanisme

FDS hanteert REST als standaard datadienst-type (NL API Strategie / REST-API Design Rules). Voor onderdelen (in elk geval bronontsluiting) stelt GBO GraphQL voor. Hiermee worden hergebruik en dataminimalisatie eenvoudiger en minder beheer-intensief.  

Wat er nog moet worden afgesproken of gerealiseerd:

- **Positionering van GraphQL als datadienst-type**: GBO introduceert GraphQL als aanvullend bevragingsmechanisme naast REST, waarbij dataminimalisatie structureel is ingebouwd en hergebruik van de API via parametrisering mogelijk is. GraphQL is in productie bewezen bij het iWlz-afsprakenstelsel en is compatibel met FSC Inway/Outway. Formele standaardisatie van GraphQL als FDS-datadienst-type vergt een wijzigingsvoorstel via Forum Standaardisatie en Digikoppeling. In de GBO pilots wordt al ervaring opgedaan met GraphQL.
- Een **GBO-vertaallaag** voor bronhouders die geen eigen GraphQL-implementatie willen of kunnen realiseren. Bronhouders die een REST-API aanbieden kunnen via de GBO-vertaallaag toch ontsloten worden als GraphQL-bron. Bronhouders worden dus niet gedwongen GraphQL zelf te implementeren.
- GBO sluit aan bij **DCAT-AP NL** voor datacatalogisering, conform de bestaande FDS-verplichting. Indien aanvullende metadata-elementen noodzakelijk blijken, wordt dit ingebracht bij de beheerder en community van DCAT-AP NL. GBO maakt geen eigen profiel bovenop DCAT-AP NL.
- Een **dienstencatalogus**: een centrale catalogus van vooraf geregistreerde gegevensvragen per toepassing. Afnemers kunnen alleen opvragen wat voor hun specifieke toepassing is geregistreerd. De dienstencatalogus worden centraal beheerd als onderdeel van GBO; dit vraagt geen inzet van de bronhouder.

### Toestemming en grondslag als afdwingbaar autorisatiemechanisme

FDS schrijft voor dat gegevensuitwisseling op een geldige grondslag berust, maar legt geen technische invulling op voor toestemmingsbeheer of real-time grondslagraadpleging. **FTV** biedt een autorisatieraamwerk dat gebruikt kan worden voor het per-uitvraag raadplegen van een extern toestemmingenregister als PIP, en de doelbindingstoets kan uitvoeren die DvTP vereist.  

Wat er nog moet worden afgesproken of gerealiseerd:

- Een **pseudonimiseringsprofiel** voor GBO/DvTP: BSNk PP als verplichte voorziening zodat het BSN private dienstverleners nooit bereikt.  
- Een **toestemmingsportaal** voor de burger: een overheidsgerichte UI voor het geven, inzien en intrekken van toestemming, gekoppeld aan het toestemmingenregister.  
- Een **toestemmingenregister** als machineleesbare centrale voorziening, waarbij toestemming gekoppeld is aan doel, afnemer en gegevensset (doelbinding), en intrekking onmiddellijk effect heeft. Het register is als PIP real-time raadpleegbaar door de autorisatieketen.  
- Een **PEP/PDP/PIP-keten** op basis van AuthZEN en een policy-taal zoals OPA/Rego, als concrete invulling van het FTV-autorisatieraamwerk voor GBO-toepassingen. Policies worden centraal beheerd via een PAP en gedistribueerd naar decentrale PDP-instanties per bronhouder.  
- Een **PAP (Policy Administration Point)** als centraal GBO-component voor het beheren en distribueren van gesigneerde policy-bundles. Dit is tevens het bestuurlijk gezagspunt van het stelsel: het bepaalt wat iedere deelnemer mag. Er is een expliciete governance-afspraak nodig over wie policies mag opstellen, wijzigen en goedkeuren. Beleidsregels worden beschreven in ODRL als machineleesbare representatielaag, aansluitend op de toepassing van ODRL in FDS en DCAT-AP NL.  

_Juridische randvoorwaarde: toestemming als afdwingbare grondslag is pas operationeel na inwerkingtreding van de daarvoor benodigde wet- en regelgeving. De technische uitwerking loopt parallel aan het wetgevingstraject._

### OOTS-aansluiting

FDS is een binnenlands afsprakenstelsel en voorziet niet in grensoverschrijdende gegevensuitwisseling. OOTS vereist AS4/eDelivery als transportprotocol en het SDG Evidence Data Model (SDG-EDM) als semantisch kader — beide vallen buiten de scope van FDS.  

Wat er nog moet worden afgesproken of gerealiseerd:

- Een **protocolvertaler** (onderdeel van OOTS basisinrichting) die AS4/eDelivery-verkeer van EU-lidstaten vertaalt naar GraphQL richting GBO en vice-versa, zodat bronhouders geen OOTS-kennis nodig hebben en uitsluitend de GBO-API zien.  
- **Semantische mappings** van GBO-canonieke definities naar SDG-EDM XML per evidence type.  


### Uitgifte van attestaties voor de EUDI-Wallet (PubEAA provider)

Het EUDI-Wallet-traject vereist dat overheidsbronnen attestaties kunnen uitreiken als verifieerbare credentials (VC) die de burger in zijn wallet opslaat en vervolgens presenteert aan dienstverleners. Dit patroon valt volledig buiten de scope van FDS.  

Wat er nog moet worden afgesproken of gerealiseerd:

- Afspraken over de **rol van GBO als PubEAA-ondersteuner**: GBO biedt de infrastructuur voor uitgifte (OpenID4VCI) en presentatie (OpenID4VP), maar is zelf geen PubEAA-verstrekker in juridische zin.  
- **Attestatieschema's per use case**: semantische mapping van bronhouder-attributen naar de attestatieschema's die door de EUDI-Wallet worden vereist.  
- Een **signing-infrastructuur** voor het digitaal ondertekenen van attestaties, conform eIDAS2/ARF en de relevante Europese Trusted Lists.  
- Standaardisatie van de **attestatieformaten**: SD-JWT VC voor online presentatie en mdoc (ISO 18013-5) voor offline/proximity-scenario's.  
- Helderheid over de **rol van QTSP's**: een PubEAA heeft onder eIDAS2 dezelfde juridische waarde als een QEAA en is als zodanig geldig voor grensoverschrijdend gebruik — een QTSP is daarvoor niet vereist. Naast de PubEAA route kan een bronhouder er echter ook voor kiezen de attestatie via een QTSP (QEAA) te laten verlopen. GBO ondersteunt beide varianten (zie ook §2.1). Over welke route de voorkeur heeft, loopt afstemming.  

### Verificatiedienst voor QTSP's (Authentic Source Interface)

Naast PubEAA-uitgifte vereist artikel 45e van eIDAS2 dat overheidsbronnen een verificatiefunctie bieden waarmee Qualified Trust Service Providers (QTSP's) bronhouder-attributen kunnen verifiëren voor eigen attestatie-uitgifte. Ook dit valt buiten de scope van FDS en is een nieuwe EU-rechtelijke verplichting.  

Wat er nog moet worden afgesproken of gerealiseerd:

- Inrichting van een **Authentic Source Interface** (conform ETSI TS 119 478) als GBO-component, inclusief de I2 Verify- en I4 Authorize-interfaces.  
- **QTSP-aansluitvoorwaarden** als mogelijke aanvulling op het FDS-Poortwachterproces, inclusief certificaatprofielen conform ETSI EN 319 412.  
- Afspraken over **QTSP-erkenning** en het bijbehorende vertrouwensanker in het GBO-stelsel.  

### Stelselafspraken en voorzieningenbeheer

Alle te ontwikkelen voorzieningen en afspraken moeten in een stelsel landen. Er moet beheer op de voorzieningen en de afspraken ingericht worden, afspraken vragen om naleving en voorzieningen vragen om monitoring. GBO wil alle te ontwikkelen afspraken en voorzieningen in bestaande stelsels opnemen. Hier zal in de projectstartarchitectuur een eerste voorzet voor gegeven worden, maar vraagt verdere uitwerking.

## Impact op betrokken partijen

Om gebruik te maken van GBO moeten bronhouders enkele componenten implementeren en beheren. De afnemers worden ook zoveel mogelijk ontzorgd, maar ook voor hen kan GBO impact hebben.  
In de onderstaande tabel is kort weergegeven wat de verwachte impact is op de betrokken partijen. NB: dit is een eerste inschatting op basis van hetgeen in dit globaal ontwerp is beschreven. Na uitwerking van het ontwerp in PSA, technisch ontwerp en technische requirements zal dit overzicht herijkt moeten worden.  

| Partij | Impact | Toelichting |
|--------|--------|-------------|
| Bronhouder | Implementatie van de componenten om de bron te ontsluiten: een GraphQL API, FSC, FTV; Beheer van de relevante catalogi (zoals de dienstencatalogus, semantische mapping, data request registry) | GBO ondersteunt met referentiecomponenten en een "GBO-vertaallaag" voor bronnen die (nog) geen GraphQL API ontsluiten. Bronhouders hoeven niet alle componenten van GBO te gebruiken, maar kunnen voor onderdelen ook eigen oplossingen gebruiken. |
| QTSP | Aansluiting op de Authentic Source Interface | Deze aansluiting volgt de Europese standaarden en moet de QTSP sowieso maken om QEAA's te kunnen uitgeven. |
| Basisinrichting OOTS | Ondersteuning van GraphQL (OOTS-V) | De huidige OOTS-V heeft al een FSC koppeling. |
| Private dienstverleners | Toetreden tot het stelsel; Aansluiten op BSNk; Implementatie FSC outway met een GraphQL API; Koppelen met toestemmingsvoorziening | Er is nog geen stelsel - dit moet nog uitgewerkt worden. |
| Burger | Mogelijkheid om gegevens te delen met private dienstverleners op basis van toestemming, die centraal gegeven en beheerd wordt. Houdt echter verschillende ingangen en stelsels voor het delen van persoonsgegevens met verschillende partijen. | Burger perspectief is (nog) niet in scope. |
