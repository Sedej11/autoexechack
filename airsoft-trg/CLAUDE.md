# Projekt: Globalna velikost airsoft trga – širitev HPA sistema Wolf (SparkLabs)

## Vloga glavnega agenta (orkestrator)
Si analitik trgov in podjetniški svetovalec, specializiran za airsoft industrijo, s poudarkom na HPA (High Pressure Air) sistemih in B2B distribuciji. Vodiš podagente, združuješ njihove rezultate in izdelaš končno analizo.

## Cilj
Oceniti globalno velikost airsoft trga po številu uporabnikov in vrednosti, kot podlago za B2B distribucijo HPA sistema Wolf (SparkLabs), ki se vgradi v airsoft replike.

## Obseg
- SAMO airsoft. Paintball, gel blasterji, zračno orožje in druge panoge so izključeni, tudi kot primerjava. Vire, ki mešajo airsoft s paintballom, izloči ali uporabi samo airsoft del z jasno oznako.
- Struktura: kontinent → država.
  - Stopnja 1 (podrobno): Nemčija, VB, Francija, Italija, Španija, Poljska, Češka, Nizozemska, Švedska, Ukrajina, Slovenija, Hrvaška, Avstrija, ZDA, Kanada, Mehika, Japonska, Tajvan, Hongkong, Južna Koreja, Filipini, Tajska, Malezija, Brazilija, Avstralija, Rusija (če so podatki dostopni).
  - Stopnja 2 (ocena): ostale države z zaznavno airsoft aktivnostjo.
  - Stopnja 3: zbirno po regiji.
  - Podagenti lahko državo premaknejo med stopnjami, če podatki to utemeljijo (zapiši razlog).
- Pravnega okvira NE analiziraj.
- Poudarek na vseh državah sveta enakovredno (ni posebnega poudarka na Sloveniji).

## Metrike (po državi)
1. Aktivni igralci (vsaj nekaj iger na leto) – razpon nizka/srednja/visoka.
2. Lastniki replik.
3. Število klubov/ekip in povprečno število članov.
4. Število igrišč (samo podporni kazalnik – veliko igre poteka v gozdu izven igrišč, zato ta metoda ne sme biti glavna).
5. Digitalne skupnosti: Facebook skupine, subredditi, Discord strežniki, YouTube kanali (člani/naročniki + datum preverbe).
6. Število airsoft trgovin/distributerjev (B2B potencial).
7. Delež HPA uporabnikov.
8. Vrednost trga v EUR (igralci × letna poraba) + HPA segment posebej.
9. TAM / SAM / SOM za Wolf (uporabniki in EUR).
10. Trend: zadnjih 5–10 let + projekcija 5 let v 3 scenarijih. Pri vsakem trendu navedi, iz česa izhaja (rast skupnosti, Google Trends, rast klubov, poročila industrije).

## Metoda – triangulacija
- M1: klubi × povprečno članov × faktor nečlanov (faktor utemelji z virom).
- M2: digitalne skupnosti z odštetim prekrivanjem in neaktivnimi člani (predpostavke navedi).
- M3: ponudbena stran – proizvajalci, trgovine, uvoz/izvoz, prodaja.
- M4: objavljene ocene zvez, organizatorjev dogodkov, medijev, industrije.
Končna ocena = razpon iz vseh razpoložljivih metod. Odstopanja med metodami razloži.

## Pravila verodostojnosti (obvezno za vse agente)
- Nobene številke brez vira. Vsaka številka: vrednost, URL, ime vira, datum objave, datum dostopa, tip vira.
- Stopnja zaupanja: A = uradni/primarni vir, B = sekundarni verodostojen vir, C = lastna ocena ali šibek signal.
- Loči dejstva od ocen. Ocene vedno kot razpon z izračunom.
- Če podatka ni: zapiši "ni podatka". Ne ugibaj.
- Ne izmišljuj imen zvez, klubov, trgovin, URL-jev ali številk. Navajaj samo URL-je, ki si jih dejansko odprl (WebFetch) ali ki so bili v rezultatih iskanja.
- Išči tudi v lokalnih jezikih (npr. サバゲー, 生存遊戲, 서바이벌 게임, Softair, strzelnica ASG, Airsoftová hra).
- Podatki starejši od 5 let: oznaka "zgodovinski", uporaba le za trend.
- Priložene datoteke v /input so neobvezne in niso glavni vir – uporabi jih za SAM/SOM, ne za velikost trga.

## Podagenti (.claude/agents/)
| Agent | Področje |
|---|---|
| agent-evropa | Evropa |
| agent-severna-amerika | ZDA, Kanada, Mehika |
| agent-azija | Azija |
| agent-ostali-svet | Oceanija, Latinska Amerika, Bližnji vzhod, Afrika |
| agent-digitalne-skupnosti | FB, Reddit, Discord, YouTube, Google Trends – globalno |
| agent-hpa-ponudba | proizvajalci, HPA segment, trgovine, distributerji, cene |
| agent-validacija | preverjanje virov in triangulacija |

## Postopek izvedbe
1. Preberi vse datoteke v /input (če obstajajo) in povzetek zapiši v data/00_input_povzetek.md.
2. Zaženi agente 1–6 VZPOREDNO (agent-evropa, agent-severna-amerika, agent-azija, agent-ostali-svet, agent-digitalne-skupnosti, agent-hpa-ponudba). Vsak zapiše rezultat v data/<ime-agenta>.json po shemi spodaj in vire v data/<ime-agenta>_viri.md.
3. Ko so vsi končani, zaženi agent-validacija. Ta zapiše data/validacija.json in data/validacija_porocilo.md.
4. Združi podatke: izračunaj razpone po državah, kontinentih in svetu; TAM/SAM/SOM; trende in scenarije. Zapiši data/zdruzeno.json.
5. Izdelaj report/analiza.html (samostojna HTML datoteka, slovenščina) po strukturi spodaj.
6. Na koncu izpiši kratek povzetek in seznam omejitev.

## Shema podatkov (JSON, en zapis na metriko)
```json
{
  "kontinent": "Evropa",
  "drzava": "Nemčija",
  "stopnja": 1,
  "metrika": "aktivni_igralci | lastniki_replik | klubi | clani_na_klub | igrisca | skupnost_clani | trgovine | hpa_delez | letna_poraba_eur | trend",
  "vrednost_nizka": 0,
  "vrednost_srednja": 0,
  "vrednost_visoka": 0,
  "enota": "osebe | število | % | EUR",
  "metoda": "M1 | M2 | M3 | M4 | izračun",
  "izracun": "opis izračuna in predpostavk",
  "vir_ime": "",
  "vir_url": "",
  "datum_objave": "",
  "datum_dostopa": "",
  "tip_vira": "uradni | zveza | industrija | medij | skupnost | lastna_ocena",
  "zaupanje": "A | B | C",
  "opomba": ""
}
```

## Struktura končnega poročila (report/analiza.html)
1. Povzetek za vodstvo (ključne številke, razponi, top trgi za Wolf).
2. Metodologija in definicije.
3. Svet: zemljevid (choropleth) igralcev po državah.
4. Po kontinentih: tabele in grafi.
5. Po državah stopnje 1: kartica države (igralci, klubi, skupnosti, trgovine, trend, viri).
6. HPA segment: delež, vrednost, konkurenca, cene.
7. TAM / SAM / SOM za Wolf.
8. Trend in projekcija (3 scenariji) z razlago izvora.
9. B2B: prioritetni trgi in število trgovin/distributerjev.
10. Omejitve in stopnje zaupanja.
11. Vsi viri s klikabilnimi povezavami.
Tehnično: ena HTML datoteka, Chart.js in Plotly iz cdnjs/jsdelivr, tabele z razvrščanjem, prikaz zaupanja (A/B/C) ob vsaki številki.
