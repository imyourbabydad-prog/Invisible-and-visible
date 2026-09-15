-- Hub GUI Invisible/Visible
-- Made by imjustabaconYT
 
local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
 
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "HubGui"
gui.ResetOnSpawn = false -- stays after death
 
-- Frame
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 240, 0, 150)
frame.Position = UDim2.new(0.5, -120, 0.5, -75)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 50)
 
Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 12)
local stroke = Instance.new("UIStroke", frame)
stroke.Thickness = 2
stroke.Color = Color3.fromRGB(0, 170, 255)
 
-- Signature text
local sig = Instance.new("TextLabel", frame)
sig.Size = UDim2.new(0, 120, 0, 20)
sig.Position = UDim2.new(0, 5, 0, 5)
sig.Text = "made by imjustabaconYT"
sig.TextScaled = true
sig.TextColor3 = Color3.fromRGB(200, 200, 200)
sig.BackgroundTransparency = 1
 
-- Close button (X)
local closeBtn = Instance.new("TextButton", frame)
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -35, 0, 5)
closeBtn.Text = "X"
closeBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
Instance.new("UICorner", closeBtn).CornerRadius = UDim.new(0, 6)
 
closeBtn.MouseButton1Click:Connect(function()
    gui:Destroy()
end)
 
-- Invisible button
local invisBtn = Instance.new("TextButton", frame)
invisBtn.Size = UDim2.new(0, 180, 0, 40)
invisBtn.Position = UDim2.new(0.5, -90, 0, 40)
invisBtn.Text = "Invisible"
invisBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 100)
invisBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
Instance.new("UICorner", invisBtn).CornerRadius = UDim.new(0, 8)
local stroke1 = Instance.new("UIStroke", invisBtn)
stroke1.Thickness = 2
stroke1.Color = Color3.fromRGB(0, 200, 255)
 
invisBtn.MouseButton1Click:Connect(function()
    for _, part in pairs(char:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Transparency = 1
        end
    end
end)
 
-- Visible button
local visBtn = Instance.new("TextButton", frame)
visBtn.Size = UDim2.new(0, 180, 0, 40)
visBtn.Position = UDim2.new(0.5, -90, 0, 90)
visBtn.Text = "Visible"
visBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 100)
visBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
Instance.new("UICorner", visBtn).CornerRadius = UDim.new(0, 8)
local stroke2 = Instance.new("UIStroke", visBtn)
stroke2.Thickness = 2
stroke2.Color = Color3.fromRGB(0, 200, 255)
 
visBtn.MouseButton1Click:Connect(function()
    for _, part in pairs(char:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Transparency = 0
        end
    end
end)
 
-- Make GUI draggable (moves when touched)
local UserInputService = game:GetService("UserInputService")
local dragging, dragInput, dragStart, startPos
 
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
 
UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
                                   startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)
