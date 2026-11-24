# Change Log

## Change Log v0.9.6

Van: versie [0.9.5](https://ictu.github.io/GBO-GO/0.9.5/) (september 2026) → Naar: 0.9.6 (oktober 2026)

De wijzigingen in v0.9.6 verduidelijken vooral de status van het ontwerp en de verantwoordelijkheden van het programma GBO, bronhouders, kanaalvoorzieningen en bestaande afsprakenstelsels. De voorgestelde oplossingsrichting is niet wezenlijk gewijzigd, maar de terminologie en beschrijving zijn aangescherpt om te voorkomen dat GBO als standaard, stelsel, voorziening, product of toekomstige beheerorganisatie wordt gelezen.

### Samenvatting in één oogopslag

| Onderdeel | Aard van de wijziging |
|---|---|
| Status en terminologie | GBO verwijst nu uitsluitend naar het programma. De voorgestelde oplossing heet het **bronontsluitingsmodel** en bestaat uit een **decentrale bronontsluiting** en **kanaalvoorzieningen**. |
| Afspraken en beheer | Duidelijker gemaakt dat het programma voorstellen doet. Aanvullende afspraken worden pas na besluitvorming onderdeel van bestaande standaarden en afsprakenstelsels; beheer moet bij bestaande stelsels en beheerorganisaties worden belegd. |
| Verantwoordelijkheden | Technische handelingen zijn waar mogelijk toegeschreven aan de verantwoordelijke actor of voorziening, in plaats van aan “GBO” als geheel. |
| EUDI-Wallet | De optionele voorziening voor PubEAA-uitgifte en de voorgestelde ASI-provider zijn preciezer afgebakend. De bronhouder blijft verantwoordelijk voor PubEAA-uitgifte en presentatie aan een dienstverlener valt buiten de uitgiftevoorziening. |
| OOTS | Verduidelijkt dat de Basisinrichting OOTS de protocolvertaling verzorgt en dat de optionele OOTS-adapter bedoeld is voor semantische vertaling. Publicatie van bewijsdiensten verloopt via bNC SDG en valt buiten het bronontsluitingsmodel. |
| Functies en componenten | GBO-basis is als naam voor de oplossing vervangen door decentrale bronontsluiting; de naam blijft alleen behouden voor het gelijknamige PSA-werkpakket. GBO-configuratie en GBO-vertaallaag zijn vervangen door bronconfiguratie en referentievertaallaag. De beschrijving van autorisatie, integratie en semantiek is aangescherpt. |
| Diagrammen en begrippenlijst | Diagrammen en begrippen zijn aangepast aan de nieuwe terminologie en verantwoordelijkheidsverdeling. Nieuwe begrippen zijn toegevoegd en vervallen GBO-specifieke begrippen zijn verwijderd. |

---

### Algemeen en hoofdstuk 1 — Inleiding

- Een afzonderlijke paragraaf **Terminologie en status** is toegevoegd.
- Vastgelegd is dat **GBO** uitsluitend verwijst naar het programma Gemeenschappelijke Bronontsluiting. Het programma onderzoekt en beproeft oplossingsrichtingen, doet voorstellen voor aanvullende afspraken en coördineert de ontwikkeling van referentiecomponenten en voorzieningen.
- De in dit globaal ontwerp voorgestelde oplossing heet nu het **bronontsluitingsmodel**. Dit model bestaat uit:
    1. een decentrale, herbruikbare bronontsluiting die iedere bronhouder zelf inricht of laat inrichten;
    2. kanaalvoorzieningen voor EUDI-Wallet, OOTS en private dienstverleners.
- Expliciet gemaakt dat het bronontsluitingsmodel zelf geen standaard, voorziening, organisatie of afsprakenstelsel is.
- Verduidelijkt dat voorgestelde aanvullende afspraken pas na besluitvorming onderdeel worden van de aangewezen standaarden en afsprakenstelsels.
- Formuleringen waarin “GBO” zelf gegevens ontsluit, autoriseert, pseudonimiseert of voorzieningen gebruikt, zijn vervangen door formuleringen die de verantwoordelijke actor of voorziening noemen.
- De documenthiërarchie en de verwijzing naar de uitwerking **Semantiek** zijn terminologisch aangescherpt.

---

### Hoofdstuk 2 — Voorgesteld bronontsluitingsmodel

- **Gemeenschappelijke bronontsluiting** is als naam voor een onderdeel vervangen door **decentrale bronontsluiting**.
- **Centrale voorzieningen** zijn in de oplossingsrichting hernoemd naar **kanaalvoorzieningen**. Daarmee wordt duidelijker dat deze voorzieningen een specifiek kanaal verbinden met de decentrale bronontsluiting.
- Verduidelijkt is dat het programma GBO voorstellen doet voor aanvullingen op GDI- en FDS-afspraken. De eerdere formulering kon de indruk wekken dat deze aanvullingen al door GBO waren vastgesteld.
- De keuzevrijheid voor bronhouders is preciezer geformuleerd: zij mogen de referentie-implementatie gebruiken of een eigen implementatie die aan dezelfde vastgestelde afspraken en standaarden voldoet.
- De scope is aangescherpt: het model ondersteunt de drie kanalen binnen de huidige programmascope; andere kanalen en gegevensstromen vallen daar nu buiten, maar hergebruik blijft mogelijk.

#### Figuur 1 — Het voorgestelde bronontsluitingsmodel

- Het bijschrift **Oplossingsrichting GBO** is vervangen door **Het voorgestelde bronontsluitingsmodel**.
- **GBO Basis** is in het diagram vervangen door **Decentrale bronontsluiting**.
- **GBO tools** zijn vervangen door de **optionele referentievertaallaag** of **optionele referentiecomponenten**.
- De legenda spreekt nu over componenten voor de decentrale bronontsluiting en voorgestelde kanaalvoorzieningen, in plaats van over voorzieningen die “GBO aanbiedt”.
- Voorbeelden van specifieke overheidsbronnen zijn uit de generieke diagrammen verwijderd.

---

### Hoofdstuk 3 — Interactiepatronen

#### Patroon A — EUDI-Wallet

- De voorziening voor PubEAA-uitgifte is explicieter als **optionele centrale voorziening** beschreven.
- Verduidelijkt is dat de bronhouder juridisch verantwoordelijk blijft voor de uitgifte. Het programma GBO en de voorziening voor PubEAA-uitgifte zijn zelf geen PubEAA-verstrekker.
- De uitgifte via OpenID4VCI is duidelijker onderscheiden van de latere presentatie via OpenID4VP. De voorziening voor PubEAA-uitgifte is niet betrokken bij die presentatie.
- De ASI-provider wordt nu als een **voorgestelde optionele voorziening** beschreven. De verify- en retrievediensten blijven inhoudelijk ongewijzigd.
- Formuleringen over autorisatie, beheer en varianten verwijzen nu naar de ASI-provider, bronhouder of het bronontsluitingsmodel in plaats van generiek naar GBO.

#### Patroon B — OOTS

- Verduidelijkt is dat **OOTS-V** het relevante onderdeel van de Basisinrichting OOTS voor bronhouders is. De onjuiste suggestie dat OOTS-V Nederlandse dienstverleners ondersteunt, is verwijderd.
- De rolverdeling tussen de Basisinrichting OOTS en de OOTS-adapter is aangescherpt:
    - de Basisinrichting OOTS vertaalt het Europese berichtenverkeer naar de bronontsluiting-API;
    - de optionele OOTS-adapter voert, als de bronhouder dit configureert, de semantische vertaling naar SDG-EDM uit.
- De OOTS-adapter wordt niet langer beschreven als voorziening voor protocolvertaling.
- Toegevoegd is dat bronhouders hun beschikbare bewijzen in het OOTS-netwerk bekendmaken via de dienstverlening van **bNC SDG**. Het bronontsluitingsmodel bevat hiervoor geen voorziening; dit valt buiten de programmascope.
- Het sequentiediagram gebruikt nu consequent **OOTS-adapter (optionele kanaalvoorziening)** en **decentrale bronontsluiting**.

#### Patroon C — Private dienstverleners (DvTP)

- Handelingen rond toestemming zijn toegeschreven aan het centrale toestemmingsregister en de centrale toestemmingsvoorziening, in plaats van aan GBO als programma.
- De eis van wettelijke verankering is niet langer in de beschrijving van de technische voorziening zelf opgenomen. De juridische voorwaarde voor toestemming als grondslag blijft elders in het document benoemd.
- Het sequentiediagram verwijst nu naar de **centrale toestemmingsvoorziening** in plaats van de **toestemmingsvoorziening GBO**.

---

### Hoofdstuk 4 — Generieke functies en stelselfuncties

- De generieke functies worden nu beschreven als functies **in het bronontsluitingsmodel**, niet als functies “van GBO”.
- Bij **F1 Identificatie & Authenticatie** is verduidelijkt welke voorzieningen burgers en organisaties identificeren en dat de pseudonimiseervoorziening het BSN pseudonimiseert.
- Bij **F2 Toegang & Interactie** is toegelicht dat één PBAC-implementatie verschillende soorten gegevensverzoeken en toegangsvoorwaarden kan verwerken. De referentie-implementatie is gekoppeld aan **OpenFTV**.
- Bij **F3 Gegevensvoorziening** is de **GBO-vertaallaag** hernoemd naar **referentievertaallaag**. Toegevoegd is dat deze bijvoorbeeld REST of SOAP naar GraphQL kan vertalen.
- De rolverdeling voor OOTS is ook hier aangescherpt: de optionele OOTS-adapter verzorgt de semantische omvorming; de Basisinrichting OOTS verzorgt de Europese verpakking en verbindingen.
- Bij **F4 Semantiek & Configuratie** is verduidelijkt dat het programma beschrijvingen laat opstellen, maar dat het beheer daarvan bij bestaande stelsels en beheerorganisaties moet landen. De bronspecifieke configuratie heet nu **bronconfiguratie**.
- Bij **F6 Grondslag & Beleid** is de algemene controle van grondslag en overige voorwaarden vóór de specifieke controle van toestemming geplaatst.
- Bij **F7 Orkestratie & Integratie** is expliciet gemaakt dat integratie aan de rand van de decentrale bronontsluiting plaatsvindt. Stelselfunctie **S07 Gegevensontsluiting** is aan het overzicht voor deze functie toegevoegd.
- Bij **F8 Beheer & Continuïteit** is de status van S09 aangepast: de standaarden voor logging en autorisatiebeslissingen zijn beschikbaar; afspraken voor ketenbrede toepassing blijven nodig.

---

### Hoofdstuk 5 — Te ontwikkelen componenten

- Het hoofdstuk spreekt nu over het **overzicht van het bronontsluitingsmodel** in plaats van over de “oplossing van GBO”.
- De drie soorten programmaresultaten zijn preciezer beschreven:
    1. **Voorstellen voor afspraken en standaarden** — deze gelden pas na vaststelling en borging in bestaande afsprakenstelsels.
    2. **Referentiecomponenten** — optioneel; een functioneel gelijkwaardig alternatief blijft mogelijk.
    3. **Kanaalvoorzieningen** — afhankelijk van de gegevensstroom verplicht of optioneel.
- **GBO-vertaallaag** en **GBO-configuratie** zijn in het componentenoverzicht vervangen door **referentievertaallaag** en **bronconfiguratie**.
- Voor PubEAA-uitgifte en de ASI-provider is verduidelijkt dat bronhouders ook zonder de voorgestelde voorziening aan hun verantwoordelijkheden kunnen voldoen.
- Bij de nog af te spreken of te realiseren onderdelen worden de betrokken partijen nu expliciet genoemd: programma GBO, afsprakenstelsels, bronhouders en afnemers.
- De beschrijving van de voorziening voor PubEAA-uitgifte beperkt zich tot uitgifte via OpenID4VCI; presentatie via OpenID4VP vindt daarna plaats tussen wallet en dienstverlener.
- De beschrijvingen van FSC, GraphQL, ODRL, BSNk PP en AS4/e-Delivery zijn aangepast zodat de verantwoordelijke actoren en voorzieningen expliciet zijn.

#### Figuur 5 — Het bronontsluitingsmodel met de voorgestelde componenten

- De figuurtitel en legenda gebruiken de termen **bronontsluitingsmodel**, **decentrale bronontsluiting** en **kanaalvoorzieningen**.
- **GBO Basis**, **GBO tools** en specifieke voorbeeldbronnen zijn vervangen door generieke, rolvaste benamingen.
- De toelichting maakt nu duidelijk dat de bronhouder met het decentrale configuratiecomponent de bronspecifieke configuratie van de kanaalvoorzieningen beheert.

---

### Hoofdstuk 6 — Impact op betrokken partijen

- De impactbeschrijving is terminologisch aangepast aan het bronontsluitingsmodel.
- Verduidelijkt is dat het programma GBO referentiecomponenten en een referentievertaallaag **laat ontwikkelen**. Bronhouders blijven verantwoordelijk voor de inrichting en mogen functioneel gelijkwaardige alternatieven gebruiken.

---

### Bijlage — Begrippenlijst

- Nieuwe begrippen toegevoegd voor **bronconfiguratie**, **bronontsluitingsmodel**, **decentrale bronontsluiting**, **kanaalvoorziening** en **referentievertaallaag**.
- Begrippen uit de projectstartarchitectuur toegevoegd voor **architectuurbesluit**, **architectuurprincipe**, **GBO-basis**, **kanaalwerkpakket**, **ontwerpprincipe**, **open besluit**, **projectstartarchitectuur** en **werkpakket**. Daarmee blijft de begrippenlijst de centrale bron voor beide architectuurdocumenten.
- **GBO-configuratie**, **GBO-vertaallaag** en **gemeenschappelijke bronontsluiting** zijn als namen voor onderdelen van de oplossing verwijderd of vervangen. **GBO-basis** is niet langer een naam voor de oplossing, maar blijft behouden als afgesproken naam van een werkpakket in de projectstartarchitectuur.
- De definitie van **GBO** beschrijft nu uitsluitend het programma en benoemt expliciet wat GBO niet is.
- De definitie van **OOTS-adapter** beperkt de functie tot de optionele semantische vertaling; protocolvertaling is geen functie van deze adapter.
- Definities van onder meer FDS, GraphQL, referentiecomponenten, kanalen en toestemming zijn aangepast aan de nieuwe terminologie en verantwoordelijkheidsverdeling.

---

### Documentpresentatie en navigatie

- De printversie bevat nu een inhoudsopgave zonder dubbele hoofdstuknummering.
- De koptekst van de printversie is gecorrigeerd naar **GBO - Globaal Ontwerp**.
- De navigatie verwijst nu rechtstreeks naar het afzonderlijke **Technisch Ontwerp**.

---

## Change Log v0.9.5

Van: versie [0.9.4](https://ictu.github.io/GBO-GO/0.9.4/) (augustus 2026) → Naar: 0.9.5 (september 2026)

De wijzigingen in v0.9.5 verduidelijken vooral de oplossingsrichting en de verantwoordelijkheidsverdeling. De inhoud van de interactiepatronen, generieke functies, stelselfuncties en impact op betrokken partijen is niet wezenlijk gewijzigd.

### Samenvatting in één oogopslag

| Onderdeel | Aard van de wijziging |
|---|---|
| Terminologie | GBO wordt aangeduid als programma in plaats van project. |
| Oplossingsrichting | Expliciet onderscheid aangebracht tussen de gemeenschappelijke bronontsluiting bij de bronhouder en centrale voorzieningen per kanaal. |
| GDI en FDS | Verduidelijkt dat de gemeenschappelijke bronontsluiting voortbouwt op afspraken en standaarden van GDI en FDS en dat aanvullingen daarop daar bij voorkeur worden geborgd. |
| Verantwoordelijkheid bronhouder | Explicieter gemaakt dat de bronhouder de gemeenschappelijke bronontsluiting zelf inricht of dit door een leverancier laat doen. GBO realiseert een referentie-implementatie als werkend voorbeeld. |
| Centrale voorzieningen | Verduidelijkt welke voorzieningen GBO centraal coördineert voor EUDI-Wallet, OOTS en DvTP, en of het gebruik daarvan optioneel of verplicht is. |
| Scope en hergebruik | De drie huidige toepassingen worden nu als kanalen benoemd. De afspraken, koppelvlakken en voorzieningen worden zo ingericht dat toekomstige kanalen en gegevensstromen dezelfde bronontsluiting kunnen hergebruiken. |
| Diagrammen | Figuur 1 en figuur 5 maken nu expliciet onderscheid tussen de bronhouder, decentrale bronontsluiting en centrale voorzieningen. |

---

### Algemeen

- De aanduiding **"project Gemeenschappelijke Bronontsluiting"** is gewijzigd in **"programma Gemeenschappelijke Bronontsluiting"**.
- De terminologie rond *gegevensstromen* en *kanalen* is aangescherpt. EUDI-Wallet, OOTS en private dienstverleners (DvTP) worden in de oplossingsrichting als drie **kanalen** onderscheiden. Een kanaal kan gebruikmaken van de gemeenschappelijke bronontsluiting voor één of meer gegevensstromen.
- In de diagrammen is duidelijker aangegeven welke onderdelen bij de bronhouder horen en welke voorzieningen centraal beschikbaar worden gesteld.

---

### Hoofdstuk 2 — Voorgestelde oplossingsrichting

De paragraaf **Oplossingsrichting** is grotendeels herschreven en nu expliciet opgebouwd uit twee samenhangende onderdelen.

#### 1. Gemeenschappelijke bronontsluiting

- Het begrip **gemeenschappelijke bronontsluiting** is expliciet geïntroduceerd en afgebakend.
- Verduidelijkt is dat bronhouders hun gegevens ontsluiten volgens bestaande afspraken en standaarden van **GDI** en **FDS**, aangevuld met afspraken die voor GBO nodig zijn.
- De intentie is toegevoegd om deze aanvullingen uiteindelijk te borgen in de GDI en/of het FDS, zodat de gemeenschappelijke bronontsluiting onderdeel wordt van bestaande afsprakenstelsels in plaats van een afzonderlijk GBO-specifiek stelsel te vormen.
- Expliciet gemaakt dat dezelfde ontsluiting kan worden hergebruikt door verschillende typen afnemers en door de kanalen EUDI-Wallet, OOTS en private dienstverleners. Ook toekomstige kanalen kunnen deze ontsluiting gebruiken.
- De verantwoordelijkheid van de bronhouder is verduidelijkt: de bronhouder richt de gemeenschappelijke bronontsluiting zelf in of laat dit door een leverancier doen.
- De bestaande uitgangspunten van één API, configuratie per gegevensstroom, PBAC en betrouwbare standaarden voor versleuteling, identificatie, authenticatie en logging zijn in deze beschrijving samengebracht.
- Toegevoegd is dat het programma GBO een **referentie-implementatie** van de gemeenschappelijke bronontsluiting laat realiseren. Gebruik daarvan is niet verplicht; een bronhouder mag een eigen oplossing gebruiken die aan dezelfde afspraken en standaarden voldoet.

#### 2. Centrale voorzieningen

- De centrale voorzieningen zijn als afzonderlijk onderdeel van de oplossingsrichting beschreven.
- Verduidelijkt is dat deze voorzieningen de drie kanalen verbinden met de gemeenschappelijke bronontsluiting.
- Het programma GBO **coördineert de realisatie** van deze voorzieningen, zodat bronhouders deze niet ieder afzonderlijk hoeven te ontwikkelen.
- Expliciet gemaakt dat sommige voorzieningen nieuw worden gerealiseerd en dat voor andere bestaande voorzieningen worden aangepast om met de gemeenschappelijke bronontsluiting te kunnen werken.
- De voorzieningen zijn compact per kanaal beschreven:
    - **EUDI-Wallet:** Authentic Source Interface voor QTSP's en een voorziening voor PubEAA-uitgifte. Gebruik is optioneel.
    - **OOTS:** OOTS-adapter voor de aansluiting op de Basisinrichting OOTS, inclusief een optionele semantische vertaalfunctie. Gebruik is optioneel.
    - **Private dienstverleners (DvTP):** toestemmingsvoorziening en pseudonimiseervoorziening. Deze zijn verplicht voor private dienstverleners die van deze gegevensstroom gebruikmaken.
- Toegevoegd is hoe de centrale voorzieningen naar verwachting worden geborgd:
    - voorzieningen voor OOTS worden geborgd in de GDI;
    - voor de voorzieningen voor de EUDI-Wallet wordt dezelfde benadering voorgesteld;
    - voor de toestemmingsvoorziening moet nog worden bepaald waar deze wordt geborgd.
- De slottekst van hoofdstuk 2 is aangepast. Niet langer alleen andere *gegevensstromen*, maar ook andere **kanalen** worden expliciet genoemd als mogelijke toekomstige gebruikers van dezelfde afspraken, koppelvlakken en voorzieningen.

#### Figuur 1 — Oplossingsrichting GBO

- Een afzonderlijke begrenzing **Bronhouder** is toegevoegd rondom de overheidsbron en de GBO-basis. Daarmee is zichtbaar gemaakt dat de gemeenschappelijke bronontsluiting een verantwoordelijkheid van de bronhouder is.
- Het diagram maakt nu onderscheid tussen:
    - groen: decentrale componenten voor de gemeenschappelijke bronontsluiting;
    - oranje: centrale voorzieningen;
    - grijs: bestaande voorzieningen waarop GBO aansluit.
- De eerdere aanduiding **"Bronontsluiting voor QTSP (Authentic Source Interface)"** is vervangen door **"Authentic Source Interface voor QTSP's"**, in lijn met de tekst van de oplossingsrichting.
- De toelichting onder het diagram is aangepast aan dit onderscheid.

---

### Hoofdstuk 5 — Te ontwikkelen componenten

#### Figuur 5 — Overzicht voorgestelde oplossing

- Ook in de gedetailleerde overzichtsplaat is een afzonderlijke begrenzing **Bronhouder** toegevoegd rondom de overheidsbron en GBO-basis.
- Hiermee wordt duidelijker dat de generieke bronontsluiting, configuratie en eventuele GBO-vertaallaag bij de bronhouder horen en niet centrale GBO-voorzieningen zijn.
- De legenda is terminologisch aangepast: **"optionele centrale aansluitvoorzieningen"** is vervangen door **"optionele centrale voorzieningen"**.
- De inhoudelijke indeling in afspraken en standaarden, referentiecomponenten en centrale voorzieningen blijft ongewijzigd.

---

## Change Log v0.9.4

Van: versie [0.9.3](https://ictu.github.io/GBO-GO/0.9.3/) (augustus 2026) → Naar: 0.9.4 (augustus 2026)

v0.9.4 bevat voornamelijk verduidelijkingen naar aanleiding van reviewfeedback op v0.9.3. De oplossingsrichting zelf is niet gewijzigd, maar de status, keuzevrijheid en verplichting van onderdelen is explicieter beschreven.

### Hoofdstuk 5 — Te ontwikkelen componenten

- Expliciet gemaakt dat GBO **drie soorten resultaten** levert:
    1. **Afspraken en standaarden** — verplicht voor deelnemers waarop deze afspraken van toepassing zijn.
    2. **Referentiecomponenten** — optioneel; een bronhouder mag ook een functioneel gelijkwaardig alternatief gebruiken.
    3. **Centrale voorzieningen** — afhankelijk van de gegevensstroom verplicht of optioneel.
- Een tabel toegevoegd die per voorziening aangeeft:
    - voor welke gegevensstroom deze bedoeld is;
    - om welk soort voorziening het gaat;
    - of gebruik verplicht of optioneel is;
    - wie de beheerder is of waar dit nog moet worden bepaald.
- Expliciet gemaakt dat publieke bronhouders die een gegevensstroom via GBO ontsluiten de bijbehorende afspraken en standaarden moeten volgen.
- Voor private dienstverleners verduidelijkt dat deelname aan de DvTP-stroom vrijwillig is, maar dat bij deelname gebruik van de toestemmingsvoorziening en BSNk PP verplicht is.

### Verduidelijking van keuzevrijheid en verplichtingen

Op verschillende plaatsen in het document is vrijblijvende formulering met **"kan"** vervangen door preciezere formuleringen die aangeven of iets een keuze, mogelijkheid of verplichting is. Onder meer:

- keuzevrijheid voor bronhouders bij het gebruik van referentiecomponenten;
- hergebruik voor andere gegevensstromen;
- keuze tussen PubEAA-uitgifte en diensten van een QTSP;
- gebruik van de ASI-provider;
- semantische mapping bij OOTS;
- verplicht gebruik van de toestemmings- en pseudonimiseervoorziening binnen DvTP;
- gebruik van het toestemmingsregister als PIP;
- aansluitvoorwaarden voor QTSP's;
- gebruik van alternatieve implementaties door bronhouders.

Waar een ontwerpkeuze nog niet is gemaakt, wordt dit expliciet aangegeven, bijvoorbeeld met **"nog te bepalen (zie PSA)"**.

---

## Change Log v0.9.3
**Van:** versie [0.9.2](https://ictu.github.io/GBO-GO/0.9.2/) (juni 2026) → **Naar:** 0.9.3 (augustus 2026)

Dit is geen uitputtende opsomming van elke los gewijzigde zin, maar een overzicht van wat er conceptueel/structureel is veranderd, per hoofdstuk/paragraaf.

---

### Samenvatting in één oogopslag

| Onderdeel | Aard van de wijziging | Details |
|---|---| --- |
| Structuur document | +1 hoofdstuk (Impact op partijen), doorlopende nummering, uitgebreidere inleidingen per generieke functie | [detailbeschrijving](#algemeen-opzet) |
| Uitgangspunten | GDI en "Keuzevrijheid" als nieuwe expliciete uitgangspunten | [detailbeschrijving](#algemeen-opzet) |
| Patroon A (EUDI) | ASI-P met verify/retrieve-rol vervangt de twee-varianten-beschrijving; OOTS-catalogi genoemd | [detailbeschrijving](#patroon-a-eudi-wallet) |
| Patroon B (OOTS) | Sterk uitgebreid: OOTS-V/OOTS-Adapter, sectorale aansluitingen, semantische omvorming; TIP-verwijzing verwijderd | [detailbeschrijving](#patroon-b-oots) |
| Patroon C (DvTP) | Terminologie "toestemmingsregister"/"-voorziening" aangescherpt; extra afrondstap in diagram | [detailbeschrijving](#patroon-c-dvtp) |
| Generieke functies | Nieuwe GDI-koppeltabel; minder harde koppeling aan OPA/Rego; diverse status-updates | [detailbeschrijving](#hoofdstuk-4-generieke-functies-en-stelselfuncties) |
| Componenten (H5) | Nieuwe kleurcodering/legenda in overzichtsplaat; LDV toegevoegd; Query Template Registry → dienstencatalogus; nieuwe slotparagraaf over stelselbeheer | [detailbeschrijving](#hoofdstuk-5-te-ontwikkelen-componenten) |
| Impact op partijen | Volledig nieuw hoofdstuk 6 | [detailbeschrijving](#hoofdstuk-6-impact-op-betrokken-partijen-volledig-nieuw) |

---

### Algemeen / opzet

- **Nieuw hoofdstuk 6 — "Impact op betrokken partijen"** toegevoegd. Dit is de belangrijkste structurele toevoeging: een tabel die per partij (Bronhouder, QTSP, Basisinrichting OOTS, Private dienstverleners, Burger) de verwachte impact en toelichting beschrijft.
- **Nieuwe bijlagen**: **Begrippenlijst** en deze **Change Log**.
- Hoofdstukken zijn nu **doorlopend genummerd** (1 Inleiding, 2 Voorgestelde oplossingsrichting, … 6 Impact op betrokken partijen) — in 0.9.2 hadden hoofdstukken geen nummer in de titel.
- Uitgangspunten (§1) zijn uitgebreid en herschreven:
    - GDI is nu als **apart uitgangspunt** benoemd (met toelichting op de 4 domeinen: toegang, interactie, gegevensuitwisseling, infrastructuur).
    - FDS-uitgangspunt is uitgebreider toegelicht, inclusief expliciete koppeling naar GDI-standaarden en het voorbeeld "Federatieve Toegangsverlening" (AuthZen, aangeboden bij Forum Standaardisatie).
    - Nieuw uitgangspunt **"Keuzevrijheid"** toegevoegd: bronhouders zijn vrij om GBO-componenten te gebruiken, te combineren met eigen oplossingen, of niet te gebruiken.
    - "Federatief Datastelsel"-omschrijving is losgekoppeld van specifieke stelselfuncties (FSC/FTV worden niet meer als uitgangspunt-bullet genoemd, maar verderop uitgewerkt).
- §1 Inleiding verwijst nu expliciet door naar de tabbladen "Gemeenschappelijke Bronontsluiting" (doelen) en "Context" (juridisch/organisatorisch kader).
- Verwijzing naar **demo** waar de voorgestelde oplossing in een demo-omgeving getoond wordt.

<span style='font-size: small;'>[terug naar overzicht](#samenvatting-in-een-oogopslag)</span>

---

### Hoofdstuk 2 — Voorgestelde oplossingsrichting

- **Nieuwe subparagraaf "Knelpuntenanalyse"** toegevoegd vóór de oplossingsrichting zelf: benoemt expliciet de vier knelpunten (verschillende gegevenssets, autorisatiemodellen, protocollen, wet- en regelgeving per gegevensstroom) en de bijbehorende oplossingsrichting in bullets.
- Oplossingsrichting-tekst is aangescherpt:
  - "generieke API" is vervangen door **"één API"**.
  - Nieuwe zin toegevoegd: als een bronhouder de koppeling (nog) niet zelf kan inrichten, biedt GBO instrumenten om toch gebruik te maken van de componenten.
  - De rol van de centrale voorzieningen per gegevensstroom (ASI/PubEAA-provider voor EUDI, semantische mapping voor OOTS, toestemmings-/pseudonimiseervoorziening voor DvTP) wordt nu expliciet in lopende tekst toegelicht, in plaats van alleen in het diagram.
- **Figuur 1** (oplossingsrichting-diagram):
  - Subgraph-label "SDG / OOTS" → **"OOTS"**.
  - Kleurstelling van bron/burger-knopen gewijzigd (van groen naar lichtblauw).
  - Bijschrift uitgebreid met legenda-achtige toelichting: "de grijze componenten zijn actoren of bestaande voorzieningen die hergebruikt worden."

  <span style='font-size: small;'>[terug naar overzicht](#samenvatting-in-een-oogopslag)</span>

---

### Hoofdstuk 3 — Interactiepatronen

#### Patroon A (EUDI-Wallet)
- Nieuwe zin: PubEAA's en QEAA's hebben **juridisch dezelfde betekenis**.
- De rolbeschrijving van GBO is verduidelijkt: GBO ondersteunt de PubEAA-uitgevende instantie én de rol van **Authentic Source Interface Provider (ASI-P)**, die zowel een *verify*- als een *retrieve*-dienst kan bieden. De oude tekst met twee losse "varianten" (burger contracteert QTSP / bronhouder contracteert QTSP) is vervangen door deze bredere ASI-P-beschrijving.
- Nieuwe alinea over de **OOTS common services**: mogelijke inzet voor de attributencatalogus (Semantic Repository) en leverancierscatalogus (Data Service Directory), en de rol van GBO daarin (nog in onderzoek).
- Sequentiediagram (Figuur 2): participant "Verificatiedienst" hernoemd naar **"Verify-/retrievedienst (Authentic Source Interface)"**; extra notitie toegevoegd over ISO15000 (geen autorisatie/authenticatie nodig).
- Kader "Afstemming lopend" is verbreed: spreekt nu over "alle mogelijke varianten" i.p.v. alleen PubEAA vs. QTSP.

<span style='font-size: small;'>[terug naar overzicht](#samenvatting-in-een-oogopslag)</span>

#### Patroon B (OOTS)
- **Grotendeels herschreven en flink uitgebreid.** Oude tekst (RINIS/BZK als nationaal OOTS-toegangspunt) is vervangen door een uitgebreidere beschrijving:
  - Sectorale aansluitingen (bv. EMREX-brug) en eigen aansluitingen worden nu genoemd als alternatief voor de Basisinrichting OOTS (buiten scope van dit ontwerp).
  - Stichting RINIS wordt genoemd als leverancier, in opdracht van BZK/EZK.
  - Nieuwe alinea over de Europese transportlaag (eDelivery, AS4, eBMS, Regrep) en het **OOTS Exchange Data Model (OOTS EDM)**.
  - Nieuwe alinea over **semantische omvorming**: niet verplicht vanuit de SDG-verordening, maar wel gestimuleerd; voorbeeld uniform bewijs van geboorte; GBO kan deze transformatie namens de bronhouder uitvoeren.
  - De oude passage over de **TIP-basisfunctie "Delivering messages"** (uitleg dat dit buiten scope van GBO valt) is **verwijderd**.
- Sequentiediagram (Figuur 3): participant "GBO (GBO voorziening)" hernoemd naar **"OOTS adapter (GBO voorziening)"**; een aparte stap voor **semantische mapping** is toegevoegd (nu stap ④, tussen ontvangst en bronbevraging), met als gevolg herschikte stapnummers t.o.v. 0.9.2.

<span style='font-size: small;'>[terug naar overzicht](#samenvatting-in-een-oogopslag)</span>

#### Patroon C (DvTP)
- Terminologie "toestemmingen**register**" is doorgaans vervangen door **"toestemmingsregister"**, en "GBO kiest voor een centraal toestemmingenregister" is herschreven naar **"GBO stelt een centrale toestemmingsvoorziening voor"**.
- De zin over real-time validatie van het consent-id op moment van uitvraag is vereenvoudigd/ingekort.
- Toestemmingsportaal wordt nu specifiek gekoppeld aan een centraal portaal in de openingsalinea (was voorheen pas later genoemd).
- Fase 2-titel in het sequentiediagram aangevuld met **"(per bron een verzoek)"**.
- Sequentiediagram (Figuur 4): kleine technische aanpassingen (consent-id-validatie response, VI/VP-doorgifte in redirect) en een extra laatste stap **"DV → Burger: Levert dienst"** toegevoegd.

<span style='font-size: small;'>[terug naar overzicht](#samenvatting-in-een-oogopslag)</span>

---

### Hoofdstuk 4 — Generieke functies en stelselfuncties

- **Nieuwe tabel** die de generieke functies koppelt aan de vier **GDI-domeinen** (Toegang, Interactie, Gegevensuitwisseling, Infrastructuur), met een toelichtende alinea over hoe dit aansluit bij de NORA/GDI-architectuur en vergelijkbare indelingen (bv. Gezondheidsinformatiestelsel). Dit ontbrak volledig in 0.9.2.
- Elke generieke functie (**F1 t/m F8**) heeft nu een **uitgebreide, inhoudelijke inleidende alinea** i.p.v. de korte cursieve one-liner uit 0.9.2. Bijvoorbeeld:
  - F1: nu met uitleg over BSN/OIN-identificatie, pseudonimisering, betrouwbaarheidsniveaus en **identity matching**.
  - F2: uitleg over PBAC en dat bronhouders een eigen implementatie mogen gebruiken als deze de centrale beleidsregels toepast.
  - F3: uitgebreide uitleg over GraphQL, GBO-vertaallaag, OOTS-adapter en attestatie-uitgifte.
  - F7: nu expliciet vermeld dat procesorkestratie voor de huidige use cases (nog) niet relevant is.
  - F8: expliciet vermeld dat beheer & continuïteit nog niet diepgaand is uitgewerkt.
- Wijzigingen in specifieke stelselfuncties:
  - **S03**: status uitgebreid met "Identity Matching nog in onderzoek".
  - **S05**: status "OPA/Rego" vervangen door **"AuthZEN NLGov profiel beschikbaar; FTV in ontwikkeling"** — minder hard gekoppeld aan één specifieke policy-engine.
  - **S06**: tekst "OCI-bundles"/PAP-omschrijving vrijwel gelijk gebleven, maar "OPA/Rego-policy-bundles" is verkort naar **"policy-bundles"** (technologieneutraler).
  - **S07**: gap/actie "Query Template Registry" vervangen door **"Dienstencatalogus"**.
  - **S08**: naam ingekort van "OOTS-adapter (Grensoverschrijdend)" naar **"OOTS-adapter"**; gap/actie uitgebreid met GraphQL-ondersteuning in OOTS-V en mapping naar het Evidence Exchange Data Model.
  - **S09**: status nu **"FSC Logging en Logboek Dataverwerking (LDV) beschikbaar"** i.p.v. het generieke "Standaarden beschikbaar".
  - **S11**: naam gewijzigd van "Attesteringsuitgifte (PubEAA / QEAA)" naar **"Attesteringsuitgifte (voor EUDI-wallet)"**; nu gekoppeld aan **F3 én F7** (was alleen F3).
- Het totaaloverzicht (samenvattende tabel) is dienovereenkomstig bijgewerkt.

<span style='font-size: small;'>[terug naar overzicht](#samenvatting-in-een-oogopslag)</span>

---

### Hoofdstuk 5 — Te ontwikkelen componenten

- **Figuur 5 (Overzichtsplaat)** is inhoudelijk het meest veranderde onderdeel:
  - Volledig **nieuwe kleurcodering met legenda**: groen = generieke decentrale bronontsluiting, paars = centrale voorzieningen (optioneel, bronhouder mag alternatief kiezen), rood = centrale voorzieningen (verplicht bij deze gegevensstroom), grijs = bestaande voorzieningen. In 0.9.2 was er alleen een generiek onderscheid tussen "gbo"- en "generieke" kleur zonder deze semantiek.
  - ASI-provider is nu expliciet "verify/retrieve dienst" i.p.v. alleen "verify dienst".
  - Koppeling OOTS-adapter ↔ Basisinrichting OOTS is nu **GraphQL** i.p.v. REST-JSON.
  - Koppeling GBO ↔ toestemmingsvoorziening is nu gestippeld en gelabeld als **PIP**-relatie i.p.v. een gewone REST-JSON-lijn.
- **Bouwstenen die hergebruikt worden**:
  - **LDV (Logboek Dataverwerking)** is toegevoegd als nieuwe herbruikbare bouwsteen.
  - **OPA/Rego** is niet langer als aparte, met naam genoemde bouwsteen opgevoerd; verwijzingen zijn generieker gemaakt ("een policy-taal zoals OPA/Rego").
  - GraphQL-bouwsteen: "Query Template Registry" vervangen door **"dienstencatalogus"**.
  - OAuth 2.0/OIDC-bouwsteen: aangevuld met een zin over **Identity Matching** wanneer het authenticatiemiddel geen BSN bevat.
- Paragraaf "GraphQL als selectief bevragingsmechanisme": de losse subparagraaf over de **Query Template Registry** is vervallen; hiervoor in de plaats staat nu een bullet over de **dienstencatalogus**.
- Paragraaf "OOTS-aansluiting": "OOTS-adapter" is hernoemd naar **"protocolvertaler"**, met toevoeging "en vice-versa" (dus ook de retourroute).
- **Nieuwe slotparagraaf "Stelselafspraken en voorzieningenbeheer"** toegevoegd: benoemt dat alle te ontwikkelen voorzieningen en afspraken in een stelsel moeten landen, met beheer, naleving en monitoring — verder uit te werken in de PSA.

<span style='font-size: small;'>[terug naar overzicht](#samenvatting-in-een-oogopslag)</span>

---

### Hoofdstuk 6 — Impact op betrokken partijen *(volledig nieuw)*

Compleet nieuw hoofdstuk met een tabel die per partij de impact en toelichting beschrijft:

| Partij | Kern van de impact |
|---|---|
| Bronhouder | Implementatie GraphQL API, FSC, FTV; beheer van catalogi (dienstencatalogus, semantische mapping, data request registry) |
| QTSP | Aansluiting op de Authentic Source Interface |
| Basisinrichting OOTS | Ondersteuning van GraphQL nodig in OOTS-V |
| Private dienstverleners | Toetreden tot het (nog uit te werken) stelsel, aansluiten op BSNk, FSC outway, koppeling toestemmingsvoorziening |
| Burger | Kan gegevens delen op basis van centraal beheerde toestemming, maar houdt losse ingangen/stelsels per partij — burgerperspectief is nog niet in scope |

<span style='font-size: small;'>[terug naar overzicht](#samenvatting-in-een-oogopslag)</span>

---
