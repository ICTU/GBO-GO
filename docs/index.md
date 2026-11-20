# Globaal Ontwerp Gemeenschappelijke Bronontsluiting

_ICTU | September 2026_

> **LET OP:** Het programma Gemeenschappelijke Bronontsluiting (GBO) is in ontwikkeling. Daarom is dit globaal ontwerp nog niet definitief. Bekijk [de status van de documentatie](https://ictu.github.io/GBO/latest/#reviewproces).

### Terminologie en status

In dit document verwijst **GBO** uitsluitend naar het programma Gemeenschappelijke Bronontsluiting. Het programma onderzoekt en beproeft oplossingsrichtingen, doet voorstellen voor aanvullende afspraken en coördineert de ontwikkeling van referentiecomponenten en voorzieningen.

Dit globaal ontwerp beschrijft het voorgestelde **bronontsluitingsmodel**. Het bronontsluitingsmodel bestaat uit:

1. een decentrale, herbruikbare bronontsluiting die iedere bronhouder zelf inricht of laat inrichten; en
2. kanaalvoorzieningen voor EUDI-Wallet, OOTS en private dienstverleners.

Het bronontsluitingsmodel is geen afzonderlijke standaard, voorziening, organisatie of afsprakenstelsel. Het bouwt voort op bestaande afspraken, standaarden en voorzieningen van onder meer GDI en FDS. Aanvullende afspraken worden pas na besluitvorming onderdeel van de daarvoor aangewezen standaarden en afsprakenstelsels. Waar dit document een technische handeling beschrijft, wordt de verantwoordelijke actor of voorziening genoemd.

## 1 Inleiding

### Documenthiërarchie

Voor het programma GBO geldt de volgende documenthiërarchie:

0. De [**inleiding**](https://ictu.github.io/GBO/) en [**context**](https://ictu.github.io/GBO/latest/context) beschrijven de doelen, de omgeving en de juridische kaders van het programma GBO.
1. Het [**globaal ontwerp**](https://ictu.github.io/GBO-GO/) beschrijft op hoofdlijnen de oplossingsrichting, interactiepatronen, generieke functies en componenten.
2. De [**projectstartarchitectuur**](https://ictu.github.io/GBO-PSA/) (PSA) beschrijft de kaders, eisen en ontwerpkeuzes voor de generieke functies en stelselfuncties.
3. Het [**technisch ontwerp**](https://ictu.github.io/GBO/main/underconstruction_to/) beschrijft de technische inrichting van de voorzieningen en koppelvlakken.
4. De [**technische requirements**](https://ictu.github.io/GBO/main/underconstruction_tr/) specificeren de componenten die partijen moeten maken of aanpassen.
5. De uitwerking [**Semantiek**](https://ictu.github.io/GBO-Semantiek/) beschrijft de informatiemodellen, begrippen, schema's en mappings voor de gegevensuitwisseling.

Bij verschillen over de oplossingsrichting of interactiepatronen is het globaal ontwerp leidend. De PSA is leidend voor de normerende architectuureisen.  

De [**demo-omgeving**](https://gbo.simulatie.datastelsel.nl/) toont aan hoe de voorgestelde oplossing in de praktijk kan werken. Let er wel op dat dit een demonstratie-omgeving is die nog in ontwikkeling is, testdata gebruikt en nog fouten kan bevatten.

### Uitgangspunten

- **Europese interoperabiliteit:** het bronontsluitingsmodel volgt Europese afspraken en standaarden, waaronder EIF, eIDAS, OOTS en EUDI. Het volgt ook de Nederlandse invulling daarvan, zoals de NL-Wallet en de Basisinrichting OOTS.
- **Generieke Digitale Infrastructuur (GDI):** de GDI bevat afsprakenstelsels, standaarden en voorzieningen voor de digitale dienstverlening van publieke dienstverleners. De GDI heeft vier domeinen: toegang, interactie, gegevensuitwisseling en infrastructuur.
- **Federatief Datastelsel (FDS):** het FDS ondersteunt organisaties met een publieke taak. Deelnemers gebruiken dezelfde standaarden en gaan daardoor op een uniforme manier met gegevens om.

> Het FDS gebruikt de GDI-standaarden voor gegevensuitwisseling. Het FDS vult deze standaarden aan als afspraken of standaarden ontbreken. Federatieve Toegangsverlening is hiervan een voorbeeld. Deze standaard is gebaseerd op AuthZEN en is aangeboden aan Forum Standaardisatie.  

- **Beleidsgedreven autorisatie (PBAC):** het bronontsluitingsmodel gebruikt een PBAC-architectuur voor autorisatie en toegang.
- **Waardengedreven inrichting:** de organisatorische en technische inrichting volgt publieke waarden. De verdeling van rollen en verantwoordelijkheden ondersteunt een gelijk speelveld.
- **Keuzevrijheid:** een bronhouder mag referentiecomponenten, onderdelen uit de referentievertaallaag of functioneel gelijkwaardige alternatieven gebruiken. Iedere implementatie moet voldoen aan de vastgestelde afspraken, standaarden en koppelvlakken.

### Leeswijzer

- [Hoofdstuk 2](#2-voorgestelde-oplossingsrichting) beschrijft de voorgestelde oplossingsrichting.
- [Hoofdstuk 3](#3-interactiepatronen) beschrijft de interactiepatronen binnen het bronontsluitingsmodel.
- [Hoofdstuk 4](#4-generieke-functies-en-stelselfuncties) beschrijft de benodigde generieke functies en stelselfuncties.
- [Hoofdstuk 5](#5-te-ontwikkelen-componenten) beschrijft de componenten en afspraken die partijen nog moeten ontwikkelen.
- [Hoofdstuk 6](#6-impact-op-betrokken-partijen) beschrijft de verwachte impact op de betrokken partijen.
- [Bijlage begrippenlijst](bijlage_begrippenlijst.md) bevat een lijst van begrippen die in dit globaal ontwerp gebruikt worden.

## 2 Voorgestelde oplossingsrichting

### Knelpuntenanalyse

De pagina [Gemeenschappelijke Bronontsluiting](https://ictu.github.io/GBO/) beschrijft de doelen van het programma GBO. De huidige situatie kent vier knelpunten die het bereiken van deze doelen beperken:

- Gegevensstromen vragen verschillende gegevenssets.
- Gegevensstromen gebruiken verschillende autorisatiemodellen.
- Gegevensstromen gebruiken verschillende protocollen.
- Gegevensstromen vallen onder verschillende wet- en regelgeving.

Met het bronontsluitingsmodel hoeven bronhouders niet voor iedere gegevensstroom een aparte oplossing te maken. Het model beoogt:

- een decentrale bronontsluiting die één keer te implementeren en daarna meervoudig te gebruiken is.
- beschikbaarstelling van gegevens voor EUDI-Wallet, OOTS en private dienstverleners op basis van configuratie.
- verstrekking van uitsluitend de gegevens die een gegevensvrager mag en kan opvragen.
- toegang met configureerbare autorisatie en een volledige audit trail.
- gemeenschappelijke aansluitingen op OOTS, attribuutverstrekking en attribuutverificatie.
- toegang voor private dienstverleners via een gemeenschappelijke toestemmingsvoorziening.

### Oplossingsrichting

Het voorgestelde bronontsluitingsmodel bestaat uit twee samenhangende onderdelen:

#### 1. Decentrale bronontsluiting

Bronhouders ontsluiten hun gegevens volgens de bestaande afspraken en standaarden van de GDI en het FDS. Het programma GBO doet voorstellen voor aanvullingen op deze afspraken en standaarden. Zo is één ontsluiting herbruikbaar voor verschillende typen afnemers. Dit is de decentrale bronontsluiting. De kanaalvoorzieningen voor EUDI-Wallet, OOTS en private dienstverleners (zie onderdeel 2) gebruiken deze ontsluiting. Andere afnemers en toekomstige kanalen kunnen dat ook. De intentie is om de voorgestelde aanvullingen te borgen in de GDI en/of het FDS. De decentrale bronontsluiting zal daarmee voldoen aan de afspraken en standaarden van de GDI en het FDS.

Bronhouders richten de ontsluiting zelf in of laten dat doen door hun leverancier. Zij ontsluiten hun gegevens via één API. Deze API kan verschillende gegevensverzoeken verwerken. Een bronhouder richt een nieuwe gegevensstroom in met configuratie. De bronhouder hoeft daarvoor geen nieuw endpoint te maken en te beheren. Beleidsregels (policies) bepalen wie welke gegevens mag opvragen (PBAC). Het koppelvlak gebruikt betrouwbare en veilige standaarden voor versleuteling, identificatie, authenticatie en logging.

Het programma GBO laat een referentie-implementatie realiseren als werkend voorbeeld. Bronhouders mogen deze gebruiken, of een eigen implementatie die aan dezelfde afspraken en standaarden voldoet.

#### 2. Kanaalvoorzieningen

Kanaalvoorzieningen verbinden de drie kanalen met de decentrale bronontsluiting. Het programma GBO coördineert de realisatie van deze voorzieningen. Bronhouders hoeven deze voorzieningen daardoor niet ieder zelf te ontwikkelen. Een deel van deze voorzieningen wordt nieuw gerealiseerd, al dan niet in combinatie met bestaande voorzieningen. Voor een ander deel worden bestaande voorzieningen aangepast, zodat ze kunnen werken met de decentrale bronontsluiting.

Het programma GBO richt zich op kanaalvoorzieningen voor de volgende kanalen:

- **EUDI-Wallet:** een Authentic Source Interface voor QTSP's en een voorziening voor PubEAA-uitgifte door overheidsbronnen. Gebruik is optioneel.
- **OOTS:** een OOTS-adapter voor de aansluiting op de Basisinrichting OOTS. De adapter biedt een optionele semantische vertaalfunctie. Gebruik is optioneel.
- **Private dienstverleners (DvTP):** een toestemmingsvoorziening en een pseudonimiseervoorziening. Deze voorkomen dat het BSN terechtkomt bij organisaties zonder wettelijke grondslag. Private dienstverleners die deze gegevensstroom gebruiken, moeten beide voorzieningen gebruiken.

De voorzieningen voor OOTS worden geborgd in de GDI. Voor de EUDI-Wallet is het voorstel om dit op dezelfde manier te doen. Later wordt bepaald waar de toestemmingsvoorziening wordt geborgd.

Het volgende diagram toont deze onderdelen in relatie tot elkaar.

<figure>
<div style="background-color: white;">
``` mermaid
--8<-- "diagrammen/gbo_swimlanes_simpel.mmd"
```
</div>
<figcaption>Figuur 1: Het voorgestelde bronontsluitingsmodel.<br>
Toelichting: Groen toont de componenten voor de decentrale bronontsluiting. Oranje toont de voorgestelde kanaalvoorzieningen. Grijs toont bestaande voorzieningen waarop het model aansluit.</figcaption>
</figure>

Het bronontsluitingsmodel ondersteunt de drie kanalen binnen de scope van het programma GBO. Andere kanalen en/of gegevensstromen vallen buiten de huidige programmascope. De afspraken, koppelvlakken en voorzieningen worden zo ingericht dat later hergebruik mogelijk is, bijvoorbeeld voor gegevensuitwisseling tussen overheidspartijen of andere kanalen.



## 3 Interactiepatronen

Dit globaal ontwerp beschrijft drie interactiepatronen binnen het bronontsluitingsmodel. Ieder patroon heeft eigen actoren, grondslagen en protocollen.

### Patroon A - burger gebruikt EUDI-Wallet

Een burger vraagt bij een overheidsbron een attestatie op voor zijn EUDI-Wallet. Deze attestatie is een verifieerbare credential (VC).

De wallet start via OpenID4VCI een ophaalverzoek bij de voorziening voor PubEAA-uitgifte. Deze voorziening bevraagt de bron en retourneert het resultaat als SD-JWT VC of mdoc (ISO 18013-5).

De uitgever verzegelt de attestatie cryptografisch. Daarna kan de burger de attestatie via OpenID4VP aan een dienstverlener tonen. De voorziening voor PubEAA-uitgifte is niet betrokken bij deze presentatie.

Een bronhouder mag attestaties rechtstreeks uitgeven als PubEAA's. Een Qualified Trust Service Provider (QTSP) mag attestaties uitgeven als QEAA's. PubEAA's en QEAA's hebben juridisch dezelfde betekenis.

Het bronontsluitingsmodel bevat een optionele centrale voorziening waarmee bronhouders PubEAA's kunnen uitgeven. Het programma GBO is geen PubEAA-verstrekker en de voorziening wordt evenmin zelf de juridisch verantwoordelijke verstrekker. Welke organisatie de voorziening gaat beheren, moet nog worden bepaald. De bronhouder gebruikt de voorziening om zelfstandig attestaties uit te geven. Een bronhouder mag PubEAA's ook zonder deze voorziening uitgeven. Die eigen uitgifte valt buiten de scope van het programma GBO.

Voor uitgifte via een QTSP bevat het bronontsluitingsmodel een optionele Authentic Source Interface Provider (ASI-provider). De ASI-provider biedt twee diensten:

- een verify-dienst die aangeleverde attributen controleert. Deze dienst geeft invulling de verplichting van lidstaten om ervoor te zorgen dat QTSP's de in artikel 45e bedoelde attributen elektronisch kunnen verifiëren bij authentieke bronnen, rechtstreeks of via een aangewezen intermediair.
- een retrieve-dienst waarmee de QTSP namens de bronhouder attributen ophaalt en kwalificeert. Deze dienst is optioneel.

De voorgestelde ASI-provider gebruikt voor autorisatie en authenticatie de gemeenschappelijke autorisatievoorzieningen uit het bronontsluitingsmodel. Een bronhouder mag een eigen ASI-provider met een eigen autorisatiedienst gebruiken. Die eigen dienst valt buiten de scope van het programma GBO.

> **Afstemming loopt:** De betrokken partijen bepalen nog de voorkeur voor PubEAA-uitgifte door overheidsbronnen of QEAA-uitgifte via een QTSP. Het bronontsluitingsmodel ondersteunt beide varianten. De governance voor deze keuze valt buiten de scope van het programma GBO.

De Europese Commissie onderzoekt of de OOTS Common Services twee catalogi kunnen ondersteunen:

- de Semantic Repository met regelingen voor de attestering van attributen.
- de Data Service Directory met leveranciers van attesteringen van attributen.

QTSP's en uitgevers van PubEAA's moeten de voorgeschreven catalogi gebruiken. Bronhouders zijn verantwoordelijk voor de juiste configuratie van deze catalogi.  
Een gedeelde voorziening voor semantische mappings vertaalt het formaat van de bronhouder naar het formaat dat de afnemer verwacht.
Het programma GBO onderzoekt nog of en hoe het bronhouders kan ondersteunen bij het vullen van de Data Service Directory.

<figure>
<div style="background-color: white;">
``` mermaid
--8<-- "diagrammen/interactiepatroon-EUDI-Wallet.mmd"
```
</div>
<figcaption>Figuur 2: Een burger haalt een gegeven op in de EUDI-Wallet.<br>
Een gegeven kan als PubEAA rechtstreeks van een overheidsbron komen. Een QEAA komt via een QTSP.</figcaption>
</figure>

### Patroon B - grensoverschrijdend verzoek via OOTS

Nederlandse bronhouders moeten op OOTS aansluiten als zij digitale gegevens leveren voor een SDG-procedure in een andere lidstaat. Zij hebben drie mogelijkheden:

- aansluiten op de Basisinrichting OOTS.
- een sectorale aansluiting gebruiken, zoals de EMREX-brug.
- zelf een aansluiting op OOTS ontwikkelen.

Stichting RINIS levert de Basisinrichting OOTS in opdracht van de ministeries van BZK en EZK. Sectorale en eigen aansluitingen vallen buiten de scope van dit globaal ontwerp.

Voor bronhouders is OOTS-V het relevante onderdeel van de Basisinrichting OOTS. Deze voorziening ontvangt bewijsverzoeken van publieke instanties uit andere lidstaten. Deze verzoeken zijn gericht aan bronhouders die op OOTS-V zijn aangesloten.

OOTS-V:

- analyseert het verzoek.
- laat de gebruiker zich opnieuw authenticeren.
- controleert op identiteitsverwisseling.
- haalt de gegevens bij de bron op.
- laat de gebruiker de gegevens voor verzending bekijken.

OOTS-V verstuurt de gegevens pas nadat de gebruiker daarmee heeft ingestemd.

De lidstaten gebruiken e-Delivery, AS4, eBMS en RegRep volgens de Europese voorschriften. Het OOTS Exchange Data Model (OOTS-EDM) specificeert de verzoek- en antwoordberichten. Het SDG Evidence Data Model (SDG-EDM) beschrijft het semantische model of schema waarmee bewijsgegevens worden beschreven.

OOTS-V gebruikt nationale standaarden voor de interactie met bronhouders. Op dit moment is dat de Digikoppeling REST API. Bronhouders hoeven daardoor de OOTS-afspraken en standaarden niet zelf toe te passen.

Voor aansluiting op de decentrale bronontsluiting moet OOTS-V ook met GraphQL-API's kunnen werken.

Bronhouders mogen hun brongegevens omvormen volgens afspraken tussen lidstaten. De SDG-verordening verplicht deze semantische omvorming niet, maar stimuleert haar wel. Lidstaten kunnen afspreken om gegevens volgens één OOTS-datamodel te leveren. Zij werken bijvoorbeeld samen aan een uniform bewijs van geboorte.  

De voorgestelde OOTS-adapter voert de semantische transformatie uit volgens de specificatie van de bronhouder. Het gebruik van deze voorziening is optioneel. Als een bronhouder de voorziening gebruikt, bevraagt OOTS-V niet rechtstreeks de API van de bronhouder. OOTS-V bevraagt de OOTS-adapter, die gegevens in het SDG-EDM-formaat levert.

Bronhouders moeten de bewijzen die zij via OOTS kunnen leveren bekendmaken in het OOTS-netwerk. Het bronontsluitingsmodel bevat hiervoor geen voorziening. Dit valt buiten de scope van het programma GBO. Bronhouders maken hiervoor gebruik van de dienstverlening van bNC SDG.

<figure>
<div style="background-color: white;">
``` mermaid
--8<-- "diagrammen/interactiepatroon-OOTS-verzoek.mmd"
```
</div>
<figcaption>Figuur 3: Gegevensverzoek van een Europese overheidsorganisatie via OOTS.</figcaption>
</figure>

### Patroon C - gegevensverzoek van private dienstverlener (DvTP)

Een private dienstverlener vraagt overheidsgegevens op bij een bronhouder. Dit mag alleen met een geldige juridische grondslag. Voor DvTP is deze grondslag een wettelijk vastgestelde toestemming voor het delen van gegevens met private dienstverleners.  

De burger authenticeert zich op een centraal toestemmingsportaal. De burger gebruikt daarvoor een eIDAS-middel met het vereiste betrouwbaarheidsniveau.  
Daarna geeft de burger geïnformeerde toestemming. De toestemming geldt voor een specifiek doel, een specifieke afnemer en een specifieke gegevensset.  
Het centrale toestemmingsregister registreert de toestemming. De private dienstverlener ontvangt een consent-id. De private dienstverlener ontvangt nooit het BSN, maar een partijspecifiek pseudoniem.

De bronhouder controleert:

- of de private dienstverlener de gegevens mag opvragen.
- of het consent-id geldig is.
- of de gegevensvraag binnen de toestemming valt.

De bronhouder herleidt het BSN uit de versleutelde identiteit. Daarna levert de bronhouder het antwoord aan de private dienstverlener.

Het programma GBO stelt een **centrale toestemmingsvoorziening** voor. Deze voorziening bestaat uit een toestemmingsportaal en een toestemmingsregister. De voorziening is verplicht voor de DvTP-stroom: iedere private dienstverlener en iedere bronhouder in deze stroom gebruikt dezelfde voorziening. Dit vereist wettelijke verankering.

Het programma GBO heeft ook decentrale registratie per bronhouder onderzocht. Het centrale model heeft de volgende voordelen:

- **Lagere kosten:** één centrale inrichting is goedkoper dan een afzonderlijke inrichting bij iedere bronhouder.
- **Herkenbaarheid:** de burger gebruikt steeds dezelfde voorziening. Dit ondersteunt herkenning en vertrouwen.
- **Inzage:** de burger kan alle toestemmingen centraal bekijken en intrekken.
- **Eén toestemming:** de burger kan in één handeling toestemming geven voor gegevens uit meerdere bronnen. Bij decentrale registratie is per bron een afzonderlijke toestemming nodig.

<figure>
<div style="background-color: white;">
``` mermaid
--8<-- "diagrammen/interactiepatroon-PP-haalt-gegevens-op.mmd"
```
</div>
<figcaption>Figuur 4: Gegevensverzoek van een private dienstverlener binnen DvTP.</figcaption>
</figure>

## 4 Generieke functies en stelselfuncties

Het gebruik van generieke functies sluit aan bij een bredere ontwikkeling binnen de Nederlandse overheid. De GDI-Architectuur introduceerde dit begrip in de NORA.

Meerdere stelsels gebruiken generieke functies. Hiermee combineren zij technische keuzevrijheid met herkenbare functies voor gebruikers. Het Gezondheidsinformatiestelsel gebruikt bijvoorbeeld een vergelijkbaar abstractieniveau.

De indeling van het bronontsluitingsmodel bouwt voort op de GDI-indeling en past deze toe op de drie interactiepatronen. Dit leidt tot acht generieke functies:

| GDI-domein | Generieke functies in het bronontsluitingsmodel |
| ---------- | -------------------------- |
| Toegang | F1 - Identiteit & Vertrouwen. F2 - Toegang & Interactie. F6 - Grondslag & Beleid |
| Interactie | F2 - Toegang & Interactie |
| Gegevensuitwisseling | F3 - Gegevensvoorziening. F4 - Semantiek & Eenheid van Taal. F5 - Gegevenskwaliteit & Validatie. F7 - Orkestratie & Integratie |
| Infrastructuur | F8 - Beheer & Continuïteit |

Eén of meer stelselfuncties vullen iedere generieke functie in. Stelselfuncties zijn concrete afspraken, standaarden of voorzieningen.

De volgende paragrafen beschrijven de generieke functies, voorgestelde stelselfuncties en huidige inrichtingsstatus.

### F1 — Identiteit & Vertrouwen

Binnen het bronontsluitingsmodel identificeren de betrokken voorzieningen burgers met het BSN en organisaties met het organisatie-identificatienummer (OIN) of het handelsregisternummer (HRN). De pseudonimiseervoorziening pseudonimiseert het BSN voor afnemers zonder wettelijke grondslag om het BSN te verwerken.

Burgers authenticeren zich met DigiD of een ander eIDAS-middel. Het betrouwbaarheidsniveau past bij de dienst en de opgevraagde gegevens.

Als het eIDAS-middel geen BSN bevat, koppelt identity matching het middel aan het BSN. Systemen authenticeren zich met PKIoverheid-certificaten.

Organisaties kunnen alleen deelnemen als zij aan de aansluitvoorwaarden voldoen.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | -------------------- | ------ | ----------------------------- |
| S03 — Burgeridentificatie & Pseudonimisering | BSNk PP. DigiD | BSNk PP is beschikbaar. Integratie is nodig. Het programma GBO onderzoekt Identity Matching nog. | DvTP-partijen als deelnemer aansluiten. Consent-id koppelen. |
| S04 — Organisatie-authenticatie & Vertrouwensstelsel | eHerkenning. PKIoverheid. Organisatie-identificatienummer (OIN). Centrale OIN Raadpleegvoorziening | FDS Poortwachter en Marktmeester zijn als concept uitgewerkt. De beschikbaarheid en toepassing binnen het bronontsluitingsmodel zijn nog niet bepaald. | Aansluitvoorwaarden opstellen. KvK, OIN en eIDAS koppelen. |

### F2 — Toegang & Interactie

Als toestemming volgens de AVG nodig is, raadpleegt de autorisatieketen een toestemmingsvoorziening. Deze voorziening bestaat uit een toestemmingsportaal en een toestemmingsregister.

De bronhouder autoriseert gegevensvragen met beleidsregels volgens PBAC. Daarmee kan één technische implementatie de toegang voor verschillende soorten gegevensverzoeken met verschillende toegangsvoorwaarden verwerken. Het programma GBO laat hiervoor een referentie-implementatie op basis van OpenFTV realiseren. Een bronhouder mag een eigen implementatie gebruiken als deze aan de eisen voldoet.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | -------------------- | ------ | ----------------------------- |
| S01 — Toestemmingsregister (primair voor DvTP) | Mogelijk functioneel verwant aan DigiD Machtigen | Nog te realiseren ⚠️ | Toestemmingsregister realiseren. Register als PIP gebruiken. Benodigde wet- en regelgeving vaststellen. |
| S02 — Toestemmingsportaal (primair voor DvTP) | MijnOverheid | Nog te realiseren ⚠️ | Inzage en intrekking mogelijk maken. Koppelen aan het toestemmingsregister en MijnOverheid. |
| S05 — Autorisatie (PEP/PDP/PIP) | - | AuthZEN NLGov-profiel (NLgov Profile for OpenID AuthZEN Authorization API 1.0.0) is beschikbaar. FTV is in ontwikkeling. De inrichting voor het bronontsluitingsmodel ontbreekt nog. | Referentie-implementatie maken. Policy Store en PAP inrichten. |
| S06 — Beleidsbeheer & -distributie (PAP) | - | Nog te ontwerpen ⚠️ | Policybundels beheren en verspreiden naar de PDP-instanties van bronhouders. Ook moet de governance bepalen wie policies mag opstellen, wijzigen en goedkeuren. |

### F3 — Gegevensvoorziening

Bronhouders ontsluiten hun gegevens via een generieke bronontsluiting-API. Het programma GBO stelt hiervoor GraphQL voor. GraphQL ondersteunt hergebruik en dataminimalisatie.

Het programma GBO laat voor bronhouders zonder GraphQL-API een optionele referentievertaallaag ontwikkelen. Deze laag vertaalt een bestaand protocol naar GraphQL. De verbindingen binnen het bronontsluitingsmodel gebruiken daarnaast de FSC-standaard.

Deze architectuur introduceert een adapter waarmee bronhouders de gegevens vanuit hun bron kunnen omvormen naar de gegevensformaten die zij via OOTS willen leveren. Bronhouders mogen deze adapter gebruiken zodra zij gegevens voor het OOTS gaan omvormen. Voor de uitwisseling van gegevens via OOTS is geen toestemming op grond van de AVG nodig. De Basisinrichting OOTS zorgt voor het verpakken van de gegevens van de bronhouder, zodat de uitwisseling voldoet aan de Europese voorschriften voor bewijsuitwisseling, zoals RegRep en OOTS-EDM. De Basisinrichting OOTS onderhoudt ook de verbindingen naar de lidstaten.

Voor de EUDI-Wallet geven bronhouders PubEAA's uit. QTSP's mogen namens bronhouders QEAA's uitgeven.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | -------------------- | ------ | ----------------------------- |
| S07 — Gegevensontsluiting (bronontsluiting-API) | API-standaarden. Digikoppeling | De NL API Strategie, API Design Rules en Digikoppeling met FSC zijn beschikbaar. GraphQL is nog niet gestandaardiseerd als API-profiel. | Dienstencatalogus maken. GraphQL binnen FDS positioneren. Referentievertaallaag maken. |
| S08 — OOTS-adapter | - | De Basisinrichting OOTS is beschikbaar. | GraphQL aan OOTS-V toevoegen. Bronformaat semantisch mappen naar SDG-EDM indien geconfigureerd, anders ongestructureerd doorleveren.
| S11 — Attesteringsuitgifte (voor EUDI-Wallet) | - | Nog te realiseren ⚠️ | OpenID4VCI-endpoint, attestatieschema's en ondertekeningsinfrastructuur maken. QTSP-diensten voor verify en retrieve maken. |

### F4 — Semantiek & Eenheid van Taal

Om de verschillende gegevensstromen vanuit één bronontsluiting te bedienen, laat het programma GBO een gedeeld begrippenkader volgens NL-SBB uitwerken. Het programma beoordeelt informatiemodellen op de toepassing van MIM.

De semantische uitwerking legt semantiek vast in RDF, SKOS of allebei en beschrijft catalogi volgens DCAT-AP-NL.

Binnen het bronontsluitingsmodel kunnen canonieke gegevensmodellen van bronhouders aan een gedeeld begrippenkader worden gekoppeld. Daarmee kunnen afnemers hun gegevensvraag beter afstemmen op het aanbod van de bronhouders.

De catalogi beschrijven ook de voorwaarden waaronder gegevens opvraagbaar zijn, zoals de grondslag en de dienst. Waar nodig bevatten de kanaalvoorzieningen mappings naar SDG-EDM en attestatieschema's.

NB: het programma GBO laat deze beschrijvingen opstellen, maar het beheer ervan moet landen bij bestaande stelsels en beheerorganisaties. In de [projectstartarchitectuur](https://ictu.github.io/GBO-PSA/) en het [semantiek-document](https://ictu.github.io/GBO-Semantiek/) wordt dit verder uitgewerkt.

Bronhouders blijven zelf verantwoordelijk voor hun gegevens en voor de manier waarop zij deze aan de kanaalvoorzieningen aanbieden. Een decentraal configuratiecomponent beheert hiervoor de bronconfiguratie. Iedere kanaalvoorziening bevraagt deze configuratie om gegevensvragen voor een specifiek kanaal af te handelen.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | -------------------- | ------ | ----------------------------- |
| S10 — Semantiek & Gegevenscatalogus | Samenwerkende Catalogi. Begrippenvoorziening. Stelselcatalogus | Nog te realiseren ⚠️ | Canonieke gegevensmodellen maken. Begrippenkader volgens NL-SBB maken. MIM toepassen. Catalogi volgens DCAT-AP-NL vastleggen. Mappings maken. |

### F5 — Gegevenskwaliteit & Validatie

Bronhouders ontsluiten overheidsgegevens voor hergebruik. Daarom moet de gegevenskwaliteit binnen het bronontsluitingsmodel voldoende zijn geborgd. De precieze inrichting is nog niet uitgewerkt.

SHACL kan RDF-representaties, validatieprofielen en kwaliteitsmetadata controleren. Andere uitwisselformaten vragen om andere mechanismen, zoals JSON Schema, GraphQL-schema's, XML Schema of domeinspecifieke regels.

PROV-O kan de herkomst van gegevens vastleggen. Het NORA Kwaliteitsraamwerk en W3C DQV kunnen de gegevenskwaliteit meten.

Afnemers moeten onjuiste, onvolledige of verouderde gegevens kunnen terugmelden aan bronhouders. De betrokken partijen moeten hiervoor een proces inrichten.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | -------------------- | ------ | ----------------------------- |
| S10 — Semantiek & Gegevenscatalogus | Samenwerkende Catalogi. Begrippenvoorziening. Stelselcatalogus | Nog te realiseren ⚠️ | Validatieprofielen per gegevensset maken. Herkomst registreren. Gegevenskwaliteit meten. Terugmeldproces inrichten. |

### F6 — Grondslag & Beleid

Als toestemming de grondslag is, moet de bronhouder deze toestemming kunnen controleren. De voorgestelde toestemmingsvoorziening bevat daarvoor een centraal toestemmingsregister.

Als een andere grondslag geldt, controleren beleidsregels deze grondslag. De PEP/PDP/PIP-keten controleert ook andere voorwaarden voor gegevensverzoeken.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | -------------------- | ------ | ----------------------------- |
| S01 — Toestemmingsregister | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) |
| S05 — Autorisatie (PEP/PDP/PIP) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) |
| S06 — Beleidsbeheer & -distributie (PAP) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) | Zie [F2](#f2-toegang-interactie) |

### F7 — Orkestratie & Integratie

Het bronontsluitingsmodel bevat voor de huidige interactiepatronen geen afzonderlijke centrale procesorkestratie.

Integratie vindt plaats aan de rand van de decentrale bronontsluiting. Voor OOTS vertaalt de Basisinrichting OOTS het Europese berichtenverkeer naar de bronontsluiting-API. Bronhouders kunnen daarnaast de optionele OOTS-adapter gebruiken voor semantische vertaling naar SDG-EDM.
Voor de EUDI-Wallet vraagt de aansluiting om integratie met EUDI-standaarden, zoals OpenID4VCI voor de uitgifte van attestaties en de ASI-interfaces voor QTSP's.

Hiervoor zijn de volgende stelselfuncties nodig:

| Stelselfunctie | Relevante bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | -------------------- | ------ | ----------------------------- |
| S07 — Gegevensontsluiting (bronontsluiting-API) | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) |
| S08 — OOTS-adapter | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) |
| S11 — Attesteringsuitgifte (voor EUDI-Wallet) | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) | Zie [F3](#f3-gegevensvoorziening) |

### F8 — Beheer & Continuïteit

Dit globaal ontwerp werkt beheer en continuïteit nog niet volledig uit. De volgende stappen moeten deze onderwerpen verder uitwerken.

Het bronontsluitingsmodel heeft hiervoor in ieder geval stelselfuncties nodig. De tabel noemt de stelselfunctie die nu het meest voor de hand ligt.

| Stelselfunctie | Relevante bouwstenen | Status | Ontbrekend onderdeel of actie |
| -------------- | -------------------- | ------ | ----------------------------- |
| S09 — Logging, Audit & Traceerbaarheid | Logboek Dataverwerking. Diginetwerk | FSC Logging, het Logboek Dataverwerking en de standaard Authorization Decision Log 1.0.0 zijn beschikbaar. De invulling voor het bronontsluitingsmodel ontbreekt nog. | Afspraken voor ketenbrede herleidbaarheid en verantwoording. Koppeling met de autorisatieketen maken. |

---

### Overzicht: stelselfuncties en generieke functies

De volgende tabel toont alle stelselfuncties en hun relatie met de generieke functies.

| Stelselfunctie | Generieke functie(s) | Status |
| -------------- | -------------------- | ------ |
| S01 — Toestemmingsregister (primair voor DvTP) | F2, F6 | Nog te realiseren ⚠️ |
| S02 — Toestemmingsportaal (primair voor DvTP) | F2 | Nog te realiseren ⚠️ |
| S03 — Burgeridentificatie & Pseudonimisering | F1 | BSNk PP is beschikbaar. Integratie is nodig ⚠️. Identity Matching is nog in onderzoek ⚠️. |
| S04 — Organisatie-authenticatie & Vertrouwensstelsel | F1 | FDS Poortwachter en Marktmeester zijn als concept uitgewerkt. Het programma GBO moet de beschikbaarheid en toepassing nog bepalen ⚠️. |
| S05 — Autorisatie (PEP/PDP/PIP) | F2, F6 | AuthZEN NLGov-profiel is beschikbaar. FTV is in ontwikkeling. De inrichting voor het bronontsluitingsmodel ontbreekt nog ⚠️. |
| S06 — Beleidsbeheer & -distributie (PAP) | F2, F6 | Nog te ontwerpen ⚠️ |
| S07 — Gegevensontsluiting (bronontsluiting-API) | F3, F7 | De NL API Strategie, API Design Rules en Digikoppeling met FSC zijn beschikbaar. GraphQL is nog niet gestandaardiseerd als API-profiel ⚠️. |
| S08 — OOTS-adapter | F3, F7 | De Basisinrichting OOTS is beschikbaar. Waar afspraken over gegevensformaten zijn gemaakt, moeten partijen de semantische mapping nog ontwikkelen ⚠️. |
| S09 — Logging, Audit & Traceerbaarheid | F8 | FSC Logging, Logboek Dataverwerking en Authorization Decision Log 1.0.0 zijn beschikbaar. De invulling voor het bronontsluitingsmodel ontbreekt nog ⚠️. |
| S10 — Semantiek & Gegevenscatalogus | F4, F5 | Nog te realiseren ⚠️ |
| S11 — Attesteringsuitgifte (voor EUDI-Wallet) | F3, F7 | Nog te realiseren ⚠️ |

_Legenda: ⚠️ betekent dat partijen een onderdeel nog moeten realiseren._

## 5 Te ontwikkelen componenten

### Overzicht van het bronontsluitingsmodel

Hoofdstuk 2 beschrijft het bronontsluitingsmodel. De volgende figuur koppelt dit model aan de componenten die de vereiste functies invullen.

<figure>
<div style="background-color: white; padding: 10px;">
``` mermaid
--8<-- "diagrammen/gbo_swimlanes.mmd"
```
</div>
<figcaption>Figuur 5: Het bronontsluitingsmodel met de voorgestelde componenten.<br>
Groen toont de generieke decentrale bronontsluiting. Oranje toont de optionele kanaalvoorzieningen. Rood toont verplichte kanaalvoorzieningen voor de betreffende gegevensstroom. Grijs toont bestaande voorzieningen waarop het model aansluit.<br/>De bronhouder beheert de bronspecifieke configuratie van de kanaalvoorzieningen met behulp van het decentrale configuratiecomponent.</figcaption>
</figure>

Het programma GBO levert drie soorten resultaten op. De verplichting verschilt per soort:

1. **Voorstellen voor afspraken en standaarden.** Na vaststelling worden deze geborgd in bestaande afsprakenstelsels. De vastgestelde afspraken gelden voor de bronontsluiting-API, de autorisatieketen, de logging en de aansluitvoorwaarden (zie [Stelselafspraken en voorzieningenbeheer](#stelselafspraken-en-voorzieningenbeheer)).
2. **Referentiecomponenten.** Deze zijn optioneel. Een bronhouder mag een referentiecomponent, de referentievertaallaag of een functioneel gelijkwaardig alternatief gebruiken. Het alternatief moet aan de vastgestelde afspraken en standaarden voldoen.
3. **Kanaalvoorzieningen.** Of een kanaalvoorziening verplicht is, hangt af van de gegevensstroom.

De volgende tabel geeft per voorziening de status.

| Voorziening | Gegevensstroom | Soort | Verplicht of optioneel | Beheerder |
| ----------- | -------------- | ---- | ---------------------- | --------- |
| Bronontsluiting-API, PEP/PDP/PAP, FSC Inway | Alle | Decentraal, bij de bronhouder | Afspraken verplicht. Referentiecomponent optioneel. | Bronhouder |
| PAP | Alle | Centraal en/of decentraal | Afspraken verplicht. Referentiecomponent optioneel. | Nog te bepalen (zie PSA) |
| Referentievertaallaag | Alle | Referentiecomponent | Optioneel | Nog te bepalen (zie PSA) |
| Bronconfiguratie | Alle | Decentraal | Verplicht voor de kanaalvoorzieningen waarvan de bronhouder gebruik wil maken | Bronhouder |
| Voorziening voor PubEAA-uitgifte | EUDI-Wallet | Centrale aansluitvoorziening | Optioneel. Een bronhouder mag PubEAA's ook zonder deze voorziening uitgeven. | Nog te bepalen (zie PSA) |
| ASI-provider (verify en retrieve) | EUDI-Wallet | Centrale aansluitvoorziening | Optioneel. De verify-functie is voor bronhouders wel wettelijk verplicht (eIDAS2, artikel 45e), maar niet via de voorgestelde ASI-provider. | Nog te bepalen (zie PSA) |
| OOTS-adapter (semantische mapping) | OOTS | Centrale aansluitvoorziening | Optioneel. Een bronhouder mag zelf rechtstreeks op OOTS of OOTS-V aansluiten. | Nog te bepalen (zie PSA) |
| Toestemmingsvoorziening (portaal en register) | DvTP | Centrale voorziening | Verplicht voor de DvTP-stroom | Nog te bepalen (zie PSA). Vereist wettelijke verankering. |
| Pseudonimiseervoorziening (BSNk PP) | DvTP | Bestaande GDI-voorziening | Verplicht voor de DvTP-stroom | Logius |

Voor publieke partijen geldt: een bronhouder die een gegevensstroom volgens het bronontsluitingsmodel ontsluit, volgt de afspraken en standaarden van die stroom.

Voor private dienstverleners geldt: deelname aan de DvTP-stroom is vrijwillig. Een private dienstverlener die deelneemt, moet de toestemmingsvoorziening en BSNk PP gebruiken en aan de aansluitvoorwaarden voldoen. Het vertrouwensstelsel voor private dienstverleners is nog niet uitgewerkt.


### Bouwstenen die hergebruikt worden

Het bronontsluitingsmodel gebruikt het Federatief Datastelsel (FDS) als basisafsprakenstelsel en de GDI-voorzieningen als basisvoorzieningen. Het bouwt zoveel mogelijk voort op bestaande bouwstenen die daaruit voortkomen:

- FSC voor koppelingen.
- FTV voor autorisatie.
- LDV voor logging en verantwoording.
- DCAT-AP-NL voor gegevenscatalogi.
- Poortwachter en Marktmeester voor aansluiting en naleving.

Poortwachter en Marktmeester zijn nog in ontwikkeling.

De oplossingsrichting hergebruikt de volgende bouwstenen.

**FSC (Federated Service Connectivity).** FSC is een binnenlands koppelnetwerk. Het verzorgt verbindingen op basis van mTLS tussen bronhouders, kanaalvoorzieningen en private dienstverleners. Iedere deelnemer beheert een eigen FSC Inway, Outway of allebei. FSC heeft een open referentie-implementatie en is de FDS-standaard voor binnenlands gegevensverkeer.

**LDV (Logboek Dataverwerking).** Het bronontsluitingsmodel gebruikt de LDV-standaard voor logging en verantwoording. Deze standaard koppelt dataverwerkingen van verschillende bronnen en afnemers aan elkaar.

**GraphQL.** Het programma GBO stelt GraphQL voor als protocol voor selectieve gegevensvragen aan de bronontsluiting-API. GraphQL is een aanvulling op REST. Bronhouders zonder GraphQL-implementatie mogen de referentievertaallaag gebruiken. Formele standaardisatie als FDS-datadiensttype verloopt via Digikoppeling en Forum Standaardisatie.

**OAuth 2.0 / OpenID Connect.** Dit protocol geeft toestemmingstokens uit na succesvolle identificatie van de burger. Voor de Nederlandse overheid wordt **NL GOV Assurance profile for OpenID Connect 1.0.1** gebruikt. De burger gebruikt DigiD of een ander eIDAS-middel. Als het middel geen BSN bevat, koppelt Identity Matching het middel aan het BSN.

**AuthZEN.** AuthZEN is de gestandaardiseerde koppelinterface tussen de PEP en de PDP. Deze interface maakt de autorisatieketen onafhankelijk van een specifiek protocol of product. Voor de Nederlandse overheid wordt **NLgov Profile for OpenID AuthZEN Authorization API 1.0.0** gebruikt.

**Authorization Decision Log 1.0.0.** Authorization Decision Log 1.0.0 beschrijft hoe organisaties autorisatiebeslissingen vastleggen. Daarmee kan men achteraf nagaan wie toegang kreeg, wanneer en op welke grondslag. Een uniek kenmerk koppelt registraties van meerdere organisaties in een proces aan elkaar.

**ODRL (Open Digital Rights Language).** ODRL is een W3C-standaard voor machineleesbare beleidsregels. Het bronontsluitingsmodel gebruikt ODRL als beschrijvingstaal voor beleidsregels in de PAP. Dit sluit aan op het gebruik van ODRL in FDS en DCAT-AP-NL.

**BSNk PP (Polymorfe Pseudonimisering).** BSNk PP is bij Logius in productie. Binnen het DvTP-kanaal gebruikt de pseudonimiseervoorziening BSNk PP voor alle gegevensverzoeken. De voorziening zet het BSN om naar een partijspecifiek en onomkeerbaar pseudoniem. Dit gebeurt voordat een private dienstverlener gegevens ontvangt.

**OpenID4VCI / OpenID4VP.** OpenID4VCI ondersteunt de uitgifte van verifieerbare credentials aan een wallet. OpenID4VP ondersteunt de presentatie van credentials door een wallet aan een dienstverlener. Deze protocollen vormen de technische basis voor de EUDI-Wallet en andere toepassingen van VC's.

**SD-JWT VC / mdoc (ISO 18013-5).** Dit zijn attestatieformaten voor de EUDI-Wallet volgens het ARF. SD-JWT VC is het standaardformaat voor online presentatie. mdoc ondersteunt ook offline presentaties op korte afstand.

**AS4 / e-Delivery via de Basisinrichting OOTS.** AS4 en e-Delivery verzorgen het Europese OOTS-berichtenverkeer. De OOTS-adapter communiceert via GraphQL met de Basisinrichting OOTS. De Basisinrichting OOTS beheert de volledige AS4-laag.


Voor de beoogde toepassingen zijn aanvullende afspraken en componenten nodig. De volgende paragrafen beschrijven deze aanvullingen.

### GraphQL als selectief bevragingsmechanisme

FDS gebruikt REST als standaardtype voor datadiensten volgens de NL API Strategie en REST API Design Rules. Het programma GBO stelt voor om voor de decentrale bronontsluiting ook GraphQL te gebruiken.
GraphQL maakt hergebruik eenvoudiger: met één API kunnen verschillende gegevensstromen bediend worden. Dit kan met configuratie in plaats van het moeten inrichten (en beheren) van een extra endpoint. Ook biedt GraphQL meer mogelijkheden voor dataminimalisatie: de vragende partij hoeft niet alle beschikbare gegevens op te vragen. GraphQL maakt selectieve veldopvraging standaard onderdeel van het querymodel. Bij REST moet een API selectieve veldopvraging expliciet ondersteunen.  

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **GraphQL als type datadienst positioneren.** Het programma GBO stelt voor GraphQL naast REST te gebruiken. GraphQL ondersteunt structurele dataminimalisatie en hergebruik via parameters. GraphQL werkt met FSC Inway en Outway. Formele standaardisatie vraagt om een wijzigingsvoorstel via het kennisplatform API's, Digikoppeling en Forum Standaardisatie. De pilots van het programma doen al ervaring op met GraphQL.
- **Een referentievertaallaag maken.** Deze laag ondersteunt bronhouders zonder eigen GraphQL-implementatie. De laag vertaalt een bestaande API naar een GraphQL-bron. Bronhouders hoeven GraphQL daardoor niet zelf te implementeren.
- **DCAT-AP-NL gebruiken.** Het bronontsluitingsmodel volgt de bestaande FDS-verplichting voor gegevenscatalogi. Als aanvullende metadata nodig zijn, bespreekt het programma GBO deze met de beheerder en gemeenschap van DCAT-AP-NL. Het programma stelt geen eigen profiel boven op het bestaande DCAT-AP-NL-profiel voor.
- **Een dienstencatalogus maken.** Deze catalogus bevat toegestane gegevensvragen per toepassing. Afnemers kunnen geen gegevens opvragen die buiten de toegestane gegevensvragen vallen. Het programma GBO stelt voor om de inhoud van de dienstencatalogus federatief te beheren met een gemeenschappelijk profiel en centrale vindbaarheid.

### Toestemming en grondslag als afdwingbaar autorisatiemechanisme

FDS verplicht een geldige grondslag voor gegevensuitwisseling. FDS schrijft geen technische oplossing voor toestemmingsbeheer of directe raadpleging van de grondslag voor.

FTV biedt een autorisatieraamwerk. Dit raamwerk kan voor ieder verzoek een extern toestemmingsregister als PIP raadplegen. Het raamwerk kan ook de doelbinding voor DvTP controleren.

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **Een pseudonimiseringsprofiel voor DvTP.** Dit profiel verplicht BSNk PP. Daardoor ontvangt een private dienstverlener nooit het BSN.
- **Een toestemmingsportaal voor burgers.** Burgers kunnen hierin toestemming geven, bekijken en intrekken. Het portaal is gekoppeld aan het toestemmingsregister.
- **Een centraal toestemmingsregister.** Het register koppelt iedere toestemming aan een doel, afnemer en gegevensset. Intrekking heeft direct effect. De autorisatieketen raadpleegt het register als PIP.
- **Een PEP/PDP/PIP-keten.** Deze keten gebruikt AuthZEN en een policytaal zoals OPA/Rego. De keten vult het FTV-autorisatieraamwerk voor het bronontsluitingsmodel in. Een PAP beheert de policies en verspreidt ze naar de PDP-instanties van bronhouders.
- **Een PAP (Policy Administration Point).** Dit component beheert en verspreidt ondertekende policybundels. De PAP is ook het bestuurlijke gezagspunt voor toegangsregels. De governance moet bepalen wie policies mag opstellen, wijzigen en goedkeuren. De beleidsregels worden in ODRL beschreven. Dit sluit aan op FDS en DCAT-AP-NL.

_Juridische voorwaarde: toestemming kan pas als afdwingbare grondslag werken nadat de benodigde wet- en regelgeving in werking is getreden. De technische uitwerking loopt parallel aan het wetgevingstraject._

### OOTS-aansluiting

FDS is een binnenlands afsprakenstelsel en ondersteunt geen grensoverschrijdende gegevensuitwisseling. OOTS gebruikt AS4/e-Delivery als transportprotocol en SDG-EDM als semantisch kader. Beide vallen buiten de scope van FDS.

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **Een protocolvertaler in de Basisinrichting OOTS.** Deze vertaler zet AS4/e-Delivery-verkeer uit andere lidstaten om naar GraphQL voor de decentrale bronontsluiting en andersom. Bronhouders hoeven daardoor geen OOTS-kennis te hebben. Zij gebruiken alleen de bronontsluiting-API.
- **Semantische mappings.** Deze mappings vertalen de gegevens in het bronformaat naar SDG-EDM, indien geconfigureerd door de bronhouder. De vertaling gebeurt centraal met de instellingen uit het decentrale configuratiecomponent.

### Uitgifte van attestaties voor de EUDI-Wallet (PubEAA-uitgifte)

Overheidsbronnen moeten attestaties kunnen uitgeven als verifieerbare credentials. De burger slaat deze credentials op in de EUDI-Wallet en kan ze daarna aan dienstverleners tonen (dit interactiepatroon valt buiten de scope van FDS).

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **Een voorziening voor PubEAA-uitgifte.** Deze voorziening ondersteunt uitgifte via OpenID4VCI. De bronhouder blijft juridisch verantwoordelijk voor de uitgifte; het programma GBO is geen PubEAA-verstrekker. Presentatie via OpenID4VP vindt daarna plaats tussen de wallet en de dienstverlener en valt buiten deze voorziening.
- **Attestatieschema's per gebruikssituatie.** Deze schema's mappen attributen van bronhouders naar de vereiste EUDI-Walletschema's. De mapping gebeurt centraal met de instellingen uit het decentrale configuratiecomponent.
- **Een ondertekeningsinfrastructuur.** Deze infrastructuur ondertekent attestaties digitaal volgens eIDAS2, het ARF en de relevante Europese Trusted Lists.
- **Standaardisatie van attestatieformaten.** SD-JWT VC ondersteunt online presentatie. Mdoc volgens ISO 18013-5 ondersteunt offline presentaties op korte afstand.
- **Duidelijkheid over de rol van QTSP's.** Een PubEAA heeft onder eIDAS2 dezelfde juridische waarde als een QEAA. Een QTSP is daarom niet verplicht voor grensoverschrijdend gebruik. Een bronhouder mag kiezen voor uitgifte via een QTSP. Het bronontsluitingsmodel ondersteunt beide varianten. De voorkeursroute is nog te besluiten (zie PSA).

### Verificatie- en retrievedienst voor QTSP's (ASI-provider)

eIDAS2 verplicht lidstaten ervoor te zorgen dat QTSP's de in artikel 45e bedoelde attributen elektronisch kunnen verifiëren bij authentieke bronnen, rechtstreeks of via een aangewezen intermediair. De verify-dienst van de voorgestelde ASI-provider kan hieraan invulling geven. Hiermee kunnen QTSP's attributen bij de bronhouder controleren voordat zij een attestatie uitgeven.
Deze verplichting valt buiten de scope van FDS en volgt uit Europese wetgeving.

Naast een verificatiedienst stelt het programma GBO voor om ook een retrievedienst aan te bieden aan QTSP's. Daarmee kunnen zij attributen namens de bronhouder uitgeven. Deze dienst is niet verplicht, maar biedt de bronhouders meer opties om attributen uit te geven.

Partijen moeten de volgende onderdelen nog afspreken of realiseren:

- **Een ASI-provider.** Dit component volgt ETSI TS 119 478 en bevat de interfaces I2 Verify, I3 Retrieve en I4 Authorize.
- **Technische aansluitvoorwaarden voor QTSP's op de ASI-provider.** Deze voorwaarden vullen het FDS-Poortwachterproces aan. QTSP-erkenning, het vertrouwensanker en de certificaatprofielen (ETSI EN 319 412) volgen uit het eIDAS/EUDI-stelsel. Het programma GBO stelt hiervoor geen eigen afspraken voor.

### Stelselafspraken en voorzieningenbeheer

Alle nieuwe afspraken en voorzieningen moeten onderdeel worden van een stelsel. Het stelsel moet het beheer, de naleving en de monitoring organiseren.

Het programma GBO wil de voorgestelde aanvullende afspraken en voorzieningen zo veel mogelijk laten opnemen in bestaande stelsels. De PSA geeft hiervoor een eerste voorstel. Verdere uitwerking blijft nodig.

## 6 Impact op betrokken partijen

Bronhouders moeten enkele componenten implementeren en beheren om volgens het bronontsluitingsmodel gegevens te ontsluiten. Het programma GBO ondersteunt hen daarbij met referentiecomponenten en de referentievertaallaag.

Het programma GBO werkt ook ondersteunende middelen voor afnemers uit. Toch heeft de aansluiting ook voor hen gevolgen.

De volgende tabel geeft een eerste inschatting. De inschatting is gebaseerd op dit globaal ontwerp. Na de PSA, het technisch ontwerp en de technische requirements moet het programma GBO de inschatting opnieuw beoordelen.

| Partij | Impact | Toelichting |
| ------ | ------ | ----------- |
| Bronhouder | Een GraphQL-bronontsluiting aanbieden, rechtstreeks of via een vertaallaag/functioneel gelijkwaardig alternatief. FSC en FTV implementeren. Relevante catalogi beheren, waaronder de dienstencatalogus en semantische mappings voor de verschillende gegevensstromen. Voor het beheer hiervan gebruikt de bronhouder één decentraal configuratiecomponent. | Het programma GBO laat referentiecomponenten en een referentievertaallaag voor bronnen zonder GraphQL-API ontwikkelen. Bronhouders mogen functioneel gelijkwaardige alternatieven gebruiken. |
| Integrators en softwareleveranciers | Decentrale componenten in software en dienstverlening implementeren. De afspraken en standaarden van het stelsel volgen. | Een integrator moet voldoen aan de technische aansluitvoorwaarden. De bronhouder blijft verantwoordelijk voor de inhoud van de gegevens. |
| QTSP | Aansluiten op de ASI-provider. | De aansluiting volgt Europese standaarden. Een QTSP heeft deze aansluiting nodig voor de uitgifte van QEAA's. |
| Basisinrichting OOTS | GraphQL ondersteunen in OOTS-V. | OOTS-V heeft al een FSC-koppeling. |
| Private dienstverlener | Toetreden tot het stelsel, aansluiten op BSNk, een FSC Outway implementeren en koppelen met de toestemmingsvoorziening. | Partijen moeten het stelsel nog uitwerken. |
| Burger | Gegevens met private dienstverleners kunnen delen op basis van centraal beheerde toestemming. | De burger houdt verschillende ingangen en stelsels voor het delen van persoonsgegevens. Het burgerperspectief valt nog buiten de scope. |
