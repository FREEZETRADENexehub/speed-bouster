--// SERVICES
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local lp = Players.LocalPlayer

--// PROTECTION CONTRE LES DOUBLONS
local oldGui = lp.PlayerGui:FindFirstChild("NexeHub_Universal")
if oldGui then oldGui:Destroy() end

--// GUI PRINCIPALE
local gui = Instance.new("ScreenGui")
gui.Name = "NexeHub_Universal"
gui.ResetOnSpawn = false
gui.Parent = lp:WaitForChild("PlayerGui")

--// BOUTON FLOTTANT (N) - Pour ouvrir/fermer
local toggleBtn = Instance.new("TextButton")
toggleBtn.Size = UDim2.new(0, 55, 0, 55)
toggleBtn.Position = UDim2.new(0.05, 0, 0.4, 0)
toggleBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
toggleBtn.Text = "N"
toggleBtn.TextColor3 = Color3.fromRGB(0, 170, 255)
toggleBtn.Font = Enum.Font.GothamBold
toggleBtn.TextSize = 28
toggleBtn.Parent = gui

Instance.new("UICorner", toggleBtn).CornerRadius = UDim.new(1, 0)
local btnStroke = Instance.new("UIStroke", toggleBtn)
btnStroke.Thickness = 2
btnStroke.Color = Color3.fromRGB(0, 170, 255)

--// LE MENU PRINCIPAL
local main = Instance.new("Frame")
main.Size = UDim2.new(0, 250, 0, 320)
main.Position = UDim2.new(0.5, -125, 0.5, -160)
main.BackgroundColor3 = Color3.fromRGB(12, 12, 12)
main.BorderSizePixel = 0
main.ClipsDescendants = true
main.Visible = true
main.Parent = gui

Instance.new("UICorner", main).CornerRadius = UDim.new(0, 15)

-- BORDURE ANIMÉE (Arc-en-ciel Bleu/Violet)
local border = Instance.new("Frame")
border.Size = UDim2.new(1, 4, 1, 4)
border.Position = UDim2.new(0, -2, 0, -2)
border.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
border.ZIndex = 0
border.Parent = main
Instance.new("UICorner", border).CornerRadius = UDim.new(0, 17)

task.spawn(function()
    while true do
        for i = 0, 1, 0.005 do
            border.BackgroundColor3 = Color3.fromHSV(i, 0.8, 1)
            task.wait(0.03)
        end
    end
end)

--// SYSTÈME DE FLOCONS (❄️)
local function spawnFlake()
    local flake = Instance.new("TextLabel")
    flake.BackgroundTransparency = 1
    flake.Text = "❄"
    flake.TextColor3 = Color3.new(1, 1, 1)
    flake.TextSize = math.random(14, 22)
    flake.Position = UDim2.new(math.random(), 0, -0.1, 0)
    flake.ZIndex = 1
    flake.Parent = main
    
    local fallInfo = TweenInfo.new(math.random(3, 6), Enum.EasingStyle.Linear)
    local t = TweenService:Create(flake, fallInfo, {Position = UDim2.new(flake.Position.X.Scale, math.random(-20, 20), 1.1, 0)})
    t:Play()
    t.Completed:Connect(function() flake:Destroy() end)
end

task.spawn(function()
    while true do
        if main.Visible then spawnFlake() end
        task.wait(0.5)
    end
end)

--// CONTENU DU MENU
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 50)
title.Text = "Nexe_hub"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.GothamBold
title.TextSize = 25
title.BackgroundTransparency = 1
title.ZIndex = 5
title.Parent = main

-- Bouton ACTIVER
local active = false
local toggle = Instance.new("TextButton")
toggle.Size = UDim2.new(0.85, 0, 0, 45)
toggle.Position = UDim2.new(0.075, 0, 0, 60)
toggle.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
toggle.Text = "DÉSACTIVÉ"
toggle.TextColor3 = Color3.fromRGB(200, 200, 200)
toggle.Font = Enum.Font.GothamBold
toggle.ZIndex = 5
toggle.Parent = main
Instance.new("UICorner", toggle)

-- Champs de saisie (Inputs)
local function addInput(name, y, def)
    local lab = Instance.new("TextLabel")
    lab.Size = UDim2.new(0.4, 0, 0, 30)
    lab.Position = UDim2.new(0.1, 0, 0, y)
    lab.Text = name
    lab.TextColor3 = Color3.fromRGB(180, 180, 180)
    lab.Font = Enum.Font.Gotham
    lab.BackgroundTransparency = 1
    lab.TextXAlignment = "Left"
    lab.ZIndex = 5
    lab.Parent = main
    
    local box = Instance.new("TextBox")
    box.Size = UDim2.new(0.35, 0, 0, 30)
    box.Position = UDim2.new(0.55, 0, 0, y)
    box.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
    box.Text = tostring(def)
    box.TextColor3 = Color3.new(1, 1, 1)
    box.Font = Enum.Font.GothamBold
    box.ZIndex = 5
    box.Parent = main
    Instance.new("UICorner", box)
    return box
end

local vIn = addInput("Vitesse", 120, 53)
local sIn = addInput("Voler", 180, 29)
local jIn = addInput("Saut", 240, 400)

--// FONCTIONNEMENT DES TRICHES
toggle.MouseButton1Click:Connect(function()
    active = not active
    toggle.Text = active and "ACTIVÉ" or "DÉSACTIVÉ"
    toggle.BackgroundColor3 = active and Color3.fromRGB(0, 170, 255) or Color3.fromRGB(30, 30, 30)
    toggle.TextColor3 = active and Color3.new(1,1,1) or Color3.fromRGB(200,200,200)
end)

RunService.Heartbeat:Connect(function()
    if active then
        local char = lp.Character
        if char and char:FindFirstChild("HumanoidRootPart") then
            local hum = char:FindFirstChild("Humanoid")
            local root = char.HumanoidRootPart
            if hum and hum.MoveDirection.Magnitude > 0 then
                local s = (hum.WalkSpeed < 20) and tonumber(sIn.Text) or tonumber(vIn.Text)
                root.Velocity = Vector3.new(hum.MoveDirection.X * s, root.Velocity.Y, hum.MoveDirection.Z * s)
            end
        end
    end
end)

UserInputService.JumpRequest:Connect(function()
    if active and lp.Character and lp.Character:FindFirstChild("HumanoidRootPart") then
        local root = lp.Character.HumanoidRootPart
        root.Velocity = Vector3.new(root.Velocity.X, tonumber(jIn.Text) or 400, root.Velocity.Z)
    end
end)

--// OUVERTURE & DRAG (DÉPLACEMENT)
toggleBtn.MouseButton1Click:Connect(function() main.Visible = not main.Visible end)

local function makeDraggable(obj)
    local drag, start, pos
    obj.InputBegan:Connect(function(i) if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then drag = true start = i.Position pos = obj.Position end end)
    obj.InputChanged:Connect(function(i) if drag and (i.UserInputType == Enum.UserInputType.MouseMovement or i.UserInputType == Enum.UserInputType.Touch) then 
        local d = i.Position - start obj.Position = UDim2.new(pos.X.Scale, pos.X.Offset + d.X, pos.Y.Scale, pos.Y.Offset + d.Y) 
    end end)
    obj.InputEnded:Connect(function(i) if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then drag = false end end)
end

makeDraggable(main)
makeDraggable(toggleBtn)
