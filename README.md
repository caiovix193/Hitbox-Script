_G.HeadSize = 50
_G.Disabled = false -- Inicialmente ativado

local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
local toggleButton = Instance.new("TextButton", screenGui)

toggleButton.Size = UDim2.new(0, 200, 0, 50)
toggleButton.Position = UDim2.new(0.5, -100, 0.5, -25)
toggleButton.Text = "Desligar"
toggleButton.BackgroundColor3 = Color3.new(0, 1, 0) -- Verde
toggleButton.TextColor3 = Color3.new(1, 1, 1)

-- Função para desligar o script
local function disableScript()
    _G.Disabled = true
    toggleButton.Text = "Desligado"
    toggleButton.BackgroundColor3 = Color3.new(1, 0, 0) -- Vermelho
end

-- Conectar a função de desligar ao botão
toggleButton.MouseButton1Click:Connect(disableScript)

game:GetService("RunService").RenderStepped:Connect(function()
    if not _G.Disabled then
        for _,v in pairs(game:GetService("Players"):GetPlayers()) do
            if v.Name ~= player.Name then
                pcall(function()
                    v.Character.HumanoidRootPart.Size = Vector3.new(_G.HeadSize, _G.HeadSize, _G.HeadSize)
                    v.Character.HumanoidRootPart.Transparency = 0.7
                    v.Character.HumanoidRootPart.BrickColor = BrickColor.new("Really blue")
                    v.Character.HumanoidRootPart.Material = "Neon"
                    v.Character.HumanoidRootPart.CanCollide = false
                end)
            end
        end
    end
end)
