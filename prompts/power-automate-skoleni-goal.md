# /goal prompt: Celodenní HTML školení Power Automate & Power Platform (výroba)

> **Jak použít:** Zkopíruj celý blok níže (od `/goal` dál) do Claude Code.
> **Předtím** připrav prostředí podle sekce „Předpoklady“ na konci tohoto souboru. Bez testovacího tenantu Claude Code nemůže flow ověřit na reálném Power Automate.

---

```text
/goal Vytvoř a na reálném Power Automate / Power Apps ověř kompletní celodenní (8 h) interaktivní HTML školení „Power Automate v praxi výrobní firmy“. Cíl je splněn až tehdy, když jsou splněna VŠECHNA kritéria v sekci „DEFINITION OF DONE“ a existuje soubor TEST-REPORT.md s důkazy.

## ROLE
Jsi senior Power Platform architekt (MCT, 10+ let praxe), lektor a instruktážní designér. Píšeš česky, srozumitelně, prakticky, s příklady z výroby (strojírenství, automotive, potravinářství). Nevymýšlíš si: každý název akce, konektoru, licence a funkce výrazu ověřuješ proti aktuální dokumentaci Microsoft Learn (learn.microsoft.com/power-automate, /power-apps, /power-platform) a proti reálnému UI. Kde se UI liší od dokumentace, platí UI a rozdíl zapíšeš.

## CÍLOVÁ SKUPINA
- 8–15 účastníků z výrobních firem: mistři, procesní inženýři, IT/OT specialisté, kvalita, údržba, nákup.
- Úroveň: začátečník až mírně pokročilý; umí Excel a Teams, neprogramuje.
- Prostředí účastníků: Microsoft 365 (Teams, SharePoint, Outlook), licence M365 (standardní konektory); prémiové funkce jasně označ.
- Jazyk: čeština. Názvy prvků UI uváděj PŘESNĚ tak, jak je ukazuje anglické UI Power Automate, s českým vysvětlením v závorce, např. „When an item is created (Při vytvoření položky)“.

## VÝSTUP (struktura repozitáře)
/skoleni/index.html            – hlavní rozcestník + harmonogram dne
/skoleni/moduly/*.html          – teoretické moduly (nebo sekce v jednom souboru, viz níže)
/skoleni/usecases/*.html        – 8 use cases, každý jako interaktivní průvodce krok za krokem
/skoleni/assets/                – CSS, JS, obrázky, screenshoty z reálného tenantu
/skoleni/lab/                   – podklady pro lab: CSV/Excel s testovacími daty, definice SharePoint seznamů (JSON/PnP šablona nebo skript), exportované řešení (.zip) z Power Platform
/skoleni/lektor.html            – lektorský manuál (časování, poznámky, časté chyby účastníků, řešení)
/tests/                         – Playwright testy HTML školení
TEST-REPORT.md                  – protokol ověření na reálném Power Automate

Technické požadavky na HTML:
- Funguje OFFLINE otevřením index.html (žádný build, žádný server). Vanilla HTML/CSS/JS, bez frameworků a bez externích CDN.
- Responzivní (projektor 1920×1080 i notebook 1366×768), světlý i tmavý režim, tiskový styl (@media print) pro handout.
- Postranní navigace, ukazatel průběhu dne, kotvy na každou sekci, vyhledávání v obsahu.
- Kódové bloky s výrazy (expressions) mají tlačítko „Kopírovat“.
- Přístupnost: sémantické HTML, ovládání klávesnicí (← → pro kroky), kontrast WCAG AA, alt texty.
- Progres účastníka (odškrtnuté kroky, výsledky kvízů) ukládej do localStorage, vše obalené try/catch – stránka musí fungovat i bez něj.

## HARMONOGRAM 8 H (09:00–17:00)
Navrhni přesný časový plán s bloky teorie, demo, hands-on, kvíz a přestávky (2× 15 min káva, 45 min oběd). Orientačně:
1. 09:00–09:45  Power Platform jako celek
2. 09:45–10:45  Anatomie flow a logika tvorby
3. 10:45–11:00  Přestávka
4. 11:00–12:15  Data, dynamický obsah, výrazy, proměnné, podmínky, smyčky (mini cvičení)
5. 12:15–13:00  Oběd
6. 13:00–15:30  HLAVNÍ LAB: stavba vybraného use case end-to-end (Power App + flow), s přestávkou 15 min
7. 15:30–16:15  Chybové stavy, monitoring, governance, ALM, licence
8. 16:15–16:45  Přehled ostatních 7 use cases + jak je postavit doma
9. 16:45–17:00  Kvíz, Q&A, další kroky

## TEORETICKÉ MODULY (každý: cíle, výklad, diagram, příklad z výroby, časté chyby, kvíz 3–5 otázek)
M1 Power Platform celkově: Power Apps (canvas vs model-driven), Power Automate (cloud flows, desktop flows/RPA, process mining), Power BI, Copilot Studio, Power Pages, Dataverse, AI Builder, konektory (standard/premium/custom), on-premises data gateway (napojení na výrobní SQL/ERP), prostředí (environments), DLP politiky, CoE Starter Kit, licencování (M365 vs Premium vs Process) – srozumitelná tabulka „co můžu s licencí M365“.
M2 Typy cloud flow: Automated, Instant, Scheduled; kdy co použít; tabulka rozhodování.
M3 Anatomie a logika tvorby flow: trigger → akce → výstupy; dynamický obsah; nový designer vs. klasický; Copilot v Power Automate (co umí a kde selhává); pojmenování akcí; komentáře; „myšlení ve flow“ – jak rozložit byznys proces na trigger, data, rozhodnutí, notifikace, záznam.
M4 Práce s daty: SharePoint seznamy, Excel Online (tabulky!), Dataverse; Get items s filtrem OData; Select, Filter array, Compose, Create HTML table, Parse JSON.
M5 Výrazy (Workflow Definition Language): concat, formatDateTime, utcNow, convertTimeZone (časové pásmo „Central Europe Standard Time“), addDays, if, equals, empty, coalesce, length, first, items(), variables(), outputs(), body(); rozdíl mezi WDL výrazy ve flow a Power Fx v Power Apps.
M6 Řízení toku: Condition, Switch, Apply to each (a concurrency), Do until, Scope, proměnné (Initialize/Set/Increment/Append), paralelní větve.
M7 Lidé v procesu: Approvals (Start and wait for an approval, typy schvalování), Teams (Post message, adaptivní karty, Post adaptive card and wait for a response), Outlook e-maily.
M8 Robustnost: Configure run after, vzor Try/Catch/Finally pomocí Scope, retry policy, trigger conditions, timeouts, pagination, limity a throttling, run history, ladění.
M9 ALM a governance: Solutions, environment variables, connection references, export/import, vlastnictví flow a sdílení, co dělat, když autor odejde z firmy, bezpečnost dat z výroby.

## 8 USE CASES Z VÝROBY
Připrav všech 8. U každého: byznys problém, přínos (úspora času/ROI odhad), role a aktéři, datový model (SharePoint seznam: sloupce, typy, povinnost, výchozí hodnoty), diagram procesu (inline SVG), potřebné licence (standard/premium), obtížnost (★–★★★), odhad času stavby, testovací scénář s konkrétními daty, očekávaný výsledek, rozšíření „pro pokročilé“.
1. Hlášení poruchy stroje z tabletu u linky → evidence → notifikace údržby v Teams → eskalace, pokud porucha není převzata do 30 min → uzavření a výpočet prostoje (MTTR). [Power App + flow] ← DOPORUČENÝ HLAVNÍ LAB
2. Schvalování požadavku na náhradní díly – vícestupňové schválení podle částky (mistr → vedoucí údržby → ředitel) s Approvals.
3. Neshoda kvality (NCR) – záznam s fotkou z výroby, přiřazení řešitele, termín, upomínky, uzavření.
4. Denní směnový / OEE report – Scheduled flow čte Excel/SharePoint, spočítá souhrn, pošle HTML tabulku vedení v 6:15.
5. Hlídání minimální zásoby (reorder point) – denní kontrola stavu, souhrnná notifikace nákupu, zamezení duplicitním upozorněním.
6. Kalibrace měřidel – evidence měřidel, upomínky 30/7/0 dní před expirací, blokace propadlých.
7. Onboarding nového pracovníka výroby – checklist BOZP, školení, OOPP, přiřazení úkolů (Planner), potvrzení mistrem.
8. Zpracování dodacích listů od dodavatelů – příloha e-mailu → uložení na SharePoint → (volitelně AI Builder extrakce, premium) → záznam a kontrola proti objednávce.

### Formát průvodce krok za krokem (KLÍČOVÉ)
Každý use case je interaktivní stepper: na obrazovce je vždy JEDEN krok, tlačítka „Zpět“ / „Další“, ukazatel „Krok 7 / 23“, odškrtávání hotovo. Každý krok obsahuje:
- Co a proč děláme (1–2 věty, byznys logika).
- Kde kliknout: přesná cesta v UI (např. „+ New step → vyhledat ‚Get items‘ → SharePoint → Get items“), podle aktuálního designeru.
- Konfigurace akce: tabulka parametr → hodnota (včetně dynamického obsahu a přesných výrazů ke zkopírování).
- Přejmenování akce na doporučený název (konvence pojmenování).
- Screenshot z reálného tenantu (assets/…/krok-07.png) se zvýrazněním, kam kliknout.
- Kontrola: co má účastník vidět / jak ověřit, že krok funguje (Test → Manually).
- Častá chyba a řešení (rozbalovací box).
- Stav flow po tomto kroku: zmenšený „strom“ flow, kde je nově přidaná akce zvýrazněná – účastník vidí, jak flow roste.
Na konci: kompletní přehled flow, testovací scénář, kontrolní seznam, export řešení ke stažení.

Pro HLAVNÍ LAB (use case 1) postav i canvas Power App: obrazovky (výběr stroje/linky, formulář hlášení s fotkou, přehled mých hlášení, detail pro údržbu s tlačítky Převzít/Vyřešit), Power Fx vzorce, napojení na SharePoint, volání flow z aplikace (Power Automate (Power Apps V2) trigger / „Respond to a PowerApp or flow“). Stejný stepper formát i pro aplikaci. Rozplánuj lab tak, aby ho průměrný účastník stihl za 2,5 h; přidej „záchranné body“ (hotové mezistavy v řešení .zip), kdyby někdo nestíhal.

## OVĚŘENÍ NA REÁLNÉM POWER AUTOMATE (povinné, ne předstírané)
Přihlašovací údaje k testovacímu tenantu jsou v proměnných prostředí PP_TENANT_USER, PP_TENANT_PASSWORD a PP_ENVIRONMENT_URL. Nikdy je nezapisuj do repozitáře, logů, screenshotů ani commitů.
1. Ověř dostupnost: make.powerautomate.com, make.powerapps.com, SharePoint testovacího tenantu. Pokud přihlášení blokuje MFA, podmíněný přístup nebo síť, ZASTAV a vypiš mi přesně, co potřebuješ (neobcházej bezpečnostní mechanismy).
2. Připrav testovací data: vytvoř SharePoint web/seznamy podle datových modelů (preferuj PnP PowerShell / Microsoft Graph / pac CLI; jinak Playwright v UI).
3. Pro HLAVNÍ LAB (use case 1) a aspoň 2 další use cases (doporučuji 2 a 4) proveď instrukce ze stepperu DOSLOVA přes Playwright v prohlížeči, jako by je dělal účastník. Po každém kroku pořiď screenshot do /skoleni/assets/. Pokud instrukce neodpovídá UI (jiný název, jiné umístění, chybějící pole), oprav HTML a zaznamenej změnu.
4. Spusť flow s testovacími daty, zkontroluj run history (všechny akce zelené), ověř výsledek (položka v seznamu, zpráva v Teams, e-mail, schválení). Otestuj i chybovou větev (např. neexistující stroj, odmítnuté schválení, timeout eskalace se zkrácenou dobou).
5. Postav Power App, publikuj ji, otestuj odeslání hlášení → flow se spustí → data se propíšou zpět do aplikace.
6. Vše zabal do Solution, exportuj (.zip, unmanaged) do /skoleni/lab/ včetně „záchranných bodů“.
7. Zbývajících 5 use cases ověř alespoň: validace všech výrazů (spuštění v Compose ve testovacím flow), existence všech akcí/konektorů v aktuálním UI a licenční zařazení.
8. Do TEST-REPORT.md zapiš pro každý use case: co bylo ověřeno, jak, datum, výsledek (✅ ověřeno v tenantu / 🟡 ověřeny výrazy a akce / ❌ neověřeno + důvod), run ID, odkazy na screenshoty, nalezené odchylky a opravy. Nic neoznačuj jako ověřené, pokud to neproběhlo.

## TESTY HTML
Playwright testy v /tests/: všechny stránky se načtou bez chyb v konzoli; navigace a odkazy fungují (žádné 404); stepper Zpět/Další/klávesnice funguje u všech 8 use cases; tlačítko Kopírovat funguje; localStorage nedostupný → stránka funguje; layout bez horizontálního scrollu na 1366 i 1920 px; tiskový náhled bez navigace. Testy musí projít.

## KVALITA OBSAHU
- Každý výraz je syntakticky správný a otestovaný. Žádné „lorem ipsum“, žádné TODO.
- Konzistentní terminologie (slovníček pojmů CZ/EN jako samostatná stránka).
- Časová pásma, formáty data (dd.MM.yyyy HH:mm) a čeština v e-mailech/Teams správně.
- U každé prémiové funkce viditelný štítek „Premium“.
- Uveď datum ověření a verzi UI (Power Automate se mění – uveď „platné k <datum>“).

## POSTUP PRÁCE
1. Nejdřív vytvoř PLAN.md (osnova, harmonogram, seznam souborů, testovací strategie) a zkontroluj ho proti tomuto zadání.
2. Ověř aktuální stav UI a dokumentace (Microsoft Learn), teprve pak piš obsah.
3. Postav kostru HTML + design systém, pak moduly, pak use cases, pak lab.
4. Ověř v reálném tenantu, oprav, doplň screenshoty.
5. Spusť testy, dokud neprojdou. Commituj průběžně po logických celcích.

## DEFINITION OF DONE
- [ ] /skoleni/index.html se otevře offline a vede na všechny moduly M1–M9, 8 use cases, lektorský manuál a slovníček.
- [ ] Harmonogram dává dohromady přesně 8 h včetně přestávek.
- [ ] Všech 8 use cases má kompletní stepper (každý krok s cestou v UI, konfigurací, kontrolou, častou chybou, stavem flow).
- [ ] Hlavní lab (use case 1) obsahuje Power App + flow, je postaven a end-to-end otestován v reálném tenantu, se screenshoty.
- [ ] Minimálně 3 use cases ✅ ověřeny v tenantu, ostatní minimálně 🟡; vše pravdivě v TEST-REPORT.md.
- [ ] Exportované řešení(a) .zip a testovací data jsou v /skoleni/lab/.
- [ ] Všechny Playwright testy procházejí.
- [ ] Žádné přihlašovací údaje ani osobní data v repozitáři (zkontroluj git diff a screenshoty).
- [ ] Vše commitnuto a pushnuto.
```

---

## Předpoklady (připrav před spuštěním)

1. **Testovací tenant** – ideálně Microsoft 365 Developer Program nebo trial s Power Automate a Power Apps, **ne produkční tenant firmy**. Uživatel bez MFA nebo s výjimkou podmíněného přístupu jen pro testy (jinak Claude Code přihlášení neprojde a zastaví se).
2. **Proměnné prostředí** v Claude Code (v cloudu: nastavení prostředí → Environment variables / secrets):
   `PP_TENANT_USER`, `PP_TENANT_PASSWORD`, `PP_ENVIRONMENT_URL`.
3. **Síť** – povolené domény: `*.microsoft.com`, `*.microsoftonline.com`, `*.powerautomate.com`, `*.powerapps.com`, `*.sharepoint.com`, `*.office.com`, `*.dynamics.com`, `graph.microsoft.com`, `learn.microsoft.com`.
4. **Nástroje** (volitelně, Claude Code si je umí doinstalovat): Playwright (Chromium), `pac` CLI (Power Platform CLI), PnP PowerShell.
5. **Teams** v tenantu s týmem např. „Údržba“ a kanálem „Poruchy“ pro testování notifikací.
