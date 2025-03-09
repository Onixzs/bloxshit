local players = game:GetService("Players")
local runService = game:GetService("RunService")
local userInputService = game:GetService("UserInputService")
local replicatedStorage = game:GetService("ReplicatedStorage")
local teleportService = game:GetService("TeleportService")
local httpService = game:GetService("HttpService")
local workspace = game:GetService("Workspace")

local player = players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local root = character:WaitForChild("HumanoidRootPart")

-- TobarPlus GUI Setup
local TobarPlus = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
local mainFrame = Instance.new("Frame", TobarPlus)
mainFrame.Size = UDim2.new(0.25, 0, 0.35, 0)
mainFrame.Position = UDim2.new(0.375, 0, 0.325, 0)
mainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 35)
mainFrame.BackgroundTransparency = 0.15
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.ClipsDescendants = true

local stroke = Instance.new("UIStroke", mainFrame)
stroke.Thickness = 2
stroke.Transparency = 0.2
stroke.Color = Color3.fromRGB(0, 255, 255)

local uiCorner = Instance.new("UICorner", mainFrame)
uiCorner.CornerRadius = UDim.new(0, 12)

local title = Instance.new("TextLabel", mainFrame)
title.Size = UDim2.new(1, 0, 0.15, 0)
title.BackgroundTransparency = 1
title.Text = "🍏 TobarPlus Blox Fruits"
title.TextScaled = true
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold

local function createButton(text, position, callback)
    local button = Instance.new("TextButton", mainFrame)
    button.Size = UDim2.new(0.6, 0, 0.1, 0)
    button.Position = UDim2.new(0.2, 0, position, 0)
    button.Text = text
    button.TextScaled = true
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
    button.Font = Enum.Font.GothamBold
    
    local uiCorner = Instance.new("UICorner", button)
    uiCorner.CornerRadius = UDim.new(0, 10)
    
    local buttonStroke = Instance.new("UIStroke", button)
    buttonStroke.Thickness = 2
    buttonStroke.Color = Color3.fromRGB(0, 255, 255)
    
    button.MouseButton1Click:Connect(function()
        print("Button clicked: " .. text)
        callback()
    end)
    
    return button
end

-- Function to find the closest fruit
local function findClosestFruit()
    local closestFruit = nil
    local shortestDistance = math.huge
    for _, obj in ipairs(workspace:GetChildren()) do
        if obj:IsA("Part") and obj.Name:lower():find("fruit") then
            local distance = (root.Position - obj.Position).Magnitude
            if distance < shortestDistance then
                shortestDistance = distance
                closestFruit = obj
            end
        end
    end
    if closestFruit then
        root.CFrame = closestFruit.CFrame
    end
end

-- Function to find a legendary fruit
local function findLegendaryFruit()
    local legendaryFruits = {"Dragon", "Dough", "Leopard", "Venom", "Soul"}
    for _, obj in ipairs(workspace:GetChildren()) do
        if obj:IsA("Part") and obj.Name:lower():find("fruit") then
            for _, fruit in ipairs(legendaryFruits) do
                if obj.Name:lower():find(fruit:lower()) then
                    root.CFrame = obj.CFrame
                    return
                end
            end
        end
    end
end

-- Function to find a mythic fruit
local function findMythicFruit()
    local mythicFruits = {"T-Rex", "Kitsune"} -- Example mythic fruits, adjust as needed
    for _, obj in ipairs(workspace:GetChildren()) do
        if obj:IsA("Part") and obj.Name:lower():find("fruit") then
            for _, fruit in ipairs(mythicFruits) do
                if obj.Name:lower():find(fruit:lower()) then
                    root.CFrame = obj.CFrame
                    return
                end
            end
        end
    end
end

-- Function to server hop
local function serverHop()
    local servers = httpService:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/2753915549/servers/Public?sortOrder=Asc&limit=100"))
    for _, server in ipairs(servers.data) do
        if server.playing < server.maxPlayers then
            teleportService:TeleportToPlaceInstance(game.PlaceId, server.id, player)
            return
        end
    end
end

createButton("🔍 Find Fruit", 0.2, findClosestFruit)
createButton("🔥 Find LEGENDARY", 0.35, findLegendaryFruit)
createButton("🌟 Find MYTHIC", 0.5, findMythicFruit)
createButton("🔄 Server Hop", 0.65, serverHop)
