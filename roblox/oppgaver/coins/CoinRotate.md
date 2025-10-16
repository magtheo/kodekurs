
Supert 🙌
Her er en **ferdig og lettfattelig oppgavepakke** som forklarer **coin-animasjonen** steg for steg – på samme pedagogiske måte som “speedBox”-oppgaven.
Dette hjelper elevene å forstå *hvordan og hvorfor* koden fungerer, ikke bare lime den inn.

---

# 🪙 Oppgave 1: Lag coin-mappen i Workspace

1. Åpne **Roblox Studio** → et nytt Baseplate-prosjekt.
2. Lag en **Folder** i `Workspace` og kall den **`coins`** (nøyaktig samme navn).
3. Lag én eller flere **Parts** inni denne mappen:

   * Gi dem navnet **`coin`**
   * Sett `Anchored = true` (så de ikke faller)
   * Sett `CanCollide = false` (så spilleren ikke dytter dem bort)
   * Endre farge til **gull**
   * Bruk `Scale`-verktøyet til å gjøre dem små og runde
4. (Valgfritt) Gi dem et **Mesh** for å se ut som ekte mynter.

✅ **Test:** Trykk **Play** (►) – du skal se coins stå stille i luften.

---

# 🪄 Oppgave 2: Plasser koden riktig (LocalScript)

1. Gå til **Explorer** → `StarterPlayer` → `StarterPlayerScripts`.
2. Høyreklikk → **Insert Object** → **LocalScript**.
3. Døp den til **`CoinAnimation`**.
4. Åpne skriptet — her skal vi lime inn koden steg for steg.

> 💡 *Hvorfor ikke under coinene selv?*
> LocalScripts kjører ikke i `Workspace`, men de gjør det i `StarterPlayerScripts` fordi de hører til spilleren.
> Vi bruker ett script som animerer **alle coins** for spilleren.

---

# ⚙️ Oppgave 3: Forstå hva koden gjør

Vi skal lage en kode som:

1. Finner alle coins i `workspace.coins`.
2. Får dem til å snurre jevnt rundt **Y-aksen**.
3. Får dem til å flyte opp og ned i en jevn rytme (bobbing).
4. Fanger opp nye coins som legges til underveis.

---

# 🧱 Oppgave 4: Start og finn coin-mappen

Lim inn dette øverst i skriptet:

```lua
local RunService = game:GetService("RunService")

-- Navnet på mappen som inneholder alle coins
local FOLDER_NAME = "coins"

-- Vent til mappen finnes i Workspace
local coinsFolder = workspace:WaitForChild(FOLDER_NAME)
```

* `RunService` lar oss kjøre en funksjon **hver frame**, perfekt for animasjoner.
* `WaitForChild` sørger for at skriptet ikke prøver å starte før mappen faktisk finnes.

✅ **Mini-test:** Sett inn en `print("Fant coins-mappen!")` under siste linje, trykk Play, og sjekk **Output**.

---

# 🔧 Oppgave 5: Lag animasjons-innstillinger

Legg til:

```lua
-- Hvor fort og hvor mye coinene beveger seg
local ROTATION_SPEED = 90   -- grader per sekund
local FLOAT_HEIGHT   = 0.5  -- høyde på bobbing
local FLOAT_SPEED    = 2    -- hvor raskt de flyter
```

* Disse verdiene gjør det lett å eksperimentere:

  * `ROTATION_SPEED` = hvor raskt de spinner.
  * `FLOAT_HEIGHT` = hvor høyt de flyter opp og ned.
  * `FLOAT_SPEED` = tempoet i bobbingen.

---

# 💾 Oppgave 6: Lag en liste over coins

Vi trenger å holde oversikt over alle coins slik at vi kan oppdatere dem hver frame.

```lua
local animated = {}  -- [Part] = { basePos = Vector3, phase = number }
```

Hver coin får sin **grunnposisjon** og en **fase** slik at de ikke bobber helt likt.

---

# 🧩 Oppgave 7: Finn riktige deler å animere

Legg inn en hjelpefunksjon:

```lua
local function getDisplayPart(inst)
	if inst:IsA("BasePart") then
		return inst
	elseif inst:IsA("Model") then
		if inst.PrimaryPart then
			return inst.PrimaryPart
		end
		return inst:FindFirstChildWhichIsA("BasePart", true)
	end
	return nil
end
```

* Coins kan være **Parts** eller **Models**.
* Denne funksjonen finner riktig del å rotere.

---

# ⚡ Oppgave 8: Legg til og fjern coins dynamisk

```lua
local function addCoin(inst)
	local part = getDisplayPart(inst)
	if not part or animated[part] then return end

	part.Anchored = true -- vi styrer posisjonen selv

	animated[part] = {
		basePos = part.Position,             -- startposisjon i verden
		phase = math.random() * math.pi * 2, -- gir ulik rytme
	}
end

local function removeCoin(inst)
	if inst:IsA("BasePart") and animated[inst] then
		animated[inst] = nil
	elseif inst:IsA("Model") then
		for part, _ in pairs(animated) do
			if part:IsDescendantOf(inst) then
				animated[part] = nil
			end
		end
	end
end
```

* `addCoin` legger til en ny coin i listen.
* `removeCoin` tar den bort hvis den forsvinner.

✅ **Mini-test:** Du kan `print(part.Name)` inne i `addCoin` for å se at den finner coins.

---

# 🔁 Oppgave 9: Koble alt sammen

Legg til disse linjene for å fange alle coins og endringer i mappen:

```lua
for _, d in ipairs(coinsFolder:GetDescendants()) do
	addCoin(d)
end

coinsFolder.DescendantAdded:Connect(addCoin)
coinsFolder.DescendantRemoving:Connect(removeCoin)
```

* `GetDescendants()` henter alle barn (og barnebarn).
* Vi kobler `addCoin` og `removeCoin` slik at nye coins begynner å animeres automatisk.

---

# 🎞️ Oppgave 10: Lag selve animasjonsloopen

Dette kjøres **hver frame** og oppdaterer posisjon og rotasjon.

```lua
local t = 0
RunService.RenderStepped:Connect(function(dt)
	t += dt
	local angle = math.rad(ROTATION_SPEED) * t

	for part, info in pairs(animated) do
		if part and part.Parent then
			local y = math.sin(t * FLOAT_SPEED + info.phase) * FLOAT_HEIGHT
			part.CFrame =
				CFrame.new(info.basePos + Vector3.new(0, y, 0)) *
				CFrame.Angles(0, angle, 0)
		else
			animated[part] = nil
		end
	end
end)
```

💬 Forklaring:

* `t` teller tiden som går.
* `math.sin(...)` lager en bølgebevegelse opp og ned.
* `FLOAT_SPEED` og `FLOAT_HEIGHT` styrer hvor fort og høyt.
* `CFrame.Angles(0, angle, 0)` roterer rundt **verdens Y-akse**.
* `CFrame.new(...)` flytter den opp/ned uten å skli sidelengs.
* Multiplikasjonen setter sammen posisjon + rotasjon.

✅ **Test:** Trykk **Play** – coins skal nå snurre og flyte rolig opp og ned!

---

# 🔍 Vanlige feil

| Problem           | Løsning                                                                     |
| ----------------- | --------------------------------------------------------------------------- |
| Coins står stille | Sjekk at LocalScript ligger i `StarterPlayerScripts`.                       |
| Feil mappe        | Mappen **må** hete `coins` i `Workspace`.                                   |
| De spinner skeivt | Sørg for at de står rett (Y-akse opp) eller bruk `Anchored = true`.         |
| Ingenting skjer   | Trykk **Play** (ikke Run) – LocalScripts kjører bare når en spiller finnes. |

---

# 🎉 Ferdig kode

```lua
-- LocalScript: StarterPlayer -> StarterPlayerScripts
-- Roterer og bobber alle coins i workspace.coins

local RunService = game:GetService("RunService")

-- === Oppsett ===
local FOLDER_NAME     = "coins"  -- mappe i Workspace
local ROTATION_SPEED  = 90       -- grader per sekund
local FLOAT_HEIGHT    = 0.5      -- bob-amplitude (meter)
local FLOAT_SPEED     = 2        -- bob-hastighet (Hz ~ svingninger/sek)

-- Hvis mesh-aksen er "liggende", kan du rotere mynten fast én gang her:
-- Sett til CFrame.Angles(0,0,0) hvis du ikke trenger dette.
local MESH_FIX = CFrame.Angles(0, 0, 0) -- evt. CFrame.Angles(math.rad(90), 0, 0)

-- === Internt lager ===
-- [BasePart] = { basePos = Vector3, baseRot = CFrame (valgfri), phase = number }
local animated = {}

-- Finn visningspart for en coin (Part direkte eller PrimaryPart/første BasePart i Model)
local function getDisplayPart(inst: Instance): BasePart?
	if inst:IsA("BasePart") then
		return inst
	elseif inst:IsA("Model") then
		if inst.PrimaryPart then
			return inst.PrimaryPart
		end
		return inst:FindFirstChildWhichIsA("BasePart", true)
	end
	return nil
end

-- Legg til én coin
local function addCoin(inst: Instance)
	local part = getDisplayPart(inst)
	if not part or animated[part] then return end

	part.Anchored = true -- stabil animasjon uten fysikk

	animated[part] = {
		basePos = part.Position,                 -- posisjon i verden
		baseRot = (part.CFrame - part.Position), -- opprinnelig tilt/roll (valgfri)
		phase   = math.random() * math.pi * 2,   -- desynk bobbing
	}
end

-- Fjern coin som forsvinner
local function removeCoin(inst: Instance)
	if inst:IsA("BasePart") and animated[inst] then
		animated[inst] = nil
	elseif inst:IsA("Model") then
		for part, _ in pairs(animated) do
			if part:IsDescendantOf(inst) then
				animated[part] = nil
			end
		end
	end
end

-- Finn/vent på mappen
local coinsFolder = workspace:WaitForChild(FOLDER_NAME)

-- Init: legg til alle nåværende coins
for _, d in ipairs(coinsFolder:GetDescendants()) do
	addCoin(d)
end

-- Reager på endringer i mappen
coinsFolder.DescendantAdded:Connect(addCoin)
coinsFolder.DescendantRemoving:Connect(removeCoin)

-- === Animasjonsloop ===
local t = 0
RunService.RenderStepped:Connect(function(dt)
	t += dt
	local angle = math.rad(ROTATION_SPEED) * t

	for part, info in pairs(animated) do
		if part and part.Parent then
			-- Bob i verdens Y
			local y = math.sin(t * FLOAT_SPEED + info.phase) * FLOAT_HEIGHT

			-- Roter rundt verdens Y, og (valgfritt) gjenbruk opprinnelig tilt + mesh-fix
			part.CFrame =
				CFrame.new(info.basePos + Vector3.new(0, y, 0)) -- pos+bob i verden
				* CFrame.Angles(0, angle, 0)                    -- ren spin rundt Y
				* info.baseRot                                   -- bevar tilt (kan fjernes)
				* MESH_FIX                                       -- fast korrigering (valgfri)
		else
			animated[part] = nil
		end
	end
end)

print("[CoinsAnim] Aktiv – roterer og bobber coins i workspace." .. FOLDER_NAME)

```

---

## 🌟 Ekstra mini-oppgaver

* **Ulike animasjoner:** Gi noen coins ulike `FLOAT_SPEED` eller `ROTATION_SPEED` ved å sette `Attributes` i Properties.
* **Glød:** Legg på en `PointLight` eller `SurfaceAppearance` for å få dem til å skinne.
* **Pickup:** Kombiner dette med et serverscript som gir spilleren poeng når de toucher coinen.
