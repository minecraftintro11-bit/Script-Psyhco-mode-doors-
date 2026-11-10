-- Psycho Mode [THE HOTEL STYLE INTRO UPDATE] by ShockerGaze
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Lighting = game:GetService("Lighting")

-- 1. Hazy Mode Fog Setup
local function setupHazyFog()
    Lighting.FogColor = Color3.fromRGB(35, 35, 40)
    Lighting.FogEnd = 35
    Lighting.FogStart = 0
    Lighting.Ambient = Color3.fromRGB(10, 10, 15)
    Lighting.OutdoorAmbient = Color3.fromRGB(10, 10, 15)
end
task.spawn(setupHazyFog)

-- 2. Massive "The Hotel" Style Intro GUI
local function showDoorsStyleIntro()
    local player = Players.LocalPlayer
    if not player then return end
    local playerGui = player:WaitForChild("PlayerGui", 5)
    if not playerGui then return end
    
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "DoorsIntroGui"
    screenGui.IgnoreGuiInset = true
    
    -- Главный огромный заголовок (как надпись "THE HOTEL")
    local mainTitle = Instance.new("TextLabel")
    mainTitle.Size = UDim2.new(1, 0, 0, 100)
    mainTitle.Position = UDim2.new(0, 0, 0.35, 0)
    mainTitle.BackgroundTransparency = 1
    mainTitle.Text = "PSYCHO MODE"
    mainTitle.TextColor3 = Color3.fromRGB(180, 0, 0)
    mainTitle.TextSize = 80 -- Огромный размер шрифта
    mainTitle.Font = Enum.Font.Onyx -- Жуткий вытянутый стиль текста
    mainTitle.TextTransparency = 1
    mainTitle.Parent = screenGui
    
    -- Описание режима чуть ниже
    local subTitle = Instance.new("TextLabel")
    subTitle.Size = UDim2.new(1, 0, 0, 30)
    subTitle.Position = UDim2.new(0, 0, 0.47, 0)
    subTitle.BackgroundTransparency = 1
    subTitle.Text = "You turned it on. Prepare to die."
    subTitle.TextColor3 = Color3.fromRGB(210, 210, 210)
    subTitle.TextSize = 22
    subTitle.Font = Enum.Font.SpecialElite
    subTitle.TextTransparency = 1
    subTitle.Parent = screenGui

    -- Авторство в самом низу экрана
    local creditsLabel = Instance.new("TextLabel")
    creditsLabel.Size = UDim2.new(1, 0, 0, 30)
    creditsLabel.Position = UDim2.new(0, 0, 0.85, 0)
    creditsLabel.BackgroundTransparency = 1
    creditsLabel.Text = "Credits by ShockerGaze"
    creditsLabel.TextColor3 = Color3.fromRGB(130, 130, 130)
    creditsLabel.TextSize = 18
    creditsLabel.Font = Enum.Font.SourceSansItalic
    creditsLabel.TextTransparency = 1
    creditsLabel.Parent = screenGui
    
    screenGui.Parent = playerGui
    
    -- Плавное пафосное появление, как в игре
    TweenService:Create(mainTitle, TweenInfo.new(2.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 0}):Play()
    task.wait(0.5)
    TweenService:Create(subTitle, TweenInfo.new(2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 0}):Play()
    TweenService:Create(creditsLabel, TweenInfo.new(2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 0}):Play()
    
    task.wait(5) -- Время отображения названия на экране
    
    -- Медленное эпичное растворение в темноте
    TweenService:Create(mainTitle, TweenInfo.new(2), {TextTransparency = 1}):Play()
    TweenService:Create(subTitle, TweenInfo.new(2), {TextTransparency = 1}):Play()
    local fadeTween = TweenService:Create(creditsLabel, TweenInfo.new(2), {TextTransparency = 1})
    fadeTween:Play()
    
    fadeTween.Completed:Wait()
    screenGui:Destroy()
end
task.spawn(showDoorsStyleIntro)

-- 3. Load Vynixu's DOORS Entity Spawner v2 API
local Spawner = loadstring(game:HttpGet("https://githubusercontent.com"))()

-- 4. Monsters Configurations
local function triggerDepth()
    local entity = Spawner.createEntity({
        Name = "Depth",
        Asset = "rbxassetid://11419914486", 
        CanvasOpacity = 0.6,
        Color = Color3.fromRGB(0, 120, 255), 
        Speed = 350,
        DelayTime = 5,
        HeightOffset = 0,
        CanKill = true,
        KillRange = 15,
        BreakLights = true,
        FlickerLights = { Duration = 5, Frequency = 0.15 },
        Shaking = { Intensity = 18, Duration = 3.5 },
        Rebound = { Enabled = true, Min = 2, Max = 4, Delay = 0.5 },
        CustomDialog = {"You died to Depth...", "He moves very fast (Speed 350) and rebounds up to 4 times!", "Watch out for the prolonged blue-tinted flickering!"}
    })
    Spawner.runEntity(entity)
end

local function triggerHim()
    local entity = Spawner.createEntity({
        Name = "Him",
        Asset = "rbxassetid://11420138981", 
        CanvasOpacity = 0.9,
        Color = Color3.fromRGB(255, 0, 0), 
        Speed = 700,
        DelayTime = 1.5,
        HeightOffset = 0,
        CanKill = true,
        KillRange = 20,
        BreakLights = true,
        FlickerLights = { Duration = 0.1, Frequency = 0.05 },
        Shaking = { Intensity = 50, Duration = 3 },
        Rebound = { Enabled = true, Min = 3, Max = 5, Delay = 0.25 },
        CustomDialog = {"That was Him.", "He is an absolute nightmare (Speed 700)!", "He rebounds up to 5 times. You have to jump in and out of closets perfectly!"}
    })
    Spawner.runEntity(entity)
end

local function triggerFoul()
    TweenService:Create(Lighting, TweenInfo.new(1), {FogEnd = 15}):Play()
    local entity = Spawner.createEntity({
        Name = "Foul",
        Asset = "rbxassetid://10850882747", 
        CanvasOpacity = 0.7,
        Color = Color3.fromRGB(120, 120, 120), 
        Speed = 180,
        DelayTime = 3,
        HeightOffset = 0,
        CanKill = true,
        KillRange = 15,
        BreakLights = false,
        FlickerLights = { Duration = 2, Frequency = 0.4 },
        Shaking = { Intensity = 22, Duration = 4.5 },
        Rebound = { Enabled = true, Min = 6, Max = 10, Delay = 0.6 },
        CustomDialog = {"Foul tricked you.", "He rebounds up to 10 times consecutively!", "Listen closely to his distorted laughter to time your hiding."}
    })
    Spawner.runEntity(entity)
    task.delay(10, function() TweenService:Create(Lighting, TweenInfo.new(2), {FogEnd = 35}):Play() end)
end

local function triggerWH1T3()
    TweenService:Create(Lighting, TweenInfo.new(0.5), {FogColor = Color3.fromRGB(255, 255, 255), FogEnd = 10}):Play()
    local entity = Spawner.createEntity({
        Name = "WH1T3",
        Asset = "rbxassetid://9416058145", 
        CanvasOpacity = 1,
        Color = Color3.fromRGB(255, 255, 255), 
        Speed = 550, 
        DelayTime = 2,
        HeightOffset = 0,
        CanKill = true,
        KillRange = 18,
        BreakLights = true,
        FlickerLights = { Duration = 3, Frequency = 0.1 },
        Shaking = { Intensity = 35, Duration = 4 }, 
        Rebound = { Enabled = true, Min = 2, Max = 5, Delay = 0.4 }, 
        CustomDialog = {"You were erased by WH1T3...", "Impossible Mode glitch entity caught you!", "He distorts the reality with speed 550. Hide in the static haze!"}
    })
    Spawner.runEntity(entity)
    task.delay(8, function() TweenService:Create(Lighting, TweenInfo.new(1.5), {FogColor = Color3.fromRGB(35, 35, 40), FogEnd = 35}):Play() end)
end

-- 5. Room Listener Mechanism (Balanced 4-Monster Chances)
local function onRoomAdded(room)
    task.wait(1.5)
    local chance = math.random(1, 100)
    
    if chance <= 10 then
        triggerDepth() 
    elseif chance > 10 and chance <= 20 then
        triggerHim()   
    elseif chance > 20 and chance <= 30 then
        triggerFoul()  
    elseif chance > 30 and chance <= 40 then
        triggerWH1T3() 
    end
end

local latestRoom = workspace:WaitForChild("CurrentRooms")
latestRoom.ChildAdded:Connect(onRoomAdded)


