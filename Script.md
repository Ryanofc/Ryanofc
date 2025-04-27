-- LocalScript (StarterPlayer -> StarterPlayerScripts)

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- Configurações de velocidade
local normalSpeed = 16
local runSpeed = 30
local running = false

-- Função para criar a GUI
local function createGui()
    -- Cria a ScreenGui
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "OMiorGui"
    screenGui.Parent = player:WaitForChild("PlayerGui")
    
    -- Cria o Título
    local titleLabel = Instance.new("TextLabel")
    titleLabel.Name = "TitleLabel"
    titleLabel.Parent = screenGui
    titleLabel.Size = UDim2.new(0, 300, 0, 50)
    titleLabel.Position = UDim2.new(0.5, -150, 0, 20)
    titleLabel.BackgroundTransparency = 1
    titleLabel.Text = "O Mior"
    titleLabel.Font = Enum.Font.Arcade
    titleLabel.TextScaled = true
    titleLabel.TextColor3 = Color3.new(1, 1, 1)
    
    -- Cria o botão de correr
    local runButton = Instance.new("TextButton")
    runButton.Name = "RunButton"
    runButton.Parent = screenGui
    runButton.Size = UDim2.new(0, 200, 0, 50)
    runButton.Position = UDim2.new(0.5, -100, 0, 100)
    runButton.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
    runButton.Text = "Correr Mais Rápido"
    runButton.Font = Enum.Font.GothamBlack
    runButton.TextScaled = true
    runButton.TextColor3 = Color3.new(1, 1, 1)
    
    -- Cria o botão de teleportar
    local teleportButton = Instance.new("TextButton")
    teleportButton.Name = "TeleportButton"
    teleportButton.Parent = screenGui
    teleportButton.Size = UDim2.new(0, 200, 0, 50)
    teleportButton.Position = UDim2.new(0.5, -100, 0, 170)
    teleportButton.BackgroundColor3 = Color3.fromRGB(255, 100, 0)
    teleportButton.Text = "Teleportar para Bola"
    teleportButton.Font = Enum.Font.GothamBlack
    teleportButton.TextScaled = true
    teleportButton.TextColor3 = Color3.new(1, 1, 1)

    -- Botão lateral para mostrar/esconder a GUI
    local toggleButton = Instance.new("TextButton")
    toggleButton.Name = "ToggleButton"
    toggleButton.Parent = screenGui
    toggleButton.Size = UDim2.new(0, 50, 0, 50)
    toggleButton.Position = UDim2.new(0, 10, 0.5, -25)
    toggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    toggleButton.Text = "GUI"
    toggleButton.Font = Enum.Font.GothamBlack
    toggleButton.TextScaled = true
    toggleButton.TextColor3 = Color3.new(1, 1, 1)

    -- Botões que serão escondidos/mostrados
    local guiElements = {titleLabel, runButton, teleportButton}

    -- Controle de visibilidade
    local guiVisible = true

    toggleButton.MouseButton1Click:Connect(function()
        guiVisible = not guiVisible
        for _, element in pairs(guiElements) do
            element.Visible = guiVisible
        end
    end)

    -- Funções dos botões principais
    runButton.MouseButton1Click:Connect(function()
        if running == false then
            humanoid.WalkSpeed = runSpeed
            runButton.Text = "Parar de Correr"
            running = true
        else
            humanoid.WalkSpeed = normalSpeed
            runButton.Text = "Correr Mais Rápido"
            running = false
        end
    end)

    teleportButton.MouseButton1Click:Connect(function()
        local ball = workspace:FindFirstChild("Ball")
        if ball and character and character:FindFirstChild("HumanoidRootPart") then
            character.HumanoidRootPart.CFrame = ball.CFrame * CFrame.new(0, 3, 0)
        end
    end)
end

-- Cria a GUI
createGui()
