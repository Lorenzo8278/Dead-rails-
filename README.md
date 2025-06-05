--[[ Interface de Teleporte - Dead Rails ]]
local TeleportLocations = {
    Lab = Vector3.new(100, 10, 100),
    End = Vector3.new(500, 10, -300),
    Casttle = Vector3.new(-200, 10, 250)
}

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Interface
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "TeleportUI"
screenGui.ResetOnSpawn = false

-- Fundo Vermelho com Rosas
local bgImage = Instance.new("ImageLabel", screenGui)
bgImage.Size = UDim2.new(1, 0, 1, 0)
bgImage.Position = UDim2.new(0, 0, 0, 0)
bgImage.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
bgImage.Image = "rbxassetid://6034317805" -- Imagem de rosas vermelhas
bgImage.ImageTransparency = 0.2

-- Função para criar botões
local function criarBotao(nome, posY, destino)
    local btn = Instance.new("TextButton")
    btn.Parent = screenGui
    btn.Size = UDim2.new(0, 200, 0, 50)
    btn.Position = UDim2.new(0, 20, 0, posY)
    btn.BackgroundColor3 = Color3.fromRGB(128, 0, 128)
    btn.Text = "Teleport " .. nome
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 24
    btn.BorderSizePixel = 2
    btn.BorderColor3 = Color3.fromRGB(255, 255, 255)

    btn.MouseButton1Click:Connect(function()
        local char = player.Character or player.CharacterAdded:Wait()
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then
            root.CFrame = CFrame.new(destino)
        end
    end)
end

-- Criando botões
criarBotao("Lab", 100, TeleportLocations.Lab)
criarBotao("End", 170, TeleportLocations.End)
criarBotao("Casttle", 240, TeleportLocations.Casttle)
