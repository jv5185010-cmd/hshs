local ScreenGui = Instance.new("ScreenGui")
local MenuButton = Instance.new("TextButton")
local UIStroke = Instance.new("UIStroke")

-u gui
ScreenGui.Name = "DeltaCustomMenu"
ScreenGui.ResetOnSpawn = false

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local localPlayer = Players.LocalPlayer

if localPlayer then
    ScreenGui.Parent = localPlayer:WaitForChild("PlayerGui", 10) or game:GetService("CoreGui")
else
    ScreenGui.Parent = game:GetService("CoreGui")
end

-- Configuração visual e propriedades do Botão
MenuButton.Name = "ToggleButton"
MenuButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
MenuButton.BackgroundTransparency = 0.5
MenuButton.Position = UDim2.new(0.1, 0, 0.2, 0)
MenuButton.Size = UDim2.new(0, 45, 0, 45)
MenuButton.Font = Enum.Font.SourceSansBold
MenuButton.Text = "J"
MenuButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MenuButton.TextSize = 29
MenuButton.Visible = true
MenuButton.ZIndex = 10
MenuButton.Parent = ScreenGui

-config
UIStroke.Parent = MenuButton
UIStroke.Thickness = 2
UIStroke.Color = Color3.fromRGB(255, 0, 0)

local isOn = false

-c n
RunService.PreSimulation:Connect(function()
    if isOn and localPlayer and localPlayer.Character then
        local character = localPlayer.Character
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        
        if humanoid then
            -- Ativa o estado de sentado para o servidor/jogos externos
            humanoid.Sit = true
            
           
            humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, false)
        end
    end
end)

-- 
MenuButton.MouseButton1Click:Connect(function()
    isOn = not isOn
    
    local character = localPlayer and localPlayer.Character
    local humanoid = character and character:FindFirstChildOfClass("Humanoid")

    if isOn then
        UIStroke.Color = Color3.fromRGB(0, 255, 0) -- Verde = Ativado
        print("Modo Fluido Ativado!")
    else
        UIStroke.Color = Color3.fromRGB(255, 0, 0) -- Vermelho = Desativado
        print("Modo Fluido Desativado!")
        
        if humanoid then
            humanoid.Sit = false
            -#1dangoBALANGOOO
            humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
            humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
        end
    end
end)
