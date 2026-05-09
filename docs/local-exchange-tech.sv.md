# Lokalt utbyte — teknisk miljö och tokensystem (utkast)

Detta dokument beskriver **teknikmiljö och logik för tokensystemet** för den som designar eller bygger lösningen. Det **ersätter inte** juridisk rådgivning, bokföring eller revisors granskning — sådana frågor hanteras för **er förening** med stöd av rätt expert. **Ämnesindelning för svensk juridik** (utkast): [local-exchange-juridik.sv.md](local-exchange-juridik.sv.md).

**Koncept och presentation:** [local-exchange-exempel-grupp.sv.md](local-exchange-exempel-grupp.sv.md) (**dubbla skyltpriser**, **självservice‑kassa**, **leverantör betalas i tokens vid såld rad**, **enbart konsignationsmodell**, **inte** löpande kronutbetalning till leverantör som standard, **samt arbete mot tokens för rådgodkända gemenskapssysslor** — se avsnitt **10**). Principer: [local-exchange-pilot.sv.md](local-exchange-pilot.sv.md).

Terminologi: ordet **boken** = samma sak som **digital boken / transaktionslogg**. I databas eller kod kallas den ofta **ledger** eller **transactions** — ingen blockkedja behövs.

---

## 1. Syfte

1. Beskriva **var** och **hur** systemet förväntas köras (klienter, självservice, nät, server, reservström).  
2. Förklara **tokens** och **bokens** struktur (_ledger_‑data): konton, hur poster skapas, när tokens **emitteras** (mint) eller bara **omfördelas**.  
3. Beskriva **lager och inleverans** så **saldot stämmer mot verkligt utbud** och **inte** risker att sälja samma förpackning två gånger om ni bokar rätt.  
4. Visa hur **splitt mellan leverantör och förening** implementeras för **två sätt att köpa samma SKU:** med tokens (medlem) eller med **turist-/kronpriset** — med **fast token‑uppdelning per vara** och/eller **procentsats** (siffrorna beslutas politiskt; **här** beskrivs hur de kodas).  
5. Beskriva **arbete mot tokens**: **Ubuntu‑liknande** koppling mellan **rapporterad arbetstid** och **ersättning i tokens** till **projekt godkända av rådet**, och hur dessa tokens sedan **kan köpa varor** i utbytes‑/butiksflödet (avsnitt **10**).

---

## 2. Arkitektur i översikt

| Lager | Typiskt innehåll |
|-------|------------------|
| Klient | Webb (telefon, surfplatta, PC), ev. streckkods-/QR-läsare. **Självservice-terminal** för medlem eller turist (samma eller separat läge kan finnas för inloggat flöde). |
| Applikation | API, affärslogik, autentisering, behörigheter. |
| Data | Databas med produkter, konton, transaktioner. |
| Utanför denna kärna | Swish/kort, föreningens bankkonto — måste ändå **kopplas** till händelser i systemet. |

**Kommunikation:** **HTTPS** över internet eller, om servern finns lokalt, **HTTPS inom LAN** (klienter och server i samma nät).

---

## 3. Klienter och roller

| Yta | Användning |
|-----|-------------|
| Medlem | Mobilvenlig webb: saldo, fylla på tokens, historik, ev. **anmält arbete för godkänd utbetalning.** |
| Kassa | Webb på plats med scan eller manuellt varuval; roller som *kassa* (sälj utan full admin). **Självservice-terminal** för medlem och turist kan vara **samma gränssnitt**, med eller utan hjälp från jour. |
| **Projekt-/bidrag** (konfigurerbar roll) | **Ansvar för projekt** som rådet aktiverat: **arbetstidrader**, **verifier**, **kreditering på medlemskonto först efter verifierad insats**. |
| Råd/admin | Priser, splittregler, **ändring av parametertabell för arbetspoäng**, bidragsprojekt, rapporter; ändringar **loggas** (vem, när). |

**Princip:** **minsta nödvändiga behörighet** per roll.

---

## 4. Driftmiljö: nät, server, el

| Mål | Praktiskt |
|-----|-----------|
| **Normal drift** | Internet för åtkomst, uppdateringar, backup. |
| **Lokal server** i föreningens lokaler | Klienter i byggnaden kan använda **lokalt nät (LAN)** till servern även om **bredbandet till omvärlden** inte fungerar — bestäm i förväg **vad** som ska fungera utan internet (t.ex. sälj med medlemskonto). |
| **Reservström** | UPS, batteri eller diesel/annan generator så att **server och kassa** kan hållas igång under planerad öppettid — **övas** regelbundet. |
| **Fysisk placering** | Torr, skyddad el; följ el- och brandskydd som gäller lokalt. |

---

## 5. Token: begrepp i systemet

| Begrepp | Betydelse här |
|---------|----------------|
| **Token** | Intern **kreditenhet** i ert register — **inte** nödvändigtvis kryptovaluta eller värdepapper. |
| **`TOKENS_PER_SEK` (konfiguration)** | Styr **medlemmens påfyllning** (“köp tokens för kronor”), t.ex. `1` ⇒ 100 kr ⇒ 100 nya tokens på medlemskontot. Detta är **en egen politik** i förhållande till **`list_price_tokens`** och **`tourist_price_sek`** på hyllan — de tre behöver **inte** vara matematiskt proportionella; tokens kan vara **stabila**, **SEK** kan **justeras** för inflation eller turism. |
| **Omfördelning** | Medlem betalar med **befintliga** tokens → poster i **boken** flyttar belopp mellan konton utan nödvändig **ökning av total tokenmängd** om inget mint sker samtidigt. |
| **Mint (nyutgivning)** | Tokens skapas **bara** mot **dokumenterad SEK** till föreningens konto eller enligt **skriftligt, redovisat beslut**. **Variant A för föreningens startsaldo:** undvik stora ”gratis” tokenposter till förenings­konto utan kron‑underlag — **tillit** (jmf exempeldokumentet §6.2). |

---

## 6. Konton

| Typ | Användning |
|-----|------------|
| Medlem | Tokensaldo; påfyllnad med SEK; kreditering vid försäljning in till butik; ev. **kreditering för verifierade arbetsinsatser** under rådsgodkända projekt (avsnitt **10**). |
| Leverantör | Ackumulerat **tokensaldo** för **var såld rad** i **konsignation** (**sålt först**). **Primärt** ingen löpande **kronlön** från föreningen för samma flöde — om ni behöver **SEK‑utbetalning** senare är det **separate avtal eller omvandlingsregler** dokumenterade i boken eller redovisning. |
| Förening / drift | Ackumulerade andelar till gemensamma kostnader. |
| **`förening_labor_budget` (valfritt underkonto)** | Token som rådet **allokerat** för **löner enligt arbetsmodell** (antal tokens som får flyttas till medlemmar mot **verifierad tid**). Kan fyllas på från **föreningens ackumulerade andelar** eller genom **mint med besluts‑ID** — **policy måste vara skriftlig och redovisningsbar.** |
| Hjälpkonto (vid behov) | För turistflöde eller intern balansering (jfr exempeldokument om gästköp). |

Saldo anges normalt i **heltal tokens** om ni inte aktivt inför decimaler.

---

## 7. Produkter, lager och skanner (**enbart konsignation / modell som i exemplet**)

För varje **SKU**:

- `supplier_account_id` — leverantör som får **token‑andel** vid **såld förpackning eller rad.**  
- `list_price_tokens` — medlemmens skylt‑**token‑pris** för raden.  
- `tourist_price_sek` — skyltat **turist-/kronpris** (får skilja sig från tokenpriset av **inflation / strategi** — jmf exempeldokumentet).  
- **Splittregel** (avsnitt 8), inbyggd eller `split_rule_id`.  
- **`stock_qty` (eller motsvarande)** — **tillgängligt antal** i butik. **Minskas** vid genomfört sälj; **ökas** vid **inleverans** av auktoriserad roll (leverantör med bekräftelse eller råd/jour som bokar in).

**Händelser som bör finnas i boken utöver köp:** `stock_inbound` (SKU, antal, tid, vem, ev. batchreferens), eventuellt `stock_adjust` med **motivering** för svinn eller räknefel — så leverantör och råd ser **aktuellt lagersaldo löpande** som i exemplet.

Vid **köp** måste betalväg vara korrekt: **tokens** vid medlemsköp, eller **Swish/kort** mot **`tourist_price_sek`** (eller separat godkänd kron‑linje om medlem saknar tokens). Poster för **leverantör + förening** måste kunna hämtas i rapport (kap. **8**).

---

## 8. Splitt av intäkt — implementationsnivå (**här får procentsats beskrivas**)

Politiskt beslut tas i gruppen; i koden måste det finnas **enda sanningen** så att två kassor inte räknar olika.

### 8.0 Två köpvägar, samma SKU

| Köpväg | Kund betalar | Vad som måste kopplas i boken |
|--------|----------------|--------------------------------|
| **Medlem med tokens** | `list_price_tokens` dras från **medlem** | Splitt (**leverantör + förening**) uttrycks i **tokens**; total debiterad = **`T`** = `list_price_tokens` för raden. |
| **Turist eller medlem med Swish för kronköp** | `tourist_price_sek` (eller annat godkänt av rådet) till **Swish/kort** | SEK‑intäkt kopplad till **`payment_external_id`** (bankspår). I **boken** används ofta **samma tokensplitt per SKU** som vid tokenköpet (samma **`tokens_till_leverantör`** / **`tokens_till_förening`**), så att **rapporten** inte kräver en **ogenomskinlig växlingsmotor**. **OBS:** turist-/SEK‑priset **behöver inte** bara vara ett omräknat tokenpris — det stämmer med **två skyltpriser** och stabila tokenlistor.

**Preferens för transparens:** **fast tokensplitt per SKU** för **båda** vägarna; SEK för **bank** och för **synlig extern intäktsrad** för sig.

### 8.1 Fast uppdelning i tokens per vara

Fält t.ex. `tokens_till_leverantör` och `tokens_till_förening` så att **summan = `list_price_tokens`** för **medlemmens tokenköp** (eller avrundningsregel som **skrivs ut**). **Samma par** kan återanvändas som **logiska poster** även när kunden betalat med **SEK** (se 8.0).

### 8.2 Procentsats (global eller per kategori)

Parameter t.ex. `forenings_andel_procent` eller värde per `kategori_id`.

För rad med totalt `T` tokens — vid tokenköp **`T = list_price_tokens`**; vid kronköp måste **`T`** vara definierad (t.ex. samma **`list_price_tokens`** som beräkningsbas för omfördelning även om kunden inte debiterades tokens för belopp — jmf 8.0):

```
forening = avrunda(T × procent / 100)   <!-- avrundning måste vara dokumenterad -->
leverantör = T − förening
```

Kontrollera att **inga negativa** belopp uppstår. **Rapporter** ska kunna visa samma beräkning som kassan utför.

### 8.3 Idempotenta köp

Varje genomfört köp ska ha **unikt id** så att samma händelse inte bokför **dubbelt** vid nätverksretry eller dubbelklick.

---

## 9. Boken — transaktionstyper (**förslag till kod / tabellposter**)

Samlingen nedan är **logiska händelser**; databasimplementering kan slå ihop eller dela upp. På svenska kallas lagret **den digitala boken**; kodnamn är ofta **`ledger_transactions`**.

| Typ | Vad som ska hända (kort) |
|-----|---------------------------|
| **Påfyllning** (`topup_member_sek`) | Bekräftad SEK till föreningen ⇒ mint **tokens på medlemskonto** enligt `TOKENS_PER_SEK`; spara betalningsreferens till bank/integration. |
| **Försäljning tokens** (`sale_member_tokens`) | Debitera medlem **`list_price_tokens`**; splitta enligt kap. 8 till **leverantör** och **förening**; **minska lagersaldo.** |
| **Försäljning turist eller Swish för kronpris** (`sale_guest_or_sek_basket`) | Registrera **SEK‑intäkt** (`tourist_price_sek` eller summerat korg); koppla **`payment_external_id`**; splitta **i tokens för leverantör/förening** enligt kap. **8.0** (preferens: **fast tokensplitt per SKU som vid tokenköp**); **minska lagersaldo.** |
| **Inleverans** (`stock_inbound`) | Öka **`stock_qty`** för SKU; associera **leverantör**, **datum**, antal och ev. signerande roll. |
| **Arbetskredit** (`work_credit_issue`) | Verifierad tid under **godkänt projekt** ⇒ **kredit tokens** till **medlem** enligt parametertabell (kap. **10**); mot **föreningens arbetsbudget** eller dokumenterad mint‑regel. |

Varje rad i **boken** bör kunna läsas öppet i rapport: **tid**, **aktör/roll**, **`amount_tokens` per kontopost**, och vid **SEK** även **`sek_amount`** + **`external_payment_ref`** om tillämpligt.

---

## 10. Arbete mot tokens — **Ubuntu‑inspirerad** modell för **rådgodkända projekt**

Tanken att **gemenskapen** ska kunna **sätta arbete i relation till token** — ungefär som i **Ubuntu Contribution / One Small Town**‑inspirerade diskussioner om **bidragstid kopplad till ekonomiskt värde** — är här **tekniskt** strukturerad utan att säga exakt **vilket lönebelopp** som rätt för er plats (det beslutar ni **öppet med rådet**).

### 10.1 Livscykel för bidrags-/community‑projekt

1. **Utkast** / idé → 2. **Rådsbehandling** (`status = council_pending`) med **tak i tokens**, **budget** eller ram för projekt godkänd i **mötesprotokoll** → 3. **`approved` / `active`** → 4. **Arbetsrader rapporterade** → 5. **Verifiering** (projektansvarig eller särskild **verifier‑roll**) → 6. **Tokens krediterade** till medlemmens konto → medlemmen **handlar** i butiken med samma **tokensaldo** som för övriga flöden.

**Viktigt för förtroende:** **inget** automatiskt påslag av tokens utan **antingen** avdragen **överföring från `förening_labor_budget`** med valt **tak vid rådsbeslut**, **eller** mint med **tydligt `council_resolution_id`** kopplat till **redovisningsbar minskning/ökning** för medlemmar.

### 10.2 Tids‑ och tokenparametrar (jämför Ubuntu: “3 timmar” ≈ referens mot timvärde)

I flera **ubuntu‑liknande** presentationer används en **referensblock‑längd** (t.ex. **3 timmar**) som motsvarar en **värdesats** i ett **genomsnitt eller blockersättning** per **liknande arbetskategori**. Tekniskt modelleras det med **två konstanter** (konfigurerbara av rådet, **loggade vid ändring**):

| Parameter | Förslag / exempel |
|-----------|-------------------|
| `HOURS_REFERENCE` | T.ex. **`3`** timmar per **referens‑block** (kan vara `1` om ni bara vill köra “tokens per arbetad timme”). |
| `TOKENS_PER_REFERENCE_BLOCK` | Antal tokens som rådet säger motsvarar **ett sådant block** i **ersättningsspannet** som ni vill jämföra med **lokalt snitt / värde** (politiskt beslut, **inte** kodat här). |

**Timersättning** (om ni vill uttrycka “per timme”) fås av:

`tokens_per_hour_equiv = TOKENS_PER_REFERENCE_BLOCK / HOURS_REFERENCE`.

**Kreditering** vid rapporterad **`reported_hours`** (decimalt eller hel):

`tokens_to_credit = avrundningsregel ( reported_hours × tokens_per_hour_equiv )`

**avrundningsregel** (tak, golv, närmaste hel) — **ska vara en enda** för hela gemenskapen och **publicerad för medlemmar**.

*(Om ni **bara** vill använda **`TOKENS_PER_HOUR` direkt i tabellen** och hoppa över 3‑blocks­tanken: sätt `HOURS_REFERENCE = 1` och `TOKENS_PER_REFERENCE_BLOCK = TOKENS_PER_HOUR`.)*

### 10.3 Datamodell (förslag till tabeller / entiteter)

| Entitet / fält | Syfte |
|----------------|--------|
| `community_project` | `id`, `title`, `description`, `status`, `approved_at`, `council_ref` (länk eller beslutsnummer), `max_tokens_labor` (valfritt tak), `project_lead_member_id`. |
| `work_timesheet` eller `contribution_line` | `project_id`, `member_id`, **`hours`**, `activity_text`, `reported_at`, `status ∈ {submitted, disputed, approved, paid_out}`. |
| `work_verification` (kan vara fält på raden) | `verified_by_member_id` eller `verified_by_role`, `verified_at`. |
| `labor_budget_allocation` (valfritt) | Kopplar **projekt** till **drag från `förening_labor_budget`** när kredit sker. |

### 10.4 Poster i **boken** vid utbetalning av arbete

| Steg | Resonemang |
|------|-------------|
| **A — Omfördelning** från **föreningens arbetsbudget till medlem** | **Debitera `förening_labor_budget`**, **kreditera `medlem`** med `tokens_to_credit`. **Ingen** ny total tokenmängd om budgeten **tidigare** mintats från dokumenterad underlag. |
| **B — Mint direkt mot beslut** | **Mint** till medlem med **`council_resolution_id`** + hänvisning till **timesheet_id** — **använd restriktivt** med samma **transparenta** rutin som övrig mint. |

Rapport: medlemmar ska kunna se **timmar → tokens** och **vilket projekt** varje rad gäller.

### 10.5 Integration med marknadsplatser

Efter **kreditering** ligger tokens på **vanligt medlemskonto** och **samma kassaflöden** gäller vid **handel** (avsnitt **7–9**). Ni behöver **inte** två samtidiga token‑slag (“arbete” kontra ”butik”) om allt för **samma kontotyp** — mindre krång för medlem.

---

## 11. SEK och avstämning

- Betalflöden måste vara **kopplade till föreningens avtal** med betaljämförelse (Swish, kortinlösen).  
- **Periodvis avstämning** mellan **bankens in/ut** och **systemets loggade påfyllningar** — rutin som någon ansvarar för.  
- Moms, bokföring och skatt: **revisor/redovisare**, inte detta dokument.

---

## 12. Backup och spårbarhet

- Transaktioner bör vara **ändringssäkra**: nya rader tilläggs, inte tysta ändringar (eller versionshantering).  
- **Säkerhetskopiering** minst dagligen till **annan plats** än primär server.  
- **Återställningsövning** innan skarp drift med verklig ekonomi.

---

## 13. Säkerhet

- Rollbaserad åtkomst (kassa ser bara sälj, leverantör ser eget flöde om ni tillåter läsning).  
- **Auditlogg** för ändring av **`list_price_tokens`**, **`tourist_price_sek`**, splittregler, **lagersaldi**, **administrativa korrigeringar**, **`HOURS_REFERENCE`**, **`TOKENS_PER_REFERENCE_BLOCK` eller `TOKENS_PER_HOUR`**, **projektstatus** och **verifier‑signaturer för arbetsrader** (synlig för rådet).

---

## 14. Arbetsområden för utveckling eller inköp

- Produktskatalog med streck/QR och leverantörskoppling  
- Kassa med scan eller manuell rad  
- **Bokens** datapersistens (**ledger**‑lik tabell): saldo, export till månadsrapport  
- **Projekt-/bidrag:** godkänd projektlista, **`work_credit_issue`**, tidsåterrapportering, verifier‑flöde (kap. **10**)  
- Identity / inloggning  
- Integration mot vald betalleverantör  

---

## 15. Visa kron‑ och tokenflöden för medlemmar (**en pott eller två spår**) 

En fråga som ofta dyker upp i **presentationen** löses lämpligen i **teknik eller redovisningsrutiner**, inte i själva skylttexten för varorna:

| Spår | Idé | Nytta |
|------|-----|--------|
| **Ett gemensamt flyt** | All inkommande SEK på **ett föreningskonto**; rapporter visar ändå **växlande kronposter** jämfört med **vad som hänt med tokens**. | Enkelt bankkonto; kräver **tydliga avstämningsrutiner.** |
| **Två synliga spår i rapporter** | Flikar eller kolumner för **krono­flöde** och **tokenflöde** även om **underlaget är samma bankkonto**. | Lättare att förklara för medlem utan blandning mellan vad som är **riktiga kronor** och vad som är **inräknade tokens.** |

Om **turist-/krono­priset** och **tokenpriset på hyllan** **skiljer sig** måste databas och självservice ha **båda fälten för samma SKU** — **`list_price_tokens`** och **`tourist_price_sek`** — och regler för **splitt för båda köpvägar** enligt avsnitt **8**.

---

## 16. Versionshistorik

| Version | Datum | Anteckning |
|---------|-------|-------------|
| 1.3 | 2026-05-02 | **§10 Arbete/Ubuntu‑modell**, bidragsprojekt, verifiering, parametertabell **`HOURS_REFERENCE`** + **`TOKENS_PER_REFERENCE_BLOCK`**, bok‑händelse **`work_credit_issue`**, **`förening_labor_budget`**, roller §3, konton §6, omnumrering §11–§16 |
| 1.2 | 2026-05-02 | Linje mot [local-exchange-exempel-grupp.sv.md](local-exchange-exempel-grupp.sv.md): dubbel prissättning, självservice, konsignation + lager, leverantör i tokens, terminologi **boken** §9, splitt för token‑ vs SEK‑köpväg §8.0, startbalans A §5 |
| 1.1 | 2026-05-02 | §14 krono/token‑rapporter; självservice i §3 |
| 1.0 | 2026-05-02 | Första teknikutkast för repot |
