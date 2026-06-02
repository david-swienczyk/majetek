# Test checklist — Majetková hlášenka prototyp

Tento soubor slouží jako ruční regression checklist. Před tím, než řekneme „hotovo“, projdi relevantní testy níže a doplň výsledek.

## Jak zapisovat výsledek

Používej jednoduché značky:

- `[ ]` netestováno
- `[x]` prošlo
- `[!]` problém / potřeba opravit
- `[-]` nerelevantní pro danou změnu

Doporučený zápis poznámky:

```md
- [!] Test název — co přesně selhalo, zařízení/prohlížeč, kroky reprodukce
```

---

## Smoke test celého flow

- [ ] Prototyp se načte bez viditelné chyby.
- [ ] Na prvním kroku je vidět produkt, stepper, nadpis a CTA.
- [ ] CTA „Pokračovat“ je na začátku disabled.
- [ ] Po vyplnění povinných polí v každém kroku jde pokračovat dál.
- [ ] Tlačítko „Zpět“ vrací na předchozí krok bez rozbití obsahu.
- [ ] Bottom navigation nepřekrývá obsah formuláře.
- [ ] Stepper odpovídá aktuálnímu kroku.
- [ ] Finální odeslání zobrazí potvrzovací obrazovku.

---

## Krok 1 — Kdo hlásí škodu

### Povinná pole

- [ ] Bez jména, příjmení nebo data narození zůstává CTA disabled.
- [ ] Po vyplnění jména, příjmení a platného data narození je CTA enabled.
- [ ] Jméno a příjmení jde zadat přes klávesnici.
- [ ] Pole mají čitelný label a focus stav.
- [ ] Nadpis kroku je „Kdo hlásí škodu“.
- [ ] Helper u data narození zobrazuje jen jeden příklad: `Např. 14.02.1988`.

### Datum narození — ruční zadání

- [ ] Postupné psaní `14021988` se zformátuje na `14.02.1988`.
- [ ] Postupné psaní `14.02.1988` zůstane funkční.
- [ ] Postupné psaní `14.2.1988` je validní a po opuštění pole se normalizuje na `14.02.1988`.
- [ ] Postupné psaní `1.1.1988` je validní a po opuštění pole se normalizuje na `01.01.1988`.
- [ ] Postupné psaní `31.3` a potom číslice roku `1` vytvoří `31.3.1`, ne chybné `31.31`.
- [ ] Postupné psaní `31.3.` vloží druhou tečku po měsíci a ponechá hodnotu `31.3.`.
- [ ] Postupné psaní `31.3.1990` je validní a po opuštění pole se normalizuje na `31.03.1990`.
- [ ] Postupné psaní `14.11.1988` zůstane jako listopad, ne jako `14.1.1988`.
- [ ] Uživatel může po dni napsat tečku ručně — tečka se nesmaže.
- [ ] Po zadání dvou číslic dne se tečka doplní automaticky.
- [ ] Po zadání dvou číslic měsíce se tečka doplní automaticky.
- [ ] Backspace z hodnoty `31.3.1` smaže postupně `1` → `31.3.` → `31.3` → `31.` → `31` a maska tečku hned znovu nenutí.
- [ ] Backspace z hodnoty `14.02.1988` umožní smazat rok, měsíc i den bez zaseknutí na automaticky doplněné tečce.
- [ ] Neplatné datum `31.02.2010` zobrazí error a CTA zůstane disabled.
- [ ] Budoucí datum zobrazí error a CTA zůstane disabled.
- [ ] Rok před `1900` zobrazí error a CTA zůstane disabled.
- [ ] Smazání data znovu disabled CTA.

### Datum narození — výběr z kalendáře

- [ ] Ikona kalendáře otevře nativní date picker, pokud ho prohlížeč podporuje.
- [ ] Výběr data z pickeru se propíše do textového pole jako `DD.MM.RRRR`.
- [ ] Po výběru platného data je CTA enabled, pokud jsou vyplněná i ostatní povinná pole.
- [ ] Ručně zadané platné datum se synchronizuje do pickeru.
- [ ] Picker nepovolí datum před `1900-01-01`.
- [ ] Picker nepovolí budoucí datum.

---

## Krok 2 — Co a kdy se stalo

- [ ] Bez adresy, data události nebo času zůstává CTA disabled.
- [ ] Adresa jde zadat přes klávesnici.
- [ ] Datum události jde vybrat.
- [ ] Přibližný čas jde zadat volným textem.
- [ ] Volitelný popis neblokuje pokračování.
- [ ] Helper texty jsou čitelné a nepřekrývají CTA.

---

## Krok 3 — Foto škody

- [ ] Bez fotky je CTA disabled.
- [ ] Upload / pořízení fotky zobrazí náhled.
- [ ] Po přidání fotky je CTA enabled.
- [ ] Po odebrání poslední fotky je CTA znovu disabled.
- [ ] Lze přidat více fotek.
- [ ] Počet fotek se správně aktualizuje.

---

## Krok 4 — AI analýza a nalezená poškození

- [ ] Loading obrazovka se zobrazí po pokračování z fotek.
- [ ] Po loadingu se zobrazí výsledky AI analýzy.
- [ ] Seznam nalezených poškození je čitelný.
- [ ] Editace poškození otevře bottom sheet.
- [ ] Uložení změny upraví položku v seznamu.
- [ ] Přidání nového poškození funguje.
- [ ] Prázdný název poškození zobrazí error.

---

## Krok 5 — Nárok na krytí

- [ ] Kryté položky se zobrazí v sekci krytých škod.
- [ ] Nekryté položky se zobrazí v sekci mimo krytí.
- [ ] Ručně přidané / čekající položky se zobrazí ve správné sekci.
- [ ] „Chci vědět více“ otevře info bottom sheet.
- [ ] Info bottom sheet jde zavřít.

---

## Krok 6 — Návrh plnění

- [ ] Návrh částky je viditelný.
- [ ] Účet pro výplatu je viditelný.
- [ ] Editace účtu jde otevřít, uložit a zavřít.
- [ ] Změněný účet se propíše do potvrzení.
- [ ] Odeslání hlášení vede na potvrzovací obrazovku.

---

## Potvrzení / OK obrazovka

- [ ] Zobrazuje se částka plnění.
- [ ] Zobrazuje se účet pro výplatu.
- [ ] Hodnocení hvězdičkami funguje.
- [ ] Odeslání hodnocení zobrazí potvrzení.
- [ ] Objednání hovoru likvidátora změní stav tlačítka / zobrazí potvrzení.

---

## Responsivita a mobilní chování

Testuj minimálně šířky:

- [ ] 320 px
- [ ] 390 px
- [ ] 430 px

Kontroly:

- [ ] Žádný obsah neuteče mimo viewport horizontálně.
- [ ] Tlačítka mají dostatečnou tap area.
- [ ] Klávesnice na mobilu nepřekryje aktivní pole nebo bottom sheet tak, že nejde pokračovat.
- [ ] Sticky header a bottom navigation se chovají stabilně.

---

## Accessibility minimum

- [ ] Všechna input pole mají label.
- [ ] CTA disabled/enabled odpovídá validaci.
- [ ] Error stav je doplněný textovou hláškou, ne jen barvou.
- [ ] Interaktivní prvky mají srozumitelný název / `aria-label`.
- [ ] Flow jde základně ovládat klávesnicí.
- [ ] Focus stav je viditelný.

---

## Technické ověření

- [ ] JS syntax check projde.
- [ ] V browser konzoli nejsou nové relevantní chyby.
- [ ] V diffu nejsou nechtěné změny mimo řešený scope.
- [ ] Lokální testovací server je po testování ukončený.
