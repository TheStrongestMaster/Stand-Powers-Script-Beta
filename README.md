local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

local player = game.Players.LocalPlayer
local Workspace = game:GetService("Workspace")

-- Janela principal
local Window = OrionLib:MakeWindow({
    Name = "TheStrongestMaster Scripts",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "OrionTest"
})

-- Notificação de boas-vindas
OrionLib:MakeNotification({
    Name = "Welcome!",
    Content = "Welcome to my hub!",
    Image = "rbxassetid://4483345998",
    Time = 5
})

-- Função para teleportar o jogador
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
        OrionLib:MakeNotification({
            Name = "Aviso",
            Content = "Nenhum " .. objectName .. " encontrado!",
            Image = "rbxassetid://4483345998",
            Time = 5
        })
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
local ESPTab = Window:MakeTab({
    Name = "Esp",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

ESPTab:AddButton({
    Name = "ESP Locacaca Fruta",
    Callback = function()
        addESP("Locacaca Fruit", "Locacaca Fruit", Color3.new(1, 0, 0))
    end
})

ESPTab:AddButton({
    Name = "ESP Flecha",
    Callback = function()
        addESP("Arrow", "Flecha", Color3.new(1, 1, 0))
    end
})

ESPTab:AddButton({
    Name = "Desativar todas",
    Callback = function()
        for _, obj in ipairs(Workspace:GetDescendants()) do
            if obj:FindFirstChild("BillboardGui") then
                obj.BillboardGui:Destroy()
            end
        end
    end
})

-- Aba Teleporte
local TeleportTab = Window:MakeTab({
    Name = "Teleport",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

TeleportTab:AddButton({
    Name = "Teleportar para Fruta",
    Callback = function()
        teleportToClosestObject("Locacaca Fruit")
    end
})

TeleportTab:AddButton({
    Name = "Teleportar para Flecha",
    Callback = function()
        teleportToClosestObject("Arrow")
    end
})

TeleportTab:AddButton({
    Name = "Teleportar para Banco",
    Callback = function()
        teleportTo(Vector3.new(-391.6630554199219, 136.99501037597656, 160.79986572265625))
    end
})

TeleportTab:AddButton({
    Name = "Teleportar para Praia",
    Callback = function()
        teleportTo(Vector3.new(-577.1709594726562, 137.1058349609375, -26.43917465209961))
    end
})

TeleportTab:AddButton({
    Name = "Teleportar para Arcade",
    Callback = function()
        teleportTo(Vector3.new(-113.06327056884766, 138.19393920898438, 48.84617614746094))
    end
})

-- Inicializando a interface
OrionLib:Init()
