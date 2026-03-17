# Roblox Studio Kodekurs - Systemoversikt

## 📊 Sammendrag

| System | Status | Tittel | Innhold |
|--------|--------|--------|---------|
| UI og Boost System | ✅ Fullstendig | Brukergrensesnitt og Boost | Boost-bokser, UI-meldinger, fart/hopp |
| Item System | ✅ Fullstendig | Item System | Eple-plukking, Tools, RemoteEvent, helse |
| Door og Security System | ✅ Fullstendig | Door og Security System | Passord-dører, terminal, sikkerhet |

## 📚 Detaljert oversikt over systemer

### ✅ UI og Boost System
**Tema:** Boost-bokser med UI-meldinger og midlertidige effekter

**Konsepter:**
- UI System (ScreenGui, TextLabel)
- Events (Touched)
- Services (Players)
- Humanoid (WalkSpeed/JumpPower)
- Timers (task.delay)
- WaitForChild

**Innhold:**
- Bygge en mappe med deler («boost-bokser») i Workspace som trigger når spilleren går gjennom.
- Lage ScreenGui med TextLabel som viser en melding.
- Gi midlertidig fart og hopphøyde med kode — og resette etter noen sekunder.
- Tilbakestilling etter tid
- Debounce for å hindre retrigger

**Mini-oppgaver:**
- Gjøre meldingen norsk med emoji (🎉)
- Lage nye bokser med forskjellige effekter
- Endre BOOST_DURATION
- Lage "boost-port" med endret Size/Plassering

**Videreutvikling:**
- Legge til debounce
- Resett ved CharacterAdded
- Bruke ProximityPrompt
- Lage nedtelling i UI

---

### ✅ Item System
**Tema:** Komplett item-system med plukking, bruk og effekter

**Konsepter:**
- Tools
- ProximityPrompt
- RemoteEvent
- ServerStorage
- Clone()
- Humanoid.Health
- Attributes

**Innhold:**
- Lage et eple i verden som faller fra et tre etter tilfeldig tid
- Bruke ProximityPrompt så spilleren kan plukke opp eplet
- Gi spilleren et Tool (eple) som de kan holde i hånden
- La spilleren spise eplet for å få tilbake helse (+20 HP)
- Bruke RemoteEvent for kommunikasjon mellom klient og server
- Stack-system for flere epler

**Struktur:**
```
ReplicatedStorage
└─ EatApple (RemoteEvent)

ServerStorage
└─ Apple (Tool)
   ├─ Handle (Part)
   ├─ Crunch (Sound)
   └─ LocalScript

ServerScriptService
└─ EatAppleHandler (Script)

Workspace
└─ AppleWorld (Part)
   └─ Script
```

**Mini-oppgaver:**
- Endre helse-boost fra 20 til 30
- Lage flere epler på forskjellige steder
- Endre venteTid for raskere testing
- Lage "gylden eple" som gir 50 helse
- Legge til ParticleEmitter på eplet

**Videreutvikling:**
- Lage "eple-tre" som respawner nye epler automatisk
- Legge til debounce
- Vise UI-melding når spilleren spiser eplet
- Lage "rotne eple" som tar bort helse
- Telle spiste epler med Leaderboard

---

### ✅ Door og Security System
**Tema:** Passordsystem med UI-terminal og dører

**Konsepter:**
- TextBox
- TextButton
- Folder
- Attributes
- Dictionary (tabeller)
- UI-script

**Innhold:**
- Bygge en dør i Workspace som kan åpnes og lukkes med kode
- Organisere dørene i en Folder (klar for mange dører)
- Lage en terminal i UI (TextBox + knapp)
- Koble passord til dører med en dictionary (tabell)
- Implementere maks antall forsøk før systemet låser seg
- Toggle-funksjonalitet for åpne/lukke dører

**Struktur:**
```
Workspace
└─ Doors (Folder)
   ├─ Door1 (Part)
   ├─ Door2 (Part)
   └─ BossDoor (Part)

StarterGui
└─ DoorTerminalGui (ScreenGui)
   └─ TerminalFrame (Frame)
      ├─ TitleLabel (TextLabel)
      ├─ DoorText (TextBox)
      └─ SubmitButton (TextButton)
         └─ LocalScript (passord-kode)
```

**Mini-oppgaver:**
- Legge til ny dør med passord
- Endre maxAttempts til 6
- Vise "Feil passord"-melding ved feil
- Endre dørfarger ved åpning

**Videreutvikling:**
- Lage "felle-dør" som åpner gulvet
- Lage forskjellige nivåer med ulike passord
- Resett attempts etter 30 sekunder
- Lage Leaderboard for riktige passord

---

## 📝 Oppgaver

### 🚀 Boost Oppgaver
**Fil:** [`oppgaver/SpeedBoost.md`](oppgaver/SpeedBoost.md:1)

**Innhold:**
- Steg-for-steg oppgaveserie for å lage boost-bokser fra grunnen av
- Bygge boost-bokser i Workspace
- Lage GUI for meldinger
- Implementere boost-effekter med kode
- Feilsøking og vanlige problemer

---

### 🪙 Coin Oppgaver
**Filer:**
- [`oppgaver/coins/CoinRotate.md`](oppgaver/coins/CoinRotate.md:1) - Coin-animasjon med rotasjon og bobbing
- [`oppgaver/coins/coinsSoundeffect.md`](oppgaver/coins/coinsSoundeffect.md:1) - Lydeffekter ved coin-henting

**Innhold:**
- Animasjon av coins med RunService
- Rotasjon rundt Y-aksen
- Bobbing opp og ned
- Dynamisk tillegg/fjerning av coins
- Lydeffekter ved pickup
- Server-side logikk for coin-henting

---

## 📈 Statistikk

- **Totalt antall systemer:** 3
- **Fullstendige systemer:** 3
- **Oppgaver tilgjengelige:** 3
- **Kursprogressjon:** 100% (3/3 systemer fullstendige)

## 🎯 Læringssti

### 🌱 Nybegynner
1. **UI og Boost System** - Lær om brukergrensesnitt og midlertidige effekter
2. **Item System** - Lær om Tools, plukking og bruk av gjenstander

### 🚀 Viderekommen
3. **Door og Security System** - Lær om passordsystemer og sikkerhet

## 💡 Fordeler med system-basert struktur

1. **Klarere fokus:** Hvert system dekker et spesifikt område
2. **Bedre navigasjon:** Lettere å finne relevant innhold
3. **Skalerbarhet:** Enkelt å legge til nye systemer
4. **Profesjonelt utseende:** Ser ut som et ferdig produkt
5. **Logisk sammenheng:** Systemer henger naturlig sammen

## 🚀 Neste steg

For å utvide kurset kan du legge til:
1. **Animation System** - Animasjoner og visuelle effekter
2. **Coin System** - Komplett system for valuta og samling
3. **Event System** - Dypere forståelse av events og triggers
4. **Client-Server Communication** - Avansert kommunikasjon mellom klient og server

---

*Sist oppdatert: 2025-03-17*