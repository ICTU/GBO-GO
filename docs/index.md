# Globaal Ontwerp Gemeenschappelijke Bronontsluiting

_ICTU | Augustus 2026_

> **LET OP:** Het project Gemeenschappelijke Bronontsluiting (GBO) is in ontwikkeling. Daarom is dit globaal ontwerp nog niet definitief. Bekijk [de status van de documentatie](https://ictu.github.io/GBO/latest/#reviewproces).

## 1 Inleiding

### Documenthiërarchie

Voor GBO geldt de volgende documenthiërarchie:

0. De [**inleiding**](https://ictu.github.io/GBO/) en [**context**](https://ictu.github.io/GBO/latest/context) beschrijven de doelen, de omgeving en de juridische kaders van GBO.
1. Het [**globaal ontwerp**](https://ictu.github.io/GBO-GO/) beschrijft op hoofdlijnen de oplossingsrichting, interactiepatronen, generieke functies en componenten.
2. De [**projectstartarchitectuur**](https://ictu.github.io/GBO-PSA/) (PSA) beschrijft de kaders, eisen en ontwerpkeuzes voor de generieke functies en stelselfuncties.
3. Het [**technisch ontwerp**](https://ictu.github.io/GBO/main/underconstruction_to/) beschrijft de technische inrichting van de voorzieningen en koppelvlakken.
4. De [**technische requirements**](https://ictu.github.io/GBO/main/underconstruction_tr/) specificeren de componenten die partijen moeten maken of aanpassen.
5. De uitwerking [**Semantiek**](https://ictu.github.io/GBO/main/underconstruction_sem/) beschrijft de informatiemodellen, begrippen, schema's en mappings voor de gegevensuitwisseling.

Bij verschillen over de oplossingsrichting of interactiepatronen is het globaal ontwerp leidend. De PSA is leidend voor de normerende architectuureisen.  

De [**demo-omgeving**](https://gbo.simulatie.datastelsel.nl/) toont aan hoe de voorgestelde oplossing in de praktijk kan werken. Let er wel op dat dit een demonstratie-omgeving is die nog in ontwikkeling is, testdata gebruikt en nog fouten kan bevatten.

### Uitgangspunten

- **Europese interoperabiliteit:** GBO volgt Europese afspraken en standaarden, waaronder EIF, eIDAS, OOTS en EUDI. GBO volgt ook de Nederlandse invulling daarvan, zoals de NL-Wallet en de Basisinrichting OOTS.
- **Generieke Digitale Infrastructuur (GDI):** de GDI bevat afsprakenstelsels, standaarden en voorzieningen voor de digitale dienstverlening van publieke dienstverleners. De GDI heeft vier domeinen: toegang, interactie, gegevensuitwisseling en infrastructuur.
- **Federatief Datastelsel (FDS):** het FDS ondersteunt organisaties met een publieke taak. Deelnemers gebruiken dezelfde standaarden en gaan daardoor op een uniforme manier met gegevens om.

  Het FDS gebruikt de GDI-standaarden voor gegevensuitwisseling. Het FDS vult deze standaarden aan als afspraken of standaarden ontbreken. Federatieve Toegangsverlening is hiervan een voorbeeld. Deze standaard is gebaseerd op AuthZEN en is aangeboden aan Forum Standaardisatie.
- **Beleidsgedreven autorisatie (PBAC):** GBO gebruikt een PBAC-architectuur voor autorisatie en toegang.
- **Waardengedreven inrichting:** de organisatorische en technische inrichting volgt publieke waarden. De verdeling van rollen en verantwoordelijkheden ondersteunt een gelijk speelveld.
- **Keuzevrijheid:** een bronhouder kan referentiecomponenten, onderdelen uit de GBO-vertaallaag of functioneel gelijkwaardige alternatieven gebruiken. Iedere oplossing moet wel voldoen aan de vastgestelde afspraken, standaarden en koppelvlakken.

### Leeswijzer

- [Hoofdstuk 2](#2-voorgestelde-oplossingsrichting) beschrijft de voorgestelde oplossingsrichting.
- [Hoofdstuk 3](#3-interactiepatronen) beschrijft de interactiepatronen die GBO ondersteunt.
- [Hoofdstuk 4](#4-generieke-functies-en-stelselfuncties) beschrijft de benodigde generieke functies en stelselfuncties.
- [Hoofdstuk 5](#5-te-ontwikkelen-componenten) beschrijft de componenten en afspraken die partijen nog moeten ontwikkelen.
- [Hoofdstuk 6](#6-impact-op-betrokken-partijen) beschrijft de verwachte impact op de betrokken partijen.
- [Bijlage begrippenlijst](bijlage_begrippenlijst/) bevat een lijst van begrippen die in dit globaal ontwerp gebruikt worden.

## 2 Voorgestelde oplossingsrichting

### Knelpuntenanalyse

De pagina [Gemeenschappelijke Bronontsluiting](https://ictu.github.io/GBO/) beschrijft de voordelen van GBO. De huidige situatie kent vier knelpunten die deze voordelen beperken:

- Gegevensstromen vragen verschillende gegevenssets.
- Gegevensstromen gebruiken verschillende autorisatiemodellen.
- Gegevensstromen gebruiken verschillende protocollen.
- Gegevensstromen vallen onder verschillende wet- en regelgeving.

GBO voorkomt dat bronhouders voor iedere gegevensstroom een aparte oplossing moeten maken. De gemeenschappelijke bronontsluiting:

- Is één keer te implementeren en daarna meervoudig te gebruiken.
- Stelt met configuratie gegevens beschikbaar voor de EUDI-Wallet, OOTS en private dienstverleners.
- Verstrekt alleen gegevens die een gegevensvrager mag en kan opvragen.
- Regelt de toegang met configureerbare autorisatie en een volledige audit trail.
- Sluit met gemeenschappelijke oplossingen aan op OOTS, attribuutverstrekking en attribuutverificatie.
- Geeft private dienstverleners toegang via een gemeenschappelijke toestemmingsvoorziening.

### Oplossingsrichting

Bronhouders ontsluiten hun gegevens voor GBO via één API. Deze API kan verschillende gegevensverzoeken verwerken.

Een bronhouder richt een nieuwe gegevensstroom in met configuratie. De bronhouder hoeft daarvoor geen nieuw endpoint te maken en te beheren.

Een generieke ontsluiting vraagt om aanvullende autorisatieregels. Beleidsregels (policies) kunnen deze regels instellen. Het koppelvlak gebruikt een betrouwbare en veilige standaard. Deze standaard borgt versleuteling, identificatie, authenticatie en logging.

GBO biedt hulpmiddelen aan bronhouders die deze inrichting nog niet zelf kunnen maken. Daarmee kunnen zij toch GBO-componenten gebruiken.

Centrale voorzieningen verbinden de gegevensstromen met bestaande protocollen en vertrouwensstelsels:

- Voor de EUDI-Wallet gaat het om een Authentic Source Interface voor QTSP's en een voorziening voor PubEAA-uitgifte door overheidsbronnen.
- Voor OOTS gaat het om een semantische mapping naar de Basisinrichting OOTS. De Basisinrichting OOTS handelt het verdere gegevensverzoek af.
- Voor private dienstverleners gaat het om een toestemmingsvoorziening en een pseudonimiseervoorziening. Deze voorzieningen voorkomen dat het BSN terechtkomt bij organisaties zonder wettelijke grondslag.

Het volgende diagram toont deze componenten.

<figure>
``` mermaid
--8<-- "diagrammen/gbo_swimlanes_simpel.mmd"
```
<figcaption>Figuur 1: Oplossingsrichting GBO.<br>
Toelichting: de rode componenten vormen samen GBO. De grijze componenten zijn bestaande voorzieningen waarop GBO aansluit.</figcaption>
</figure>

De oplossingsrichting ondersteunt de drie gegevensstromen binnen de scope van GBO. Andere gegevensstromen kunnen dezelfde inrichting ook gebruiken. De configureerbare bronontsluiting-API en autorisatieregels ondersteunen bijvoorbeeld gegevensuitwisseling tussen overheidspartijen. Partijen kunnen zulke uitwisselingen snel en betrouwbaar inrichten.

De volgende paragrafen werken de componenten verder uit.

## 3 Interactiepatronen

GBO ondersteunt drie interactiepatronen. Ieder patroon heeft eigen actoren, grondslagen en protocollen.

### Patroon A - burger gebruikt EUDI-Wallet

Een burger vraagt bij een overheidsbron een attestatie op voor zijn EUDI-Wallet. Deze attestatie is een verifieerbare credential (VC).

De wallet start via OpenID4VCI een ophaalverzoek bij GBO. GBO bevraagt de bron en retourneert het resultaat als SD-JWT VC of mdoc (ISO 18013-5).

De uitgever verzegelt de attestatie cryptografisch. Daarna kan de burger de attestatie via OpenID4VP aan een dienstverlener tonen. GBO is niet betrokken bij deze presentatie.

Een bronhouder kan attestaties rechtstreeks uitgeven als PubEAA's. Een Qualified Trust Service Provider (QTSP) kan attestaties uitgeven als QEAA's. PubEAA's en QEAA's hebben juridisch dezelfde betekenis.

GBO ondersteunt de technische rol van een instantie voor PubEAA-uitgifte. GBO is zelf geen PubEAA-verstrekker. De bronhouder gebruikt de instantie om zelfstandig attestaties uit te geven. Een bronhouder kan hiervoor ook een eigen instantie gebruiken. Die eigen instantie valt buiten de scope van GBO.

Voor uitgifte via een QTSP ondersteunt GBO de rol van Authentic Source Interface Provider (ASI-provider). De ASI-provider kan twee diensten aanbieden:

- een verify-dienst die aangeleverde attributen controleert.
- een retrieve-dienst waarmee de QTSP namens de bronhouder attributen ophaalt en kwalificeert.

De ASI-provider kan voor autorisatie en authenticatie de autorisatiedienst van GBO gebruiken. Een bronhouder kan hiervoor ook een eigen dienst gebruiken. Die eigen dienst valt buiten de scope van GBO.

> **Afstemming loopt:** De betrokken partijen bepalen nog de voorkeur voor PubEAA-uitgifte door overheidsbronnen of QEAA-uitgifte via een QTSP. GBO ondersteunt beide varianten. De governance voor deze keuze valt buiten GBO.

De Europese Commissie onderzoekt of de OOTS Common Services twee catalogi kunnen ondersteunen:

- de Semantic Repository met regelingen voor de attestering van attributen.
- de Data Service Directory met leveranciers van attesteringen van attributen.

QTSP's en uitgevers van PubEAA's moeten de voorgeschreven catalogi gebruiken. Bronhouders zijn verantwoordelijk voor de juiste configuratie van deze catalogi.

GBO kan een gedeelde voorziening bieden voor semantische mappings. Deze voorziening vertaalt het formaat van de bronhouder naar het formaat dat de afnemer verwacht.

GBO onderzoekt nog of en hoe het bronhouders ondersteunt bij het vullen van de Data Service Directory.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-EUDI-Wallet.mmd"
```
<figcaption>Figuur 2: Een burger haalt een gegeven op in de EUDI-Wallet.<br>
Een gegeven kan als PubEAA rechtstreeks van een overheidsbron komen. Een QEAA komt via een QTSP.</figcaption>
</figure>

### Patroon B - grensoverschrijdend verzoek via OOTS

Nederlandse bronhouders moeten op OOTS aansluiten als zij digitale gegevens leveren voor een SDG-procedure in een andere lidstaat. Zij hebben drie mogelijkheden:

- aansluiten op de Basisinrichting OOTS.
- een sectorale aansluiting gebruiken, zoals de EMREX-brug.
- zelf een aansluiting op OOTS ontwikkelen.

Stichting RINIS levert de Basisinrichting OOTS in opdracht van de ministeries van BZK en EZK. Sectorale en eigen aansluitingen vallen buiten de scope van dit globaal ontwerp.

Voor bronhouders is OOTS-V het relevante onderdeel van de Basisinrichting OOTS. OOTS-V ondersteunt Nederlandse dienstverleners.

OOTS-V ontvangt bewijsverzoeken van publieke instanties uit andere lidstaten. Deze verzoeken zijn gericht aan bronhouders die op OOTS-V zijn aangesloten.

OOTS-V:

- analyseert het verzoek.
- laat de gebruiker zich opnieuw authenticeren.
- controleert op identiteitsverwisseling.
- haalt de gegevens bij de bron op.
- laat de gebruiker de gegevens voor verzending bekijken.

OOTS-V verstuurt de gegevens pas nadat de gebruiker daarmee heeft ingestemd.

De lidstaten gebruiken eDelivery, AS4, eBMS en Regrep volgens de Europese voorschriften. Het OOTS Exchange Data Model (OOTS-EDM) specificeert de verzoek- en antwoordberichten.

OOTS-V gebruikt nationale standaarden voor de interactie met bronhouders. Op dit moment is dat de Digikoppeling REST API. Bronhouders hoeven daardoor de OOTS-afspraken en standaarden niet zelf toe te passen.

Voor GBO moet OOTS-V ook met GraphQL-API's kunnen werken.

Bronhouders kunnen hun brongegevens omvormen volgens afspraken tussen lidstaten. De SDG-verordening verplicht deze semantische omvorming niet, maar stimuleert haar wel.

Lidstaten kunnen afspreken om gegevens volgens één OOTS-datamodel te leveren. Zij werken bijvoorbeeld samen aan een uniform bewijs van geboorte.

GBO biedt een voorziening die de semantische transformatie volgens de specificatie van de bronhouder uitvoert. OOTS-V bevraagt dan niet rechtstreeks de API van de bronhouder. OOTS-V bevraagt de GBO-voorziening, die gegevens in het OOTS-datamodelformaat levert.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-OOTS-verzoek.mmd"
```
<figcaption>Figuur 3: Gegevensverzoek van een Europese overheidsorganisatie via OOTS.</figcaption>
</figure>

### Patroon C - gegevensverzoek van private dienstverlener (DvTP)

Een private dienstverlener vraagt overheidsgegevens op bij een bronhouder. Dit mag alleen met een geldige juridische grondslag.

Voor DvTP is deze grondslag een wettelijk vastgestelde toestemming voor het delen van gegevens met private dienstverleners.

De burger authenticeert zich op een centraal toestemmingsportaal. De burger gebruikt daarvoor een eIDAS-middel met het vereiste betrouwbaarheidsniveau.

Daarna geeft de burger geïnformeerde toestemming. De toestemming geldt voor een specifiek doel, een specifieke afnemer en een specifieke gegevensset.

GBO registreert de toestemming in een toestemmingsregister. De private dienstverlener ontvangt een consent-id. De private dienstverlener ontvangt nooit het BSN, maar een partijspecifiek pseudoniem.

De bronhouder controleert:

- of de private dienstverlener de gegevens mag opvragen.
- of het consent-id geldig is.
- of de gegevensvraag binnen de toestemming valt.

De bronhouder herleidt het BSN uit de versleutelde identiteit. Daarna levert de bronhouder het antwoord aan de private dienstverlener.

GBO stelt een **centrale toestemmingsvoorziening** voor. Deze voorziening bestaat uit een toestemmingsportaal en een toestemmingsregister.

GBO heeft ook decentrale registratie per bronhouder onderzocht. Het centrale model heeft de volgende voordelen:

- **Lagere kosten:** één centrale inrichting is goedkoper dan een afzonderlijke inrichting bij iedere bronhouder.
- **Herkenbaarheid:** de burger gebruikt steeds dezelfde voorziening. Dit ondersteunt herkenning en vertrouwen.
- **Inzage:** de burger kan alle toestemmingen centraal bekijken en intrekken.
- **Eén toestemming:** de burger kan in één handeling toestemming geven voor gegevens uit meerdere bronnen. Bij decentrale registratie is per bron een afzonderlijke toestemming nodig.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-PP-haalt-gegevens-op.mmd"
```
<figcaption>Figuur 4: Gegevensverzoek van een private dienstverlener binnen DvTP.</figcaption>
</figure>

## 4 Generieke functies en stelselfuncties

Het gebruik van generieke functies sluit aan bij een bredere ontwikkeling binnen de Nederlandse overheid. De GDI-Architectuur introduceerde dit begrip in de NORA.

Meerdere stelsels gebruiken generieke functies. Hiermee combineren zij technische keuzevrijheid met herkenbare functies voor gebruikers. Het Gezondheidsinformatiestelsel gebruikt bijvoorbeeld een vergelijkbaar abstractieniveau.

De indeling van GBO bouwt voort op de GDI-indeling. GBO past deze indeling toe op de eigen interactiepatronen. Dit leidt tot acht generieke functies:

| GDI-domein | Generieke functies van GBO |
| ---------- | -------------------------- |
| Toegang | F1 - Identiteit & Vertrouwen. F2 - Toegang & Interactie. F6 - Grondslag & Beleid |
| Interactie | F2 - Toegang & Interactie |
| Gegevensuitwisseling | F3 - Gegevensvoorziening. F4 - Semantiek & Eenheid van Taal. F5 - Gegevenskwaliteit & Validatie. F7 - Orkestratie & Integratie |
| Infrastructuur | F8 - Beheer & Continuïteit |

Eén of meer stelselfuncties vullen iedere generieke functie in. Stelselfuncties zijn concrete afspraken, standaarden of voorzieningen.

De volgende paragrafen beschrijven de generieke functies, voorgestelde stelselfuncties en huidige inrichtingsstatus.

### F1 — Identiteit & Vertrouwen

GBO identificeert burgers met het BSN en organisaties met het OIN of sub-OIN. GBO pseudonimiseert het BSN voor afnemers zonder wettelijke grondslag om het BSN te verwerken.

Burgers authenticeren zich met DigiD of een ander eIDAS-middel. Het betrouwbaarheidsniveau past bij de dienst en de opgevraagde gegevens.

Als het eIDAS-middel geen BSN bevat, koppelt identity matching het middel aan het BSN. Systemen authenticeren zich met PKIoverheid-certificaten.

Organisaties kunnen alleen deelnemen als zij aan de aansluitvoorwaarden voldoen.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante GDI-bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | ------------------------ | ------ | ----------------------------- |
| S03 — Burgeridentificatie & Pseudonimisering | BSNk PP. DigiD | BSNk PP is beschikbaar. Integratie is nodig. Identity Matching is nog in onderzoek. | DvTP-partijen als deelnemer aansluiten. consent-id koppelen. |
| S04 — Organisatie-authenticatie & Vertrouwensstelsel | eHerkenning. PKIoverheid. Organisatie-identificatienummer (OIN). Centrale OIN Raadpleegvoorziening | FDS Poortwachter en Marktmeester zijn als concept uitgewerkt. De beschikbaarheid en toepassing binnen GBO zijn nog niet bepaald. | GBO-aansluitvoorwaarden opstellen. KvK, OIN en eIDAS koppelen. |

### F2 — Toegang & Interactie

Als toestemming volgens de AVG nodig is, gebruikt GBO een toestemmingsvoorziening. Deze voorziening bestaat uit een toestemmingsportaal en een toestemmingsregister.

GBO autoriseert gegevensvragen met beleidsregels volgens PBAC. GBO biedt hiervoor een referentie-implementatie op basis van FTV. Een bronhouder kan ook een eigen implementatie gebruiken als deze aan de eisen voldoet.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante GDI-bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | ------------------------ | ------ | ----------------------------- |
| S01 — Toestemmingsregister (primair voor DvTP) | Mogelijk functioneel verwant aan DigiD Machtigen | Nog te realiseren ⚠️ | Toestemmingsregister realiseren. register als PIP gebruiken. benodigde wet- en regelgeving vaststellen. |
| S02 — Toestemmingsportaal (primair voor DvTP) | MijnOverheid | Nog te realiseren ⚠️ | Inzage en intrekking mogelijk maken. koppelen aan het toestemmingsregister en MijnOverheid. |
| S05 — Autorisatie (PEP/PDP/PIP) | - | AuthZEN NLGov-profiel is beschikbaar. FTV is in ontwikkeling. De GBO-inrichting ontbreekt nog. | Referentie-implementatie per bronhouder maken. Policy Store en PAP inrichten. |
| S06 — Beleidsbeheer & -distributie (PAP) | - | Nog te ontwerpen ⚠️ | Policybundels beheren en verspreiden naar de PDP-instanties van bronhouders. Ook moet de governance bepalen wie policies mag opstellen, wijzigen en goedkeuren. |

### F3 — Gegevensvoorziening

Bronhouders ontsluiten hun gegevens via een generieke bronontsluiting-API. GBO stelt hiervoor GraphQL voor. GraphQL ondersteunt hergebruik en dataminimalisatie.

GBO biedt een vertaallaag aan bronhouders zonder GraphQL-API. Deze laag vertaalt een bestaand protocol naar GraphQL. GBO gebruikt daarnaast de FSC-standaard.

Voor OOTS zet een adapter de brongegevens om naar de vereiste evidence types. De Basisinrichting OOTS regelt de toestemming van de burger, de omzetting naar AS4/eDelivery en de aansluiting op portalen in andere EER-lidstaten.

Voor de EUDI-Wallet geven bronhouders PubEAA's uit. QTSP's kunnen namens bronhouders QEAA's uitgeven.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante GDI-bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | ------------------------ | ------ | ----------------------------- |
| S07 — Gegevensontsluiting (bronontsluiting-API) | API-standaarden. Digikoppeling | De NL API Strategie, API Design Rules en Digikoppeling met FSC zijn beschikbaar. GraphQL is nog niet gestandaardiseerd als API-profiel. | Dienstencatalogus maken. GraphQL binnen FDS positioneren. GBO-vertaallaag maken. |
| S08 — OOTS-adapter | - | De Basisinrichting OOTS is beschikbaar. | GraphQL aan OOTS-V toevoegen. Bronformaat semantisch mappen naar SDG-EDM. |
| S11 — Attesteringsuitgifte (voor EUDI-Wallet) | - | Nog te realiseren ⚠️ | OpenID4VCI-endpoint, attestatieschema's en ondertekeningsinfrastructuur maken. QTSP-diensten voor verify en retrieve maken. |

### F4 — Semantiek & Eenheid van Taal

GBO gebruikt een gedeeld begrippenkader volgens NL-SBB. GBO beoordeelt informatiemodellen op de toepassing van MIM.

GBO verankert semantiek in RDF, SKOS of allebei. GBO beschrijft catalogi volgens DCAT-AP NL.

GBO geeft inzicht in beschikbare gegevenssets. Dit inzicht bevat de canonieke gegevensmodellen van bronhouders en de koppeling aan het gedeelde begrippenkader.

GBO beschrijft ook de voorwaarden waaronder gegevens opvraagbaar zijn, zoals de grondslag en de dienst. Waar nodig biedt GBO mappings naar SDG-EDM en attestatieschema's.

GBO biedt hiervoor voorzieningen en hulpmiddelen. Bronhouders blijven verantwoordelijk voor hun gegevens en de koppeling aan gegevensverzoeken.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante GDI-bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | ------------------------ | ------ | ----------------------------- |
| S10 — Semantiek & Gegevenscatalogus | Samenwerkende Catalogi. Begrippenvoorziening. Stelselcatalogus | Nog te realiseren ⚠️ | Canonieke gegevensmodellen maken. begrippenkader volgens NL-SBB maken. MIM toepassen. catalogi volgens DCAT-AP NL vastleggen. mappings maken. |

### F5 — Gegevenskwaliteit & Validatie

GBO ontsluit overheidsgegevens voor hergebruik. Daarom moet de gegevenskwaliteit voldoende zijn geborgd. De precieze inrichting is nog niet uitgewerkt.

SHACL kan RDF-representaties, validatieprofielen en kwaliteitsmetadata controleren. Andere uitwisselformaten vragen om andere mechanismen, zoals JSON Schema, GraphQL-schema's, XML Schema of domeinspecifieke regels.

PROV-O kan de herkomst van gegevens vastleggen. Het NORA Kwaliteitsraamwerk en W3C DQV kunnen de gegevenskwaliteit meten.

Afnemers moeten onjuiste, onvolledige of verouderde gegevens kunnen terugmelden aan bronhouders. GBO moet hiervoor een proces inrichten.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante GDI-bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | ------------------------ | ------ | ----------------------------- |
| S10 — Semantiek & Gegevenscatalogus | Samenwerkende Catalogi. Begrippenvoorziening. Stelselcatalogus | Nog te realiseren ⚠️ | Validatieprofielen per gegevensset maken. herkomst registreren. gegevenskwaliteit meten. terugmeldproces inrichten. |

### F6 — Grondslag & Beleid

Als toestemming de grondslag is, moet de bronhouder deze toestemming kunnen controleren. GBO biedt daarvoor een centraal toestemmingsregister.

Als een andere grondslag geldt, controleren beleidsregels deze grondslag. De PEP/PDP/PIP-keten controleert ook andere voorwaarden voor gegevensverzoeken.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante GDI-bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | ------------------------ | ------ | ----------------------------- |
| S01 — Toestemmingsregister | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) |
| S05 — Autorisatie (PEP/PDP/PIP) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) |
| S06 — Beleidsbeheer & -distributie (PAP) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) |

### F7 — Orkestratie & Integratie

GBO voorziet voor de huidige interactiepatronen geen afzonderlijke centrale procesorkestratie.

De aansluiting op het OOTS Intermediair Platform vraagt om een OOTS-adapter. De aansluiting op de EUDI-Wallet vraagt om integratie met EUDI-standaarden.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante GDI-bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | ------------------------ | ------ | ----------------------------- |
| S08 — OOTS-adapter | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) |
| S11 — Attesteringsuitgifte (voor EUDI-Wallet) | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) |

### F8 — Beheer & Continuïteit

Dit globaal ontwerp werkt beheer en continuïteit nog niet volledig uit. De volgende stappen moeten deze onderwerpen verder uitwerken.

GBO heeft hiervoor in ieder geval stelselfuncties nodig. De tabel noemt de stelselfunctie die nu het meest voor de hand ligt.

| Stelselfunctie | Relevante GDI-bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | ------------------------ | ------ | ----------------------------- |
| S09 — Logging, Audit & Traceerbaarheid | Logboek Dataverwerkingen. Diginetwerk | FSC Logging en het Logboek Dataverwerking zijn beschikbaar. De GBO-invulling ontbreekt nog. | Afspraken voor ketenbrede herleidbaarheid en verantwoording. Koppeling met de autorisatieketen maken. |

---

### Overzicht: stelselfuncties en generieke functies

De volgende tabel toont alle stelselfuncties en hun relatie met de generieke functies.

| Stelselfunctie | Generieke functie(s) | Status |
| -------------- | -------------------- | ------ |
| S01 — Toestemmingsregister (primair voor DvTP) | F2, F6 | Nog te realiseren ⚠️ |
| S02 — Toestemmingsportaal (primair voor DvTP) | F2 | Nog te realiseren ⚠️ |
| S03 — Burgeridentificatie & Pseudonimisering | F1 | BSNk PP is beschikbaar. Integratie is nodig ⚠️. Identity Matching is nog in onderzoek ⚠️. |
| S04 — Organisatie-authenticatie & Vertrouwensstelsel | F1 | FDS Poortwachter en Marktmeester zijn als concept uitgewerkt. GBO moet de beschikbaarheid en toepassing nog bepalen ⚠️. |
| S05 — Autorisatie (PEP/PDP/PIP) | F2, F6 | AuthZEN NLGov-profiel is beschikbaar. FTV is in ontwikkeling. De GBO-inrichting ontbreekt nog ⚠️. |
| S06 — Beleidsbeheer & -distributie (PAP) | F2, F6 | Nog te ontwerpen ⚠️ |
| S07 — Gegevensontsluiting (bronontsluiting-API) | F3, F7 | De NL API Strategie, API Design Rules en Digikoppeling met FSC zijn beschikbaar. GraphQL is nog niet gestandaardiseerd als API-profiel ⚠️. |
| S08 — OOTS-adapter | F3, F7 | De Basisinrichting OOTS is beschikbaar. Partijen moeten de semantische mapping nog ontwikkelen ⚠️. |
| S09 — Logging, Audit & Traceerbaarheid | F8 | FSC Logging en het Logboek Dataverwerking zijn beschikbaar. De GBO-invulling ontbreekt nog ⚠️. |
| S10 — Semantiek & Gegevenscatalogus | F4, F5 | Nog te realiseren ⚠️ |
| S11 — Attesteringsuitgifte (voor EUDI-Wallet) | F3, F7 | Nog te realiseren ⚠️ |

_Legenda: ⚠️ betekent dat partijen een onderdeel nog moeten realiseren._

## 5 Te ontwikkelen componenten

### Overzichtsplaat oplossing

Hoofdstuk 2 beschrijft de oplossingsrichting. De volgende figuur koppelt deze oplossingsrichting aan de componenten die de vereiste functies kunnen invullen.

<figure>
``` mermaid
--8<-- "diagrammen/gbo_swimlanes.mmd"
```
<figcaption>Figuur 5: Oplossingsrichting met de gekozen componenten.<br>
Groen toont de generieke decentrale bronontsluiting. Paars toont optionele centrale aansluitvoorzieningen. Rood toont verplichte centrale voorzieningen voor de betreffende gegevensstroom. Grijs toont bestaande voorzieningen waarop GBO aansluit.</figcaption>
</figure>

De volgende paragrafen beschrijven welke componenten GBO kan hergebruiken. Ze beschrijven ook welke aanpassingen en aanvullingen nog nodig zijn.

### Bouwstenen die hergebruikt worden

GBO gebruikt het Federatief Datastelsel (FDS) als basisafsprakenstelsel. GBO bouwt zoveel mogelijk voort op bestaande FDS-bouwstenen:

- FSC voor koppelingen.
- FTV voor autorisatie.
- LDV voor logging en verantwoording.
- DCAT-AP NL voor gegevenscatalogi.
- Poortwachter en Marktmeester voor aansluiting en naleving.

Poortwachter en Marktmeester zijn nog in ontwikkeling.

De oplossingsrichting hergebruikt de volgende bouwstenen.

**FSC (Federated Service Connectivity).** FSC is een binnenlands koppelnetwerk. Het verzorgt verbindingen op basis van mTLS tussen GBO, bronhouders en private dienstverleners. Iedere deelnemer beheert een eigen FSC Inway, Outway of allebei. FSC heeft een open referentie-implementatie en is de FDS-standaard voor binnenlands gegevensverkeer.

**LDV (Logboek Dataverwerking).** GBO gebruikt de LDV-standaard voor logging en verantwoording. Deze standaard koppelt dataverwerkingen van verschillende bronnen en afnemers aan elkaar.

**GraphQL.** GBO stelt GraphQL voor als protocol voor selectieve gegevensvragen aan de bronontsluiting-API. GraphQL is een aanvulling op REST. Bronhouders zonder GraphQL-implementatie kunnen de GBO-vertaallaag gebruiken. Formele standaardisatie als FDS-datadiensttype verloopt via Digikoppeling en Forum Standaardisatie.

**OAuth 2.0 / OpenID Connect.** Dit protocol geeft toestemmingstokens uit na succesvolle identificatie van de burger. De burger gebruikt DigiD of een ander eIDAS-middel. Als het middel geen BSN bevat, koppelt Identity Matching het middel aan het BSN.

**AuthZEN.** AuthZEN is de gestandaardiseerde koppelinterface tussen de PEP en de PDP. Deze interface maakt de autorisatieketen onafhankelijk van een specifiek protocol of product.

**ODRL (Open Digital Rights Language).** ODRL is een W3C-standaard voor machineleesbare beleidsregels. GBO gebruikt ODRL als beschrijvingstaal voor beleidsregels in de PAP. Zie [S06](#f2-toegang-interactie). Dit sluit aan op het gebruik van ODRL in FDS en DCAT-AP NL.

**BSNk PP (Polymorfe Pseudonimisering).** BSNk PP is bij Logius in productie. GBO gebruikt deze voorziening voor alle DvTP-verzoeken. De voorziening zet het BSN om naar een partijspecifiek en onomkeerbaar pseudoniem. Dit gebeurt voordat een private dienstverlener gegevens ontvangt.

**OpenID4VCI / OpenID4VP.** OpenID4VCI ondersteunt de uitgifte van verifieerbare credentials aan een wallet. OpenID4VP ondersteunt de presentatie van credentials door een wallet aan een dienstverlener. Deze protocollen vormen de technische basis voor de EUDI-Wallet en andere toepassingen van VC's.

**SD-JWT VC / mdoc (ISO 18013-5).** Dit zijn attestatieformaten voor de EUDI-Wallet volgens het ARF. SD-JWT VC is het standaardformaat voor online presentatie. mdoc ondersteunt ook offline presentaties op korte afstand.

**AS4 / eDelivery via de Basisinrichting OOTS.** AS4 en eDelivery verzorgen het Europese OOTS-berichtenverkeer. GBO communiceert via GraphQL met de Basisinrichting OOTS. De Basisinrichting OOTS beheert de volledige AS4-laag.

Voor de beoogde toepassingen zijn aanvullende afspraken en componenten nodig. De volgende paragrafen beschrijven deze aanvullingen.

### GraphQL als selectief bevragingsmechanisme

FDS gebruikt REST als standaardtype voor datadiensten volgens de NL API Strategie en REST API Design Rules. GBO stelt voor de bronontsluiting ook GraphQL voor.

GraphQL maakt hergebruik en dataminimalisatie eenvoudiger. Het kan ook de beheerlast verlagen.

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **GraphQL als type datadienst positioneren.** GBO stelt voor GraphQL naast REST te gebruiken. GraphQL ondersteunt structurele dataminimalisatie en hergebruik via parameters. GraphQL werkt met FSC Inway en Outway. Formele standaardisatie vraagt om een wijzigingsvoorstel via het kennisplatform API's, Digikoppeling en Forum Standaardisatie. De GBO-pilots doen al ervaring op met GraphQL.
- **Een GBO-vertaallaag maken.** Deze laag ondersteunt bronhouders zonder eigen GraphQL-implementatie. De laag vertaalt een REST-API naar een GraphQL-bron. Bronhouders hoeven GraphQL daardoor niet zelf te implementeren.
- **DCAT-AP NL gebruiken.** GBO volgt de bestaande FDS-verplichting voor gegevenscatalogi. Als aanvullende metadata nodig zijn, bespreekt GBO deze met de beheerder en gemeenschap van DCAT-AP NL. GBO maakt geen eigen profiel boven op DCAT-AP NL.
- **Een dienstencatalogus maken.** Deze catalogus bevat toegestane gegevensvragen per toepassing. Afnemers kunnen geen gegevens opvragen die buiten de toegestane gegevensvragen vallen. GBO stelt voor om de inhoud van de dienstencatalogus federatief te beheren met een gemeenschappelijk profiel en centrale vindbaarheid.

### Toestemming en grondslag als afdwingbaar autorisatiemechanisme

FDS verplicht een geldige grondslag voor gegevensuitwisseling. FDS schrijft geen technische oplossing voor toestemmingsbeheer of directe raadpleging van de grondslag voor.

FTV biedt een autorisatieraamwerk. Dit raamwerk kan voor ieder verzoek een extern toestemmingsregister als PIP raadplegen. Het raamwerk kan ook de doelbinding voor DvTP controleren.

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **Een pseudonimiseringsprofiel voor GBO en DvTP.** Dit profiel verplicht BSNk PP. Daardoor ontvangt een private dienstverlener nooit het BSN.
- **Een toestemmingsportaal voor burgers.** Burgers kunnen hierin toestemming geven, bekijken en intrekken. Het portaal is gekoppeld aan het toestemmingsregister.
- **Een centraal toestemmingsregister.** Het register koppelt iedere toestemming aan een doel, afnemer en gegevensset. Intrekking heeft direct effect. De autorisatieketen kan het register direct als PIP raadplegen.
- **Een PEP/PDP/PIP-keten.** Deze keten gebruikt AuthZEN en een policytaal zoals OPA/Rego. De keten vult het FTV-autorisatieraamwerk voor GBO in. Een PAP beheert de policies en verspreidt ze naar de PDP-instanties van bronhouders.
- **Een PAP (Policy Administration Point).** Dit component beheert en verspreidt ondertekende policybundels. De PAP is ook het bestuurlijke gezagspunt voor toegangsregels. De governance moet bepalen wie policies mag opstellen, wijzigen en goedkeuren. GBO beschrijft de beleidsregels in ODRL. Dit sluit aan op FDS en DCAT-AP NL.

_Juridische voorwaarde: toestemming kan pas als afdwingbare grondslag werken nadat de benodigde wet- en regelgeving in werking is getreden. De technische uitwerking loopt parallel aan het wetgevingstraject._

### OOTS-aansluiting

FDS is een binnenlands afsprakenstelsel en ondersteunt geen grensoverschrijdende gegevensuitwisseling. OOTS gebruikt AS4/eDelivery als transportprotocol en SDG-EDM als semantisch kader. Beide vallen buiten de scope van FDS.

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **Een protocolvertaler in de Basisinrichting OOTS.** Deze vertaler zet AS4/eDelivery-verkeer uit andere lidstaten om naar GraphQL voor GBO en andersom. Bronhouders hoeven daardoor geen OOTS-kennis te hebben. Zij gebruiken alleen de bronontsluiting-API.
- **Semantische mappings.** Deze mappings vertalen canonieke gegevensmodellen naar SDG-EDM XML voor ieder evidence type.

### Uitgifte van attestaties voor de EUDI-Wallet (PubEAA-uitgifte)

Overheidsbronnen moeten attestaties kunnen uitgeven als verifieerbare credentials. De burger slaat deze credentials op in de EUDI-Wallet en kan ze daarna aan dienstverleners tonen.

Dit interactiepatroon valt buiten de scope van FDS.

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **De rol van GBO als ondersteuner van PubEAA-uitgifte.** GBO biedt infrastructuur voor uitgifte via OpenID4VCI en presentatie via OpenID4VP. GBO is juridisch geen PubEAA-verstrekker.
- **Attestatieschema's per gebruikssituatie.** Deze schema's mappen attributen van bronhouders naar de vereiste EUDI-Walletschema's.
- **Een ondertekeningsinfrastructuur.** Deze infrastructuur ondertekent attestaties digitaal volgens eIDAS2, het ARF en de relevante Europese Trusted Lists.
- **Standaardisatie van attestatieformaten.** SD-JWT VC ondersteunt online presentatie. mdoc volgens ISO 18013-5 ondersteunt offline presentaties op korte afstand.
- **Duidelijkheid over de rol van QTSP's.** Een PubEAA heeft onder eIDAS2 dezelfde juridische waarde als een QEAA. Een QTSP is daarom niet verplicht voor grensoverschrijdend gebruik. Een bronhouder kan wel kiezen voor uitgifte via een QTSP. GBO ondersteunt beide varianten. De voorkeursroute is nog niet bepaald.

### Verificatiedienst voor QTSP's (ASI-provider)

Artikel 45e van eIDAS2 verplicht overheidsbronnen om een verificatiefunctie aan QTSP's te bieden. Hiermee kunnen QTSP's attributen bij de bronhouder controleren voordat zij een attestatie uitgeven.

Deze verplichting valt buiten de scope van FDS en volgt uit Europese wetgeving.

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **Een ASI-provider.** Deze GBO-component volgt ETSI TS 119 478 en bevat de interfaces I2 Verify en I4 Authorize.
- **Aansluitvoorwaarden voor QTSP's.** Deze voorwaarden kunnen het FDS-Poortwachterproces aanvullen. Ze bevatten certificaatprofielen volgens ETSI EN 319 412.
- **Erkenning van QTSP's.** Het GBO-stelsel moet afspraken maken over QTSP-erkenning en het bijbehorende vertrouwensanker.

### Stelselafspraken en voorzieningenbeheer

Alle nieuwe afspraken en voorzieningen moeten onderdeel worden van een stelsel. Het stelsel moet het beheer, de naleving en de monitoring organiseren.

GBO wil de nieuwe afspraken en voorzieningen zo veel mogelijk opnemen in bestaande stelsels. De PSA geeft hiervoor een eerste voorstel. Verdere uitwerking blijft nodig.

## 6 Impact op betrokken partijen

Bronhouders moeten enkele componenten implementeren en beheren om GBO te gebruiken. GBO ondersteunt hen daarbij met referentiecomponenten en de GBO-vertaallaag.

GBO probeert ook de afnemers zo veel mogelijk te ondersteunen. Toch heeft de aansluiting ook voor hen gevolgen.

De volgende tabel geeft een eerste inschatting. De inschatting is gebaseerd op dit globaal ontwerp. Na de PSA, het technisch ontwerp en de technische requirements moet GBO de inschatting opnieuw beoordelen.

| Partij | Impact | Toelichting |
| ------ | ------ | ----------- |
| Bronhouder | Een GraphQL-API, FSC en FTV implementeren. Relevante catalogi beheren, waaronder de dienstencatalogus en semantische mappings. | GBO biedt referentiecomponenten en een vertaallaag voor bronnen zonder GraphQL-API. Bronhouders kunnen functioneel gelijkwaardige alternatieven gebruiken. |
| Integrators en softwareleveranciers | Decentrale componenten in software en dienstverlening implementeren. De afspraken en standaarden van het stelsel volgen. | Een integrator moet voldoen aan de technische aansluitvoorwaarden. De bronhouder blijft verantwoordelijk voor de inhoud van de gegevens. |
| QTSP | Aansluiten op de ASI-provider. | De aansluiting volgt Europese standaarden. Een QTSP heeft deze aansluiting ook nodig voor de uitgifte van QEAA's. |
| Basisinrichting OOTS | GraphQL ondersteunen in OOTS-V. | OOTS-V heeft al een FSC-koppeling. |
| Private dienstverlener | Toetreden tot het stelsel, aansluiten op BSNk, een FSC Outway implementeren en koppelen met de toestemmingsvoorziening. | Partijen moeten het stelsel nog uitwerken. |
| Burger | Gegevens met private dienstverleners kunnen delen op basis van centraal beheerde toestemming. | De burger houdt verschillende ingangen en stelsels voor het delen van persoonsgegevens. Het burgerperspectief valt nog buiten de scope. |
