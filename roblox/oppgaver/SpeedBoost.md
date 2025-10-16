Klart! Her er en **steg-for-steg oppgaveserie** som leder elevene fra blankt prosjekt til akkurat koden du har – med små tester underveis så de ser at ting virker.

---

# Oppgave 1: Lag “speedBox”-feltet i verden

1. Åpne **Roblox Studio** → et tomt baseplate-prosjekt.
2. Sett inn en **Part** (kube) i `Workspace`.
3. Gi den navnet **`speedBox`** (viktig – koden leter etter akkurat dette navnet).
4. Egenskaper for `speedBox`:

   * `Anchored = true` (den skal ikke falle).
   * `CanCollide = false` (spilleren går gjennom).
   * `Transparency = 0.5` (slik at den ser “magisk” ut).
   * (Valgfritt) Endre farge til noe tydelig, f.eks. grønn.
5. Flytt `speedBox` til et sted spilleren lett kan løpe gjennom etter spawn.

✅ **Test:** Trykk **Play** (►). Spilleren skal kunne løpe gjennom boksen uten å stoppe.

---

# Oppgave 2: Lag GUI som viser beskjed

1. Høyreklikk `StarterGui` → **Insert Object** → **ScreenGui**.
2. Inni `ScreenGui` → **Insert Object** → **TextLabel**.
3. Velg `TextLabel` og sett:

   * `Text = ""` (tom først)
   * `Visible = false` (vi skrur den på i koden)
   * `AnchorPoint = 0.5, 0`
   * `Position = (0.5, 0), (0.05, 0)` (midt på toppen)
   * `Size = (0.6, 0), (0.1, 0)` (god bredde)
   * `TextScaled = true`
   * (Valgfritt) Bakgrunn litt gjennomsiktig: `BackgroundTransparency = 0.2`

✅ **Test:** Du skal *ikke* se labelen når du trykker Play (fordi `Visible = false`).

---

# Oppgave 3: Plasser koden riktig (LocalScript)

1. Høyreklikk **`TextLabel`** → **Insert Object** → **LocalScript**.

   * Viktig: Fordi vi bruker `Players.LocalPlayer`, **må** dette være en LocalScript under en GUI (eller i `StarterPlayerScripts`).
2. Åpne LocalScriptet – vi fyller inn koden steg for steg i neste oppgaver.

---

# Oppgave 4: Finn spiller, figur og humanoid

Lim inn og forklar denne første blokken i LocalScriptet:

```lua
local textLabel = script.Parent
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
```

* Her peker vi på tekstfeltet, henter lokalt spiller-objektet, venter på at figuren skal spawne, og finner `Humanoid`.

✅ **Mini-test:** Sett midlertidig `textLabel.Visible = true; textLabel.Text = "Hei!"` over koden, trykk Play, se at tekst vises, så fjern de to linjene igjen.

---

# Oppgave 5: Finn `speedBox` i Workspace

Legg til:

```lua
local speedBox = workspace:WaitForChild("speedBox")
```

* Dette venter på at delen med riktig navn finnes. Om du skrev feil navn i oppgave 1 vil det feile – fint tidspunkt å oppdage det!

---

# Oppgave 6: Lag innstillinger for boost

Legg til:

```lua
-- Settings
local BOOST_SPEED = 32 -- normal is 16
local BOOST_JUMPPOWER = 150 -- normal is 50
local BOOST_DURATION = 2 -- seconds
```

* Vi samler alle tall på ett sted, lett å endre for eksperimenter.

---

# Oppgave 7: Lagre spillerens normalverdier

Legg til:

```lua
-- Store defaults so we can reset
local NORMAL_SPEED = humanoid.WalkSpeed
local NORMAL_JUMPPOWER = humanoid.JumpPower
```

* Vi tar vare på “original” fart og hoppekraft slik at vi kan tilbakestille etterpå.

---

# Oppgave 8: Reager når spilleren toucher boksen

Legg til hele “Touched”-koblingen med sjekk for **din** karakter:

```lua
speedBox.Touched:Connect(function(hit)
	if hit.Parent == character then
		print("box hit")
        -- her fyller vi på i neste oppgave
	end
end)
```

* `hit` er delen som berørte `speedBox`. `hit.Parent` er vanligvis en del av karakteren (f.eks. fot).
* Sjekken sikrer at det er **din** figur, ikke andre objekter.

✅ **Mini-test:** Trykk Play og løp gjennom boksen. Se “box hit” i **Output**-vinduet.

---

# Oppgave 9: Vis tekst + gi boost + reset

Fyll inn resten inne i `if hit.Parent == character then ... end`:

```lua
-- Show text
textLabel.Visible = true
textLabel.Text = "You get speed and jumpboost for 2 seconds!"
task.delay(3, function()
	textLabel.Visible = false
end)

-- Ensure we’re using JumpPower
humanoid.UseJumpPower = true

-- Apply boost
humanoid.WalkSpeed = BOOST_SPEED
humanoid.JumpPower = BOOST_JUMPPOWER
print("Boost applied!")

-- Reset after delay
task.delay(BOOST_DURATION, function()
	if humanoid then
		humanoid.WalkSpeed = NORMAL_SPEED
		humanoid.JumpPower = NORMAL_JUMPPOWER
		print("Boost reset.")
	end
end)
```

✅ **Test hele flyten:**

1. Trykk Play.
2. Løp gjennom `speedBox`.
3. Se at teksten dukker opp, farten og hoppen øker, og at alt går tilbake til normalt etter 2 sekunder.

---

# Vanlige feil (hurtigsjekk)

* **Script-type:** Sørg for at dette er en **LocalScript** under **TextLabel**. ServerScript vil ikke ha `LocalPlayer`.
* **Navn på del:** Delen **må** hete `speedBox` i `Workspace`.
* **CanCollide:** Hvis du ikke skrur av `CanCollide`, kan spilleren bli stoppet i boksen og “Touched” kan kjennes “sticky”.
* **Humanoid finnes ikke:** Hvis du starter skriptet et annet sted, må du fortsatt vente på `CharacterAdded` og `Humanoid` som i koden over.

---

# Ferdig kode (lim inn i LocalScript under TextLabel)

```lua
local textLabel = script.Parent
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

local speedBox = workspace:WaitForChild("speedBox")

-- Settings
local BOOST_SPEED = 32 -- normal is 16
local BOOST_JUMPPOWER = 150 -- normal is 50
local BOOST_DURATION = 2 -- seconds

-- Store defaults so we can reset
local NORMAL_SPEED = humanoid.WalkSpeed
local NORMAL_JUMPPOWER = humanoid.JumpPower

speedBox.Touched:Connect(function(hit)
	if hit.Parent == character then
		print("box hit")

		-- Show text
		textLabel.Visible = true
		textLabel.Text = "You get speed and jumpboost for 2 seconds!"
		task.delay(3, function()
			textLabel.Visible = false
		end)

		-- Ensure we’re using JumpPower
		humanoid.UseJumpPower = true

		-- Apply boost
		humanoid.WalkSpeed = BOOST_SPEED
		humanoid.JumpPower = BOOST_JUMPPOWER
		print("Boost applied!")

		-- Reset after delay
		task.delay(BOOST_DURATION, function()
			if humanoid then
				humanoid.WalkSpeed = NORMAL_SPEED
				humanoid.JumpPower = NORMAL_JUMPPOWER
				print("Boost reset.")
			end
		end)
	end
end)
```

---

## Ekstra (valgfritt) mini-oppgaver

* **Cooldown:** Legg til en `debounce` så man ikke kan trigge boost igjen før reset er ferdig.
* **Flere bokser:** Dupliser `speedBox` og gi forskjellige farger/verdier (f.eks. en “super jump” boks).
* **Lyd/partikler:** Spill av en lyd eller lag partikkel-effekt når boost aktiveres.

Si fra om du vil at jeg legger til en **cooldown-versjon** eller en **modul** for flere bokser!
