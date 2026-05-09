# Konkret exempel — för presentation i mindre grupp

**Vad det här är:** Ett **tankeexempel** som liknar en **riktig butik**: rådet väljer varor, sätter **priser i tokens och i kronor**, tar in varor från **lokala leverantörer** och lägger dem på hyllan. **Medlemmar** betalar i första hand med **tokens**; de kan **fylla på tokens med kronor**, **sälja in varor** mot tokens, eller — om rådet godkänner **bidragsprojekt** — **tjäna tokens genom insats i gemenskapen** och sedan handla för dem i butiken. **Turister** kan betala **Swish eller kort** utan konto — allt finns i den **digitala boken** (samma synlighetsidé för alla). **Öppna siffror** för allt som rör **riktiga kronor**.

**Mer bakgrund:** [local-exchange-pilot.sv.md](local-exchange-pilot.sv.md). Vision: [manifest.sv.md](manifest.sv.md). Teknik och tokensystem: [local-exchange-tech.sv.md](local-exchange-tech.sv.md). Juridik och svensk lag (utkast, ej rådgivning): [local-exchange-juridik.sv.md](local-exchange-juridik.sv.md).

**Arbete och tokens (rådsgodkända projekt, ubuntu‑liknande koppling mellan tid och tokenvärde):** se **[local-exchange-tech.sv.md](local-exchange-tech.sv.md)** — avsnitt **§10** (*Arbete mot tokens — Ubuntu‑inspirerad modell för rådgodkända projekt*).

---

## Elevatorpitch (ungefär en minut)

Vi driver en **liten butik** med varor **från trakten** (bygden och de som finns nära oss). **Utbytesrådet** bestämmer sortiment och **vad varan ska kosta för medlem i tokens**, och vad **turist eller kronkunnig kund ska betala**. **Tokens** är tänkta att kunna ligga mer **stabilt** över år jämfört med **SEK‑priset**, som får hantera inflation och löpande lönsamhet. **Medlemmar** kan betala **tokens**, fylla på med **Swish/kort**, eller sälja in varor och få **tokens**. **Turister** betalar i regel **i kronor**. Alla **kronor redovisas öppet** för den som har rätt till insyn; hur **intäkt delas mellan leverantör och förenings­drift** är **inte dold kedjeavgift**.

---

## 1. Utbytesrådet — sortiment, priser och bokföring

**Vad rådet är:** Få personer (t.ex. 3–5) som medlemmarna litar på. De styr **butiken** och ser till att den **digitala boken** följer beslut och **regelbundna säkerhetskopior**.

| Uppgift | Praktiskt |
|---------|-----------|
| **Sortiment** | Välja vilka produkter som står först i butiken; avtal med lokala leverantörer (**kvalitet, hur ofta, hur mycket**). |
| **Priser** | Sätta **token-pris** för medlem / lokalt åtagande och **särskilt kron-/turistpris** för dem som inte handlar på token — se avsnitt 2. |
| **Ersättning till leverantör** | I det här exemplet **betalas leverantörer med tokens** när deras varor säljs (se avsnitt 6) — inte löpande i kronor från föreningen, om ni inte **uttryckligen avtalat** något annat. |
| **Boken** | **Medlemsköp**, **token-påfyllning**, **turistköp med kronor** — allt redovisas för transparenssyfte; säkerhetskopior. |
| **Öppenhet** | Se avsnitt 7 — redovisning i tid och i begripligt format. |

**Rotation:** gärna **ett år i taget**.

---

## 2. Den fysiska butiken och skyltarna

- **Lokal:** t.ex. hörn i sockenhus, bygdegård, eller container — skylt folk ser, återkommande **öppettider**, **hyllor + kyl**.  
- **Skyltning — två priser:** Visa **båda** tydligt för samma vara:  
  - **Lokala / med tokens:** ett **antal tokens** som ni kan hålla **mer stabilt** över säsong och år.  
  - **Turist eller direktköp med kronor:** ett **pris i SEK** som ni kan **justera löpande** när elkostnad, arbetsbehov eller inflation kräver det — utan att **hela tiden omräkna tokenlistan.**

  **Tanke bakom dubbla priser:** lokala åtaganden bygger mest på **tokens**; **turist-/kronpriset** kan sättas högre eller annorlunda så **lokala medlemmar upplever ett förmånspris jämfört med turisten** eller så täcker det **bredare kringkostnader** för butiken.

- **Självservice‑kassa:** surfplatta, stor skärm eller liknande där köpare själv (medlem eller turist) väljer rader och betalar med **tokens** eller **Swish/kort**. Saknar medlemmen tokens kan hen i samma flöde **fylla på** eller — om rådet så beslutar — **betala med Swish för just det köpet**. Detaljer i [local-exchange-tech.sv.md](local-exchange-tech.sv.md).  
  Behövs **hjälp** finns jour eller värd på plats, men målet är **kö utan klassisk mänsklig kasse­disk**.

*(Större tekniska mål som **lokal server** och **reservström** beskrivs i [local-exchange-tech.sv.md](local-exchange-tech.sv.md).)*

---

## 3. Varor i start (exempel — rådet väljer och värderar)

*(Siffror är påhittade — sätt era egna kolumner för **turist-/kronpris**. )*

| Produkt | Leverantör (exempel) | Token-pris medlem (ex) | Turist-/kronpris (ex) |
|---------|----------------------|-------------------------|------------------------|
| Ägg, 6-pack | Lokal hönsägare | 5 tokens | 59 kr |
| Honung, burk | Lokal biodlare | 12 tokens | 155 kr |
| Bröd, limpa | Lokalt bageri | 8 tokens | 95 kr |
| Säsongens grönt, påse | Närodlare | 6 tokens | 79 kr |
| Saft / mos | Trädgårdar på ön | 7 tokens | 85 kr |

**Inköp / lager:** varan ligger i **lager** med känd mängd; när någon köper fördelas intäkten enligt **regler ni beslutat** mellan **leverantör** och **förening** — teknisk uträkning i [local-exchange-tech.sv.md](local-exchange-tech.sv.md). **Lagret** **uppdateras automatiskt** när sälj registreras och när leverantör **rapporterar inlevering** till butiken — då kan **råd och leverantör se hur mycket som finns** hela tiden.

---

## 4. Medlemmar — tokens, påfyllning och betalning

**Token-pris** vid handel i butik följer **skyltens token‑kolumn** — medlemmen betalar med **tokens** från sitt konto.

**Fylla på tokens med kronor:** medlem använder **Swish/kort** enligt **kurs som rådet beslutat** (t.ex. hur många tokens per insatt hundralapp) — detaljer i teknikdokumentet; kursen ska vara **öppen**.

**Sälja in varor till butiken:** rådet godkänner; **ersättning sker i tokens** på medlemmens konto enligt avtal; varan går i **lager**.

**Betala i butiken (självservice eller app):**

1. Logga in i **webbappen** eller vid **butikens betalstation**.  
2. **Scanna** varan (eller välj rad).  
3. **Priset i tokens** dras från medlemmens konto; beloppet **fördelas i boken** till **leverantör** och **förening** enligt era regler.  
4. Kvitto i appen; lagret minskar.

Köpet syns i **boken** med tid, belopp och **vilken vara** som sålts.

---

## 5. Turister — Swish eller kort

Turisten behöver **inget medlemskonto**.

1. Vid **självservice** eller med hjälp: välj varor — betala **med skyltat kronpris** med **Swish eller kort**.  
2. **Kronorna** går till **föreningens konto**.  
3. I **boken** registreras köpet så att **omsättning** och **fördelning till leverantör/förening** kan följas — tekniskt kan det göras med **en rad per gästköp** och ev. **jämförande token‑värde för statistik** utan att skapa konto för turisten (jämför [local-exchange-tech.sv.md](local-exchange-tech.sv.md)).

**Turistens kronor och transparens:** saldo för **inseende medlemmar eller råd** ska **löpande** kunna jämföra **värdet på tokenhandel jämfört gästkronor**.

**Användning av överskotten** beslutar **rådet** med **korta protokoll** som visas öppet.

---

## 6. Leverantör — betalning när **något säljs** (inte modell ”betala först för lager ni inte sålt”)

I detta exempel finns **enbart ett arbetssätt**:

**Lämnad vara säljs först** (**konsignation** på vardags­språk): leverantören fyller på butiken med **färska** varor efter avtal. **När en rad säljs** krediteras **leverantörens konto i tokens** automatiskt i **boken** (plus föreningens andel enligt beslut). **Leverantören får alltså betalt i tokens — inte i löpande småutbetalningar i kronor** från föreningen, såvida ni inte **uttryckligen** skriver något annat i avtal.

**Varför det här passar er idé:**  

- leverantören har **orsak** att hålla **lager färskt** och **påfyllt**;  
- **lager står alltid i systemet** (så länge in/ut bokförs) så **alla ser hur mycket som finns**.

**Enkel kassa:** **skanna produkt** — varan är redan kopplad till **leverantör** och **pris**; vid genomfört köp uppdateras **leverantör** och **förening** i **boken** utan manuell mellanrad.

**Turist med kronor:** samma **säljsplit** som för medlemmar kan speglas i **kronor** i boken (enligt hur ni bygger det — se teknikdokumentet).

**Mellanhand?** Nej i traditionell mening: föreningen tar **ett synligt, beslutat** bidrag för **gemensam drift** — inte dold kedjeprovision.

---

### 6.1 När skapas nya tokens och när ”bara flyttas de”?

| Situation | Kort förklaring |
|-----------|----------------|
| Medlem betalar med **befintliga** tokens | Belopp **flyttas** mellan konton (**omfördelning**). **Totalt tokens i systemet** behöver **inte öka.** |
| Nya tokens | Tas fram när **kronor** kommer in enligt **beslutad kurs** (t.ex. medlem fyller på, eller turistflöden som ni väljer att koppla till utgivning) — **med tydlig koppling till bank/kassa** om ni vill behålla **tillit**. |

**Automatik** i kassan betyder här: **rätt konton uppdateras utan handpåläggning** — inte att värde skapas ur tomma intet.

---

### 6.2 Startvärde på föreningens tokenkonto — **tillit först**

**Ni väljer variant A:** föreningen får **tokens på sitt konto först när det finns dokumenterade kronor** (insättning, bidrag, eller medlems­liknande köp av tokens) — **samma princip som för övriga**. Det ger **starkast tillit** till att systemet står på **riktiga inflöden**, inte gratismynt.

---

### 6.3 Kort sammanfattning

- **En modell:** såld rad → **tokens till leverantör + andel till förening**; **lager synligt**.  
- **Betala leverantör i tokens**, inte som vanlig **kronlön per leverans** i det här exemplet.  
- **Turist:** kronor till föreningen; **boken** visar fördelning enligt beslut.  
- **Start:** **A** — **kronor först**, sedan motsvarande tokens till föreningens konto om ni behöver saldo där.

---

## 7. Öppenhet — miniminivå (exempel)

| Vad | Hur |
|-----|-----|
| **SEK in** | Medlems-påfyllning + gästbetalningar — gärna **separerade kolumner** för att se turism. |
| **Tokenrörelser** | Dragningar från medlemmar, ackumulering hos leverantörer och förening — **samma siffror för alla med insynsrätt**. |
| **Utgifter i kronor** | Hyra, el, betaltjänst — **per post**; **leverantörers uttag i tokens** eller omvandling enligt **senare politiskt beslut** dokumenteras **tydligt** (detaljer i teknik och avtal). |
| **Beslut** | Korta protokoll från rådet så folk förstår **varför** siffrorna ändras. |

---

## 8. Checklista inför första mötet

- [ ] **Butiksplats** och **öppettider**.  
- [ ] **Råd** — antal, mandat.  
- [ ] **Sortiment** med **token-pris** och **turist-/kronpris** per rad.  
- [ ] **Kurs** för hur medlemmar **köper tokens för kronor** (öppet beslut).  
- [ ] **Självservice-kassa** — vem sätter upp, hur får folk hjälp första gången.  
- [ ] **Leverantörsavtal:** **ersättning i tokens vid såld rad**, lager­rutiner.  
- [ ] **Fördelning leverantör/förening** — hur det läggs in i systemet ([local-exchange-tech.sv.md](local-exchange-tech.sv.md)).  
- [ ] **Var Swish/kort landar** (juridiskt konto).  
- [ ] **Månadsrapport** — vem, var (webb, anslag).  
- [ ] **IT-kontakt** för webbapp, scan, inloggning.

---

*När ni har riktiga namn, priser och konto — skriv in dem här så blir dokumentet er presentationsversion.*
