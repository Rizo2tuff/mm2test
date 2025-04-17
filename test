local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game:GetService("CoreGui")

local notificationFrame = Instance.new("Frame")
notificationFrame.Size = UDim2.new(0.4, 0, 0.08, 0)
notificationFrame.Position = UDim2.new(0.3, 0, 0.9, 0)
notificationFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
notificationFrame.BackgroundTransparency = 0.3
notificationFrame.BorderSizePixel = 0
notificationFrame.Parent = screenGui
notificationFrame.Visible = false

local notificationUICorner = Instance.new("UICorner")
notificationUICorner.CornerRadius = UDim.new(0.1, 0)
notificationUICorner.Parent = notificationFrame

local notificationGradient = Instance.new("UIGradient")
notificationGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(45, 45, 45)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(25, 25, 25))
}
notificationGradient.Parent = notificationFrame

local notificationText = Instance.new("TextLabel")
notificationText.Size = UDim2.new(1, 0, 1, 0)
notificationText.Position = UDim2.new(0, 0, 0, 0)
notificationText.BackgroundTransparency = 1
notificationText.TextColor3 = Color3.fromRGB(255, 255, 255)
notificationText.TextSize = 20
notificationText.Font = Enum.Font.GothamBold
notificationText.TextScaled = true
notificationText.Parent = notificationFrame

local function showNotification(message)
    notificationText.Text = message
    notificationFrame.Visible = true
    notificationFrame:TweenPosition(UDim2.new(0.3, 0, 0.85, 0), "Out", "Quad", 0.5, true)
    wait(3)
    notificationFrame:TweenPosition(UDim2.new(0.3, 0, 1.1, 0), "Out", "Quad", 0.5, true)
    wait(0.5)
    notificationFrame.Visible = false
end

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0.35, 0, 0.45, 0)
frame.Position = UDim2.new(0.325, 0, 0.275, 0)
frame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
frame.BackgroundTransparency = 0.3
frame.BorderSizePixel = 0
frame.Parent = screenGui

local frameUICorner = Instance.new("UICorner")
frameUICorner.CornerRadius = UDim.new(0.1, 0)
frameUICorner.Parent = frame

local frameGradient = Instance.new("UIGradient")
frameGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(50, 50, 50)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(30, 30, 30))
}
frameGradient.Parent = frame

local textLabel = Instance.new("TextLabel")
textLabel.Size = UDim2.new(1, 0, 0.2, 0)
textLabel.Position = UDim2.new(0, 0, 0, 0)
textLabel.BackgroundTransparency = 1
textLabel.Text = "MM2 Local Spawner"
textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
textLabel.TextSize = 26
textLabel.Font = Enum.Font.GothamBold
textLabel.TextStrokeTransparency = 0.8
textLabel.Parent = frame

local itemTextBox = Instance.new("TextBox")
itemTextBox.Size = UDim2.new(0.8, 0, 0.2, 0)
itemTextBox.Position = UDim2.new(0.1, 0, 0.3, 0)
itemTextBox.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
itemTextBox.PlaceholderText = "Enter item name"
itemTextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
itemTextBox.TextSize = 20
itemTextBox.Font = Enum.Font.Gotham
itemTextBox.Parent = frame

local itemTextBoxUICorner = Instance.new("UICorner")
itemTextBoxUICorner.CornerRadius = UDim.new(0.1, 0)
itemTextBoxUICorner.Parent = itemTextBox

local spawnButton = Instance.new("TextButton")
spawnButton.Size = UDim2.new(0.8, 0, 0.2, 0)
spawnButton.Position = UDim2.new(0.1, 0, 0.6, 0)
spawnButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
spawnButton.Text = "Spawn"
spawnButton.TextSize = 20
spawnButton.TextColor3 = Color3.fromRGB(255, 255, 255)
spawnButton.Font = Enum.Font.Gotham
spawnButton.Parent = frame

local spawnButtonUICorner = Instance.new("UICorner")
spawnButtonUICorner.CornerRadius = UDim.new(0.1, 0)
spawnButtonUICorner.Parent = spawnButton

local function buttonHoverEffect(button)
    button.MouseEnter:Connect(function()
        button.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
    end)

    button.MouseLeave:Connect(function()
        button.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
    end)

    button.MouseButton1Click:Connect(function()
        button.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
        wait(0.1)
        button.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
    end)
end

buttonHoverEffect(spawnButton)

local crate = "Christmas2024Box"
local _R = game:GetService("ReplicatedStorage")
local _B = _R:WaitForChild("Remotes"):WaitForChild("Shop"):WaitForChild("BoxController")

local function fireBoxController(crate, item)
    _B:Fire(crate, item)
end

local function spawnWeapon(name)
    local DataBase = require(game:GetService("ReplicatedStorage").Database.Sync.Item)
    local PlayerData = require(game:GetService("ReplicatedStorage").Modules.ProfileData)

    local newOwned = {}
    newOwned[name] = 1
    local PlayerWeapons = PlayerData.Weapons

    game:GetService("RunService"):BindToRenderStep("InventoryUpdate", 0, function()
        PlayerWeapons.Owned = newOwned
    end)
end

spawnButton.MouseButton1Click:Connect(function()
    local itemName = itemTextBox.Text
    if itemName ~= "" then
        fireBoxController(crate, itemName)
        showNotification("Rolling box for: " .. itemName)
        task.delay(3, function()
            spawnWeapon(itemName)
            game.Players.LocalPlayer.Character:BreakJoints()
        end)
    else
        showNotification("Please enter an item name.")
    end
end)

local UIS = game:GetService("UserInputService")
local dragging, dragInput, dragStart, startPos

local function update(input)
    local delta = input.Position - dragStart
    frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = frame.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

frame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UIS.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        update(input)
    end
end)
