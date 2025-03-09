--// Biblioteca UI
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/uwuware"))()

--// Criar Janela Principal
local Window = Library:CreateWindow("Dragon Blox Ultimate")

--// Variáveis
local AutoFarm = false
local AutoStats = false
local AutoTeleport = false

--// Seção de Auto Farm
local FarmTab = Window:AddFolder("Auto Farm")

FarmTab:AddToggle({text = "Ativar Auto Farm", flag = "AutoFarm"}, function(state)
    AutoFarm = state
    while AutoFarm do
        task.wait(1)
        for _, v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
            if v:FindFirstChild("HumanoidRootPart") then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
                game.ReplicatedStorage.RemoteEvent:FireServer("Attack", v)
            end
        end
    end
end)

--// Seção de Auto Stats
local StatsTab = Window:AddFolder("Auto Stats")

StatsTab:AddToggle({text = "Ativar Auto Stats", flag = "AutoStats"}, function(state)
    AutoStats = state
    while AutoStats do
        task.wait(5)
        game.ReplicatedStorage.RemoteEvent:FireServer("UpgradeStat", "Strength")
        game.ReplicatedStorage.RemoteEvent:FireServer("UpgradeStat", "Ki")
        game.ReplicatedStorage.RemoteEvent:FireServer("UpgradeStat", "Defense")
    end
end)

--// Seção de Teleporte
local TeleportTab = Window:AddFolder("Teleporte")

TeleportTab:AddButton({text = "Teleportar para Arena"}, function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 100, 0)
end)

TeleportTab:AddButton({text = "Teleportar para NPCs"}, function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(500, 50, 500)
end)

--// Finalizando o Menu
Window:AddButton({text = "Fechar Menu"}, function()
    Library:Close()
end)

Library:Init()
