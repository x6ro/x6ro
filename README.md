-- Load Library
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Nigger Hub", "Midnight")

-- MAIN Tab and Section
local main = Window:NewTab("MAIN")
local sec = main:NewSection("Features")

-- CFrame Speed Button
sec:NewButton("CFrame Speed (Z) speed [ to increase, ] to decrease", "Toggle and adjust speed", function()
    local p = game.Players.LocalPlayer
    local input = game:GetService('UserInputService')
    local run = game:GetService('RunService')
    local speed, moving = 0.1, false

    -- Movement function
    local function move()
        run.Stepped:Connect(function()
            if moving then
                p.Character.HumanoidRootPart.CFrame += p.Character.Humanoid.MoveDirection * speed
            end
        end)
    end

    -- Keybinds
    input.InputBegan:Connect(function(key)
        if key.KeyCode == Enum.KeyCode.Z then
            moving = not moving
        elseif key.KeyCode == Enum.KeyCode.LeftBracket then
            speed = speed + 0.05
            print("Speed: ", speed)
        elseif key.KeyCode == Enum.KeyCode.RightBracket then
            speed = math.max(0.05, speed - 0.05)
            print("Speed: ", speed)
        end
    end)

    move()
end)

-- FPS Booster Button
sec:NewButton("FPS Booster (Remove All Effects)", "Remove all visual effects in the game", function()
    local lighting = game:GetService("Lighting")
    lighting.FogEnd, lighting.FogStart, lighting.GlobalShadows, lighting.Brightness = 1e6, 1e6, false, 1
    lighting.Ambient, lighting.OutdoorAmbient = Color3.new(0.5, 0.5, 0.5), Color3.new(0.5, 0.5, 0.5)

    -- Remove visual effects
    for _, v in pairs(lighting:GetChildren()) do
        if v:IsA("BlurEffect") or v:IsA("SunRaysEffect") or v:IsA("BloomEffect") or v:IsA("DepthOfFieldEffect") or v:IsA("Sky") then
            v:Destroy()
        end
    end

    -- Disable particle effects and trails
    for _, v in pairs(workspace:GetDescendants()) do
        if v:IsA("ParticleEmitter") or v:IsA("Trail") then v.Enabled = false end
        if v:IsA("MeshPart") or v:IsA("Part") then v.Material, v.Reflectance, v.Color = Enum.Material.Plastic, 0, Color3.new(0.8, 0.8, 0.8) v.Transparency = 1 end
        if v:IsA("Decal") or v:IsA("Texture") then v:Destroy() end
        if v:IsA("SurfaceLight") then v:Destroy() end
    end
    print("FPS Booster: All visual effects removed.")
end)

-- E No Delay Button
sec:NewButton("E No Delay", "Remove delay", function()
    for _, v in pairs(workspace:GetDescendants()) do
        if v:IsA("ProximityPrompt") then v.HoldDuration = 0 end
    end
end)

-- Rejoin Button
sec:NewButton("Rejoin", "Rejoin the game", function()
    game:GetService("TeleportService"):Teleport(game.PlaceId, game.Players.LocalPlayer)
end)

-- Toggle UI Keybind
sec:NewKeybind("Toggle UI", "Show/Hide UI", Enum.KeyCode.V, function()
    Library.ToggleUI()
end)

-- GAME Tab and Section
local gameTab = Window:NewTab("GAME")
local gsec = gameTab:NewSection("Scripts")

-- Script Buttons
gsec:NewButton("PrestineHub", "Load script", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/RSenix3/PrestineHub/refs/heads/main/PrestineKeyless"))()
end)

gsec:NewButton("Sex GUI", "Load script", function()
    loadstring(game:HttpGet('https://raw.githubusercontent.com/4gh9/Bang-Script-Gui/main/bang%20gui.lua'))()
end)

gsec:NewButton("System for TP", "Load script", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/H20CalibreYT/SystemBroken/main/script"))()
end)

gsec:NewButton("Admin Script", "Load script", function()
    loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
end)

-- ESP Toggle Button
gsec:NewButton("ESP (Toggle on P)", "Load script", function()
    getgenv().EspSettings = {
        TeamCheck = false,
        ToggleKey = "P",
        RefreshRate = 10,
        MaximumDistance = 300,
        FaceCamera = true,
        AlignPoints = true,
        MouseVisibility = {
            Enabled = true,
            Radius = 60,
            Transparency = 0.3,
            Method = "Hover",
            HoverRadius = 50,
            Selected = { Boxes = true, Tracers = true, Names = true, Skeletons = true, HealthBars = true, HeadDots = true, LookTracers = true }
        },
        Highlights = { Enabled = false, Players = {}, Transparency = 1, Color = Color3.fromRGB(255, 150, 0), AlwaysOnTop = true },
        NPC = { Color = Color3.fromRGB(150, 150, 150), Transparency = 1, Overrides = { Boxes = true, Tracers = true, Names = true, Skeletons = true, HealthBars = true, HeadDots = true, LookTracers = true } },
        Boxes = { Enabled = false, Transparency = 1, Color = Color3.fromRGB(255, 255, 255), UseTeamColor = true, Outline = true, OutlineColor = Color3.fromRGB(0, 0, 0), OutlineThickness = 1, Thickness = 1 },
        Tracers = { Enabled = false, Transparency = 1, Color = Color3.fromRGB(255, 255, 255), UseTeamColor = true, Outline = true, OutlineColor = Color3.fromRGB(0, 0, 0), OutlineThickness = 1, Origin = "Top", Thickness = 1 },
        Names = { Enabled = true, Transparency = 1, Color = Color3.fromRGB(255, 255, 255), UseTeamColor = true, Outline = true, OutlineColor = Color3.fromRGB(0, 0, 0), Font = Drawing.Fonts.UI, Size = 12, ShowHealth = false },
        Skeletons = { Enabled = true, Transparency = 1, Color = Color3.fromRGB(255, 255, 255), UseTeamColor = true, Outline = false, Thickness = 1 },
        HealthBars = { Enabled = false, Transparency = 1, Color = Color3.fromRGB(0, 255, 0), UseTeamColor = true, Outline = true, OutlineColor = Color3.fromRGB(0, 0, 0), OutlineThickness = 1, Origin = "None", OutlineBarOnly = true },
        HeadDots = { Enabled = false, Transparency = 1, Color = Color3.fromRGB(255, 255, 255), UseTeamColor = true, Outline = true, OutlineColor = Color3.fromRGB(0, 0, 0), OutlineThickness = 1, Thickness = 1 },
        LookTracers = { Enabled = false, Transparency = 1, Color = Color3.fromRGB(255, 255, 255), UseTeamColor = true, Outline = true, OutlineColor = Color3.fromRGB(0, 0, 0), OutlineThickness = 1, Length = 5 }
    }

    -- Toggle ESP on P Key press
    local ESPEnabled = true
    local function ToggleESP()
        ESPEnabled = not ESPEnabled
        print(ESPEnabled and "ESP Enabled" or "ESP Disabled")
    end

    -- Listen for P key press
    game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        if input.KeyCode == Enum.KeyCode.P then ToggleESP() end
    end)

    -- Load the ESP script
    loadstring(game:HttpGet("https://raw.githubusercontent.com/Dragon5819/Main/main/esp", "UniversalEsp"))()
end)
