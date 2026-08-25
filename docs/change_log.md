## Change Log v0.9.3
**Van:** versie 0.9.2 (juni 2026) → **Naar:** 0.9.3 (augustus 2026)

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
