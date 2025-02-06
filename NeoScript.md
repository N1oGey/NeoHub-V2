local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local Badge = Instance.new("TextLabel")
Badge.Size = UDim2.new(0, 200, 0, 50)
Badge.Position = UDim2.new(0.5, -100, 0, 50)
Badge.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Badge.BackgroundTransparency = 0.3
Badge.Text = "Created by nexus14888"
Badge.TextColor3 = Color3.fromRGB(255, 255, 255)
Badge.Font = Enum.Font.SourceSansBold
Badge.TextSize = 20
Badge.Parent = ScreenGui

local UICornerBadge = Instance.new("UICorner", Badge)
UICornerBadge.CornerRadius = UDim.new(0, 10)

task.delay(3, function()
    Badge:Destroy()
end)

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 400, 0, 300)
MainFrame.Position = UDim2.new(0.5, -200, 0.5, -150)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.BackgroundTransparency = 0.5
MainFrame.Parent = ScreenGui

local UICorner = Instance.new("UICorner", MainFrame)
UICorner.CornerRadius = UDim.new(0, 10)

local function createRainbowGradient(instance)
    local UIGradient = Instance.new("UIGradient", instance)
    UIGradient.Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 0)),
        ColorSequenceKeypoint.new(0.17, Color3.fromRGB(255, 165, 0)),
        ColorSequenceKeypoint.new(0.33, Color3.fromRGB(255, 255, 0)),
        ColorSequenceKeypoint.new(0.5, Color3.fromRGB(0, 255, 0)),
        ColorSequenceKeypoint.new(0.67, Color3.fromRGB(0, 0, 255)),
        ColorSequenceKeypoint.new(0.83, Color3.fromRGB(75, 0, 130)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(238, 130, 238))
    }
    UIGradient.Rotation = 0
    game:GetService("RunService").RenderStepped:Connect(function()
        UIGradient.Rotation = (UIGradient.Rotation + 1) % 360
    end)
end

createRainbowGradient(MainFrame)

local TitleBar = Instance.new("Frame")
TitleBar.Size = UDim2.new(1, 0, 0, 30)
TitleBar.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
TitleBar.Parent = MainFrame

local TitleText = Instance.new("TextLabel")
TitleText.Size = UDim2.new(1, 0, 1, 0)
TitleText.BackgroundTransparency = 1
TitleText.Text = "Neo Hub v2"
TitleText.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleText.Font = Enum.Font.SourceSansBold
TitleText.TextSize = 20
TitleText.Parent = TitleBar
createRainbowGradient(TitleText)

local scripts = {
    {"Sander x", "loadstring(game:HttpGet('https://rawscripts.net/raw/Brookhaven-RP-Sander-x-22769'))()"},
    {"c00lgui v3rx", "loadstring(game:HttpGet('https://raw.githubusercontent.com/cnPthPiGon/c00lgui-v3rx/refs/heads/main/Brokhaven%20rp%20best%20scripts'))()"},
    {"Brookhaven R4D", "loadstring(game:HttpGet('https://raw.githubusercontent.com/M1ZZ001/BrookhavenR4D/main/Brookhaven%20R4D%20Script'))()"},
    {"GhostHub", "loadstring(game:HttpGet('https://raw.githubusercontent.com/GhostPlayer352/Test4/main/GhostHub'))()"},
    {"Rochips Loader", "if \"you wanna use rochips universal\" then\n local z_x,z_z=\"gzrux646yj/raw/main.ts\",\"https://glot.io/snippets/\"\n local im,lonely,z_c=task.wait,game,loadstring\n z_c(lonely:HttpGet(z_z..\"\"..z_x))()\n return (\"This will load in about 2 - 30 seconds\" or \"according to your device and executor\") end"},
    {"FE Black Hole", "loadstring(game:HttpGet('https://rawscripts.net/raw/Universal-Script-FE-black-hole-18879'))()"},
    {"Infinite Yield", "loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()"},
    {"Brook Haven GUI", "loadstring(game:HttpGet('https://raw.githubusercontent.com/TheDarkoneMarcillisePex/Other-Scripts/main/Brook%20Haven%20Gui'))()"},
}

for i, v in ipairs(scripts) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0.3, -10, 0, 50)
    button.Position = UDim2.new(0.05 + 0.32 * ((i-1) % 3), 0, 0.15 + math.floor((i-1) / 3) * 0.2, 0)
    button.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    button.Text = v[1]
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 18
    button.Parent = MainFrame

    local UICorner = Instance.new("UICorner", button)
    UICorner.CornerRadius = UDim.new(0, 8)
    createRainbowGradient(button)

    button.MouseButton1Click:Connect(function()
        loadstring(v[2])()
    end)
end

local function makeDraggable(frame)
    local dragging = false
    local dragInput, dragStart, startPos
    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = frame.Position
            input.Changed:Connect(function()
                if not input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    frame.InputChanged:Connect(function(input)
        if dragging and input.UserInputType == Enum.UserInputType.Touch then
            local delta = input.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
end

makeDraggable(MainFrame)
