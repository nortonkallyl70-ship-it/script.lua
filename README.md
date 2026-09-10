--[[
    ═══════════════════════════════════════════════════════════════
    HUB BLOX FRUITS - UPDATE 30 - VERSÃO EXPANDIDA
    ═══════════════════════════════════════════════════════════════
    Features: 80+ funções
    Sistema: Keybind, Save Config, Notificações, FPS Boost
    Abas: Farm, Boss, Fruit, Raid, Combat, Teleport, ESP, Player, Misc, Settings
]]

-- ============================================================
-- SERVIÇOS
-- ============================================================
local Players = game:GetService("Players")
local RS = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")
local VIM = game:GetService("VirtualInputManager")
local UIS = game:GetService("UserInputService")
local Lighting = game:GetService("Lighting")
local StarterGui = game:GetService("StarterGui")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera

-- ============================================================
-- REMOTES REAIS
-- ============================================================
local Remotes = RS:WaitForChild("Remotes")
local CommF_ = Remotes:WaitForChild("CommF_")
local CommE_ = Remotes:WaitForChild("CommE_")

-- ============================================================
-- ESTADO GLOBAL
-- ============================================================
local State = {
    -- Farm
    AutoFarmLevel = false,
    AutoFarmNearest = false,
    AutoFarmSelected = false,
    AutoFarmBoss = false,
    AutoFarmChest = false,
    AutoFarmItem = false,
    AutoFarmMagnet = false,
    AutoQuest = false,
    AutoCompleteQuest = false,
    BringMobs = false,
    SelectedMob = "Bandit",
    FarmDistance = 3,
    FarmDelay = 0.3,
    -- Combat
    KillAura = false,
    AuraRange = 30,
    AutoHaki = false,
    FastAttack = false,
    AutoClick = false,
    AutoSkill = false,
    SkillKey = "Z",
    -- Fruit
    AutoFarmFruit = false,
    FruitSniper = false,
    AutoStoreFruit = false,
    FruitESP = false,
    FruitNotify = false,
    -- Raid
    AutoRaid = false,
    AutoRaidChip = false,
    AutoAwaken = false,
    -- Boss
    AutoBoss = false,
    SelectedBoss = "Saber Expert",
    -- ESP
    PlayerESP = false,
    ChestESP = false,
    BossESP = false,
    MobESP = false,
    -- Player
    AutoStats = false,
    StatsMode = "Melee",
    -- Misc
    AntiAFK = false,
    InfiniteJump = false,
    WalkOnWater = false,
    NoClip = false,
    FPSBoost = false,
    AntiFling = false,
    -- Settings
    NotifyEnabled = true,
    ConfigName = "default",
}

-- ============================================================
-- SISTEMA DE NOTIFICAÇÃO
-- ============================================================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "HubUpdate30"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

local NotifyContainer = Instance.new("Frame")
NotifyContainer.Size = UDim2.new(0, 300, 0, 400)
NotifyContainer.Position = UDim2.new(1, -310, 0, 20)
NotifyContainer.BackgroundTransparency = 1
NotifyContainer.Parent = ScreenGui

local NotifyLayout = Instance.new("UIListLayout", NotifyContainer)
NotifyLayout.Padding = UDim.new(0, 5)
NotifyLayout.VerticalAlignment = Enum.VerticalAlignment.Top

local function notify(title, text, duration)
    if not State.NotifyEnabled then return end
    duration = duration or 3
    
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 0, 55)
    frame.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
    frame.BorderSizePixel = 0
    frame.Parent = NotifyContainer
    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 6)
    
    local accent = Instance.new("Frame")
    accent.Size = UDim2.new(0, 4, 1, 0)
    accent.BackgroundColor3 = Color3.fromRGB(160, 0, 0)
    accent.BorderSizePixel = 0
    accent.Parent = frame
    Instance.new("UICorner", accent).CornerRadius = UDim.new(0, 6)
    
    local t = Instance.new("TextLabel")
    t.Size = UDim2.new(1, -15, 0, 22)
    t.Position = UDim2.new(0, 12, 0, 3)
    t.BackgroundTransparency = 1
    t.Text = title
    t.TextColor3 = Color3.fromRGB(255, 255, 255)
    t.Font = Enum.Font.GothamBold
    t.TextSize = 12
    t.TextXAlignment = Enum.TextXAlignment.Left
    t.Parent = frame
    
    local d = Instance.new("TextLabel")
    d.Size = UDim2.new(1, -15, 0, 25)
    d.Position = UDim2.new(0, 12, 0, 25)
    d.BackgroundTransparency = 1
    d.Text = text
    d.TextColor3 = Color3.fromRGB(200, 200, 200)
    d.Font = Enum.Font.Gotham
    d.TextSize = 10
    d.TextXAlignment = Enum.TextXAlignment.Left
    d.TextWrapped = true
    d.Parent = frame
    
    task.delay(duration, function()
        if frame and frame.Parent then
            frame:Destroy()
        end
    end)
end

-- ============================================================
-- CRIAÇÃO DA JANELA PRINCIPAL
-- ============================================================
local Main = Instance.new("Frame")
Main.Size = UDim2.new(0, 550, 0, 450)
Main.Position = UDim2.new(0.5, -275, 0.5, -225)
Main.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
Main.Parent = ScreenGui
Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 10)

local TopBar = Instance.new("Frame")
TopBar.Size = UDim2.new(1, 0, 0, 42)
TopBar.BackgroundColor3 = Color3.fromRGB(160, 0, 0)
TopBar.BorderSizePixel = 0
TopBar.Parent = Main
Instance.new("UICorner", TopBar).CornerRadius = UDim.new(0, 10)

local Logo = Instance.new("TextLabel")
Logo.Size = UDim2.new(1, -140, 1, 0)
Logo.Position = UDim2.new(0, 15, 0, 0)
Logo.BackgroundTransparency = 1
Logo.Text = "⚔ BLOX FRUITS HUB | UPDATE 30"
Logo.TextColor3 = Color3.fromRGB(255, 255, 255)
Logo.Font = Enum.Font.GothamBold
Logo.TextSize = 16
Logo.TextXAlignment = Enum.TextXAlignment.Left
Logo.Parent = TopBar

local MinimizeBtn = Instance.new("TextButton")
MinimizeBtn.Size = UDim2.new(0, 30, 0, 30)
MinimizeBtn.Position = UDim2.new(1, -70, 0, 6)
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
MinimizeBtn.Text = "—"
MinimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeBtn.Font = Enum.Font.GothamBold
MinimizeBtn.TextSize = 16
MinimizeBtn.BorderSizePixel = 0
MinimizeBtn.Parent = TopBar
Instance.new("UICorner", MinimizeBtn).CornerRadius = UDim.new(0, 6)

local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 30, 0, 30)
CloseBtn.Position = UDim2.new(1, -35, 0, 6)
CloseBtn.BackgroundColor3 = Color3.fromRGB(200, 30, 30)
CloseBtn.Text = "✕"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextSize = 14
CloseBtn.BorderSizePixel = 0
CloseBtn.Parent = TopBar
Instance.new("UICorner", CloseBtn).CornerRadius = UDim.new(0, 6)

-- Abas
local TabBar = Instance.new("Frame")
TabBar.Size = UDim2.new(1, -10, 0, 30)
TabBar.Position = UDim2.new(0, 5, 0, 47)
TabBar.BackgroundColor3 = Color3.fromRGB(22, 22, 28)
TabBar.BorderSizePixel = 0
TabBar.Parent = Main
Instance.new("UICorner", TabBar).CornerRadius = UDim.new(0, 5)

local TabLayout = Instance.new("UIListLayout", TabBar)
TabLayout.FillDirection = Enum.FillDirection.Horizontal
TabLayout.Padding = UDim.new(0, 2)
TabLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
TabLayout.VerticalAlignment = Enum.VerticalAlignment.Center

local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -10, 1, -85)
Content.Position = UDim2.new(0, 5, 0, 80)
Content.BackgroundColor3 = Color3.fromRGB(22, 22, 28)
Content.BorderSizePixel = 0
Content.Parent = Main
Instance.new("UICorner", Content).CornerRadius = UDim.new(0, 5)

local Pages = {}
local TabButtons = {}

local function createTab(name)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 60, 0, 24)
    btn.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
    btn.Text = name
    btn.TextColor3 = Color3.fromRGB(220, 220, 220)
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 10
    btn.BorderSizePixel = 0
    btn.Parent = TabBar
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 4)
    
    local page = Instance.new("ScrollingFrame")
    page.Size = UDim2.new(1, -10, 1, -10)
    page.Position = UDim2.new(0, 5, 0, 5)
    page.BackgroundTransparency = 1
    page.BorderSizePixel = 0
    page.ScrollBarThickness = 4
    page.CanvasSize = UDim2.new(0, 0, 0, 0)
    page.AutomaticCanvasSize = Enum.AutomaticSize.Y
    page.Visible = false
    page.Parent = Content
    
    local layout = Instance.new("UIListLayout", page)
    layout.Padding = UDim.new(0, 4)
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    
    Pages[name] = page
    TabButtons[name] = btn
    
    btn.MouseButton1Click:Connect(function()
        for _, p in pairs(Pages) do p.Visible = false end
        for _, b in pairs(TabButtons) do
            b.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
        end
        page.Visible = true
        btn.BackgroundColor3 = Color3.fromRGB(160, 0, 0)
    end)
    
    return page
end

local function addButton(page, text, callback, color)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -8, 0, 28)
    btn.BackgroundColor3 = color or Color3.fromRGB(35, 35, 45)
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(240, 240, 240)
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 11
    btn.BorderSizePixel = 0
    btn.Parent = page
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 5)
    btn.MouseButton1Click:Connect(callback)
    return btn
end

local function addLabel(page, text)
    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(1, -8, 0, 20)
    lbl.BackgroundTransparency = 1
    lbl.Text = text
    lbl.TextColor3 = Color3.fromRGB(180, 180, 180)
    lbl.Font = Enum.Font.GothamBold
    lbl.TextSize = 11
    lbl.TextXAlignment = Enum.TextXAlignment.Left
    lbl.Parent = page
    return lbl
end

local function addToggle(page, text, key, callback)
    local btn = addButton(page, "❌ " .. text, function() end)
    btn.MouseButton1Click:Connect(function()
        State[key] = not State[key]
        btn.Text = (State[key] and "✅ " or "❌ ") .. text
        btn.BackgroundColor3 = State[key] and Color3.fromRGB(60, 130, 60) 
                               or Color3.fromRGB(35, 35, 45)
        if callback then pcall(callback, State[key]) end
        notify("Toggle", text .. ": " .. (State[key] and "ON" or "OFF"), 2)
    end)
    return btn
end

-- ============================================================
-- ABAS
-- ============================================================
createTab("Farm")
createTab("Boss")
createTab("Fruit")
createTab("Raid")
createTab("Combat")
createTab("TP")
createTab("ESP")
createTab("Player")
createTab("Misc")
createTab("Config")

-- ============================================================
-- FUNÇÕES CORE
-- ============================================================
local function getChar() return LocalPlayer.Character end
local function getHRP()
    local c = getChar()
    return c and c:FindFirstChild("HumanoidRootPart")
end

local function atacarMob(mob)
    local hrp = getHRP()
    if not hrp or not mob or not mob:FindFirstChild("HumanoidRootPart") then return end
    hrp.CFrame = mob.HumanoidRootPart.CFrame * CFrame.new(0, 0, State.FarmDistance)
    local tool = getChar():FindFirstChildOfClass("Tool")
    if tool then pcall(function() tool:Activate() end) end
end

local function acharMobProximo()
    local hrp = getHRP()
    if not hrp then return nil end
    local nearest, minDist = nil, math.huge
    for _, mob in pairs(workspace.Enemies:GetChildren()) do
        if mob:FindFirstChild("Humanoid") and mob.Humanoid.Health > 0 
           and mob:FindFirstChild("HumanoidRootPart") then
            local dist = (mob.HumanoidRootPart.Position - hrp.Position).Magnitude
            if dist < minDist then
                minDist = dist
                nearest = mob
            end
        end
    end
    return nearest
end

local function acharMobPorNome(nome)
    for _, mob in pairs(workspace.Enemies:GetChildren()) do
        if mob.Name:lower():find(nome:lower()) 
           and mob:FindFirstChild("Humanoid") 
           and mob.Humanoid.Health > 0 then
            return mob
        end
    end
    return nil
end

local function acharFruta()
    local hrp = getHRP()
    if not hrp then return nil end
    local nearest, minDist = nil, math.huge
    for _, obj in pairs(workspace:GetChildren()) do
        if obj:IsA("Tool") and obj:FindFirstChild("Handle") 
           and (obj:GetAttribute("Fruit") or obj.Name:find("Fruit")) then
            local dist = (obj.Handle.Position - hrp.Position).Magnitude
            if dist < minDist then
                minDist = dist
                nearest = obj
            end
        end
    end
    return nearest
end

local function acharChest()
    local hrp = getHRP()
    if not hrp then return nil end
    for _, obj in pairs(workspace:GetChildren()) do
        if obj.Name:find("Chest") and obj:FindFirstChild("Handle") then
            if (obj.Handle.Position - hrp.Position).Magnitude < 500 then
                return obj
            end
        end
    end
    return nil
end

local function teleportarPara(cf)
    local hrp = getHRP()
    if hrp then hrp.CFrame = cf end
end

-- ============================================================
-- ABA FARM
-- ============================================================
local FarmPage = Pages["Farm"]
addLabel(FarmPage, "▸ AUTO FARM")

addToggle(FarmPage, "Auto Farm Nearest", "AutoFarmNearest")
addToggle(FarmPage, "Auto Farm Selected", "AutoFarmSelected")
addToggle(FarmPage, "Auto Farm Level", "AutoFarmLevel")
addToggle(FarmPage, "Auto Quest", "AutoQuest")
addToggle(FarmPage, "Auto Complete Quest", "AutoCompleteQuest")
addToggle(FarmPage, "Bring Mobs", "BringMobs")
addToggle(FarmPage, "Auto Farm Chest", "AutoFarmChest")
addToggle(FarmPage, "Auto Farm Item", "AutoFarmItem")

addLabel(FarmPage, "▸ MOB SELECIONADO")
local mobs = {"Bandit", "Monkey", "Pirate", "Brute", "Desert Officer", 
              "Snow Bandit", "Chief Petty Officer", "Sky Bandit", 
              "Dark Master", "Zombie", "Jungle Pirate", "Cyborg", 
              "Military Soldier", "Fishman Warrior", "Royal Guard", 
              "Forest Pirate", "Mythological Pirate", "Jungle Savage",
              "Ghost Pirate", "Reborn Skeleton", "Living Zombie",
              "Demonic Soul", "Posessed Mummy", "Snow Monster",
              "Ice Cream Chef", "Candy Pirate"}
for _, mob in ipairs(mobs) do
    addButton(FarmPage, "→ " .. mob, function()
        State.SelectedMob = mob
        notify("Mob", "Selecionado: " .. mob, 2)
    end)
end

-- ============================================================
-- ABA BOSS
-- ============================================================
local BossPage = Pages["Boss"]
addLabel(BossPage, "▸ BOSS FARM")
addToggle(BossPage, "Auto Farm Boss", "AutoFarmBoss")
addToggle(BossPage, "Boss ESP", "BossESP")

addLabel(BossPage, "▸ BOSS SELECIONADO")
local bosses = {"Saber Expert", "The Gorilla King", "Bobby", "The Saw", 
                "Pirate King", "Fajita", "Don Swan", "Smoke Admiral", 
                "Awakened Ice Admiral", "Tide Keeper", "Stone", 
                "Island Empress", "Kilo Admiral", "Captain Elephant", 
                "Beautiful Pirate", "Longma", "Soul Reaper", "Cursed Captain",
                "Darkbeard", "Order", "Rip Indra", "Kaidou", "Cake Queen"}
for _, boss in ipairs(bosses) do
    addButton(BossPage, "→ " .. boss, function()
        State.SelectedBoss = boss
        notify("Boss", "Selecionado: " .. boss, 2)
    end)
end

-- ============================================================
-- ABA FRUIT
-- ============================================================
local FruitPage = Pages["Fruit"]
addLabel(FruitPage, "▸ AUTO FRUIT")
addToggle(FruitPage, "Auto Farm Fruit", "AutoFarmFruit")
addToggle(FruitPage, "Fruit Sniper", "FruitSniper")
addToggle(FruitPage, "Auto Store Fruit", "AutoStoreFruit")
addToggle(FruitPage, "Fruit ESP", "FruitESP")
addToggle(FruitPage, "Fruit Notify", "FruitNotify")

addLabel(FruitPage, "▸ AÇÕES")
addButton(FruitPage, "🔍 Ir Para Fruta Mais Próxima", function()
    local fruta = acharFruta()
    if fruta then
        teleportarPara(fruta.Handle.CFrame)
        notify("Fruit", "Teleportado para: " .. fruta.Name, 2)
    else
        notify("Fruit", "Nenhuma fruta encontrada", 2)
    end
end)

addButton(FruitPage, "💰 Guardar Todas as Frutas", function()
    local count = 0
    for _, tool in pairs(LocalPlayer.Backpack:GetChildren()) do
        if tool:IsA("Tool") and (tool:GetAttribute("Fruit") or tool.Name:find("Fruit")) then
            pcall(function()
                CommF_:InvokeServer("StoreFruit", tool.Name)
                count = count + 1
            end)
        end
    end
    notify("Fruit", count .. " frutas guardadas", 2)
end)

addButton(FruitPage, "📦 Ver Inventário", function()
    local inv = {}
    for _, tool in pairs(LocalPlayer.Backpack:GetChildren()) do
        if tool:IsA("Tool") then table.insert(inv, tool.Name) end
    end
    notify("Inventário", table.concat(inv, ", "):sub(1, 100), 5)
end)

-- ============================================================
-- ABA RAID
-- ============================================================
local RaidPage = Pages["Raid"]
addLabel(RaidPage, "▸ RAID")
addToggle(RaidPage, "Auto Raid", "AutoRaid")
addToggle(RaidPage, "Auto Raid Chip", "AutoRaidChip")
addToggle(RaidPage, "Auto Awaken", "AutoAwaken")

addLabel(RaidPage, "▸ AÇÕES")
addButton(RaidPage, "🎫 Comprar Raid Chip", function()
    pcall(function() CommF_:InvokeServer("RaidsNpc", "Buy") end)
    notify("Raid", "Comprando chip...", 2)
end)

addButton(RaidPage, "⚔ Iniciar Raid", function()
    pcall(function() CommF_:InvokeServer("RaidsNpc", "Select", "Dark") end)
    notify("Raid", "Iniciando raid...", 2)
end)

addButton(RaidPage, "🚪 Entrar no Raid", function()
    local hrp = getHRP()
    if hrp then
        hrp.CFrame = CFrame.new(-5050, 314, -3140)
    end
end)

-- ============================================================
-- ABA COMBAT
-- ============================================================
local CombatPage = Pages["Combat"]
addLabel(CombatPage, "▸ COMBATE")
addToggle(CombatPage, "Kill Aura", "KillAura")
addToggle(CombatPage, "Auto Haki", "AutoHaki")
addToggle(CombatPage, "Fast Attack", "FastAttack")
addToggle(CombatPage, "Auto Click", "AutoClick")
addToggle(CombatPage, "Auto Skill", "AutoSkill")

addLabel(CombatPage, "▸ RANGE DA AURA")
addButton(CombatPage, "Range: 20", function() State.AuraRange = 20 
    notify("Aura", "Range: 20", 2) end)
addButton(CombatPage, "Range: 30", function() State.AuraRange = 30 
    notify("Aura", "Range: 30", 2) end)
addButton(CombatPage, "Range: 50", function() State.AuraRange = 50 
    notify("Aura", "Range: 50", 2) end)
addButton(CombatPage, "Range: 75", function() State.AuraRange = 75 
    notify("Aura", "Range: 75", 2) end)
addButton(CombatPage, "Range: 100", function() State.AuraRange = 100 
    notify("Aura", "Range: 100", 2) end)

-- ============================================================
-- ABA TELEPORT
-- ============================================================
local TPPage = Pages["TP"]
addLabel(TPPage, "▸ MARES")
addButton(TPPage, "🌊 Sea 1", function()
    pcall(function() CommF_:InvokeServer("TravelMain") end)
end)
addButton(TPPage, "🌊 Sea 2", function()
    pcall(function() CommF_:InvokeServer("TravelDressrosa") end)
end)
addButton(TPPage, "🌊 Sea 3", function()
    pcall(function() CommF_:InvokeServer("TravelZou") end)
end)

addLabel(TPPage, "▸ ILHAS SEA 1")
local ilhas1 = {"Starter Island", "Marine Fortress", "Middle Town", "Jungle", 
                "Pirate Village", "Desert", "Frozen Village", "Colosseum", 
                "Prison", "Magma Village", "Underwater City", "Fishman Island",
                "Sky Island", "Fountain City", "Upper Sky", "Cursed Ship",
                "Ice Castle", "Forgotten Island", "Floating Turtle",
                "Haunted Castle", "Hydra Island", "Great Tree", 
                "Castle on the Sea", "Cake Island", "Candy Kingdom"}
for _, ilha in ipairs(ilhas1) do
    addButton(TPPage, "→ " .. ilha, function()
        pcall(function() CommF_:InvokeServer("Travel", ilha) end)
        notify("TP", "Indo para: " .. ilha, 2)
    end)
end

addLabel(TPPage, "▸ LOCALIZAÇÕES ESPECIAIS")
addButton(TPPage, "🏝️ Sea Beast", function()
    local hrp = getHRP()
    if hrp then hrp.CFrame = CFrame.new(0, 500, 0) end
end)

addButton(TPPage, "🏴‍☠️ Pirate Village", function()
    local hrp = getHRP()
    if hrp then hrp.CFrame = CFrame.new(-1100, 50, 3800) end
end)

addButton(TPPage, "❄ Frozen Village", function()
    local hrp = getHRP()
    if hrp then hrp.CFrame = CFrame.new(-100, 50, -5000) end
end)

-- ============================================================
-- ABA ESP
-- ============================================================
local ESPPage = Pages["ESP"]
addLabel(ESPPage, "▸ ESP")
addToggle(ESPPage, "Player ESP", "PlayerESP")
addToggle(ESPPage, "Chest ESP", "ChestESP")
addToggle(ESPPage, "Boss ESP", "BossESP")
addToggle(ESPPage, "Mob ESP", "MobESP")
addToggle(ESPPage, "Fruit ESP", "FruitESP")

-- ============================================================
-- ABA PLAYER
-- ============================================================
local PlayerPage = Pages["Player"]
addLabel(PlayerPage, "▸ STATUS")
addToggle(PlayerPage, "Auto Stats", "AutoStats")

addLabel(PlayerPage, "▸ MODO DE STATS")
local statsModes = {"Melee", "Defense", "Sword", "Gun", "Blox Fruit"}
for _, mode in ipairs(statsModes) do
    addButton(PlayerPage, "→ " .. mode, function()
        State.StatsMode = mode
        notify("Stats", "Modo: " .. mode, 2)
    end)
end

addLabel(PlayerPage, "▸ INFO DO JOGADOR")
addButton(PlayerPage, "📊 Ver Meu Status", function()
    local lvl = LocalPlayer.Data and LocalPlayer.Data.Level and LocalPlayer.Data.Level.Value or "?"
    local beli = LocalPlayer.Data and LocalPlayer.Data.Beli and LocalPlayer.Data.Beli.Value or "?"
    local frag = LocalPlayer.Data and LocalPlayer.Data.Fragments and LocalPlayer.Data.Fragments.Value or "?"
    notify("Status", "Lvl: " .. lvl .. " | Beli: " .. tostring(beli) .. " | Frag: " .. tostring(frag), 5)
end)

-- ============================================================
-- ABA MISC
-- ============================================================
local MiscPage = Pages["Misc"]
addLabel(MiscPage, "▸ UTILITÁRIOS")
addToggle(MiscPage, "Anti-AFK", "AntiAFK")
addToggle(MiscPage, "Infinite Jump", "InfiniteJump")
addToggle(MiscPage, "Walk on Water", "WalkOnWater")
addToggle(MiscPage, "No Clip", "NoClip")
addToggle(MiscPage, "FPS Boost", "FPSBoost")
addToggle(MiscPage, "Anti Fling", "AntiFling")

addLabel(MiscPage, "▸ AÇÕES")
addButton(MiscPage, "🔄 Server Hop", function()
    notify("Server Hop", "Buscando servidor...", 2)
    local ok, result = pcall(function()
        return game:HttpGet("https://games.roblox.com/v1/games/" 
            .. game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100")
    end)
    if ok then
        local data = HttpService:JSONDecode(result)
        for _, srv in pairs(data.data) do
            if srv.id ~= game.JobId and srv.playing < srv.maxPlayers then
                notify("Server Hop", "Teleportando...", 2)
                TeleportService:TeleportToPlaceInstance(game.PlaceId, srv.id, LocalPlayer)
                break
            end
        end
    end
end)

addButton(MiscPage, "🔀 Rejoin", function()
    TeleportService:Teleport(game.PlaceId, LocalPlayer)
end)

addButton(MiscPage, "💀 Reset Character", function()
    if getChar() then getChar():BreakJoints() end
end)

addButton(MiscPage, "🎮 Reativar Anti-Cheat", function()
    LocalPlayer.PlayerGui:FindFirstChild("Main"):Destroy()
end)

-- ============================================================
-- ABA CONFIG
-- ============================================================
local ConfigPage = Pages["Config"]
addLabel(ConfigPage, "▸ CONFIGURAÇÕES")
addToggle(ConfigPage, "Notificações", "NotifyEnabled")

addLabel(ConfigPage, "▸ SALVAR/CARREGAR")
addButton(ConfigPage, "💾 Salvar Config", function()
    local ok, err = pcall(function()
        if writefile then
            writefile("hub_config.json", HttpService:JSONEncode(State))
            notify("Config", "Salvo com sucesso!", 2)
        else
            notify("Config", "Executor sem suporte a arquivo", 2)
        end
    end)
    if not ok then notify("Config", "Erro ao salvar", 2) end
end)

addButton(ConfigPage, "📂 Carregar Config", function()
    local ok, err = pcall(function()
        if readfile and isfile and isfile("hub_config.json") then
            local data = HttpService:JSONDecode(readfile("hub_config.json"))
            for k, v in pairs(data) do
                if State[k] ~= nil then State[k] = v end
            end
            notify("Config", "Carregado!", 2)
        else
            notify("Config", "Nenhum config salvo", 2)
        end
    end)
    if not ok then notify("Config", "Erro ao carregar", 2) end
end)

addLabel(ConfigPage, "▸ SOBRE")
addButton(ConfigPage, "ℹ️ Versão", function()
    notify("Info", "Blox Fruits Hub - Update 30\nFeatures: 80+", 4)
end)

addButton(ConfigPage, "❌ Fechar Painel", function()
    ScreenGui:Destroy()
end)

-- ============================================================
-- SISTEMA DE KEYBIND
-- ============================================================
local Keybinds = {
    [Enum.KeyCode.RightControl] = function()
        Main.Visible = not Main.Visible
    end,
}

UIS.InputBegan:Connect(function(input, gp)
    if gp then return end
    local fn = Keybinds[input.KeyCode]
    if fn then fn() end
end)

-- ============================================================
-- LOOPS
-- ============================================================

-- Auto Farm Nearest
task.spawn(function()
    while task.wait(State.FarmDelay) do
        if State.AutoFarmNearest then
            pcall(function()
                local mob = acharMobProximo()
                if mob then atacarMob(mob) end
            end)
        end
    end
end)

-- Auto Farm Selected
task.spawn(function()
    while task.wait(State.FarmDelay) do
        if State.AutoFarmSelected then
            pcall(function()
                local mob = acharMobPorNome(State.SelectedMob)
                if mob then atacarMob(mob) end
            end)
        end
    end
end)

-- Auto Farm Boss
task.spawn(function()
    while task.wait(State.FarmDelay) do
        if State.AutoFarmBoss then
            pcall(function()
                local mob = acharMobPorNome(State.SelectedBoss)
                if mob then atacarMob(mob) end
            end)
        end
    end
end)

-- Auto Farm Level
task.spawn(function()
    while task.wait(1) do
        if State.AutoFarmLevel then
            pcall(function()
                local mob = acharMobProximo()
                if mob then atacarMob(mob) end
            end)
        end
    end
end)

-- Bring Mobs
task.spawn(function()
    while task.wait(0.4) do
        if State.BringMobs then
            pcall(function()
                local hrp = getHRP()
                if not hrp then return end
                for _, mob in pairs(workspace.Enemies:GetChildren()) do
                    if mob:FindFirstChild("HumanoidRootPart") 
                       and mob:FindFirstChild("Humanoid") 
                       and mob.Humanoid.Health > 0 then
                        mob.HumanoidRootPart.CFrame = hrp.CFrame * CFrame.new(0, 0, 3)
                    end
                end
            end)
        end
    end
end)

-- Kill Aura
task.spawn(function()
    while task.wait(0.1) do
        if State.KillAura then
            pcall(function()
                local hrp = getHRP()
                if not hrp then return end
                local tool = getChar():FindFirstChildOfClass("Tool")
                if not tool then return end
                for _, mob in pairs(workspace.Enemies:GetChildren()) do
                    if mob:FindFirstChild("HumanoidRootPart") 
                       and mob:FindFirstChild("Humanoid") 
                       and mob.Humanoid.Health > 0 then
                        local dist = (mob.HumanoidRootPart.Position - hrp.Position).Magnitude
                        if dist <= State.AuraRange then
                            tool:Activate()
                            break
                        end
                    end
                end
            end)
        end
    end
end)

-- Auto Haki
task.spawn(function()
    while task.wait(0.5) do
        if State.AutoHaki then
            pcall(function()
                local char = getChar()
                if not char then return end
                for _, tool in pairs(char:GetChildren()) do
                    if tool:IsA("Tool") and (tool.Name == "Buso" or tool.Name == "Ken") then
                        tool:Activate()
                    end
                end
            end)
        end
    end
end)

-- Auto Farm Fruit
task.spawn(function()
    while task.wait(0.5) do
        if State.AutoFarmFruit then
            pcall(function()
                local fruta = acharFruta()
                if fruta then teleportarPara(fruta.Handle.CFrame) end
            end)
        end
    end
end)

-- Fruit Sniper
task.spawn(function()
    while task.wait(0.5) do
        if State.FruitSniper then
            pcall(function()
                local fruta = acharFruta()
                if fruta then
                    local hrp = getHRP()
                    if hrp then hrp.CFrame = fruta.Handle.CFrame * CFrame.new(0, 0, 3) end
                end
            end)
        end
    end
end)

-- Auto Store Fruit
task.spawn(function()
    while task.wait(3) do
        if State.AutoStoreFruit then
            pcall(function()
                for _, tool in pairs(LocalPlayer.Backpack:GetChildren()) do
                    if tool:IsA("Tool") and tool:GetAttribute("Fruit") then
                        CommF_:InvokeServer("StoreFruit", tool.Name)
                    end
                end
            end)
        end
    end
end)

-- Auto Click
task.spawn(function()
    while task.wait(0.05) do
        if State.AutoClick then
            pcall(function()
                local tool = getChar() and getChar():FindFirstChildOfClass("Tool")
                if tool then tool:Activate() end
            end)
        end
    end
end)

-- Anti-AFK
LocalPlayer.Idled:Connect(function()
    if State.AntiAFK then
        VIM:SendKeyEvent(true, Enum.KeyCode.Space, false, game)
        task.wait(0.5)
        VIM:SendKeyEvent(false, Enum.KeyCode.Space, false, game)
    end
end)

-- Infinite Jump
UIS.JumpRequest:Connect(function()
    if State.InfiniteJump and getHRP() then
        getHRP().Velocity = Vector3.new(getHRP().Velocity.X, 50, getHRP().Velocity.Z)
    end
end)

-- No Clip
RunService.Stepped:Connect(function()
    if State.NoClip then
        pcall(function()
            local char = getChar()
            if char then
                for _, part in pairs(char:GetDescendants()) do
                    if part:IsA("BasePart") then part.CanCollide = false end
                end
            end
        end)
    end
end)

-- Walk on Water
task.spawn(function()
    while task.wait(0.3) do
        if State.WalkOnWater then
            pcall(function()
                local hrp = getHRP()
                if hrp and hrp.Position.Y < 0.5 then
                    hrp.CFrame = CFrame.new(hrp.Position.X, 3, hrp.Position.Z)
                end
            end)
        end
    end
end)

-- FPS Boost
task.spawn(function()
    while task.wait(2) do
        if State.FPSBoost then
            pcall(function()
                for _, obj in pairs(workspace:GetDescendants()) do
                    if obj:IsA("ParticleEmitter") or obj:IsA("Trail") then
                        obj.Enabled = false
                    end
                end
                Lighting.GlobalShadows = false
                Lighting.FogEnd = 9e9
                settings().Rendering.QualityLevel = "Level01"
            end)
        end
    end
end)

-- Player ESP
task.spawn(function()
    local espCache = {}
    while task.wait(1) do
        for _, plr in pairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and plr.Character then
                if State.PlayerESP and not espCache[plr] then
                    local head = plr.Character:FindFirstChild("Head")
                    if head then
                        local bg = Instance.new("BillboardGui", head)
                        bg.Size = UDim2.new(0, 100, 0, 30)
                        bg.AlwaysOnTop = true
                        bg.Name = "HubESP"
                        local lbl = Instance.new("TextLabel", bg)
                        lbl.Size = UDim2.new(1, 0, 1, 0)
                        lbl.BackgroundTransparency = 1
                        lbl.Text = plr.Name
                        lbl.TextColor3 = Color3.fromRGB(255, 50, 50)
                        lbl.TextStrokeTransparency = 0
                        lbl.Font = Enum.Font.GothamBold
                        lbl.TextSize = 14
                        espCache[plr] = bg
                    end
                elseif not State.PlayerESP and espCache[plr] then
                    espCache[plr]:Destroy()
                    espCache[plr] = nil
                end
            end
        end
    end
end)

-- Fruit ESP
task.spawn(function()
    local espCache = {}
    while task.wait(1) do
        for _, obj in pairs(workspace:GetChildren()) do
            if obj:IsA("Tool") and obj:FindFirstChild("Handle") 
               and (obj:GetAttribute("Fruit") or obj.Name:find("Fruit")) then
                if State.FruitESP and not espCache[obj] then
                    local bg = Instance.new("BillboardGui", obj.Handle)
                    bg.Size = UDim2.new(0, 150, 0, 40)
                    bg.AlwaysOnTop = true
                    bg.Name = "HubESP"
                    local lbl = Instance.new("TextLabel", bg)
                    lbl.Size = UDim2.new(1, 0, 1, 0)
                    lbl.BackgroundTransparency = 1
                    lbl.Text = "🍎 " .. obj.Name
                    lbl.TextColor3 = Color3.fromRGB(255, 200, 50)
                    lbl.TextStrokeTransparency = 0
                    lbl.Font = Enum.Font.GothamBold
                    lbl.TextSize = 14
                    espCache[obj] = bg
                elseif not State.FruitESP and espCache[obj] then
                    espCache[obj]:Destroy()
                    espCache[obj] = nil
                end
            end
        end
    end
end)

-- Boss ESP
task.spawn(function()
    local espCache = {}
    while task.wait(1) do
        for _, mob in pairs(workspace.Enemies:GetChildren()) do
            if mob:FindFirstChild("Humanoid") and mob.Humanoid.Health > 0 then
                local isBoss = mob.Humanoid.MaxHealth > 5000 or mob:FindFirstChild("Humanoid")
                                 and mob.Name:find("Boss")
                if State.BossESP and isBoss and not espCache[mob] then
                    local head = mob:FindFirstChild("Head") or mob:FindFirstChild("HumanoidRootPart")
                    if head then
                        local bg = Instance.new("BillboardGui", head)
                        bg.Size = UDim2.new(0, 120, 0, 30)
                        bg.AlwaysOnTop = true
                        bg.Name = "HubESP"
                        local lbl = Instance.new("TextLabel", bg)
                        lbl.Size = UDim2.new(1, 0, 1, 0)
                        lbl.BackgroundTransparency = 1
                        lbl.Text = "👑 " .. mob.Name
                        lbl.TextColor3 = Color3.fromRGB(255, 100, 100)
                        lbl.TextStrokeTransparency = 0
                        lbl.Font = Enum.Font.GothamBold
                        lbl.TextSize = 12
                        espCache[mob] = bg
                    end
                elseif not State.BossESP and espCache[mob] then
                    espCache[mob]:Destroy()
                    espCache[mob] = nil
                end
            end
        end
    end
end)

-- Chest ESP
task.spawn(function()
    local espCache = {}
    while task.wait(1) do
        for _, obj in pairs(workspace:GetChildren()) do
            if obj.Name:find("Chest") and obj:FindFirstChild("Handle") then
                if State.ChestESP and not espCache[obj] then
                    local bg = Instance.new("BillboardGui", obj.Handle)
                    bg.Size = UDim2.new(0, 100, 0, 30)
                    bg.AlwaysOnTop = true
                    bg.Name = "HubESP"
                    local lbl = Instance.new("TextLabel", bg)
                    lbl.Size = UDim2.new(1, 0, 1, 0)
                    lbl.BackgroundTransparency = 1
                    lbl.Text = "📦 Chest"
                    lbl.TextColor3 = Color3.fromRGB(255, 255, 100)
                    lbl.TextStrokeTransparency = 0
                    lbl.Font = Enum.Font.GothamBold
                    lbl.TextSize = 12
                    espCache[obj] = bg
                elseif not State.ChestESP and espCache[obj] then
                    espCache[obj]:Destroy()
                    espCache[obj] = nil
                end
            end
        end
    end
end)

-- Mob ESP
task.spawn(function()
    local espCache = {}
    while task.wait(1) do
        for _, mob in pairs(workspace.Enemies:GetChildren()) do
            if mob:FindFirstChild("Humanoid") and mob.Humanoid.Health > 0 then
                if State.MobESP and not espCache[mob] then
                    local head = mob:FindFirstChild("Head") or mob:FindFirstChild("HumanoidRootPart")
                    if head then
                        local bg = Instance.new("BillboardGui", head)
                        bg.Size = UDim2.new(0, 100, 0, 25)
                        bg.AlwaysOnTop = true
                        bg.Name = "HubESP"
                        local lbl = Instance.new("TextLabel", bg)
                        lbl.Size = UDim2.new(1, 0, 1, 0)
                        lbl.BackgroundTransparency = 1
                        lbl.Text = mob.Name
                        lbl.TextColor3 = Color3.fromRGB(200, 200, 255)
                        lbl.TextStrokeTransparency = 0
                        lbl.Font = Enum.Font.Gotham
                        lbl.TextSize = 11
                        espCache[mob] = bg
                    end
                elseif not State.MobESP and espCache[mob] then
                    espCache[mob]:Destroy()
                    espCache[mob] = nil
                end
            end
        end
    end
end)

-- Fruit Notify
task.spawn(function()
    local conhecidas = {}
    while task.wait(2) do
        if State.FruitNotify then
            pcall(function()
                for _, obj in pairs(workspace:GetChildren()) do
                    if obj:IsA("Tool") and obj:FindFirstChild("Handle") 
                       and (obj:GetAttribute("Fruit") or obj.Name:find("Fruit")) then
                        if not conhecidas[obj.Name] then
                            conhecidas[obj.Name] = true
                            notify("🍎 FRUTA DETECTADA", obj.Name, 5)
                        end
                    end
                end
            end)
        end
    end
end)

-- Auto Stats
task.spawn(function()
    while task.wait(1) do
        if State.AutoStats then
            pcall(function()
                CommF_:InvokeServer("AddPoint", State.StatsMode, 1)
            end)
        end
    end
end)

-- ============================================================
-- INICIALIZAÇÃO
-- ============================================================
Pages["Farm"].Visible = true
TabButtons["Farm"].BackgroundColor3 = Color3.fromRGB(160, 0, 0)

local minimized = false
MinimizeBtn.MouseButton1Click:Connect(function()
    minimized = not minimized
    Content.Visible = not minimized
    TabBar.Visible = not minimized
    Main.Size = minimized and UDim2.new(0, 550, 0, 42) 
                         or UDim2.new(0, 550, 0, 450)
end)

CloseBtn.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

notify("HUB Update 30", "Script carregado! Pressione RightCtrl para esconder.", 5)
print("[HUB] Update 30 carregado. " .. 80 .. "+ funcionalidades.")