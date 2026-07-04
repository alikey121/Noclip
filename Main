-- Js wall - Noclip Agresivo (Diseño Corregido)
local CoreGui = game:GetService("CoreGui")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer
local noclipActive = false
local noclipConnection = nil

-- Crear GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "JsWallGui"
ScreenGui.ResetOnSpawn = false
if gethui then 
    ScreenGui.Parent = gethui() 
else 
    ScreenGui.Parent = CoreGui 
end

-- LA BOLITA (Botón)
local MainButton = Instance.new("TextButton")
MainButton.Name = "JsWallButton"
MainButton.Parent = ScreenGui
MainButton.Size = UDim2.new(0, 55, 0, 55) -- Tamaño exacto para que se vea como en tu foto
MainButton.Position = UDim2.new(0.5, -27, 0.2, 0)
MainButton.BackgroundColor3 = Color3.fromRGB(15, 15, 15) -- Fondo Negro
MainButton.Text = "Js" -- Solo "Js", como en tu imagen
MainButton.TextColor3 = Color3.fromRGB(220, 40, 40) -- Letras rojas
MainButton.Font = Enum.Font.GothamBlack -- Fuente gruesa y clara
MainButton.TextScaled = true -- Esto hace que la letra se adapte y NUNCA se vea borrosa o pequeña
MainButton.AutoButtonColor = false

-- Ajuste para que las letras no choquen con los bordes
local UIPadding = Instance.new("UIPadding")
UIPadding.PaddingTop = UDim.new(0, 10)
UIPadding.PaddingBottom = UDim.new(0, 10)
UIPadding.PaddingLeft = UDim.new(0, 10)
UIPadding.PaddingRight = UDim.new(0, 10)
UIPadding.Parent = MainButton

-- HACERLA REDONDA
local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(1, 0)
UICorner.Parent = MainButton

-- EL BORDE ROJITO (Corregido para que sí se vea en el contorno)
local UIStroke = Instance.new("UIStroke")
UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border -- ESTO ERA LO QUE FALTABA
UIStroke.Color = Color3.fromRGB(220, 40, 40) -- Borde rojo
UIStroke.Thickness = 3 -- Más grueso para que resalte
UIStroke.Parent = MainButton

-- LÓGICA PARA ARRASTRAR LA BOLITA
local dragging, dragStart, startPos
MainButton.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = MainButton.Position
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        MainButton.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then 
        dragging = false 
    end
end)

-- LÓGICA DEL WALL (Agresivo)
MainButton.MouseButton1Click:Connect(function()
    noclipActive = not noclipActive
    if noclipActive then
        -- MODO ACTIVO: Bolita roja, letras negras, borde negro
        MainButton.BackgroundColor3 = Color3.fromRGB(220, 40, 40)
        MainButton.TextColor3 = Color3.fromRGB(15, 15, 15)
        UIStroke.Color = Color3.fromRGB(15, 15, 15)
        
        noclipConnection = RunService.Stepped:Connect(function()
            if player.Character then
                for _, p in pairs(player.Character:GetDescendants()) do
                    if p:IsA("BasePart") and p.CanCollide then p.CanCollide = false end
                end
            end
        end)
    else
        -- MODO INACTIVO: Bolita negra, letras rojas, borde rojo
        MainButton.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
        MainButton.TextColor3 = Color3.fromRGB(220, 40, 40)
        UIStroke.Color = Color3.fromRGB(220, 40, 40)
        
        if noclipConnection then noclipConnection:Disconnect() end
    end
end)
