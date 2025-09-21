-- Referências
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

local gui = script.Parent:WaitForChild("MainFrame")
local toggleButton = gui:WaitForChild("ToggleButton")
local speedButton = gui:WaitForChild("SpeedButton")
local invisButton = gui:WaitForChild("InvisibilityButton")

-- Variáveis de controle
local speedActive = false
local invisActive = false
local defaultSpeed = humanoid.WalkSpeed
local boostedSpeed = 50 -- velocidade quando ativo

-- Botão 1: abre/fecha interface
toggleButton.MouseButton1Click:Connect(function()
    gui.Visible = not gui.Visible
end)

-- Botão 2: correr rápido
speedButton.MouseButton1Click:Connect(function()
    speedActive = not speedActive
    if speedActive then
        humanoid.WalkSpeed = boostedSpeed
        speedButton.Text = "Speed: ON"
    else
        humanoid.WalkSpeed = defaultSpeed
        speedButton.Text = "Speed: OFF"
    end
end)

-- Botão 3: invisibilidade
invisButton.MouseButton1Click:Connect(function()
    invisActive = not invisActive
    for _, part in pairs(character:GetDescendants()) do
        if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
            part.Transparency = invisActive and 1 or 0
        end
    end
    invisButton.Text = invisActive and "Invisible: ON" or "Invisible: OFF"
end)StarterGui
 └─ MainGui (ScreenGui)
     └─ MainFrame (Frame)
         ├─ ToggleButton (TextButton) → botão 1
         ├─ SpeedButton (TextButton)  → botão 2
         └─ InvisibilityButton (TextButton) → botão 3
