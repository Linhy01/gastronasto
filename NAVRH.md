# Gastro Na Sto: návrh na zlepšení webu gastronasto.eu

*Audit a návrh ze dne 22. 9. 2026. Klikací prototyp je v [`navrh/index.html`](navrh/index.html), fotky z webu v [`puvodni-web/fotky/`](puvodni-web/fotky/).*

---

## 1. Shrnutí

Web má dobrý základ. Silný slogan **„Naživo chutná líp“**, jasná červeno-bílá identita, fotky z opravdových akcí a jednoduchá jednostránková struktura. Obsahu je ale málo: tři krátké karty, galerie a kontakt. Google i AI asistenti (ChatGPT, Perplexity, Gemini, Google AI Overviews) proto o firmě skoro nic nevědí. Návštěvník nemá žádný formulář, na mobilu nemá tlačítko pro rychlé zavolání a nedozví se, jak objednávka probíhá.

**Deset nejdůležitějších kroků (seřazeno podle poměru dopadu a úsilí):**

| # | Krok | Dopad | Úsilí |
|---|---|---|---|
| 1 | Založit a vyplnit **Google Business Profile** a **Firmy.cz (Seznam)**, sbírat recenze | ★★★★★ | 2 h |
| 2 | Opravit `<title>`, doplnit **meta description**, `lang="cs"`, Open Graph | ★★★★ | 30 min |
| 3 | Přidat **strukturovaná data** (LocalBusiness + FAQ), hotová jsou v prototypu | ★★★★ | 30 min |
| 4 | Vyřešit **dvě domény**: logo říká `NA STO.CZ`, web běží na `.eu` a `.cz` je zaheslovaný WordPress | ★★★★ | 1 h |
| 5 | **Poptávkový formulář** (typ akce, datum, místo, počet hostů) a na mobilu tlačítko „Zavolat“ | ★★★★ | 2 h |
| 6 | Rozšířit texty: pro koho, kde, co nabízíte, jak to funguje, FAQ | ★★★★ | 3 h |
| 7 | **Alt texty** u fotek (dnes jsou všechny prázdné) a popisné názvy souborů | ★★★ | 30 min |
| 8 | Smazat „Hello world!“, „Sample Page“ a prázdné stránky, zapnout `robots.txt` a `sitemap.xml` | ★★★ | 20 min |
| 9 | Doplnit **zákonné údaje** (provozovatel, IČO, sídlo), které podnikatel musí mít na webu | ★★★ | 10 min |
| 10 | Použít **nevyužité fotky** (15 z 22 leží v knihovně) a zmenšit je do WebP | ★★ | 1 h |

---

## 2. Audit současného stavu

### Co funguje a musí zůstat
- **Slogan „Naživo chutná líp“** je výborný: krátký, zapamatovatelný a sedí k tomu, že se jídlo připravuje přímo před hosty.
- **Barvy a logo:** červená `#e53935`, černá a bílá, logo s fajfkou ✔. Stejnou identitu nesou i fotky (červený stan, károvaný ubrus, kamenný pult s logem), takže web a realita k sobě sedí.
- **Struktura:** jedna stránka, sticky hlavička, velký hero s tlačítkem „Nezávazná poptávka“ a karty služeb. Je to správný typ webu pro malý catering.
- **Proklik na telefon a e-mail** (`tel:` a `mailto:`) a Instagram.
- **HTTPS** včetně přesměrování `www` a `http`, komprese gzip a `canonical`.

### Co nefunguje

**Obsah a UX**
- Texty mají dohromady asi 80 slov. Chybí nabídka, počty hostů, oblast působnosti, postup objednávky, reference a FAQ.
- Tlačítko „Nezávazná poptávka“ vede jen na seznam kontaktů. **Chybí formulář**, takže klient musí sám vymyslet, co napsat.
- Sekce `#speciality` je **prázdná**. V HTML je navíc prázdný odstavec a komentář „HERO se bere ze šablony…“.
- V menu jsou jen dvě položky (Služby, Galerie) a chybí odkaz na Kontakt.
- Na mobilu není žádné stálé tlačítko pro zavolání.
- Hero fotka je **na výšku** (1200×1600), ale zobrazuje se na šířku, takže se na desktopu hodně ořízne.
- Logo se v hero opakuje podruhé hned pod logem v hlavičce.

**SEO**
- `<html lang="en-US">`, přestože je web česky. Google i čtečky obrazovky tak dostávají špatný jazyk.
- **Chybí meta description**, Open Graph (náhled při sdílení na Facebooku či WhatsAppu) i strukturovaná data.
- `<title>` je „Gastro Na Sto – Partner vaší akce“ a neobsahuje klíčová slova (catering, koktejlový bar, Mariánské Lázně).
- H1 je jen „Naživo chutná líp“, takže Google z něj nepozná, o čem stránka je.
- **Všech 7 fotek v galerii má prázdný `alt`** a soubory se jmenují `279509da-1787-….jpeg`.
- `robots.txt` i `sitemap.xml` vrací **404**.
- Veřejně indexovatelné jsou stránky **„Hello world!“** (`/?p=1`) a **„Sample Page“** s anglickým textem o kurýrovi z Los Angeles. K tomu prázdné stránky Rezervovat, Galerie a Služby (`/?page_id=33,35,36`).
- Adresy mají tvar `?page_id=` místo hezkých URL (permalinky nejsou nastavené).

**Lokální vyhledávání (GEO)**
- „Mariánské Lázně“ se na webu objevuje jen jednou, v šedém podtitulku.
- Chybí adresa, oblast působnosti, mapa i odkaz na Google nebo Mapy.cz.
- Nevím, jestli existuje profil na Googlu nebo Firmy.cz. Pokud ne, je to **priorita č. 1**.

**Značka a důvěra**
- **Doménový zmatek:** logo i stan nesou nápis **„Gastro NA STO.CZ“**, web ale běží na **gastronasto.eu** a na **gastronasto.cz** je zaheslovaná instalace WordPressu. Kdo si z plachty opíše `.cz`, narazí na přihlašovací obrazovku.
- Kontaktní e-mail je osobní Gmail. Působí méně profesionálně než `info@gastronasto.cz`.
- Chybí identifikace provozovatele (jméno nebo firma, IČO, sídlo). Podnikatel ji musí na webu uvádět podle § 435 občanského zákoníku.
- Nejsou tu žádné recenze ani reference.

**Technika a výkon**
- Obrázky na úvodní stránce mají **asi 1,36 MB** a jsou ve formátu JPEG. Ve WebP by vyšly asi na třetinu.
- Obrázky nemají cache hlavičky (`Cache-Control`/`Expires`), takže se při každé návštěvě stahují znovu.
- Načítá se jQuery a jQuery Migrate, které šablona nepotřebuje (`main.js` je prázdný). Font Awesome se stahuje kvůli pluginu lightbox, který se nepoužívá.
- Web ukazuje verzi WordPressu (`generator`), má otevřené `xmlrpc.php` a veřejné REST API se seznamem médií i stránek. Je to běžné, ale zbytečně to zvětšuje prostor pro útok.

---

## 3. Design a UX: co zachovat a co změnit

Cílem je **evoluce, ne revoluce**. Stávající zákazník má web poznat.

### Zachovat (DNA značky)
| Prvek | Dnes | V návrhu |
|---|---|---|
| Slogan | H1 „Naživo chutná líp“ | Zůstává jako velký nadpis v hero |
| Červená | `#e53935` | Stejná na dekorace. Na tlačítka tmavší `#c62828`, protože bílý text na původní červené má kontrast jen 4,2:1 (WCAG vyžaduje 4,5:1) |
| Logo | Hlavička + hero | Hlavička a patička. V hero ho nahrazuje fotka |
| Tlačítko | Červená „pilulka“ | Stejný tvar a druhé průhledné tlačítko s telefonem |
| Hero | Fotka s tmavým překryvem | Stejný princip. Přechod překryvu nechává fotku nahoře víc vidět |
| Karty | Zaoblení 14 px, jemný stín | Stejné, jen s fotkou nahoře |
| Emoji 🍸🔥🍳 | V nadpisech karet | Ponechány, jsou to „lidské“ prvky značky |

### Přidat
- **Písmo Montserrat** na nadpisy. Je to geometrický bezpatkový font velmi podobný písmu v logu, takže web a logo budou působit jednotně. Text zůstává v Inter.
- **Károvaný proužek** jako motiv ubrusu ze stánku (červeno-bílý „gingham“). Odděluje sekce a na webu i u stánku působí stejně.
- **Tmavá sekce galerie.** Večerní fotky baru pod červeným stanem na tmavém pozadí vyniknou.
- **Mozaiková galerie** s osmi nejlepšími fotkami místo tří nesourodých bloků. Kuchař u plotny, večerní bar a hamburger dnes na webu vůbec nejsou.

### Nová struktura stránky
1. **Hero**: slogan, jedna věta o čem to je, dvě tlačítka (Poptávka, Zavolat) a čtyři výhody s ✓
2. **Úvodní odstavec**: kdo jste, odkud a pro koho, ve dvou větách (důležité pro AI, viz kap. 6)
3. **Služby**: tři karty s fotkou a štítky „Pro jaké akce“ (svatby, firemní akce, festivaly…)
4. **Ukázka nabídky**: koktejly a grill jako menu. Položky jsem vzal z fotek tabulí na stánku
5. **Jak to funguje**: poptávka, nabídka, potvrzení, akce
6. **Galerie**
7. **Reference**: recenze klientů
8. **Poptávkový formulář** a kontakty
9. **FAQ**: pět častých otázek
10. **Patička**: firemní údaje, IČO, adresa

### Použitelnost (UX)
- **Formulář** místo holého kontaktu: typ akce, datum, místo, počet hostů, služby a telefon. Díky tomu dostanete poptávky se vším potřebným najednou.
- **Plovoucí tlačítko „☎ Zavolat“** na mobilu, kde je volání nejčastější akce.
- **Hamburger menu** na mobilu. Dnešní šablona ho nemá, `main.js` je prázdný.
- **Přístupnost:** odkaz „Přeskočit na obsah“, viditelný fokus, `alt` texty, správný jazyk a kontrast tlačítek.
- Sticky hlavička s tlačítkem **„Poptávka“** vpravo, dostupná odkudkoli.

---

## 4. SEO (klasické vyhledávání)

### Klíčová slova a kam patří
| Dotaz (odhad záměru) | Kam ho umístit |
|---|---|
| catering Mariánské Lázně | title, H1 podtitul, úvodní odstavec |
| koktejlový bar na akci / mobilní bar | title, karta Služby, podstránka (fáze 2) |
| catering na svatbu Karlovarský kraj | FAQ, podstránka „Svatby“ (fáze 2) |
| bramboráky / grill na akci | nabídka, karta Grill |
| firemní catering Cheb / Karlovy Vary | úvodní odstavec, oblast působnosti |

Skutečné objemy hledání ověřte v Google Search Console (po 4–6 týdnech provozu) nebo v Seznam Sklik plánovači. Tabulka je výchozí odhad.

### Konkrétní úpravy (vše je hotové v prototypu)
```html
<html lang="cs">
<title>Catering a koktejlový bar na akce | Mariánské Lázně | Gastro Na Sto</title>
<meta name="description" content="Mobilní koktejlový bar a grill na svatby, firemní večírky,
  oslavy a festivaly v Mariánských Lázních a okolí. Alko i nealko koktejly, bramboráky,
  klobásy. Nezávazná poptávka do 24 h.">
```
- **H1** „Naživo chutná líp.“ a v něm podtitul „Mobilní koktejlový bar a grill na svatby, firemní akce…“. Slogan tak zůstává a Google dostane klíčová slova.
- **Open Graph** a obrázek 1200×630 (`navrh/img/og-image.jpg`) pro hezký náhled na Facebooku, WhatsAppu a Messengeru.
- **Alt texty** u všech fotek. Návrhy jsou v [`puvodni-web/fotky/README.md`](puvodni-web/fotky/README.md).
- **Popisné názvy souborů** (`kuchar-smazi-bramboraky.webp` místo `IMG_3160.jpeg`).
- **Permalinky** ve WordPressu (Nastavení → Trvalé odkazy → „Název příspěvku“).
- **Smazat** stránky Hello world, Sample Page a prázdné stránky Rezervovat, Galerie a Služby.
- **Sitemap a robots:** SEO plugin (Rank Math nebo Yoast) je vygeneruje. Vzor je v `navrh/robots.txt` a `navrh/sitemap.xml`.
- **Google Search Console** a **Seznam Webmaster**: ověřit web a odeslat sitemapu. V Česku má Seznam pořád podstatný podíl vyhledávání.

### Fáze 2: podstránky
Jedna stránka má strop. Až bude obsah, vyplatí se samostatné stránky, z nichž každá cílí na jeden dotaz:
- `/koktejlovy-bar-na-akci/`: nabídka drinků, fotky baru, ceník od…
- `/catering-svatba/`: svatby, reference ze svateb, FAQ ke svatbám
- `/firemni-catering/`: firemní akce, fakturace, kapacity
- případně `/akce/` s kalendářem veřejných akcí, kde budete stát („Kde nás najdete tento víkend“). To je skvělé pro lokální vyhledávání i Instagram.

---

## 5. GEO: lokální vyhledávání (mapy, „catering poblíž“)

U malé firmy s lokálním působením rozhoduje o zakázkách víc **profil v mapách** než samotný web.

1. **Google Business Profile** (business.google.com)
   - Kategorie: *Catering*, doplňkové *Koktejlový bar* a *Mobilní občerstvení*
   - Typ „firma poskytující služby v oblasti“, bez veřejné adresy, s oblastí Mariánské Lázně, Cheb, Karlovy Vary, Tachov…
   - Nahrát 15–20 fotek z `puvodni-web/fotky/`, doplnit popis (převzít úvodní odstavec), odkaz na web a telefon
   - **Sbírat recenze:** po každé akci poslat klientovi krátký odkaz na recenzi. Recenze jsou nejsilnější lokální signál.
2. **Firmy.cz (Seznam)**: totéž. Zobrazuje se v Mapy.cz a ve výsledcích Seznamu.
3. **Stejné údaje všude (NAP):** název, telefon a web musí být **stejné** na webu, Googlu, Firmy.cz, Instagramu a Facebooku. Proto je nutné vyřešit `.cz` a `.eu`.
4. **Katalogy:** svatební portály a katalogy dodavatelů, stránky akcí a slavností v regionu, turistické informační centrum Mariánských Lázní, spolupráce se svatebními místy a hotely v okolí (odkaz „doporučení dodavatelé“).
5. **Na webu:** oblast působnosti vypsaná slovy (města), `areaServed` ve strukturovaných datech (hotovo v prototypu) a do budoucna i mapa s okruhem.
6. **Instagram:** do bia doplnit „Catering & koktejlový bar · Mariánské Lázně“ a odkaz na web.

---

## 6. GEO: viditelnost v AI vyhledávačích a asistentech

*(Generative Engine Optimization: aby ChatGPT, Perplexity, Gemini, Claude a Google AI Overviews firmu našly a doporučily.)*

Když se někdo zeptá asistenta *„kdo dělá koktejlový bar na svatbu u Mariánských Lázní?“*, AI potřebuje najít **jasná, stručná a strojově čitelná fakta**. Dnes jich na webu je minimum.

1. **„Odpovědní“ odstavec hned pod hero:** kdo, co, kde, pro koho a kolik hostů ve dvou větách. AI modely takové shrnutí citují doslova. Hotovo v prototypu.
2. **Strukturovaná data JSON-LD:** `LocalBusiness`/`FoodEstablishment` (název, telefon, město, `areaServed`, služby, Instagram v `sameAs`) a `FAQPage`. Hotovo v prototypu, jen doplnit IČO a adresu.
3. **FAQ sekce** s otázkami tak, jak je lidé kladou („Kde všude jezdíte?“, „Kolik to stojí?“). Otázka s odpovědí je formát, který AI přebírá nejraději.
4. **`llms.txt`** v kořeni webu: stručný popis firmy v Markdownu pro AI crawlery. Vzor je v `navrh/llms.txt`.
5. **`robots.txt`** výslovně povolující AI crawlery (GPTBot, OAI-SearchBot, ClaudeBot, PerplexityBot, Google-Extended). Vzor je v `navrh/robots.txt`.
6. **Text v HTML, ne v obrázcích:** ceny a nabídka dnes existují jen na tabulích na fotkách a AI je nepřečte. V prototypu jsou jako text.
7. **Konzistence napříč webem:** AI si fakta ověřuje z více zdrojů (Google profil, Firmy.cz, Instagram, katalogy). Proto stejné údaje všude.
8. **Konkrétní čísla a fakta:** počet hostů, rozměr stánku, požadavky na elektřinu, jak dlouho dopředu objednat. Vágní text („rádi pro vás připravíme“) AI nemá co citovat.

---

## 7. Technika a výkon

| Opatření | Jak |
|---|---|
| Obrázky do **WebP**, max. 1280 px, `srcset` | Plugin (např. Converter for Media / Imagify) nebo ručně. Hotové verze jsou v `navrh/img/` |
| Hero **na šířku** | V prototypu je hero fotka na šířku, obsluha podává nápoj (`hero-1280.webp`, asi 200 kB) |
| `loading="lazy"` a `width`/`height` u obrázků | Hotovo v prototypu, žádné poskakování layoutu (CLS) |
| Cache hlavičky pro obrázky, CSS a JS | `.htaccess`: `ExpiresByType image/* "access plus 1 year"` |
| Odebrat jQuery, jQuery Migrate a nepoužívaný lightbox plugin | Šablona je nepotřebuje |
| Skrýt verzi WP, vypnout `xmlrpc.php` | Bezpečnostní plugin nebo `.htaccess` |
| Pravidelné aktualizace a záloha WordPressu | – |

**Cíl:** PageSpeed Insights (mobil) nad 90 a LCP pod 2,5 s.

---

## 8. Doménová strategie (`.cz` a `.eu`)

Dnes: logo a stan říkají **gastronasto.cz**, web běží na **gastronasto.eu** a `.cz` je zaheslovaná instalace WordPressu.

**Doporučení:** jako hlavní doménu zvolit **gastronasto.cz**. Je na logu i na stanu, lidé si ji zapamatují a pro českého zákazníka je přirozenější. Doménu `.eu` přesměrovat na `.cz` trvalým přesměrováním 301. Druhou možností je opačný směr (`.cz` → `.eu`), ale pak by bylo potřeba upravit logo i plachtu.

Zaheslovanou instalaci na `.cz` buď dokončit jako hlavní web, nebo smazat. Stejně tak **e-mail na vlastní doméně** (`info@gastronasto.cz` nebo `filip@gastronasto.cz`).

> Prototyp zatím počítá s `gastronasto.eu`. Po rozhodnutí stačí nahradit doménu v `index.html`, `robots.txt`, `sitemap.xml` a `llms.txt`.

---

## 9. Co je potřeba od majitele doplnit

Tyto údaje jsem nemohl zjistit a v prototypu jsou **žlutě zvýrazněné**:

- [ ] Jméno provozovatele nebo firmy, **IČO**, sídlo (povinné na webu)
- [ ] Skutečná **oblast působnosti** (jak daleko jezdíte, za příplatek?)
- [ ] **Kapacita**: pro kolik hostů minimálně a maximálně
- [ ] Jak rychle odpovídáte na poptávku (v návrhu „do 24 h“)
- [ ] Požadavky na místo (plocha, elektřina, voda)
- [ ] Jak dlouho dopředu rezervovat, záloha ano či ne
- [ ] Aktuální nabídka a ceny (převzato z fotek tabulí, ověřit), je hamburger stále v nabídce?
- [ ] 2–3 **reference** od klientů (jméno, typ akce, datum) a svolení je zveřejnit
- [ ] Seznam akcí, kde jste byli (festivaly, slavnosti), pro sekci reference a důvěryhodnost
- [ ] Rozhodnutí **.cz nebo .eu**
- [ ] Svolení osob na fotkách (obsluha, kuchař) s použitím na webu a v Google profilu

---

## 10. Plán realizace

**Fáze 1: rychlé opravy (1 den, ve stávajícím WordPressu)**
- lang, title, description, OG, JSON-LD, alt texty
- smazat Hello world, Sample Page a prázdné stránky, nastavit permalinky, SEO plugin se sitemapou a robots.txt
- Google Business Profile a Firmy.cz
- doplnit IČO a adresu do patičky

**Fáze 2: nová podoba (asi 1 týden)**
- převést prototyp `navrh/` do šablony `gns-bistro-editable` (stejné názvy tříd `gns-*`, přechod je přímočarý)
- formulář přes Contact Form 7 nebo WPForms s odesíláním na e-mail
- WebP obrázky, cache, odebrat jQuery
- vyřešit doménu a firemní e-mail

**Fáze 3: růst (průběžně)**
- podstránky Svatby, Firemní akce a Koktejlový bar
- recenze po každé akci
- sekce „Kde nás najdete“ s veřejnými akcemi
- Search Console a Seznam Webmaster, po dvou měsících vyhodnotit dotazy

**Alternativa:** protože jde o jednostránkový web, dá se prototyp nasadit rovnou jako **statický web** (Cloudflare Pages, Netlify, GitHub Pages) zdarma, bez WordPressu a bez nutnosti aktualizací. Nevýhodou je, že změny textů vyžadují úpravu HTML. Pokud majitel web často sám upravuje, zůstaňte u WordPressu.

---

## Obsah repozitáře

```
NAVRH.md                  ← tento dokument
navrh/                    ← klikací prototyp nového webu
  index.html              ← otevřít v prohlížeči
  style.css
  img/                    ← fotky zmenšené do WebP (≈ 2 MB celkem, na stránce se načítá výrazně méně)
  robots.txt, sitemap.xml, llms.txt  ← vzory pro nasazení
puvodni-web/
  fotky/                  ← všech 24 unikátních fotek z webu v plném rozlišení + README s popisy
  snapshot-2026-09/       ← HTML a CSS původní stránky pro srovnání
```
