fez tudo com ia
Maya deobfucator killer achou que o obsfucator dele era baum



if not game then return end

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")
local player = Players.LocalPlayer

local EggState, AreasData, RarityData, AssetsData, PetsData
pcall(function() EggState = require(ReplicatedStorage.Client.EggState) end)
pcall(function() AreasData = require(ReplicatedStorage.Data.Areas) end)
pcall(function() RarityData = require(ReplicatedStorage.Data.Rarity) end)
pcall(function() AssetsData = require(ReplicatedStorage.Data.Assets) end)
pcall(function() PetsData = require(ReplicatedStorage.Data.Pets) end)

local RARITY_SCORE_MAP = {
    ["Light & Dark"]    = 1300, ["Titan"]           = 1100,
    ["Divine"]          = 1000, ["Transcendent"]    = 1000,
    ["Superior"]        = 1000, ["Eternal"]         = 900,
    ["Limited"]         = 900,  ["Secret"]          = 800,
    ["Exotic"]          = 800,  ["Cosmic"]          = 700,
    ["Exclusive"]       = 700,  ["Admin"]           = 700,
    ["Mythic"]          = 600,  ["Mythical"]        = 600,
    ["Prismatic"]       = 600,  ["Rainbow"]         = 600,
    ["Squishy God"]     = 600,  ["BrainrotGod"]     = 600,
    ["Legendary"]       = 500,  ["Epic"]            = 400,
    ["Rare"]            = 300,  ["SuperRare"]       = 200,
    ["Celestial"]       = 200,  ["Uncommon"]        = 200,
    ["Basic"]           = 100,  ["Common"]          = 100,
}

local preservar = {
    "killerhub", "killer", "delta", "executor", "fluxus", 
    "arceus", "codex", "roblox", "chat", "core", "prompt", "interact", 
    "hold", "press", "action", "hud", "inventory", "item", "pickup",
    "proximity", "dialog", "bar", "health", "stamina", "touch"
}

local termosHubs = {
    "miranda", "foxname", "orion", "rayfield", "kavo", "fluent", 
    "windui", "venom", "loader", "uilib", "library"
}

local function devePreservar(nome)
    local n = nome:lower()
    for _, termo in ipairs(preservar) do
        if n:find(termo) then return true end
    end
    return false
end

local function ehHubSecundario(nome)
    local n = nome:lower()
    for _, termo in ipairs(termosHubs) do
        if n:find(termo) then return true end
    end
    return false
end

local function esconderOuDestruirUI(parent)
    if not parent then return end
    for _, gui in ipairs(parent:GetChildren()) do
        if gui:IsA("ScreenGui") then
            local nome = gui.Name
            if not devePreservar(nome) and ehHubSecundario(nome) then
                pcall(function()
                    gui.Enabled = false
                    gui:Destroy()
                end)
            end
        end
    end
end

task.spawn(function()
    while task.wait(0.5) do
        pcall(function()
            local pGui = player:FindFirstChild("PlayerGui")
            if pGui then esconderOuDestruirUI(pGui) end
            local hui = (gethui and gethui()) or game:GetService("CoreGui")
            if hui then esconderOuDestruirUI(hui) end
        end)
    end
end)

task.spawn(function()
    pcall(function()
        
    end)
end)

local TEMA = {
    fundo      = Color3.fromRGB(15, 15, 20),
    painel     = Color3.fromRGB(25, 25, 35),
    destaque   = Color3.fromRGB(46, 204, 113),
    texto      = Color3.fromRGB(240, 240, 245),
    textoFraco = Color3.fromRGB(150, 150, 160),
    verde      = Color3.fromRGB(50, 220, 100),
    vermelho   = Color3.fromRGB(231, 76, 60),
    borda      = Color3.fromRGB(45, 45, 60),
}

local espOvosAtivo = false
local maxEspDistance = 1000
local targetRarityName = "Todos" -- Filtro exato por nome

local SG = Instance.new("ScreenGui")
SG.Name = "KillerHubV1"
SG.ResetOnSpawn = false
SG.IgnoreGuiInset = true
SG.DisplayOrder = 999999999
SG.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
SG.Parent = (gethui and gethui()) or player:WaitForChild("PlayerGui")

local Main = Instance.new("Frame")
Main.Size = UDim2.new(0, 290, 0, 350)
Main.Position = UDim2.new(0.5, -145, 0.5, -175)
Main.BackgroundColor3 = TEMA.fundo
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
Main.Visible = false
Main.ZIndex = 10
Main.Parent = SG

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 12)
MainCorner.Parent = Main

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = TEMA.borda
MainStroke.Thickness = 1.5
MainStroke.Parent = Main

local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 50)
Header.BackgroundColor3 = TEMA.painel
Header.BorderSizePixel = 0
Header.Parent = Main

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 12)
HeaderCorner.Parent = Header

local LinhaDecor = Instance.new("Frame")
LinhaDecor.Size = UDim2.new(0, 4, 0, 30)
LinhaDecor.Position = UDim2.new(0, 12, 0.5, -15)
LinhaDecor.BackgroundColor3 = TEMA.destaque
LinhaDecor.BorderSizePixel = 0
LinhaDecor.Parent = Header

local Logo = Instance.new("TextLabel")
Logo.Size = UDim2.new(0, 180, 0, 20)
Logo.Position = UDim2.new(0, 24, 0, 8)
Logo.BackgroundTransparency = 1
Logo.Text = "KILLER HUB"
Logo.TextColor3 = TEMA.texto
Logo.Font = Enum.Font.GothamBlack
Logo.TextSize = 16
Logo.TextXAlignment = Enum.TextXAlignment.Left
Logo.Parent = Header

local Versao = Instance.new("TextLabel")
Versao.Size = UDim2.new(0, 180, 0, 15)
Versao.Position = UDim2.new(0, 25, 0, 26)
Versao.BackgroundTransparency = 1
Versao.Text = "By KILLER | ESP"
Versao.TextColor3 = TEMA.textoFraco
Versao.Font = Enum.Font.Gotham
Versao.TextSize = 10
Versao.TextXAlignment = Enum.TextXAlignment.Left
Versao.Parent = Header

local BtnMin = Instance.new("TextButton")
BtnMin.Size = UDim2.new(0, 30, 0, 30)
BtnMin.Position = UDim2.new(1, -38, 0, 10)
BtnMin.BackgroundColor3 = TEMA.fundo
BtnMin.Text = "—"
BtnMin.TextColor3 = TEMA.texto
BtnMin.Font = Enum.Font.GothamBold
BtnMin.TextSize = 16
BtnMin.Parent = Header

local BtnMinCorner = Instance.new("UICorner")
BtnMinCorner.CornerRadius = UDim.new(0, 6)
BtnMinCorner.Parent = BtnMin

local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -20, 1, -65)
Content.Position = UDim2.new(0, 10, 0, 60)
Content.BackgroundTransparency = 1
Content.Parent = Main

local UIList = Instance.new("UIListLayout")
UIList.SortOrder = Enum.SortOrder.LayoutOrder
UIList.Padding = UDim.new(0, 8)
UIList.Parent = Content

local SecESP = Instance.new("TextLabel")
SecESP.Size = UDim2.new(1, 0, 0, 20)
SecESP.BackgroundTransparency = 1
SecESP.Text = "— CONFIGURAÇÕES DE ESP —"
SecESP.TextColor3 = TEMA.destaque
SecESP.Font = Enum.Font.GothamBold
SecESP.TextSize = 11
SecESP.Parent = Content

local BtnToggleESP = Instance.new("TextButton")
BtnToggleESP.Size = UDim2.new(1, 0, 0, 36)
BtnToggleESP.BackgroundColor3 = TEMA.painel
BtnToggleESP.Text = "ESP Ovos: OFF"
BtnToggleESP.TextColor3 = TEMA.vermelho
BtnToggleESP.Font = Enum.Font.GothamBold
BtnToggleESP.TextSize = 12
BtnToggleESP.Parent = Content

local BtnToggleESPCorner = Instance.new("UICorner")
BtnToggleESPCorner.CornerRadius = UDim.new(0, 6)
BtnToggleESPCorner.Parent = BtnToggleESP

BtnToggleESP.MouseButton1Click:Connect(function()
    espOvosAtivo = not espOvosAtivo
    BtnToggleESP.Text = "ESP Ovos: " .. (espOvosAtivo and "ON" or "OFF")
    BtnToggleESP.TextColor3 = espOvosAtivo and TEMA.verde or TEMA.vermelho
end)

local niveisFiltro = {
    "Todos",
    "Common",
    "Uncommon",
    "Rare",
    "Epic",
    "Legendary",
    "Mythic",
    "Cosmic",
    "Secret",
    "Eternal",
    "Divine"
}
local idxFiltro = 1

local BtnFiltro = Instance.new("TextButton")
BtnFiltro.Size = UDim2.new(1, 0, 0, 36)
BtnFiltro.BackgroundColor3 = TEMA.painel
BtnFiltro.Text = "Filtro Raridades: Todos"
BtnFiltro.TextColor3 = TEMA.texto
BtnFiltro.Font = Enum.Font.GothamBold
BtnFiltro.TextSize = 12
BtnFiltro.Parent = Content

local BtnFiltroCorner = Instance.new("UICorner")
BtnFiltroCorner.CornerRadius = UDim.new(0, 6)
BtnFiltroCorner.Parent = BtnFiltro

BtnFiltro.MouseButton1Click:Connect(function()
    idxFiltro = idxFiltro + 1
    if idxFiltro > #niveisFiltro then idxFiltro = 1 end
    targetRarityName = niveisFiltro[idxFiltro]
    BtnFiltro.Text = "Filtro Raridade: " .. targetRarityName
end)

local DistLabel = Instance.new("TextLabel")
DistLabel.Size = UDim2.new(1, 0, 0, 20)
DistLabel.BackgroundTransparency = 1
DistLabel.Text = "Distância Máxima do ESP:"
DistLabel.TextColor3 = TEMA.textoFraco
DistLabel.Font = Enum.Font.Gotham
DistLabel.TextSize = 11
DistLabel.Parent = Content

local DistInput = Instance.new("TextBox")
DistInput.Size = UDim2.new(1, 0, 0, 36)
DistInput.BackgroundColor3 = TEMA.painel
DistInput.TextColor3 = TEMA.texto
DistInput.Font = Enum.Font.GothamBold
DistInput.TextSize = 14
DistInput.Text = tostring(maxEspDistance)
DistInput.PlaceholderText = "Ex: 1000"
DistInput.Parent = Content

local DistInputCorner = Instance.new("UICorner")
DistInputCorner.CornerRadius = UDim.new(0, 6)
DistInputCorner.Parent = DistInput

DistInput.FocusLost:Connect(function()
    local valor = tonumber(DistInput.Text)
    if valor and valor > 0 then
        maxEspDistance = valor
    else
        DistInput.Text = tostring(maxEspDistance)
    end
end)

local BtnFloat = Instance.new("TextButton")
BtnFloat.Size = UDim2.new(0, 55, 0, 55)
BtnFloat.Position = UDim2.new(0, 15, 0.5, -27)
BtnFloat.BackgroundColor3 = TEMA.destaque
BtnFloat.Text = "K"
BtnFloat.TextColor3 = TEMA.texto
BtnFloat.Font = Enum.Font.GothamBlack
BtnFloat.TextSize = 22
BtnFloat.ZIndex = 10
BtnFloat.Parent = SG

local BtnFloatCorner = Instance.new("UICorner")
BtnFloatCorner.CornerRadius = UDim.new(0, 30)
BtnFloatCorner.Parent = BtnFloat

local BtnFloatStroke = Instance.new("UIStroke")
BtnFloatStroke.Color = Color3.fromRGB(255, 255, 255)
BtnFloatStroke.Thickness = 2
BtnFloatStroke.Transparency = 0.5
BtnFloatStroke.Parent = BtnFloat

local dragando = false
local movendo = false
local dragStart = nil
local startPos = nil

BtnFloat.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragando = true
        movendo = false
        dragStart = input.Position
        startPos = BtnFloat.Position
    end
end)

BtnFloat.InputChanged:Connect(function(input)
    if dragando and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        if delta.Magnitude > 6 then movendo = true end
        if movendo then
            BtnFloat.Position = UDim2.new(
                startPos.X.Scale, startPos.X.Offset + delta.X,
                startPos.Y.Scale, startPos.Y.Offset + delta.Y
            )
        end
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragando = false
    end
end)

local function abrir()
    BtnFloat.Visible = false
    Main.Visible = true
end

local function fechar()
    Main.Visible = false
    BtnFloat.Visible = true
end

BtnFloat.MouseButton1Click:Connect(function()
    if not movendo then abrir() end
end)
BtnMin.MouseButton1Click:Connect(fechar)

local function GetEggRarityInfo(egg)
    if not egg then return "Common", 100 end

    if egg.Rarity then
        local r = egg.Rarity
        local name = type(r) == "table" and (r.DisplayName or r._id or r.Name) or tostring(r)
        return name, RARITY_SCORE_MAP[name] or 100
    end

    local cat = egg.AssetCategory or egg.Category or egg.Name
    if cat and AssetsData then
        local aInfo = (AssetsData.Directory or AssetsData)[cat]
        if aInfo and aInfo.Rarity then
            local r = aInfo.Rarity
            local name = type(r) == "table" and (r.DisplayName or r._id or r.Name) or tostring(r)
            return name, RARITY_SCORE_MAP[name] or 100
        end
    end

    local areaData = AreasData and (AreasData.Directory or AreasData) and (AreasData.Directory or AreasData)[egg.AreaId]
    local rarity = areaData and areaData.Rarity
    local rarityId = (type(rarity) == "table" and (rarity._id or rarity.DisplayName or rarity.Name)) or (type(rarity) == "string" and rarity) or "Common"
    local rInfo = (RarityData and (RarityData.Rarities or RarityData) or {})[rarityId] or {}
    local rarityDisplayName = (type(rInfo) == "table" and (rInfo.DisplayName or rInfo._id)) or (type(rarity) == "table" and rarity.DisplayName) or rarityId or "Common"
    
    return rarityDisplayName, RARITY_SCORE_MAP[rarityDisplayName] or 100
end

local function GetPetIcon(record)
    if not record then return nil end

    local rawIcon = record.Icon or record.PetIcon or record.ImageAsset or record.TextureId
    if rawIcon then
        return (type(rawIcon) == "number" or not string.match(tostring(rawIcon), "://")) and ("rbxassetid://" .. tostring(rawIcon)) or tostring(rawIcon)
    end

    local targetName = record.Pet or record.PetId or record.PetName or record.AssetCategory or record.Category
    if targetName then
        if PetsData then
            local pInfo = (PetsData.Directory or PetsData)[targetName]
            if pInfo and (pInfo.Icon or pInfo.Image or pInfo.AssetId) then
                local img = pInfo.Icon or pInfo.Image or pInfo.AssetId
                return (type(img) == "number" or not string.match(tostring(img), "://")) and ("rbxassetid://" .. tostring(img)) or tostring(img)
            end
        end

        if AssetsData then
            local aInfo = (AssetsData.Directory or AssetsData)[targetName]
            if aInfo and (aInfo.Icon or aInfo.Image or aInfo.AssetId) then
                local img = aInfo.Icon or aInfo.Image or aInfo.AssetId
                return (type(img) == "number" or not string.match(tostring(img), "://")) and ("rbxassetid://" .. tostring(img)) or tostring(img)
            end
        end
    end
    return nil
end

local espFolder = Instance.new("Folder")
espFolder.Name = "KILLER_HUB_ESP_STORAGE"
espFolder.Parent = Workspace

local activeEggESP = {}

local function limparObjetoESP(tbl, id)
    if tbl[id] then
        pcall(function()
            if tbl[id].gui then tbl[id].gui:Destroy() end
        end)
        tbl[id] = nil
    end
end

local function limparTudoESP(tbl)
    for id in pairs(tbl) do
        limparObjetoESP(tbl, id)
    end
end

task.spawn(function()
    while task.wait(0.2) do
        pcall(function()
            local char = player.Character
            local hrp = char and char:FindFirstChild("HumanoidRootPart")
            local myPos = hrp and hrp.Position or Vector3.zero

            if espOvosAtivo and EggState and EggState.ReadFieldEggs then
                local ok, snapshot = pcall(EggState.ReadFieldEggs)
                if ok and snapshot and snapshot.Records then
                    local currentUids = {}

                    for _, record in ipairs(snapshot.Records) do
                        if record.State == "Slot" and record.BoundsCFrame then
                            local eggPos = record.BoundsCFrame.Position
                            local dist = math.floor((eggPos - myPos).Magnitude)
                            
                            
                            if dist <= maxEspDistance then
                                local rarityName, _ = GetEggRarityInfo(record)
                                
                               
                                if targetRarityName == "Todos" or (rarityName:lower() == targetRarityName:lower()) then
                                    local uid = record.Uid or tostring(record.BoundsCFrame)
                                    currentUids[uid] = true

                                    if not activeEggESP[uid] then
                                        local bb = Instance.new("BillboardGui")
                                        bb.Name = "ESP_EGG_" .. uid
                                        bb.AlwaysOnTop = true
                                        bb.Size = UDim2.fromOffset(140, 80)
                                        bb.StudsOffset = Vector3.new(0, 3, 0)

                                        local container = Instance.new("Frame")
                                        container.Size = UDim2.fromScale(1, 1)
                                        container.BackgroundTransparency = 1
                                        container.Parent = bb

                                        local layout = Instance.new("UIListLayout")
                                        layout.SortOrder = Enum.SortOrder.LayoutOrder
                                        layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
                                        layout.VerticalAlignment = Enum.VerticalAlignment.Center
                                        layout.Padding = UDim.new(0, 2)
                                        layout.Parent = container

                                        local petImage = Instance.new("ImageLabel")
                                        petImage.Name = "PetIcon"
                                        petImage.Size = UDim2.fromOffset(36, 36)
                                        petImage.BackgroundTransparency = 1
                                        petImage.ScaleType = Enum.ScaleType.Fit
                                        petImage.LayoutOrder = 1
                                        petImage.Parent = container

                                        local textLabel = Instance.new("TextLabel")
                                        textLabel.Name = "EggText"
                                        textLabel.Size = UDim2.new(1, 0, 0, 30)
                                        textLabel.BackgroundTransparency = 1
                                        textLabel.Font = Enum.Font.GothamBold
                                        textLabel.TextSize = 12
                                        textLabel.TextColor3 = Color3.fromRGB(0, 255, 0) 
                                        textLabel.TextStrokeTransparency = 0.2
                                        textLabel.LayoutOrder = 2
                                        textLabel.Parent = container

                                        bb.Parent = espFolder
                                        activeEggESP[uid] = { gui = bb, label = textLabel, image = petImage }
                                    end

                                    local espItem = activeEggESP[uid]
                                    if espItem then
                                        espItem.gui.StudsOffsetWorldSpace = eggPos + Vector3.new(0, 2.5, 0)
                                        espItem.label.Text = string.format("%s\n[%s] - %dm", record.AssetCategory or "Ovo", rarityName, dist)

                                        local iconAsset = GetPetIcon(record)
                                        if iconAsset then
                                            espItem.image.Image = iconAsset
                                            espItem.image.Visible = true
                                        else
                                            espItem.image.Visible = false
                                        end
                                    end
                                end
                            end
                        end
                    end

                    
                    for uid in pairs(activeEggESP) do
                        if not currentUids[uid] then
                            limparObjetoESP(activeEggESP, uid)
                        end
                    end
                end
            else
                limparTudoESP(activeEggESP)
            end
        end)
    end
end)

task.wait(1)
abrir()
print("✅ KILLER HUB ESP EXECUTADO")
