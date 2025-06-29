local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- GUI container
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "DraggableMenuGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Tip Label (nápis nahoře)
local tipLabel = Instance.new("TextLabel")
tipLabel.Size = UDim2.new(1, 0, 0, 30)
tipLabel.Position = UDim2.new(0, 0, 0, 0)
tipLabel.BackgroundTransparency = 1
tipLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
tipLabel.Font = Enum.Font.SourceSansBold
tipLabel.TextSize = 22
tipLabel.Text = ""
tipLabel.Parent = screenGui

local function showTip(message, duration)
	tipLabel.Text = message
	task.delay(duration, function()
		tipLabel.Text = ""
	end)
end

-- ✅ Zobrazí zprávu po spuštění


-- Right Shift pro toggle menu
local guiVisible = true

-- 💡 VLASTNÍ POZICE MENU (změň podle potřeby)
local customPosition = UDim2.new(-0, 555, 0, 600) -- Vlevo nahoře (x, offsetX, y, offsetY)

-- Hlavní menu (frame)
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 250, 0, 80)
mainFrame.Position = customPosition -- ✅ Používá vlastní pozici
mainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Visible = guiVisible
mainFrame.Parent = screenGui

-- Zavírací tlačítko v pravém horním rohu menu
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 30, 0, 30)
closeButton.Position = UDim2.new(1, -30, 0, 0)
closeButton.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
closeButton.Text = "X"
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.Font = Enum.Font.SourceSansBold
closeButton.TextSize = 18
closeButton.Parent = mainFrame


-- Název panelu
local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 0, 30)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
titleLabel.Text = "Made by vit3g"
titleLabel.Font = Enum.Font.SourceSansBold
titleLabel.TextSize = 20
titleLabel.TextColor3 = Color3.fromRGB(240, 6, 2)
titleLabel.Parent = mainFrame

-- Layout pro tlačítka
local buttonHolder = Instance.new("Frame")
buttonHolder.Size = UDim2.new(1, 0, 1, -30)
buttonHolder.Position = UDim2.new(0, 0, 0, 30)
buttonHolder.BackgroundTransparency = 1
buttonHolder.Parent = mainFrame

local layout = Instance.new("UIListLayout")
layout.Padding = UDim.new(0, 10)
layout.FillDirection = Enum.FillDirection.Vertical
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
layout.VerticalAlignment = Enum.VerticalAlignment.Top
layout.SortOrder = Enum.SortOrder.LayoutOrder
layout.Parent = buttonHolder

-- Funkce pro vytvoření tlačítek
local function createButton(text, callback)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(0, 200, 0, 40)
	button.BackgroundColor3 = Color3.fromRGB(240, 6, 2)
	button.TextColor3 = Color3.fromRGB(0, 0, 0)
	button.Text = text
	button.Font = Enum.Font.SourceSans
	button.TextSize = 35
	button.AutoButtonColor = true
	button.Parent = buttonHolder

	button.MouseButton1Click:Connect(callback)
end

-- Zavřít tlačítkem
createButton("Close This", function()
	guiVisible = false
	mainFrame.Visible = false
	
end)

