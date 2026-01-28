--// Orion UI
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()

local Window = OrionLib:MakeWindow({
	Name = "🌸 Kaka Hub | Anime Edition",
	HidePremium = false,
	SaveConfig = true,
	ConfigFolder = "KakaHub"
})

-- =====================
-- TEMA ANIME
-- =====================

OrionLib.Themes.Anime = {
	Main = Color3.fromRGB(24, 20, 35),
	Second = Color3.fromRGB(38, 30, 60),
	Stroke = Color3.fromRGB(190, 120, 255),
	Divider = Color3.fromRGB(150, 90, 230),
	Text = Color3.fromRGB(240, 225, 255),
	TextDark = Color3.fromRGB(170, 150, 210)
}

OrionLib.SelectedTheme = "Anime"

OrionLib:MakeNotification({
	Name = "🌸 Kaka Hub",
	Content = "Tema Anime carregado com sucesso.",
	Time = 3
})

-- Tabs
local PlayerTab = Window:MakeTab({Name="Player",Icon="rbxassetid://4483345998",PremiumOnly=false})
local HBTab = Window:MakeTab({Name="Hitbox",Icon="rbxassetid://4483345998",PremiumOnly=false})
local MacroTab = Window:MakeTab({Name="Macro",Icon="rbxassetid://4483345998",PremiumOnly=false})
local SettingsTab = Window:MakeTab({Name="Settings",Icon="rbxassetid://4483345998",PremiumOnly=false})

local player = game.Players.LocalPlayer
local VIM = game:GetService("VirtualInputManager")

-- =====================
-- VARS
-- =====================

local StamOn = false
local BallHB = false
local SelfHB = false
local MacroOn = false

local BallSize = 12
local SelfSize = 6
local MacroDelay = 0.05

local BallsCache = {}

-- =====================
-- CACHE DAS BOLAS
-- =====================

local function CacheBalls()
	BallsCache = {}
	for _,v in pairs(workspace:GetDescendants()) do
		if v:IsA("BasePart") and v.Name:lower():find("ball") then
			table.insert(BallsCache,v)
		end
	end
end

CacheBalls()
workspace.DescendantAdded:Connect(function(v)
	if v:IsA("BasePart") and v.Name:lower():find("ball") then
		table.insert(BallsCache,v)
	end
end)

-- =====================
-- PLAYER
-- =====================

PlayerTab:AddToggle({
	Name = "⚡ Stamina Infinity",
	Default = false,
	Callback = function(Value)
		StamOn = Value
	end
})

task.spawn(function()
	while true do
		if StamOn then
			pcall(function()
				if player.Character and player.Character:FindFirstChild("Stamina") then
					player.Character.Stamina.Value = math.huge
				end
			end)
		end
		task.wait(0.15)
	end
end)

-- =====================
-- HB BALL
-- =====================

HBTab:AddToggle({
	Name = "⚽ HB Expansiva da Bola",
	Default = false,
	Callback = function(Value)
		BallHB = Value
	end
})

HBTab:AddSlider({
	Name = "📏 Tamanho HB Bola",
	Min = 3,
	Max = 25,
	Default = 12,
	Increment = 1,
	ValueName = "Size",
	Callback = function(Value)
		BallSize = Value
	end
})

task.spawn(function()
	while true do
		if BallHB then
			for _,v in pairs(BallsCache) do
				pcall(function()
					v.Size = Vector3.new(BallSize,BallSize,BallSize)
					v.Transparency = 0.4
					v.Material = Enum.Material.Neon
					v.CanCollide = false
				end)
			end
		end
		task.wait(0.25)
	end
end)

-- =====================
-- HB SELF
-- =====================

HBTab:AddToggle({
	Name = "🧍 HB Expansiva do Player",
	Default = false,
	Callback = function(Value)
		SelfHB = Value
	end
})

HBTab:AddSlider({
	Name = "📏 Tamanho HB Player",
	Min = 2,
	Max = 15,
	Default = 6,
	Increment = 1,
	ValueName = "Size",
	Callback = function(Value)
		SelfSize = Value
	end
})

task.spawn(function()
	while true do
		if SelfHB then
			pcall(function()
				if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
					local hrp = player.Character.HumanoidRootPart
					hrp.Size = Vector3.new(SelfSize,SelfSize,SelfSize)
					hrp.Transparency = 0.4
					hrp.Material = Enum.Material.Neon
					hrp.CanCollide = false
				end
			end)
		end
		task.wait(0.2)
	end
end)

-- =====================
-- MACRO
-- =====================

MacroTab:AddToggle({
	Name = "🤖 Macro Auto Click",
	Default = false,
	Callback = function(Value)
		MacroOn = Value
	end
})

MacroTab:AddSlider({
	Name = "⏱ Delay do Macro",
	Min = 0.01,
	Max = 0.3,
	Default = 0.05,
	Increment = 0.01,
	ValueName = "Sec",
	Callback = function(Value)
		MacroDelay = Value
	end
})

task.spawn(function()
	while true do
		if MacroOn then
			VIM:SendMouseButtonEvent(0,0,0,true,game,0)
			VIM:SendMouseButtonEvent(0,0,0,false,game,0)
		end
		task.wait(MacroDelay)
	end
end)

-- =====================
-- SETTINGS
-- =====================

SettingsTab:AddBind({
	Name = "⌨ Tecla Abrir/Fechar Hub",
	Default = Enum.KeyCode.RightControl,
	Hold = false,
	Callback = function()
		OrionLib:Toggle()
	end
})

SettingsTab:AddParagraph("🔥 Kaka Hub","Hub premium anime otimizado, sem loop duplicado e sem lag.")

OrionLib:Init()
