# Globaal Ontwerp Gemeenschappelijke Bronontsluiting

_ICTU | Juni 2026_

> LET OP: Het project gemeenschappelijke bronontsluiting is in ontwikkeling en de documentatie volgt dit. De huidige versie van dit globaal ontwerp is daarom niet definitief. De status van de documentatie is [hier](https://ictu.github.io/GBO/latest/#reviewproces) te vinden.

## Inleiding

### Globaal ontwerp

In dit globaal ontwerp wordt op hoofdlijnen uiteengezet welke stelselfuncties nodig zijn voor een gemeenschappelijke bronontsluiting en hoe deze ingericht kunnen worden. Het doel is om input op de voorgestelde oplossingsrichting op te halen en het ontwerp vast te stellen, zodat dit als basis kan dienen voor verdere uitwerking in de volgende documenten:

- Projectstartarchitectuur: kaders en richtlijnen voor het ontwerp en de inrichting van de stelselfuncties.  
- Technisch ontwerp: technisch ontwerp van de benodigde voorzieningen.  
- Technische requirements: de specificaties van de in te richten componenten.  
- Semantiek: informatiemodellen en begrippenkaders van de gegevens die uitgewisseld worden, zowel de gegevens die opgevraagd worden, als gegevens die nodig zijn voor veilige, betrouwbare uitwisseling (zoals GraphQL-schema's, mappings tussen verschillende formaten, toestemmingen, etc.).  

### Uitgangspunten

- Europees interoperabel: Europese afspraken en standaarden (o.a. EIF, eIDAS, OOTS en EUDI) en de Nederlandse invulling hiervan, zoals de NL-Wallet en het centrale Nederlandse OOTS-toegangspunt.  
- Federatief Datastelsel (FDS): Relevante en toepasbare FDS-afspraken en standaarden, zoals FSC en FTV voor gefedereerde connectiviteit en toegang, voor publiek-publieke bronontsluiting.  
- Generieke Digitale Infrastructuur (GDI): Relevante en toepasbare GDI-afspraken, standaarden en voorzieningen, zoals DigiD en het BSN-koppelregister voor polymorfe pseudoniemen (BSNk PP).  
- Beleidsgedreven autorisatie (PBAC): PBAC-architectuur voor autorisatie en toegang.  
- Waardengedreven inrichting: De organisatorische en technische inrichting is gebaseerd op publieke waarden en op het principe van een gelijk speelveld bij de rollen en verantwoordelijkheden.  


### Leeswijzer

Het globaal ontwerp wordt als volgt uitgewerkt:

- [Hoofdstuk 2](#2-voorgestelde-oplossingsrichting) schetst de oplossingsrichting voor de gemeenschappelijke bronontsluiting  
- [Hoofdstuk 3](#3-interactiepatronen) beschrijft de interactiepatronen waar de gemeenschappelijke bronontsluiting invulling aan geeft  
- [Hoofdstuk 4](#4-generieke-functies-en-stelselfuncties) beschrijft de generieke functies die nodig zijn en de stelselfuncties waarmee dit mogelijk wordt  
- [Hoofdstuk 5](#5-te-ontwikkelen-componenten) gaat in op de stelselfuncties die nog ontwikkeld moeten worden  


## Voorgestelde oplossingsrichting

Dit hoofdstuk beschrijft de voorgestelde oplossingsrichting voor GBO. Het onderstaande diagram vormt hiervoor de basis.

<figure>
``` mermaid
--8<-- "diagrammen/gbo_swimlanes_simpel.mmd"
```
<figcaption>Figuur 1: Oplossingsrichting GBO.</figcaption>
</figure>

Voor GBO stellen bronhouders hun gegevens bloot via een generieke API, die voor verschillende gegevensverzoeken gebruikt kan worden. Een nieuw gegevensverzoek kan dan met configuraties ingesteld worden, in plaats van het moeten inrichten en beheren van een nieuw endpoint. Generieke ontsluiting vraagt extra autorisatieregels, die met beleidsregels (eventueel ook federatief) in te stellen moeten zijn. Het koppelvlak moet met een betrouwbare en veilige standaard beschikbaar gesteld worden; zaken als versleuteling, identificatie, authenticatie en logging moeten daarin geborgd zijn. Voor de verschillende gegevensstromen zorgen centrale voorzieningen voor aansluiting op bestaande protocollen en vertrouwensstelsels.  

In de volgende paragrafen worden deze componenten uitgewerkt en wordt toegewerkt naar een invulling daarvan.  

## Interactiepatronen

GBO ondersteunt drie interactiepatronen, elk met eigen actoren, grondslagen en protocollen. De drie interactiepatronen worden in de volgende paragrafen geschetst.

### Patroon A - burger gebruikt EUDI-Wallet

Een burger vraagt een attestatie op bij een overheidsbron als verifieerbare credential (VC) voor opname in zijn EUDI-Wallet. De wallet initieert een OpenID4VCI-ophaalverzoek richting GBO, dat de bron bevraagt en het resultaat retourneert als SD-JWT VC of mdoc (ISO 18013-5). De attestatie is cryptografisch gezegeld en kan daarna door de burger worden gepresenteerd aan dienstverleners via OpenID4VP, zonder verdere tussenkomst van GBO.

GBO ondersteunt functioneel/technisch in dit patroon de rol van PubEAA-uitgevende instantie, maar is zelf geen PubEAA verstrekker. De verificatiedienst voor QTSP's die attestaties willen verifiëren is een aanvullend GBO-component. Beide diensten maken gebruik van een autorisatiedienst die ook door GBO aangeboden wordt.

Voor attestatie-uitgifte via een QTSP (QEAA) zijn twee varianten mogelijk:

1. **Burger contracteert QTSP:** de burger levert attributen aan bij de QTSP, waarna de QTSP verifieert bij de verificatiedienst van de bronhouder of de aangewezen intermediair. Deze variant moet door bronhouders ondersteund worden en hiervoor wil GBO een centrale verify-dienst beschikbaar stellen.  
2. **Bronhouder contracteert QTSP:** de bronhouder verwijst de burger naar de QTSP, waarna de QTSP de attributen ophaalt bij de retrieval-dienst van de bronhouder of de aangewezen intermediair. Er is geen wettelijke verplichting voor bronnen om dit te ondersteunen, maar een retrieval-dienst kan functioneel dezelfde implementatie (Authentic Source Interface provider) gebruiken als de verify-dienst die in de eerste variant wordt gebruikt.  

De attribuutcatalogus die de Europese Commissie op basis van OOTS Common Services implementeert, is relevant voor zowel PubEAA als QEAA: GBO wil vanuit de semantiek-uitwerking aansluiten bij deze catalogus voor de definitie van attributen, informatiemodellen en endpoints.

> **Afstemming lopend:** Over de keuze tussen PubEAA-uitgifte door overheidsbronnen en attestatie via een QTSP loopt nog afstemming. GBO positioneert beide varianten als ondersteund; de governance-keuze wordt extern belegd.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-EUDI-Wallet.mmd"
```
<figcaption>Figuur 2: Interactiepatroon burger deelt gegeven via EUDI-Wallet met dienstverlener.  
NB: een gegeven kan als PubEAA (rechtstreeks van overheidsbron) of QEAA (via QTSP) in de Wallet komen.
</figcaption>
</figure>

### Patroon B - grensoverschrijdend verzoek via OOTS

Een Europese overheidsdienst stuurt via het OOTS-netwerk een Evidence Request voor een Nederlandse burger. BZK heeft RINIS aangewezen als nationaal OOTS-toegangspunt, waar de OOTS-basisinrichting in beheer is. Die verzorgt de toestemmingsinteractie met de burger en de identiteitsvaststelling, en geeft de payload als GraphQL-request door aan GBO. GBO verzorgt de bronontsluiting en de semantische mapping naar het SDG Evidence-formaat. Bronhouders zien uitsluitend de GBO-API en hoeven geen OOTS-kennis te hebben. De terugkoppeling volgt de omgekeerde route: GBO retourneert aan de OOTS-basisinrichting, waar het bericht in AS4 wordt verpakt.

De cross-border uitwisseling tussen nationale OOTS-aansluitpunten sluit aan bij de TIP-basisfunctie *Delivering messages* (elektronisch aangetekende bezorging), die het juridische en technische kader biedt voor betrouwbare beveiligde berichtuitwisseling tussen organisaties in verschillende lidstaten. Dit is echter buiten scope van GBO: de afhandeling van de OOTS-berichten gebeurt via de OOTS-basisinrichting, waar GBO op aansluit.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-OOTS-verzoek.mmd"
```
<figcaption>Figuur 3: Interactiepatroon gegevensverzoek vanuit Europese overheidsorganisatie via OOTS.</figcaption>
</figure>


### Patroon C - gegevensverzoek van private dienstverlener (DvTP)

Een private dienstverlener haalt overheidsgegevens op bij een bronhouder, uitsluitend op basis van een geldige juridische grondslag. In het geval van DvTP is dit een wettelijk vastgestelde toestemming voor het delen van gegevens met private dienstverleners. De burger authenticeert zich met een eIDAS authenticatiemiddel op het vereiste betrouwbaarheidsniveau en geeft geïnformeerde toestemming voor een specifiek doel, een specifieke afnemer en een specifieke set gegevens. GBO registreert de toestemming in een toestemmingenregister, levert een consent-id aan de private dienstverlener, valideert deze op het moment van uitvraag real-time, en zorgt dat het BSN de private dienstverlener nooit bereikt - in de plaats daarvan ontvangt de afnemer een partijspecifiek pseudoniem.

De bronhouder controleert of de private dienstverlener bevoegd is om de gegevens op te vragen, controleert het consent-id en beoordeelt of de gegevensvraag binnen de scope valt. Via het consent-id wordt het BSN van de betrokkene herleid en het antwoord aan de private dienstverlener wordt geleverd als response in het afnemersformaat.

GBO kiest voor een **centraal toestemmingenregister** als kern van dit patroon. Decentrale alternatieven (zoals toestemmingsregistratie per bronhouder) zijn overwogen, maar het centrale model heeft doorslaggevende voordelen:

- **Kostenbesparing:** eenmalig inrichten en beheren is goedkoper dan dat iedere bronhouder dit zelf regelt.
- **Herkenbaarheid voor de burger:** een centrale voorziening biedt de burger telkens dezelfde ervaring, wat herkenning en vertrouwen opbouwt.
- **Inzage voor de burger:** met een centrale voorziening is het aanzienlijk eenvoudiger om de burger inzage te geven in al zijn toestemmingen via het Toestemmingsportaal.
- **Eén keer toestemmen:** de burger kan in één handeling toestemming geven voor een set gegevens die mogelijk uit meerdere bronnen afkomstig zijn. Bij decentrale registratie per bron zou de burger voor elke bron apart moeten toestemmen.

Het Toestemmingsportaal biedt de burger inzage in alle actieve toestemmingen en de mogelijkheid toestemming in te trekken.

<figure>
``` mermaid
--8<-- "diagrammen/interactiepatroon-PP-haalt-gegevens-op.mmd"
```
<figcaption>Figuur 4: Interactiepatroon DvTP (dienstverlener is een private partij).</figcaption>
</figure>


## Generieke functies en stelselfuncties

GBO is opgebouwd uit acht generieke functies die samen de volledige gegevensstroom afdekken, van identiteitsvaststelling en toestemmingsbeheer tot bronontsluiting en beheer. Deze generieke functies zijn technologieneutraal.  
Elke generieke functie wordt ingevuld door een of meer stelselfuncties: concrete afspraken, standaarden en/of voorzieningen. In de paragrafen hieronder zijn de generieke functies uitgewerkt, met de stelselfuncties die GBO in beeld heeft om de functie in te vullen en hun huidige inrichtingsstatus.  

### F1 — Identiteit & Vertrouwen

_Burgers worden geïdentificeerd via het BSN, organisaties worden geïdentificeerd via het (sub)OIN. Om het BSN te verbergen voor afnemers die geen wettelijke grondslag hebben om het BSN te verwerken, wordt dit gegeven gepseudonimiseerd. Als een burger inlogt met een EIDAS middel waar geen BSN aan is gekoppeld, moet het BSN via "identity matching" achterhaald worden.
Burgers authenticeren zich met DigiD of een ander EIDAS middel met een betrouwbaarheidsniveau dat past bij de afgenomen dienst en de op te vragen gegevens. Systemen authenticeren zich met PKIo certificaten. Organisaties mogen enkel deelnemen aan het stelsel als ze voldoen aan de aansluitvoorwaarden._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                                   | **Status**                                                        | **Voornaamste gap / actie**                                              |
| ---------------------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------------ |
| S03 — Burgeridentificatie & Pseudonimisering         | BSNk PP beschikbaar - integratie nodig;Identity Matching nog in onderzoek | Onboarding DvTP-partijen als deelnemer; consent-id-koppeling             |
| S04 — Organisatie-authenticatie & Vertrouwensstelsel | FDS Poortwachter/Marktmeester uitgewerkt als concept; feitelijke beschikbaarheid en GBO-toepassing nog te bepalen | GBO-aansluitvoorwaarden; KvK↔OIN↔eIDAS-koppeling |

### F2 — Toegang & Interactie

_Gegevensvragen worden geautoriseerd met behulp van beleidsregels (PBAC). Als er toestemming (in de betekenis van de AVG) van de burger nodig is, wordt hiervoor een toestemmingsvoorziening gebruikt._

Hiervoor zijn de volgende stelselfuncties nodig:


| **Stelselfunctie**                            | **Status**                         | **Voornaamste gap / actie**                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------------------------------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| S01 — Toestemmingenregistratie                | Nog te realiseren ⚠️               | Toestemmingsregister; gebruik als PIP; afhankelijk van benodigde wet- en regelgeving                                                                                                                                                                                                                                                                                                                                                                         |
| S02 — Toestemmingsportaal (Burger Interactie) | Nog te realiseren ⚠️               | DvTP; inzage & intrekking; koppeling toestemmingenregister; aansluiting MijnOverheid                                                                                                                                                                                                                                                                                                                                                                        |
| S05 — Autorisatie (PEP/PDP/PIP)               | OPA/Rego; GBO-inrichting nog nodig | PEP/PDP referentie-implementatie per bronhouder; AuthZEN NLGov profiel; Policy Store / PAP (zie S06)                                                                                                                                                                                                                                                                                                                                                                     |
| S06 — Beleidsbeheer & -distributie (PAP)      | Nog te ontwerpen ⚠️                | Centrale voorziening voor het beheren en distribueren van OPA/Rego-policy-bundles naar alle bronhouder-PDP-instanties en de FSC Manager. Policies worden als gesigneerde OCI-bundles beschikbaar gesteld en asynchroon opgehaald door decentrale PDP-instanties (OPA Bundle API). De PAP is het technisch-bestuurlijke gezagspunt van het stelsel: hij bepaalt wat iedere deelnemer mag. Vereist een expliciete governance-afspraak over wie policies mag schrijven, wijzigen en goedkeuren. |

### F3 — Gegevensvoorziening

_Bronhouders ontsluiten hun gegevens via een generieke API. Hiervoor wordt GraphQL voorgesteld: daarmee is hergebruik en dataminimalisatie eenvoudiger te verwezenlijken. Voor bronhouders die geen GraphQL API beschikbaar kunnen stellen, wordt een "GBO-vertaallaag" aangeboden om een bestaand protocol te vertalen naar GraphQL. Verder wordt gebruik gemaakt van de FSC standaard.
Voor aansluiting op OOTS wordt een adapter beschikbaar gesteld waarmee brongegevens omgezet worden naar de gewenste "evidence types". De Basisinrichting OOTS zorgt voor burgerconsent, de omzetting naar het OOTS protocol (AS4/eDelivery) en de aansluiting op de portalen in andere EER-lidstaten._

Hiervoor zijn de volgende stelselfuncties nodig:

| **Stelselfunctie**                              | **Status**                                                       | **Voornaamste gap / actie**                                                            |
| ----------------------------------------------- | ---------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| S07 — Gegevensontsluiting (bronontsluiting-API) | FSC beschikbaar; GraphQL nog niet gestandaardiseerd als API type | Dienstencatalogus; GraphQL positionering in FDS; GBO-vertaallaag                 |
| S08 — OOTS-adapter (Grensoverschrijdend)        | Basisinrichting OOTS beschikbaar                                | GBO ↔ REST-koppeling; GBO-SDG mapping |
| S11 — Attesteringsuitgifte (PubEAA / QEAA)     | Nog te realiseren ⚠️                                             | OpenID4VCI-endpoint; attestatieschema's; signing-infrastructuur; QTSP-verificatiedienst   |

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

_Toestemmingenregister; consent-records; grondslagen-/doelbindingstoets vanuit policies; PEP/PDP/PIP-keten._

Van toepassing op: alle drie de patronen.

| **Stelselfunctie**                       | **Status**                                                     | **Voornaamste gap / actie** |
| ---------------------------------------- | -------------------------------------------------------------- | --------------------------- |
| S01 — Toestemmingenregistratie           | Nog te realiseren ⚠️                                           | Zie F2                      |
| S05 — Autorisatie (PEP/PDP/PIP)          | OPA/Rego (als bewezen implementatie); GBO-inrichting nog nodig | Zie F2                      |
| S06 — Beleidsbeheer & -distributie (PAP) | Nog te ontwerpen ⚠️                                            | Zie F2                      |

### F7 — Orkestratie & Integratie

_Procesorkestratie over patronen; formaat-mapping; event-afhandeling._

Van toepassing op: alle drie de patronen.

| **Stelselfunctie**                              | **Status**                                                       | **Voornaamste gap / actie** |
| ----------------------------------------------- | ---------------------------------------------------------------- | --------------------------- |
| S07 — Gegevensontsluiting (bronontsluiting-API) | FSC beschikbaar; GraphQL nog niet gestandaardiseerd als FDS-type | Zie F3                      |
| S08 — OOTS-adapter (Grensoverschrijdend)        | OOTS-basisinrichting beschikbaar                                | Zie F3                      |

### F8 — Beheer & Continuïteit

_Logging; monitoring; versiebeheer; incidentbeheer; SLA-bewaking._

Van toepassing op: stelselbreed.

| **Stelselfunctie**                     | **Status**                                   | **Voornaamste gap / actie**                                                |
| -------------------------------------- | -------------------------------------------- | -------------------------------------------------------------------------- |
| S09 — Logging, Audit & Traceerbaarheid | Standaarden beschikbaar; GBO-invulling nodig | Centraal auditlog; herleidbaarheidsprofiel; koppeling aan autorisatieketen |

---

### Overzicht: stelselfuncties en generieke functies

De onderstaande tabel geeft een totaaloverzicht van alle stelselfuncties met hun relatie naar de generieke functies.

| **Stelselfunctie**                                   | **Generieke functie(s)** | **Status**                                                       |
| ---------------------------------------------------- | ------------------------ | ---------------------------------------------------------------- |
| S01 — Toestemmingenregistratie                       | F2, F6                   | Nog te realiseren ⚠️                                             |
| S02 — Toestemmingsportaal (Burger Interactie)        | F2                       | Nog te realiseren ⚠️                                             |
| S03 — Burgeridentificatie & Pseudonimisering         | F1                       | BSNk PP beschikbaar; integratie nodig                            |
| S04 — Organisatie-authenticatie & Vertrouwensstelsel | F1                       | FDS Poortwachter/Marktmeester uitgewerkt als concept; GBO-toepassing nog te bepalen |
| S05 — Autorisatie (PEP/PDP/PIP)                      | F2, F6                   | OPA/Rego; GBO-inrichting nog nodig                               |
| S06 — Beleidsbeheer & -distributie (PAP)             | F2, F6                   | Nog te ontwerpen ⚠️                                              |
| S07 — Gegevensontsluiting (bronontsluiting-API)      | F3, F7                   | FSC beschikbaar; GraphQL nog niet gestandaardiseerd als FDS-type |
| S08 — OOTS-adapter (Grensoverschrijdend)             | F3, F7                   | OOTS-basisinrichting beschikbaar                                |
| S09 — Logging, Audit & Traceerbaarheid               | F8                       | Standaarden beschikbaar; GBO-invulling nodig                     |
| S10 — Semantiek & Gegevenscatalogus                  | F4, F5                   | DCAT-AP NL verplicht in FDS                                      |
| S11 — Attesteringsuitgifte (PubEAA / QEAA)          | F3                       | Nog te realiseren ⚠️                                             |

_Legenda: ⚠️ = nog te realiseren als nieuwe GBO-voorziening._

## Te ontwikkelen componenten

### Overzichtsplaat oplossing

De oplossingsrichting die in het tweede hoofdstuk voorgesteld werd, kan nu ingevuld worden. In de onderstaande figuur zijn in het overzicht de componenten benoemd die invulling geven aan de vereiste functies.

<figure>
``` mermaid
--8<-- "diagrammen/gbo_swimlanes.mmd"
```
<figcaption>Figuur 5: De oplossingsrichting met de gekozen componenten.</figcaption>
</figure>

In de volgende paragrafen wordt aangegeven welke componenten hergebruikt kunnen worden en waar aanpassingen/aanvullingen nodig zijn om de gemeenschappelijke bronontsluiting mogelijk te maken.

### Bouwstenen die hergebruikt worden

GBO gebruikt het Federatief Datastelsel (FDS) als basisafsprakenstelsel en bouwt daar zoveel mogelijk op voort. FDS biedt al een aantal cruciale bouwstenen: FSC als standaard voor koppelingen, FTV als standaard voor autorisatie, DCAT-AP NL voor datacatalogisering en de in ontwikkeling zijnde stelselfuncties Poortwachter en Marktmeester voor onboarding en nalevingsbeheer.

De oplossingsrichting gaat uit van hergebruik van de volgende bouwstenen:

**FSC (Federated Service Connectivity).** Binnenlands koppelnetwerk dat mTLS-gebaseerde verbindingen tussen GBO, bronhouders en private afnemers verzorgt. Elke deelnemer beheert een eigen FSC Inway (bronhouder) of Outway (afnemer). FSC is beschikbaar als open referentie-implementatie en is de standaard voor binnenlands dataverkeer in het FDS.

**GraphQL.** Voorgesteld bevragingsprotocol voor selectieve gegevensuitvraag op de bronontsluiting-API, naast REST als huidige standaard. Toegestane gegevensverzoeken zijn vooraf geregistreerd in de dienstencatalogus en afdwingbaar door het PDP-beleid. Bronhouders die geen eigen GraphQL-implementatie realiseren kunnen gebruik maken van GBO-tooling voor vertaling naar GraphQL. Formele standaardisatie als FDS-datadienst-type verloopt via Digikoppeling en Forum Standaardisatie.

**OAuth 2.0 / OpenID Connect.** Autorisatieprotocol voor de uitgifte van toestemmingstokens na succesvolle burgeridentificatie (DigiD of ander eIDAS-middel). Het toestemmingstoken bevat de consent-id als brug naar het toestemmingenregister; het BSN zit niet in het token.

**AuthZEN.** Gestandaardiseerde koppelinterface (OpenID Foundation, draft) tussen de PEP en de OPA-PDP. Maakt de autorisatieketen protocolonafhankelijk en vervangbaar per component.

**OPA/Rego (Open Policy Agent).** Policy Decision Point voor real-time beleidsevaluatie. Policies zijn machineleesbaar, per traject instelbaar en centraal beheerd in een PAP. OPA/Rego is in productie bij het iWlz-afsprakenstelsel voor gevoelige zorgdata en is daarmee een bewezen keuze voor een overheidscontext met hoge privacyvereisten.

**ODRL (Open Digital Rights Language).** W3C-standaard voor machineleesbare beleidsrepresentatie. Ingezet als beschrijvingstaal voor beleidsregels in de PAP (zie §4.1), aansluitend op de toepassing in FDS en DCAT-AP NL. De machine-executeerbare invulling vindt plaats in Rego (OPA).

**BSNk PP (Polymorf Pseudonimiseringsstelsel).** In productie bij Logius. Verplicht voor alle DvTP-uitvragen: zet het BSN om naar een partijspecifiek, onomkeerbaar pseudoniem vóór enige verstrekking aan een private dienstverlener.

**OpenID4VCI / OpenID4VP.** OpenID-protocollen voor respectievelijk de uitgifte (GBO → wallet) en de presentatie (wallet → dienstverlener) van verifieerbare credentials. Vormt het technische fundament van het EUDI-Wallet-patroon en mogelijke andere toepassingen van VC's.

**SD-JWT VC / mdoc (ISO 18013-5).** Attestatieformaten voor de EUDI-Wallet, conform het ARF. SD-JWT VC is het standaardformaat voor online presentatie; mdoc ondersteunt ook offline (proximity) scenario's.

**AS4 / eDelivery (via OOTS-basisinrichting).** EU-transportprotocol voor het OOTS-berichtenverkeer. GBO communiceert via REST/JSON met de OOTS-basisinrichting; de AS4-laag is volledig bij de OOTS-basisinrichting belegd.


Voor de toepassingen die in beeld zijn is echter meer nodig. In dit hoofdstuk wordt per onderwerp beschreven wat er nog ontbreekt, en wat er dus afgesproken of ontwikkeld moet worden.

### GraphQL als selectief bevragingsmechanisme

FDS hanteert REST als standaard datadienst-type (NL API Strategie / REST-API Design Rules). Voor onderdelen (in elk geval bronontsluiting) stelt GBO GraphQL voor. Hiermee worden hergebruik, dataminimalisatie  

Wat er nog moet worden afgesproken of gerealiseerd:

- **Positionering van GraphQL als FDS-datadienst-type**: GBO introduceert GraphQL als aanvullend bevragingsmechanisme naast REST, waarbij dataminimalisatie structureel is ingebouwd en hergebruik van de API via parametrisering mogelijk is. GraphQL is in productie bewezen bij het iWlz-afsprakenstelsel en is compatibel met FSC Inway/Outway. Formele standaardisatie van GraphQL als FDS-datadienst-type vergt een wijzigingsvoorstel via Forum Standaardisatie en Digikoppeling. In de GBO pilots wordt al ervaring opgedaan met GraphQL.
- Een **GBO-vertaallaag** voor bronhouders die geen eigen GraphQL-implementatie willen of kunnen realiseren. Bronhouders die een REST-API aanbieden kunnen via de GBO-vertaallaag toch ontsloten worden als GraphQL-bron. Bronhouders worden dus niet gedwongen GraphQL zelf te implementeren.
- GBO sluit aan bij **DCAT-AP NL** voor datacatalogisering, conform de bestaande FDS-verplichting. Indien aanvullende metadata-elementen noodzakelijk blijken, wordt dit ingebracht bij de beheerder en community van DCAT-AP NL. GBO maakt geen eigen profiel bovenop DCAT-AP NL.
- Een **Dienstencatalogus**: een centrale catalogus van vooraf geregistreerde gegevensvragen per toepassing. Afnemers kunnen alleen opvragen wat voor hun specifieke toepassing is geregistreerd. De dienstencatalogus worden centraal beheerd als onderdeel van GBO; dit vraagt geen inzet van de bronhouder.
- Een

### Toestemming en grondslag als afdwingbaar autorisatiemechanisme

FDS schrijft voor dat gegevensuitwisseling op een geldige grondslag berust, maar legt geen technische invulling op voor toestemmingsbeheer of real-time grondslagraadpleging. **FTV** biedt een autorisatieraamwerk dat gebruikt kan worden voor het per-uitvraag raadplegen van een extern toestemmingenregister als PIP, en de doelbindingstoets kan uitvoeren die DvTP vereist.  

Wat er nog moet worden afgesproken of gerealiseerd:

- Een **pseudonimiseringsprofiel** voor GBO/DvTP: BSNk PP als verplichte voorziening zodat het BSN private dienstverleners nooit bereikt. De consent-id fungeert als brug tussen pseudoniem aan de private zijde en BSN-resolving aan de bronhouderzijde.
- Een **toestemmingsportaal** voor de burger: een overheidsgerichte UI voor het geven, inzien en intrekken van toestemming, gekoppeld aan het toestemmingenregister.
- Een **toestemmingenregister** als machineleesbare centrale voorziening, waarbij toestemming gekoppeld is aan doel, afnemer en gegevensset (doelbinding), en intrekking onmiddellijk effect heeft. Het register is als PIP real-time raadpleegbaar door de autorisatieketen.
- Een **PEP/PDP/PIP-keten** op basis van AuthZEN en OPA/Rego, als concrete invulling van het FTV-autorisatieraamwerk voor GBO-toepassingen. Policies worden centraal beheerd via een PAP en gedistribueerd naar decentrale PDP-instanties per bronhouder.
- Een **PAP (Policy Administration Point)** als centraal GBO-component voor het beheren en distribueren van gesigneerde OPA/Rego-policy-bundles. Dit is tevens het bestuurlijk gezagspunt van het stelsel: het bepaalt wat iedere deelnemer mag. Er is een expliciete governance-afspraak nodig over wie policies mag opstellen, wijzigen en goedkeuren. Beleidsregels worden beschreven in ODRL als machineleesbare representatielaag, aansluitend op de toepassing van ODRL in FDS en DCAT-AP NL. De machine-executeerbare invulling vindt plaats in Rego (OPA).

_Juridische randvoorwaarde: toestemming als afdwingbare grondslag is pas operationeel na inwerkingtreding van de daarvoor benodigde wet- en regelgeving. De technische uitwerking loopt parallel aan het wetgevingstraject._

### OOTS-aansluiting

FDS is een binnenlands afsprakenstelsel en voorziet niet in grensoverschrijdende gegevensuitwisseling. OOTS vereist AS4/eDelivery als transportprotocol en het SDG Evidence Data Model (SDG-EDM) als semantisch kader — beide vallen buiten de scope van FDS.  

Wat er nog moet worden afgesproken of gerealiseerd:

- Een **OOTS-adapter** (onderdeel van OOTS-basisinrichting) die AS4/eDelivery-verkeer van EU-lidstaten vertaalt naar GraphQL richting GBO, zodat bronhouders geen OOTS-kennis nodig hebben en uitsluitend de GBO-API zien.
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
