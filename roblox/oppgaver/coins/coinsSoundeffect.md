
```lua
-- ServerScript under coin-Part
local coin = script.Parent
local COIN_VALUE = 1

-- Valgfritt: hvis lyden ligger som barn av coinen (f.eks. "Coin_collect")
local soundTemplate = coin:FindFirstChild("Coin_collect")

local SoundService = game:GetService("SoundService")
local Debris = game:GetService("Debris")

local taken = false

local function onTouch(otherPart)
	if taken then return end

	local character = otherPart.Parent
	local player = game.Players:GetPlayerFromCharacter(character)
	if not player then return end

	-- Finn wallet/Coins (tilpass hvis du bruker leaderstats)
	local wallet = player:FindFirstChild("wallet")
	if not wallet then return end
	local coins = wallet:FindFirstChild("Coins")
	if not coins then return end

	-- Lås umiddelbart så vi ikke kan plukke dobbelt
	taken = true
	coin.CanTouch = false

	-- Gi verdi
	coins.Value += COIN_VALUE

	-- Spill lyd ETTER at vi har klonet den til SoundService
	if soundTemplate then
		local s = soundTemplate:Clone()
		s.Parent = SoundService
		s:Play()

		-- Rydd opp automatisk etter at lyden er ferdig (med litt margin)
		local ttl = (s.TimeLength > 0) and (s.TimeLength + 0.5) or 2
		Debris:AddItem(s, ttl)
	end

	-- (Valgfritt) Emit partikler før vi fjerner coinen
	for _, d in ipairs(coin:GetDescendants()) do
		if d:IsA("ParticleEmitter") then
			d:Emit(25)
		end
	end

	-- FÅ COINEN BORT MED EN GANG (visuelt og fysisk)
	coin.Transparency = 1
	coin.CanCollide = false
	coin.CanQuery = false
	coin.CanTouch = false

	-- Slett coinen helt (lyden fortsetter siden den er i SoundService)
	coin:Destroy()
end

coin.Touched:Connect(onTouch)
```