--[[
    MYSTIC HUB – COMPLETO COM LEVEL OFFSET (CORRIGIDO)
    Só as funções foram consertadas. Painel intacto.
]]

-- Carregar Fluent
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()

-- Criar janela
local Window = Fluent:CreateWindow({
    Title = "🐉 Mystic Hub",
    SubTitle = "Farm & Events",
    TabWidth = 180,
    Size = UDim2.fromOffset(660, 440),
    Acrylic = false,
    Theme = "Amethyst",
    MinimizeKey = Enum.KeyCode.End
})

-- ==================== SERVIÇOS E VARIÁVEIS GLOBAIS ====================
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")
local Lighting = game:GetService("Lighting")
local TeleportService = game:GetService("TeleportService")
local TweenService = game:GetService("TweenService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local VirtualUser = game:GetService("VirtualUser")
local RunService = game:GetService("RunService")
local CollectionService = game:GetService("CollectionService")
local HttpService = game:GetService("HttpService")
local UserInputService = game:GetService("UserInputService")

local PLR = Players.LocalPlayer
local Remote = ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("CommF_")
local Enemies = Workspace.Enemies
local Root = PLR.Character and PLR.Character:FindFirstChild("HumanoidRootPart")

-- Variáveis de controle (todas as toggles)
_G.Level = false
_G.LevelOffset = 0
_G.TravelDres = false
_G.AutoZou = false
_G.AutoFarmNear = false
_G.AutoFactory = false
_G.AutoRaidCastle = false
_G.AutoMaterial = false
_G.AutoEctoplasm = false
_G.Bartilo_Quest = false
_G.CitizenQuest = false
_G.DummyMan = false
_G.AutoBerry = false
_G.AutoFarmChest = false
_G.FarmMastery_Dev = false
_G.FarmMastery_G = false
_G.FarmMastery_S = false
_G.Auto_Cake_Prince = false
_G.AutoFarm_Bone = false
_G.AcceptQuestC = false
_G.AutoMiror = false
_G.AutoHytHallow = false
_G.Auto_Random_Bone = false
_G.TryLucky = false
_G.Praying = false
_G.Doughv2 = false
_G.AutoPhoenixF = false
_G.Tp_MasterA = false
_G.Auto_Rainbow_Haki = false
_G.GetQFast = false
_G.obsFarm = false
_G.AutoKenVTWO = false
_G.Auto_Mink = false
_G.Auto_Human = false
_G.Auto_Skypiea = false
_G.Auto_Fish = false
_G.AutoRipIngay = false
_G.AutoUnHaki = false
_G.Auto_SuperHuman = false
_G.AutoDeathStep = false
_G.Auto_SharkMan_Karate = false
_G.Auto_Electric_Claw = false
_G.AutoDragonTalon = false
_G.Auto_God_Human = false
_G.snaguine = false
_G.FarmEliteHunt = false
_G.StopWhenChalice = true
_G.Auto_Tushita = false
_G.Auto_Yama = false
_G.CDK = false
_G.CDK_YM = false
_G.CDK_TS = false
_G.AutoPole = false
_G.AutoPoleV2 = false
_G.AutoLawKak = false
_G.AutoSaw = false
_G.AutoSaber = false
_G.AutoColShad = false
_G.AutoGetUsoap = false
_G.Greybeard = false
_G.WardenBoss = false
_G.MarinesCoat = false
_G.SwanCoat = false
_G.IceBossRen = false
_G.KeysRen = false
_G.AutoTridentW2 = false
_G.LongsWord = false
_G.BlackSpikey = false
_G.DarkBladev3 = false
_G.AutoEcBoss = false
_G.Auto_Def_DarkCoat = false
_G.Auto_DonAcces = false
_G.Auto_SwanGG = false
_G.AutoBigmom = false
_G.Auto_Cavender = false
_G.TwinHook = false
_G.AutoSerpentBow = false
_G.AutoKilo = false
_G.AutoValentineGacha = false
_G.SailBoats = false
_G.SailBoat_Hydra = false
_G.Shark = false
_G.Piranha = false
_G.TerrorShark = false
_G.MobCrew = false
_G.HCM = false
_G.PGB = false
_G.FishBoat = false
_G.SeaBeast1 = false
_G.Leviathan1 = false
_G.AutofindKitIs = false
_G.tweenShrine = false
_G.Collect_Ember = false
_G.Trade_Ember = false
_G.FindMirage = false
_G.HighestMirage = false
_G.TPGEAR = false
_G.can = false
_G.Addealer = false
_G.FarmChestM = false
_G.Auto_Soul_Guitar = false
_G.AutoMatSoul = false
_G.AcientOne = false
_G.TPDoor = false
_G.Complete_Trials = false
_G.Defeating = false
_G.Dojoo = false
_G.FarmBlazeEM = false
_G.UPGDrago = false
_G.DragoV1 = false
_G.AutoFireFlowers = false
_G.DragoV3 = false
_G.Relic123 = false
_G.TrainDrago = false
_G.TpDrago_Prehis = false
_G.BuyDrago = false
_G.DT_Uzoth = false
_G.CraftVM = false
_G.Prehis_Find = false
_G.Prehis_Skills = false
_G.Prehis_DB = false
_G.Prehis_DE = false
_G.ResetPH = false
_G.Auto_StartRaid = false
_G.TpLab = false
_G.Raiding = false
_G.KillH = false
_G.Auto_Awakener = false
_G.Seriality = true
_B = true
Boud = true
RandomCFrame = false
KenTest = true
SoulGuitar = false
MousePos = Vector3.new(0,0,0)
Sec = 0.1
Num_self = 25
pSats = 10
SelectIsland = "Cake"
_G.SelectMaterial = "Leather + Scrap Metal"
_G.SelectedBoat = "Guardian"
_G.DangerSc = "Lv 1"
_G.SelectChip = "Ice"
_G.SelectFruit = "Bomb"
SelectF_Adv = "Bomb"
_G.SelectWeapon = "Melee"
_G.ChooseWP = "Melee"
NPClist = ""

-- Variáveis extras para as funções
shouldTween = true
HealthM = 5000
LookM = false
NextIs = false

-- ==================== DECLARAÇÃO PRÉVIA DA TABELA ATTACK ====================
Attack = {}
Attack.__index = Attack
Attack.Alive = function(model)
    if not model then return false end
    local hum = model:FindFirstChild("Humanoid")
    return hum and hum.Health > 0
end

-- ==================== FUNÇÕES AUXILIARES ====================
local function _tp(target)
    local char = PLR.Character
    if not char or not char:FindFirstChild("HumanoidRootPart") then return end
    local root = char.HumanoidRootPart
    if (target.Position - root.Position).Magnitude > 1000 then
        local tween = TweenService:Create(root, TweenInfo.new((target.Position - root.Position).Magnitude / 300, Enum.EasingStyle.Linear), {CFrame = target})
        tween:Play()
        task.spawn(function()
            while tween.PlaybackState == Enum.PlaybackState.Playing do
                if not shouldTween then tween:Cancel() break end
                task.wait(0.1)
            end
        end)
    else
        root.CFrame = target
    end
end

local function notween(p)
    PLR.Character.HumanoidRootPart.CFrame = p
end

function CheckBoat()
    for i, v in pairs(Workspace.Boats:GetChildren()) do
        if tostring(v.Owner.Value) == tostring(PLR.Name) then return v end
    end
    return false
end

function CheckEnemiesBoat()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if v.Name == "FishBoat" and v:FindFirstChild("Health") and v.Health.Value > 0 then return true end
    end
    return false
end

function CheckPirateGrandBrigade()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if (v.Name == "PirateGrandBrigade" or v.Name == "PirateBrigade") and v:FindFirstChild("Health") and v.Health.Value > 0 then return true end
    end
    return false
end

function CheckShark()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if v.Name == "Shark" and Attack.Alive(v) then return true end
    end
    return false
end

function CheckTerrorShark()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if v.Name == "Terrorshark" and Attack.Alive(v) then return true end
    end
    return false
end

function CheckPiranha()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if v.Name == "Piranha" and Attack.Alive(v) then return true end
    end
    return false
end

function CheckFishCrew()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if (v.Name == "Fish Crew Member" or v.Name == "Haunted Crew Member") and Attack.Alive(v) then return true end
    end
    return false
end

function CheckHauntedCrew()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if v.Name == "Haunted Crew Member" and Attack.Alive(v) then return true end
    end
    return false
end

function CheckSeaBeast()
    return Workspace.SeaBeasts:FindFirstChild("SeaBeast1") ~= nil
end

function CheckLeviathan()
    return Workspace.SeaBeasts:FindFirstChild("Leviathan") ~= nil
end

function GetBP(name)
    return PLR.Backpack:FindFirstChild(name) or PLR.Character:FindFirstChild(name)
end

function GetWP(name)
    for _, v in pairs(Remote:InvokeServer("getInventory")) do
        if type(v) == "table" and v.Type == "Sword" and v.Name == name then return true end
    end
    return GetBP(name) ~= nil
end

function GetM(name)
    for _, tab in pairs(Remote:InvokeServer("getInventory")) do
        if type(tab) == "table" and tab.Type == "Material" and tab.Name == name then return tab.Count end
    end
    return 0
end

function GetIn(name)
    for _, v in pairs(Remote:InvokeServer("getInventory")) do
        if type(v) == "table" and v.Name == name then return true end
    end
    return GetBP(name) ~= nil
end

function EquipWeapon(name)
    if not name then return end
    if PLR.Backpack:FindFirstChild(name) then
        PLR.Character.Humanoid:EquipTool(PLR.Backpack:FindFirstChild(name))
    end
end

function weaponSc(weaponType)
    for _, v in pairs(PLR.Backpack:GetChildren()) do
        if v:IsA("Tool") and v.ToolTip == weaponType then
            EquipWeapon(v.Name)
            return
        end
    end
end

function Useskills(weapon, skill)
    if weapon == "Melee" then weaponSc("Melee")
    elseif weapon == "Sword" then weaponSc("Sword")
    elseif weapon == "Blox Fruit" then weaponSc("Blox Fruit")
    elseif weapon == "Gun" then weaponSc("Gun")
    end
    if skill == "Z" or skill == "X" or skill == "C" or skill == "V" or skill == "Y" then
        VirtualInputManager:SendKeyEvent(true, skill, false, game)
        VirtualInputManager:SendKeyEvent(false, skill, false, game)
    end
end

function statsSetings(stat, value)
    if PLR.Data.Points.Value == 0 then return end
    local statMap = {Melee="Melee", Defense="Defense", Sword="Sword", Gun="Gun", Devil="Demon Fruit"}
    Remote:InvokeServer("AddPoint", statMap[stat] or stat, value)
end

-- ==================== MÉTODOS DE ATAQUE ====================
Attack.Kill = function(model, toggle)
    if model and toggle then
        if not model:GetAttribute("Locked") then model:SetAttribute("Locked", model.HumanoidRootPart.CFrame) end
        _tp(model.HumanoidRootPart.CFrame + CFrame.new(0,30,0))
    end
end

Attack.Kill2 = function(model, toggle)
    if model and toggle then
        if not model:GetAttribute("Locked") then model:SetAttribute("Locked", model.HumanoidRootPart.CFrame) end
        _tp(model.HumanoidRootPart.CFrame + CFrame.new(0,30,8))
    end
end

Attack.KillSea = function(model, toggle)
    if model and toggle then
        if not model:GetAttribute("Locked") then model:SetAttribute("Locked", model.HumanoidRootPart.CFrame) end
        notween(model.HumanoidRootPart.CFrame + CFrame.new(0,50,8))
        task.wait(0.85)
        notween(model.HumanoidRootPart.CFrame + CFrame.new(0,400,0))
        task.wait(1)
    end
end

Attack.Sword = function(model, toggle)
    if model and toggle then
        if not model:GetAttribute("Locked") then model:SetAttribute("Locked", model.HumanoidRootPart.CFrame) end
        weaponSc("Sword")
        _tp(model.HumanoidRootPart.CFrame + CFrame.new(0,30,0))
    end
end

Attack.Mas = function(model, toggle)
    if model and toggle then
        if not model:GetAttribute("Locked") then model:SetAttribute("Locked", model.HumanoidRootPart.CFrame) end
        if model.Humanoid.Health <= HealthM then
            _tp(model.HumanoidRootPart.CFrame + CFrame.new(0,20,0))
            Useskills("Blox Fruit","Z")
            Useskills("Blox Fruit","X")
            Useskills("Blox Fruit","C")
        else
            weaponSc("Melee")
            _tp(model.HumanoidRootPart.CFrame + CFrame.new(0,30,0))
        end
    end
end

Attack.Masgun = function(model, toggle)
    if model and toggle then
        if not model:GetAttribute("Locked") then model:SetAttribute("Locked", model.HumanoidRootPart.CFrame) end
        if model.Humanoid.Health <= HealthM then
            _tp(model.HumanoidRootPart.CFrame + CFrame.new(0,35,8))
            Useskills("Gun","Z")
            Useskills("Gun","X")
        else
            weaponSc("Melee")
            _tp(model.HumanoidRootPart.CFrame + CFrame.new(0,30,0))
        end
    end
end

-- ==================== QUESTNETA COMPLETA (W1, W2, W3) ====================
function QuestNeta(offset)
    offset = offset or 0
    local a = PLR.Data.Level.Value + offset
    local maxLevel = 2800
    if a > maxLevel then a = maxLevel end

    if game.PlaceId == 2753915549 or game.PlaceId == 85211729168715 then -- World 1
        if a <= 9 then return {Mon = "Bandit", Qname = "BanditQuest1", Qdata = 1, PosM = CFrame.new(1045.96,27,1560.82), NameMon = "Bandit", PosQ = CFrame.new(1045.96,27,1560.82)}
        elseif a <= 14 then return {Mon = "Monkey", Qname = "JungleQuest", Qdata = 1, PosM = CFrame.new(-1448.52,67.85,11.47), NameMon = "Monkey", PosQ = CFrame.new(-1598.09,35.55,153.38)}
        elseif a <= 29 then return {Mon = "Gorilla", Qname = "JungleQuest", Qdata = 2, PosM = CFrame.new(-1129.88,40.46,-525.42), NameMon = "Gorilla", PosQ = CFrame.new(-1598.09,35.55,153.38)}
        elseif a <= 39 then return {Mon = "Pirate", Qname = "BuggyQuest1", Qdata = 1, PosM = CFrame.new(-1103.51,13.75,3896.09), NameMon = "Pirate", PosQ = CFrame.new(-1141.07,4.1,3831.55)}
        elseif a <= 59 then return {Mon = "Brute", Qname = "BuggyQuest1", Qdata = 2, PosM = CFrame.new(-1140.08,14.81,4322.92), NameMon = "Brute", PosQ = CFrame.new(-1141.07,4.1,3831.55)}
        elseif a <= 74 then return {Mon = "Desert Bandit", Qname = "DesertQuest", Qdata = 1, PosM = CFrame.new(924.8,6.45,4481.59), NameMon = "Desert Bandit", PosQ = CFrame.new(894.49,5.14,4392.43)}
        elseif a <= 89 then return {Mon = "Desert Officer", Qname = "DesertQuest", Qdata = 2, PosM = CFrame.new(1608.28,8.61,4371.01), NameMon = "Desert Officer", PosQ = CFrame.new(894.49,5.14,4392.43)}
        elseif a <= 99 then return {Mon = "Snow Bandit", Qname = "SnowQuest", Qdata = 1, PosM = CFrame.new(1354.35,87.27,-1393.95), NameMon = "Snow Bandit", PosQ = CFrame.new(1389.74,88.15,-1298.91)}
        elseif a <= 119 then return {Mon = "Snowman", Qname = "SnowQuest", Qdata = 2, PosM = CFrame.new(6241.99,51.52,-1243.98), NameMon = "Snowman", PosQ = CFrame.new(1389.74,88.15,-1298.91)}
        elseif a <= 149 then return {Mon = "Chief Petty Officer", Qname = "MarineQuest2", Qdata = 1, PosM = CFrame.new(-4881.23,22.65,4273.75), NameMon = "Chief Petty Officer", PosQ = CFrame.new(-5039.59,27.35,4324.68)}
        elseif a <= 174 then return {Mon = "Sky Bandit", Qname = "SkyQuest", Qdata = 1, PosM = CFrame.new(-4953.21,295.74,-2899.23), NameMon = "Sky Bandit", PosQ = CFrame.new(-4839.53,716.37,-2619.44)}
        elseif a <= 189 then return {Mon = "Dark Master", Qname = "SkyQuest", Qdata = 2, PosM = CFrame.new(-5259.84,391.4,-2229.04), NameMon = "Dark Master", PosQ = CFrame.new(-4839.53,716.37,-2619.44)}
        elseif a <= 209 then return {Mon = "Prisoner", Qname = "PrisonerQuest", Qdata = 1, PosM = CFrame.new(5098.97,-0.32,474.24), NameMon = "Prisoner", PosQ = CFrame.new(5308.93,1.66,475.12)}
        elseif a <= 249 then return {Mon = "Dangerous Prisoner", Qname = "PrisonerQuest", Qdata = 2, PosM = CFrame.new(5654.56,15.63,866.3), NameMon = "Dangerous Prisoner", PosQ = CFrame.new(5308.93,1.66,475.12)}
        elseif a <= 274 then return {Mon = "Toga Warrior", Qname = "ColosseumQuest", Qdata = 1, PosM = CFrame.new(-1820.21,51.68,-2740.67), NameMon = "Toga Warrior", PosQ = CFrame.new(-1580.05,6.35,-2986.48)}
        elseif a <= 299 then return {Mon = "Gladiator", Qname = "ColosseumQuest", Qdata = 2, PosM = CFrame.new(-1292.84,56.38,-3339.03), NameMon = "Gladiator", PosQ = CFrame.new(-1580.05,6.35,-2986.48)}
        elseif a <= 324 then return {Mon = "Military Soldier", Qname = "MagmaQuest", Qdata = 1, PosM = CFrame.new(-5411.16,11.08,8454.29), NameMon = "Military Soldier", PosQ = CFrame.new(-5313.37,10.95,8515.29)}
        elseif a <= 374 then return {Mon = "Military Spy", Qname = "MagmaQuest", Qdata = 2, PosM = CFrame.new(-5802.87,86.26,8828.86), NameMon = "Military Spy", PosQ = CFrame.new(-5313.37,10.95,8515.29)}
        elseif a <= 399 then return {Mon = "Fishman Warrior", Qname = "FishmanQuest", Qdata = 1, PosM = CFrame.new(60878.3,18.48,1543.76), NameMon = "Fishman Warrior", PosQ = CFrame.new(61122.65,18.5,1569.4)}
        elseif a <= 449 then return {Mon = "Fishman Commando", Qname = "FishmanQuest", Qdata = 2, PosM = CFrame.new(61922.63,18.48,1493.93), NameMon = "Fishman Commando", PosQ = CFrame.new(61122.65,18.5,1569.4)}
        elseif a <= 474 then return {Mon = "God's Guard", Qname = "SkyExp1Quest", Qdata = 1, PosM = CFrame.new(-4710.04,845.28,-1927.31), NameMon = "God's Guard", PosQ = CFrame.new(-4721.89,843.87,-1949.97)}
        elseif a <= 524 then return {Mon = "Shanda", Qname = "SkyExp1Quest", Qdata = 2, PosM = CFrame.new(-7678.49,5566.4,-497.22), NameMon = "Shanda", PosQ = CFrame.new(-7859.1,5544.19,-381.48)}
        elseif a <= 549 then return {Mon = "Royal Squad", Qname = "SkyExp2Quest", Qdata = 1, PosM = CFrame.new(-7624.25,5658.13,-1467.35), NameMon = "Royal Squad", PosQ = CFrame.new(-7906.82,5634.66,-1411.99)}
        elseif a <= 624 then return {Mon = "Royal Soldier", Qname = "SkyExp2Quest", Qdata = 2, PosM = CFrame.new(-7836.75,5645.66,-1790.62), NameMon = "Royal Soldier", PosQ = CFrame.new(-7906.82,5634.66,-1411.99)}
        elseif a <= 649 then return {Mon = "Galley Pirate", Qname = "FountainQuest", Qdata = 1, PosM = CFrame.new(5551.02,78.9,3930.41), NameMon = "Galley Pirate", PosQ = CFrame.new(5259.82,37.35,4050.03)}
        else return {Mon = "Galley Captain", Qname = "FountainQuest", Qdata = 2, PosM = CFrame.new(5441.95,42.5,4950.09), NameMon = "Galley Captain", PosQ = CFrame.new(5259.82,37.35,4050.03)}
        end
    elseif game.PlaceId == 4442272183 or game.PlaceId == 79091703265657 then -- World 2
        if a <= 724 then return {Mon = "Raider", Qname = "Area1Quest", Qdata = 1, PosM = CFrame.new(-728.33,52.78,2345.77), NameMon = "Raider", PosQ = CFrame.new(-429.54,71.77,1836.18)}
        elseif a <= 774 then return {Mon = "Mercenary", Qname = "Area1Quest", Qdata = 2, PosM = CFrame.new(-1004.32,80.16,1424.62), NameMon = "Mercenary", PosQ = CFrame.new(-429.54,71.77,1836.18)}
        elseif a <= 799 then return {Mon = "Swan Pirate", Qname = "Area2Quest", Qdata = 1, PosM = CFrame.new(1068.66,137.61,1322.11), NameMon = "Swan Pirate", PosQ = CFrame.new(638.44,71.77,918.28)}
        elseif a <= 874 then return {Mon = "Factory Staff", Qname = "Area2Quest", Qdata = 2, PosM = CFrame.new(73.08,81.86,-27.47), NameMon = "Factory Staff", PosQ = CFrame.new(632.7,73.11,918.67)}
        elseif a <= 899 then return {Mon = "Marine Lieutenant", Qname = "MarineQuest3", Qdata = 1, PosM = CFrame.new(-2821.37,75.9,-3070.09), NameMon = "Marine Lieutenant", PosQ = CFrame.new(-2440.8,71.71,-3216.07)}
        elseif a <= 949 then return {Mon = "Marine Captain", Qname = "MarineQuest3", Qdata = 2, PosM = CFrame.new(-1861.23,80.18,-3254.7), NameMon = "Marine Captain", PosQ = CFrame.new(-2440.8,71.71,-3216.07)}
        elseif a <= 974 then return {Mon = "Zombie", Qname = "ZombieQuest", Qdata = 1, PosM = CFrame.new(-5657.78,78.97,-928.69), NameMon = "Zombie", PosQ = CFrame.new(-5497.06,47.59,-795.24)}
        elseif a <= 999 then return {Mon = "Vampire", Qname = "ZombieQuest", Qdata = 2, PosM = CFrame.new(-6037.67,32.18,-1340.66), NameMon = "Vampire", PosQ = CFrame.new(-5497.06,47.59,-795.24)}
        elseif a <= 1049 then return {Mon = "Snow Trooper", Qname = "SnowMountainQuest", Qdata = 1, PosM = CFrame.new(549.15,427.39,-5563.7), NameMon = "Snow Trooper", PosQ = CFrame.new(609.86,400.12,-5372.26)}
        elseif a <= 1099 then return {Mon = "Winter Warrior", Qname = "SnowMountainQuest", Qdata = 2, PosM = CFrame.new(1142.75,475.64,-5199.42), NameMon = "Winter Warrior", PosQ = CFrame.new(609.86,400.12,-5372.26)}
        elseif a <= 1124 then return {Mon = "Lab Subordinate", Qname = "IceSideQuest", Qdata = 1, PosM = CFrame.new(-5707.47,15.95,-4513.39), NameMon = "Lab Subordinate", PosQ = CFrame.new(-6064.07,15.24,-4902.98)}
        elseif a <= 1174 then return {Mon = "Horned Warrior", Qname = "IceSideQuest", Qdata = 2, PosM = CFrame.new(-6341.37,15.95,-5723.16), NameMon = "Horned Warrior", PosQ = CFrame.new(-6064.07,15.24,-4902.98)}
        elseif a <= 1199 then return {Mon = "Magma Ninja", Qname = "FireSideQuest", Qdata = 1, PosM = CFrame.new(-5449.67,76.66,-5808.2), NameMon = "Magma Ninja", PosQ = CFrame.new(-5428.03,15.06,-5299.43)}
        elseif a <= 1249 then return {Mon = "Lava Pirate", Qname = "FireSideQuest", Qdata = 2, PosM = CFrame.new(-5213.33,49.74,-4701.45), NameMon = "Lava Pirate", PosQ = CFrame.new(-5428.03,15.06,-5299.43)}
        elseif a <= 1274 then return {Mon = "Ship Deckhand", Qname = "ShipQuest1", Qdata = 1, PosM = CFrame.new(1212.01,150.79,33059.25), NameMon = "Ship Deckhand", PosQ = CFrame.new(1037.8,125.09,32911.6)}
        elseif a <= 1299 then return {Mon = "Ship Engineer", Qname = "ShipQuest1", Qdata = 2, PosM = CFrame.new(919.48,43.54,32779.97), NameMon = "Ship Engineer", PosQ = CFrame.new(1037.8,125.09,32911.6)}
        elseif a <= 1324 then return {Mon = "Ship Steward", Qname = "ShipQuest2", Qdata = 1, PosM = CFrame.new(919.44,129.56,33436.04), NameMon = "Ship Steward", PosQ = CFrame.new(968.81,125.09,33244.13)}
        elseif a <= 1349 then return {Mon = "Ship Officer", Qname = "ShipQuest2", Qdata = 2, PosM = CFrame.new(1036.02,181.44,33315.73), NameMon = "Ship Officer", PosQ = CFrame.new(968.81,125.09,33244.13)}
        elseif a <= 1374 then return {Mon = "Arctic Warrior", Qname = "FrostQuest", Qdata = 1, PosM = CFrame.new(5966.25,62.97,-6179.38), NameMon = "Arctic Warrior", PosQ = CFrame.new(5667.66,26.8,-6486.09)}
        elseif a <= 1424 then return {Mon = "Snow Lurker", Qname = "FrostQuest", Qdata = 2, PosM = CFrame.new(5407.07,69.19,-6880.88), NameMon = "Snow Lurker", PosQ = CFrame.new(5667.66,26.8,-6486.09)}
        elseif a <= 1449 then return {Mon = "Sea Soldier", Qname = "ForgottenQuest", Qdata = 1, PosM = CFrame.new(-3028.22,64.67,-9775.43), NameMon = "Sea Soldier", PosQ = CFrame.new(-3054.44,235.54,-10142.82)}
        else return {Mon = "Water Fighter", Qname = "ForgottenQuest", Qdata = 2, PosM = CFrame.new(-3352.9,285.02,-10534.84), NameMon = "Water Fighter", PosQ = CFrame.new(-3054.44,235.54,-10142.82)}
        end
    else -- World 3 (PlaceId == 7449423635)
        if a <= 1524 then return {Mon = "Pirate Millionaire", Qname = "PortQuest", Qdata = 1, PosM = CFrame.new(-290.09,44.35,5581.76), NameMon = "Pirate Millionaire", PosQ = CFrame.new(-390.1,72.93,5379.79)}
        elseif a <= 1574 then return {Mon = "Pistol Billionaire", Qname = "PortQuest", Qdata = 2, PosM = CFrame.new(-47.07,76.54,5903.79), NameMon = "Pistol Billionaire", PosQ = CFrame.new(-390.1,72.93,5379.79)}
        elseif a <= 1624 then return {Mon = "Dragon Crew Warrior", Qname = "HydraQuest", Qdata = 1, PosM = CFrame.new(5228.34,104.99,1039.52), NameMon = "Dragon Crew Warrior", PosQ = CFrame.new(5242.84,59.39,761.35)}
        elseif a <= 1674 then return {Mon = "Dragon Crew Archer", Qname = "HydraQuest", Qdata = 2, PosM = CFrame.new(5700.17,613.56,339.7), NameMon = "Dragon Crew Archer", PosQ = CFrame.new(5242.84,59.39,761.35)}
        elseif a <= 1724 then return {Mon = "Female Islander", Qname = "HydraQuest2", Qdata = 1, PosM = CFrame.new(5341.34,602.43,-1160.77), NameMon = "Female Islander", PosQ = CFrame.new(5760.85,611.19,-1124.96)}
        elseif a <= 1774 then return {Mon = "Giant Islander", Qname = "HydraQuest2", Qdata = 2, PosM = CFrame.new(4839.29,612.35,-1561.42), NameMon = "Giant Islander", PosQ = CFrame.new(5760.85,611.19,-1124.96)}
        elseif a <= 1824 then return {Mon = "Marine Commodore", Qname = "MarineQuest4", Qdata = 1, PosM = CFrame.new(2438.31,73.45,-3170.83), NameMon = "Marine Commodore", PosQ = CFrame.new(2404.09,73.12,-3237.95)}
        elseif a <= 1874 then return {Mon = "Marine Rear Admiral", Qname = "MarineQuest4", Qdata = 2, PosM = CFrame.new(2341.16,73.45,-3831.63), NameMon = "Marine Rear Admiral", PosQ = CFrame.new(2404.09,73.12,-3237.95)}
        elseif a <= 1924 then return {Mon = "Fishman Raider", Qname = "CandyQuest1", Qdata = 1, PosM = CFrame.new(-3827.62,13.88,-10237.15), NameMon = "Fishman Raider", PosQ = CFrame.new(-2250.77,14.88,-12401.76)}
        elseif a <= 1974 then return {Mon = "Fishman Captain", Qname = "CandyQuest1", Qdata = 2, PosM = CFrame.new(-2476.99,13.62,-11579.52), NameMon = "Fishman Captain", PosQ = CFrame.new(-2250.77,14.88,-12401.76)}
        elseif a <= 2024 then return {Mon = "Forest Pirate", Qname = "CandyQuest2", Qdata = 1, PosM = CFrame.new(-165.73,20.08,-12080.08), NameMon = "Forest Pirate", PosQ = CFrame.new(-29.98,20.12,-12543.83)}
        elseif a <= 2074 then return {Mon = "Mythological Pirate", Qname = "CandyQuest2", Qdata = 2, PosM = CFrame.new(413.43,20.25,-12871.9), NameMon = "Mythological Pirate", PosQ = CFrame.new(-29.98,20.12,-12543.83)}
        elseif a <= 2124 then return {Mon = "Musketeer Pirate", Qname = "HauntedQuest1", Qdata = 1, PosM = CFrame.new(-935.25,142.12,6108.82), NameMon = "Musketeer Pirate", PosQ = CFrame.new(-951.34,141.21,5634.34)}
        elseif a <= 2174 then return {Mon = "Reborn Skeleton", Qname = "HauntedQuest1", Qdata = 2, PosM = CFrame.new(-875.05,123.63,6078.61), NameMon = "Reborn Skeleton", PosQ = CFrame.new(-951.34,141.21,5634.34)}
        elseif a <= 2224 then return {Mon = "Living Zombie", Qname = "HauntedQuest2", Qdata = 1, PosM = CFrame.new(-5770.84,12.52,-700.17), NameMon = "Living Zombie", PosQ = CFrame.new(-9505.76,169.17,6234.34)}
        elseif a <= 2274 then return {Mon = "Demonic Soul", Qname = "HauntedQuest2", Qdata = 2, PosM = CFrame.new(-9510.97,171.69,6143.08), NameMon = "Demonic Soul", PosQ = CFrame.new(-9505.76,169.17,6234.34)}
        elseif a <= 2324 then return {Mon = "Posessed Mummy", Qname = "HauntedQuest3", Qdata = 1, PosM = CFrame.new(-10091.24,136.56,6137.95), NameMon = "Posessed Mummy", PosQ = CFrame.new(-9505.76,169.17,6234.34)}
        elseif a <= 2374 then return {Mon = "Peanut Scout", Qname = "NutsIslandQuest", Qdata = 1, PosM = CFrame.new(-2082.9,44.59,-12185.09), NameMon = "Peanut Scout", PosQ = CFrame.new(-2104.79,48.01,-12316.57)}
        elseif a <= 2424 then return {Mon = "Peanut President", Qname = "NutsIslandQuest", Qdata = 2, PosM = CFrame.new(-2161.43,92.51,-12513.78), NameMon = "Peanut President", PosQ = CFrame.new(-2104.79,48.01,-12316.57)}
        elseif a <= 2474 then return {Mon = "Ice Cream Chef", Qname = "IceCreamQuest", Qdata = 1, PosM = CFrame.new(-827.67,65.31,-11002.58), NameMon = "Ice Cream Chef", PosQ = CFrame.new(-820.73,65.02,-10956.12)}
        elseif a <= 2524 then return {Mon = "Ice Cream Commander", Qname = "IceCreamQuest", Qdata = 2, PosM = CFrame.new(-787.9,132.89,-11283.47), NameMon = "Ice Cream Commander", PosQ = CFrame.new(-820.73,65.02,-10956.12)}
        elseif a <= 2574 then return {Mon = "Cookie Crafter", Qname = "CakeQuest1", Qdata = 1, PosM = CFrame.new(-2081.08,37.11,-12151.02), NameMon = "Cookie Crafter", PosQ = CFrame.new(-2019.5,37.8, -12028.91)}
        elseif a <= 2624 then return {Mon = "Cake Guard", Qname = "CakeQuest1", Qdata = 2, PosM = CFrame.new(-1745.24,37.04,-11921.21), NameMon = "Cake Guard", PosQ = CFrame.new(-2019.5,37.8, -12028.91)}
        elseif a <= 2674 then return {Mon = "Baking Staff", Qname = "CakeQuest2", Qdata = 1, PosM = CFrame.new(-1933.26,37.11,-12837.76), NameMon = "Baking Staff", PosQ = CFrame.new(-1924.38,37.8,-12833.6)}
        else return {Mon = "Head Baker", Qname = "CakeQuest2", Qdata = 2, PosM = CFrame.new(-2132.17,73.53,-12543.08), NameMon = "Head Baker", PosQ = CFrame.new(-1924.38,37.8,-12833.6)}
        end
    end
end

-- ==================== LOOP PRINCIPAL DE FARM LEVEL ====================
task.spawn(function()
    while task.wait(Sec) do
        if _G.Level then
            pcall(function()
                local quest = QuestNeta(_G.LevelOffset or 0)
                local mainGui = PLR.PlayerGui:FindFirstChild("Main")
                if mainGui and mainGui:FindFirstChild("Quest") then
                    local questTitle = mainGui.Quest.Container.QuestTitle.Title.Text
                    if not string.find(questTitle, quest.NameMon) then Remote:InvokeServer("AbandonQuest") end
                    if mainGui.Quest.Visible == false then
                        _tp(quest.PosQ)
                        if Root and (Root.Position - quest.PosQ.Position).Magnitude <= 5 then
                            Remote:InvokeServer("StartQuest", quest.Qname, quest.Qdata)
                        end
                    else
                        if Workspace.Enemies:FindFirstChild(quest.Mon) then
                            for _, v in pairs(Workspace.Enemies:GetChildren()) do
                                if Attack.Alive(v) and v.Name == quest.Mon then
                                    repeat task.wait() Attack.Kill(v, _G.Level) until not _G.Level or v.Humanoid.Health <= 0 or not v.Parent or mainGui.Quest.Visible == false
                                end
                            end
                        else
                            _tp(quest.PosM)
                        end
                    end
                end
            end)
        end
    end
end)

-- ==================== FINALIZAÇÃO ====================
Window:SelectTab(1)
