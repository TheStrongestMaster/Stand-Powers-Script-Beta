local player = game.Players.LocalPlayer 
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))() 

local Window = OrionLib:MakeWindow({
    Name = "TheStrongestMaster Scripts",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "OrionTest"
})

local Tab = Window:MakeTab({
    Name = "Esp",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Section = Tab:AddSection({
    Name = "LocalPlayer"
})

-- Notificação de boas-vindas
OrionLib:MakeNotification({
    Name = "Welcome!",
    Content = "Welcome to my hub!",
    Image = "rbxassetid://4483345998",
    Time = 5
})

-- ESP Locacaca Fruta
Tab:AddButton({
    Name = "Esp Rokaka Fruta",
    Callback = function()
        local Workspace = game:GetService("Workspace")
        local highlightedObjects = {}

        local function highlightObject(obj)
            if obj:IsA('MeshPart') and obj.Parent and obj.Parent:IsA('Model') and obj.Parent.Name == 'Locacaca Fruit' then
                if not highlightedObjects[obj] and not obj.Parent:FindFirstChild("BillboardGui") then
                    local BillboardGui = Instance.new('BillboardGui')
                    local TextLabel = Instance.new('TextLabel')

                    BillboardGui.Parent = obj.Parent
                    BillboardGui.Name = "BillboardGui"
                    BillboardGui.AlwaysOnTop = true
                    BillboardGui.Size = UDim2.new(0, 50, 0, 50)
                    BillboardGui.StudsOffset = Vector3.new(0, 2, 0)

                    TextLabel.Parent = BillboardGui
                    TextLabel.BackgroundTransparency = 1
                    TextLabel.Size = UDim2.new(1, 0, 1, 0)
                    TextLabel.Text = "Locacaca Fruit"
                    TextLabel.TextScaled = true
                    TextLabel.TextStrokeTransparency = 0.5
                    TextLabel.TextColor3 = Color3.new(1, 0, 0)

                    highlightedObjects[obj] = true
                end
            end
        end

        local function processExistingObjects()
            for _, obj in ipairs(Workspace:GetDescendants()) do
                highlightObject(obj)
            end
        end

        Workspace.DescendantAdded:Connect(highlightObject)
        processExistingObjects()
    end
})

-- ESP Flecha
Tab:AddButton({
    Name = "Esp flecha",
    Callback = function()
        local Workspace = game:GetService("Workspace")
        local highlightedObjects = {}

        local function highlightObject(obj)
            if obj:IsA('MeshPart') and obj.Parent and obj.Parent:IsA('Model') and obj.Parent.Name == 'Arrow' then
                if not highlightedObjects[obj] and not obj.Parent:FindFirstChild("BillboardGui") then
                    local BillboardGui = Instance.new('BillboardGui')
                    local TextLabel = Instance.new('TextLabel')

                    BillboardGui.Parent = obj.Parent
                    BillboardGui.Name = "BillboardGui"
                    BillboardGui.AlwaysOnTop = true
                    BillboardGui.Size = UDim2.new(0, 50, 0, 50)
                    BillboardGui.StudsOffset = Vector3.new(0, 2, 0)

                    TextLabel.Parent = BillboardGui
                    TextLabel.BackgroundTransparency = 1
                    TextLabel.Size = UDim2.new(1, 0, 1, 0)
                    TextLabel.Text = "Flecha"
                    TextLabel.TextScaled = true
                    TextLabel.TextStrokeTransparency = 0.5
                    TextLabel.TextColor3 = Color3.new(1, 1, 0)

                    highlightedObjects[obj] = true
                end
            end
        end

        local function processExistingObjects()
            for _, obj in ipairs(Workspace:GetDescendants()) do
                highlightObject(obj)
            end
        end

        Workspace.DescendantAdded:Connect(highlightObject)
        processExistingObjects()
    end
})

-- Desativar todas as funções ESP
Tab:AddButton({
    Name = "Desativar todas",
    Callback = function()
        local Workspace = game:GetService("Workspace")

        for _, obj in ipairs(Workspace:GetDescendants()) do
            if obj:FindFirstChild("BillboardGui") then
                obj.BillboardGui:Destroy()
            end
        end
    end
})
