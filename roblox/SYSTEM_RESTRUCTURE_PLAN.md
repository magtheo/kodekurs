# Plan for å restrukturere Roblox-kurs til system-basert struktur

## 🎯 Mål
- Endre fra dag-basert til system-basert navngivning
- Fjerne plassholdere (dag1-3,5-6,9-16)
- Beholde eksisterende innholdssider uten å splitte dem
- Oppdatere navigasjon og oversikt

## 📊 Analyse av eksisterende sider

### ✅ Fullstendige sider (beholdes og omdøpes)

#### 1. **dag4.html** → **ui-boost-system.html**
**Systemer dekket:**
- UI System (ScreenGui, TextLabel)
- Boost/Power-up System (WalkSpeed, JumpPower)
- Animation System (enkel)
- Event System (Touched)

**Hvorfor denne navngivelsen?**
- Hovedfokus er UI-meldinger kombinert med boost-effekter
- Naturlig kombinasjon av to relaterte systemer

#### 2. **dag7.html** → **item-system.html**
**Systemer dekket:**
- Item System (Tools, Handle, stacking)
- Sound System (lyd ved bruk)
- Client-Server Communication (RemoteEvent)
- Attribute System (Stack, MaxStack)

**Hvorfor denne navngivelsen?**
- Hovedfokus er komplett item-system med plukking og bruk
- Andre systemer er støtte for item-systemet

#### 3. **dag8.html** → **door-security-system.html**
**Systemer dekket:**
- Door System (åpne/lukke dører)
- Security System (passord, låsing)
- UI System (TextBox, TextButton)
- Attribute System (Open-tilstand)
- Event System (MouseButton1Click)

**Hvorfor denne navngivningen?**
- Hovedfokus er dørsystem med sikkerhet
- UI er en del av sikkerhetssystemet

### ❌ Plassholdere (slettes)

**Sider som skal slettes:**
- dag1.html
- dag2.html
- dag3.html
- dag5.html
- dag6.html
- dag9.html
- dag10.html
- dag11.html
- dag12.html
- dag13.html
- dag14.html
- dag15.html
- dag16.html

## 🔄 Endringsplan

### Steg 1: Omdøp eksisterende sider
```bash
dag4.html → ui-boost-system.html
dag7.html → item-system.html
dag8.html → door-security-system.html
```

### Steg 2: Slett plassholdere
```bash
Slett: dag1.html, dag2.html, dag3.html, dag5.html, dag6.html
Slett: dag9.html, dag10.html, dag11.html, dag12.html
Slett: dag13.html, dag14.html, dag15.html, dag16.html
```

### Steg 3: Oppdater innhold i omdøpte sider

#### ui-boost-system.html
- Endre tittel fra "Dag 4" til "UI og Boost System"
- Oppdater navigasjonslenker
- Fjern dag-referanser i teksten

#### item-system.html
- Endre tittel fra "Dag 7" til "Item System"
- Oppdater navigasjonslenker
- Fjern dag-referanser i teksten

#### door-security-system.html
- Endre tittel fra "Dag 8" til "Door og Security System"
- Oppdater navigasjonslenker
- Fjern dag-referanser i teksten

### Steg 4: Oppdater index.html
**Nåværende navigasjon:**
```html
<a href="dag1.html">Dag 1</a>
<a href="dag2.html">Dag 2</a>
...
<a href="dag16.html">Dag 16</a>
```

**Ny navigasjon:**
```html
<a href="ui-boost-system.html">🎨 UI og Boost System</a>
<a href="item-system.html">🎒 Item System</a>
<a href="door-security-system.html">🚪 Door og Security System</a>
```

### Steg 5: Oppdater oversikt.md
- Endre fra dag-basert til system-basert oversikt
- Fjern plassholdere fra tabellen
- Oppdater statistikk

## 📋 Ny struktur

```
roblox/
├── index.html (oppdatert)
├── ui-boost-system.html (dag4.html omdøpt)
├── item-system.html (dag7.html omdøpt)
├── door-security-system.html (dag8.html omdøpt)
├── oppgaver/
│   ├── SpeedBoost.md
│   └── coins/
│       ├── CoinRotate.md
│       └── coinsSoundeffect.md
├── dag7/ (beholdes - inneholder script-eksempler)
└── oversikt.md (oppdatert)
```

## 🎨 Designprinsipper for nye titler

### UI og Boost System
- **Emoji:** 🎨 eller ⚡
- **Fokus:** Brukergrensesnitt og midlertidige effekter
- **Målgruppe:** Nybegynnere til viderekomne

### Item System
- **Emoji:** 🎒 eller 🍎
- **Fokus:** Komplett system for gjenstander
- **Målgruppe:** Viderekomne til avanserte

### Door og Security System
- **Emoji:** 🚪 eller 🔐
- **Fokus:** Adgangskontroll og sikkerhet
- **Målgruppe:** Viderekomne til avanserte

## 📝 Oppgaver og oppdateringer

### For hver omdøpt side:
1. [ ] Endre `<title>` tag
2. [ ] Endre `<h1>` overskrift
3. [ ] Fjern "Dag X" referanser
4. [ ] Oppdater navigasjonsdropdown
5. [ ] Oppdater forrige/neste lenker

### For index.html:
1. [ ] Fjern dag-navigasjon
2. [ ] Legg til system-navigasjon
3. [ ] Oppdater beskrivelser
4. [ ] Fjern referanser til slettede dager

### For oversikt.md:
1. [ ] Endre til system-basert oversikt
2. [ ] Fjern plassholdere
3. [ ] Oppdater statistikk
4. [ ] Legg til kryssreferanser

## 🚀 Implementeringsrekkefølge

1. ✅ Analyse og planlegging
2. ⏳ Omdøp eksisterende sider
3. ⏳ Slett plassholdere
4. ⏳ Oppdater innhold i omdøpte sider
5. ⏳ Oppdater index.html
6. ⏳ Oppdater oversikt.md
7. ⏳ Test alle lenker og navigasjon

## 📊 Endelig struktur

### Hovedsider (3)
1. **ui-boost-system.html** - UI og Boost System
2. **item-system.html** - Item System
3. **door-security-system.html** - Door og Security System

### Oppgaver (3)
1. **SpeedBoost.md** - Boost system oppgaver
2. **CoinRotate.md** - Animation system oppgaver
3. **coinsSoundeffect.md** - Sound system oppgaver

### Støttefiler
- **index.html** - Hovedoversikt
- **oversikt.md** - Detaljert oversikt
- **dag7/** - Script-eksempler

## 💎 Fordeler med ny struktur

1. **Klarere fokus:** Hver side dekker et spesifikt system
2. **Mindre forvirring:** Ingen plassholdere som forvirrer
3. **Bedre navigasjon:** Lettere å finne relevant innhold
4. **Skalerbarhet:** Enkelt å legge til nye systemer
5. **Profesjonelt:** Ser ut som et ferdig produkt

---

*Plan opprettet: 2025-03-17*
*Status: Klar for implementering*