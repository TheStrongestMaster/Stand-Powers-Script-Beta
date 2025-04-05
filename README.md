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

-- Função para localizar e teleportar para objetos; se não encontrar, notifica o usuário
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
    game.StarterGui:SetCore("SendNotification", {  
        Title = "Erro",  
        Text = "Nenhum " .. objectName .. " encontrado!",  
        Icon = "rbxassetid://4483345998",  
        Duration = 5  
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
local ESPTab = DrRayLibrary.newTab("ESP", "ImageIdHere")

-- ESP para itens não-Saint
ESPTab.newButton("ESP Locacaca Fruit", "Adiciona ESP para Locacaca Fruit", function()
addESP("Locacaca Fruit", "Locacaca Fruit", Color3.new(1, 0, 0))  -- Vermelho
end)

ESPTab.newButton("ESP Flecha", "Adiciona ESP para Flechas", function()
addESP("Arrow", "Flecha", Color3.new(1, 1, 0))  -- Amarelo
end)

ESPTab.newButton("ESP Requiem Arrow", "Adiciona ESP para Requiem Arrow", function()
addESP("Requiem Arrow", "Requiem Arrow", Color3.fromRGB(128, 0, 128))  -- Roxa
end)

ESPTab.newButton("ESP New Locacaca", "Adiciona ESP para New Locacaca", function()
addESP("New Locacaca", "New Locacaca", Color3.new(0, 1, 0))  -- Verde (exemplo)
end)

-- ESP para itens do Saint (todos com cor azul)
local saintColor = Color3.new(0, 0, 1)  -- Azul
ESPTab.newButton("ESP Heart of the Saint", "Adiciona ESP para Heart of the Saint", function()
addESP("Heart of the Saint", "Heart of the Saint", saintColor)
end)
ESPTab.newButton("ESP Right Leg of the Saint", "Adiciona ESP para Right Leg of the Saint", function()
addESP("Right Leg of the Saint", "Right Leg of the Saint", saintColor)
end)
ESPTab.newButton("ESP Left Eye of the Saint", "Adiciona ESP para Left Eye of the Saint", function()
addESP("Left Eye of the Saint", "Left Eye of the Saint", saintColor)
end)
ESPTab.newButton("ESP Right Eye of the Saint", "Adiciona ESP para Right Eye of the Saint", function()
addESP("Right Eye of the Saint", "Right Eye of the Saint", saintColor)
end)
ESPTab.newButton("ESP Skull of the Saint", "Adiciona ESP para Skull of the Saint", function()
addESP("Skull of the Saint", "Skull of the Saint", saintColor)
end)
ESPTab.newButton("ESP Ribcage of the Saint", "Adiciona ESP para Ribcage of the Saint", function()
addESP("Ribcage of the Saint", "Ribcage of the Saint", saintColor)
end)
ESPTab.newButton("ESP Left Arm of the Saint", "Adiciona ESP para Left Arm of the Saint", function()
addESP("Left Arm of the Saint", "Left Arm of the Saint", saintColor)
end)
ESPTab.newButton("ESP Right Arm of the Saint", "Adiciona ESP para Right Arm of the Saint", function()
addESP("Right Arm of the Saint", "Right Arm of the Saint", saintColor)
end)
ESPTab.newButton("ESP Left Leg of the Saint", "Adiciona ESP para Left Leg of the Saint", function()
addESP("Left Leg of the Saint", "Left Leg of the Saint", saintColor)
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

TeleportTab.newButton("Teleportar para Locacaca Fruit", "Teleporta para Locacaca Fruit mais próxima", function()
teleportToClosestObject("Locacaca Fruit")
end)

TeleportTab.newButton("Teleportar para Flecha", "Teleporta para a Flecha mais próxima", function()
teleportToClosestObject("Arrow")
end)

TeleportTab.newButton("Teleportar para Requiem Arrow", "Teleporta para Requiem Arrow mais próxima", function()
teleportToClosestObject("Requiem Arrow")
end)

TeleportTab.newButton("Teleportar para Heart of the Saint", "Teleporta para Heart of the Saint mais próxima", function()
teleportToClosestObject("Heart of the Saint")
end)

TeleportTab.newButton("Teleportar para Right Leg of the Saint", "Teleporta para Right Leg of the Saint mais próxima", function()
teleportToClosestObject("Right Leg of the Saint")
end)

TeleportTab.newButton("Teleportar para Left Eye of the Saint", "Teleporta para Left Eye of the Saint mais próxima", function()
teleportToClosestObject("Left Eye of the Saint")
end)

TeleportTab.newButton("Teleportar para Right Eye of the Saint", "Teleporta para Right Eye of the Saint mais próxima", function()
teleportToClosestObject("Right Eye of the Saint")
end)

TeleportTab.newButton("Teleportar para Skull of the Saint", "Teleporta para Skull of the Saint mais próxima", function()
teleportToClosestObject("Skull of the Saint")
end)

TeleportTab.newButton("Teleportar para Ribcage of the Saint", "Teleporta para Ribcage of the Saint mais próxima", function()
teleportToClosestObject("Ribcage of the Saint")
end)

TeleportTab.newButton("Teleportar para Left Arm of the Saint", "Teleporta para Left Arm of the Saint mais próxima", function()
teleportToClosestObject("Left Arm of the Saint")
end)

TeleportTab.newButton("Teleportar para Right Arm of the Saint", "Teleporta para Right Arm of the Saint mais próxima", function()
teleportToClosestObject("Right Arm of the Saint")
end)

TeleportTab.newButton("Teleportar para Left Leg of the Saint", "Teleporta para Left Leg of the Saint mais próxima", function()
teleportToClosestObject("Left Leg of the Saint")
end)

TeleportTab.newButton("Teleportar para New Locacaca", "Teleporta para New Locacaca mais próxima", function()
teleportToClosestObject("New Locacaca")
end)

TeleportTab.newButton("Teleportar para Jotaro Kujo", "Teleporta para Jotaro Kujo", function()
teleportTo(Vector3.new(1028.8409423828125, 3.158618450164795, -390.45904541015625))
end)

TeleportTab.newButton("Teleportar para Quarto de Dio", "Teleporta para Quarto de Dio", function()
teleportTo(Vector3.new(1929.6566162109375, 49.989036560058594, -388.8101806640625))
end)

TeleportTab.newButton("Teleportar para Frente da Mansão de Dio", "Teleporta para a frente da Mansão de Dio", function()
teleportTo(Vector3.new(1720.30908203125, -22.1832275390625, -341.65350341796875))
end)

TeleportTab.newButton("Teleportar para Padre Pucchi", "Teleporta para Padre Pucchi", function()
teleportTo(Vector3.new(-190.82945251464844, 3.158618450164795, -684.6744995117188))
end)

TeleportTab.newButton("Teleportar para Gyro Zeppeli e Johnny Joestar", "Teleporta para Gyro Zeppeli", function()
teleportTo(Vector3.new(-196.90049743652344, 4.459641933441162, 91.6489028930664))
end)

TeleportTab.newButton("Teleportar para Jonathan Joestar", "Teleporta para Jonathan Joestar", function()
teleportTo(Vector3.new(426.8250732421875, 4.4602251052856445, -66.74285888671875))
end)

TeleportTab.newButton("Teleportar para Funny Valentime Boss", "Teleporta para Funny Valentime Boss", function()
teleportTo(Vector3.new(-402.7161865234375, -37.16085433959961, 505.7417907714844))
end)

TeleportTab.newButton("Teleportar para Ippo Boxeador", "Teleporta para Ippo Boxeador", function()
teleportTo(Vector3.new(732.7675170898438, 64.35753631591797, 563.5234985351562))
end)

TeleportTab.newButton("Teleportar para Diego Brando Boss", "Teleporta para Diego Brando Boss", function()
teleportTo(Vector3.new(573.0200805664062, 61.15618896484375, 888.8558959960938))
end)

TeleportTab.newButton("Teleportar para The Rock Store", "Teleporta para The Rock Store", function()
teleportTo(Vector3.new(945.5636596679688, 3.67349910736084, -547.20556640625))
end)

TeleportTab.newButton("Teleportar para Arcade", "Teleporta para o novo Arcade", function()
teleportTo(Vector3.new(229.74317932128906, 4.361627101898193, -130.280029296875))
end)

TeleportTab.newButton("Teleportar para Banco", "Teleporta para o novo Banco", function()
teleportTo(Vector3.new(-43.0844841003418, 2.8666749000549316, -4.446100234985352))
end)

TeleportTab.newButton("Teleportar para Correio", "Teleporta para o Correio", function()
teleportTo(Vector3.new(120.9356918334961, 729.2530517578125, -1420.5677490234375))
end)

-- Configurações finais
window:Init()
