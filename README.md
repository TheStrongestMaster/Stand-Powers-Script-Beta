local DrRayLibrary = loadstring(game:HttpGet("https://raw.githubusercontent.com/AZYsGithub/DrRay-UI-Library/main/DrRay.lua"))()
local player = game.Players.LocalPlayer
local Workspace = game:GetService("Workspace")

local window = DrRayLibrary:Load("TheStrongestMaster Scripts", "Default")

-- Função para teleportar o jogador usando CFrame
local function teleportTo(position)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        player.Character.HumanoidRootPart.CFrame = CFrame.new(position)
    end
end

-- Função para localizar e teleportar para objetos
local function teleportToClosestObject(objectName)
    local closestObject = nil
    local closestDistance = math.huge
    local playerPosition = player.Character.HumanoidRootPart.Position

    for _, obj in pairs(Workspace:GetDescendants()) do
        if obj:IsA("MeshPart") and obj.Parent and obj.Parent.Name == objectName then
            local distance = (obj.Position - playerPosition).Magnitude
            if distance < closestDistance then
                closestDistance = distance
                closestObject = obj
            end
        end
    end

    if closestObject then
        teleportTo(closestObject.Position)
    else
        warn("Nenhum " .. objectName .. " encontrado!")
    end
end

-- Função para adicionar ESP em objetos
local function addESP(objectName, displayName, textColor)
    for _, obj in ipairs(Workspace:GetDescendants()) do
        if obj:IsA('MeshPart') and obj.Parent and obj.Parent.Name == objectName and not obj.Parent:FindFirstChild("BillboardGui") then
            local BillboardGui = Instance.new('BillboardGui', obj.Parent)
            BillboardGui.AlwaysOnTop = true
            BillboardGui.Size = UDim2.new(0, 50, 0, 50)
            BillboardGui.StudsOffset = Vector3.new(0, 2, 0)

            local TextLabel = Instance.new('TextLabel', BillboardGui)
            TextLabel.Text = displayName
            TextLabel.Size = UDim2.new(1, 0, 1, 0)
            TextLabel.BackgroundTransparency = 1
            TextLabel.TextColor3 = textColor
            TextLabel.TextScaled = true
        end
    end
end

-- Aba ESP
local ESPTab = DrRayLibrary.newTab("ESP", "ImageIdHere")

ESPTab.newButton("ESP Locacaca Fruta", "Adiciona ESP para Locacaca Fruit", function()
    addESP("Locacaca Fruit", "Locacaca Fruit", Color3.new(1, 0, 0))
end)

ESPTab.newButton("ESP Flecha", "Adiciona ESP para Flechas", function()
    addESP("Arrow", "Flecha", Color3.new(1, 1, 0))
end)

ESPTab.newButton("Desativar todas", "Remove todos os ESPs", function()
    for _, obj in ipairs(Workspace:GetDescendants()) do
        if obj:FindFirstChild("BillboardGui") then
            obj.BillboardGui:Destroy()
        end
    end
end)

-- Aba Teleporte
local TeleportTab = DrRayLibrary.newTab("Teleport", "ImageIdHere")

TeleportTab.newButton("Teleportar para Fruta", "Teleporta para Locacaca Fruit mais próxima", function()
    teleportToClosestObject("Locacaca Fruit")
end)

TeleportTab.newButton("Teleportar para Flecha", "Teleporta para a Flecha mais próxima", function()
    teleportToClosestObject("Arrow")
end)

TeleportTab.newButton("Teleportar para Pilar Man", "Teleporta para Pilar Man", function()
    teleportTo(Vector3.new(-210.0548858642578, 141.8389129638672, 1180.2388916015625)) -- Usando CFrame
end)

TeleportTab.newButton("Teleportar para Loja Mr Monster", "Teleporta para a Loja Mr Monster", function()
    teleportTo(Vector3.new(596.81884765625, 137.6195526123047, -382.5865478515625)) -- Usando CFrame
end)

TeleportTab.newButton("Teleportar para Correio", "Teleporta para o Correio", function()
    teleportTo(Vector3.new(-249.5177001953125, 863.7474975585938, -1233.9884033203125)) -- Usando CFrame
end)

TeleportTab.newButton("Teleportar para Banco", "Teleporta para o Banco", function()
    teleportTo(Vector3.new(-391.6630554199219, 136.99501037597656, 160.79986572265625)) -- Usando CFrame
end)

TeleportTab.newButton("Teleportar para Praia", "Teleporta para a Praia", function()
    teleportTo(Vector3.new(-577.1709594726562, 137.1058349609375, -26.43917465209961)) -- Usando CFrame
end)

TeleportTab.newButton("Teleportar para Arcade", "Teleporta para o Arcade", function()
    teleportTo(Vector3.new(-113.06327056884766, 138.19393920898438, 48.84617614746094)) -- Usando CFrame
end)

TeleportTab.newButton("Remover Tempo de Espera", "Remove o tempo de espera de flechas, frutas e etc", function()
    local function removeHoldDuration(prompt)
        if prompt:IsA("ProximityPrompt") and not prompt:GetAttribute("Optimized") then
            prompt.HoldDuration = 0
            prompt:SetAttribute("Optimized", true)
        end
    end

    local function scanAndOptimize(folder)
        for _, descendant in ipairs(folder:GetDescendants()) do
            removeHoldDuration(descendant)
        end
    end

    -- Primeira execução
    scanAndOptimize(Workspace)

    -- Monitora o jogo para novos prompts
    Workspace.DescendantAdded:Connect(function(descendant)
        removeHoldDuration(descendant)
    end)
end)

-- Inicialização da interface
window:Ready()
