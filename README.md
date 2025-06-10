-- Carregar Rayfield UI Library
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
    Name = "Rayfield Hub",
    LoadingTitle = "Rayfield Hub",
    LoadingSubtitle = "by SeuNome",
    ConfigurationSaving = {
        Enabled = true,
        FolderName = "RayfieldHubConfig",
        FileName = "Config"
    }
})

local MainTab = Window:CreateTab("Principal", 4483362458)

-- Função para criar botão para arma (giver)
local function criarBotaoArma(nomeArma)
    MainTab:CreateButton({
        Name = "Teleportar para o 2º filho da " .. nomeArma,
        Callback = function()
            local player = game.Players.LocalPlayer
            local char = player.Character or player.CharacterAdded:Wait()
            local giver = workspace:FindFirstChild("Prison_ITEMS")
                and workspace.Prison_ITEMS:FindFirstChild("giver")
                and workspace.Prison_ITEMS.giver:FindFirstChild(nomeArma)
            if giver then
                local children = giver:GetChildren()
                if #children >= 2 and char and char:FindFirstChild("HumanoidRootPart") then
                    local obj = children[2]
                    if obj:IsA("BasePart") then
                        char.HumanoidRootPart.CFrame = obj.CFrame + Vector3.new(0, 2, 0)
                        Rayfield:Notify({
                            Title = "Rayfield Hub",
                            Content = "Você foi teleportado para o 2º filho da " .. nomeArma .. "!",
                            Duration = 4
                        })
                    else
                        Rayfield:Notify({
                            Title = "Rayfield Hub",
                            Content = "O segundo filho não é um BasePart.",
                            Duration = 4
                        })
                    end
                else
                    Rayfield:Notify({
                        Title = "Rayfield Hub",
                        Content = "Não foi possível encontrar o segundo filho.",
                        Duration = 4
                    })
                end
            else
                Rayfield:Notify({
                    Title = "Rayfield Hub",
                    Content = "Não foi possível encontrar a " .. nomeArma .. ".",
                    Duration = 4
                })
            end
        end,
    })
end

-- Adicione suas armas aqui
criarBotaoArma("AK-47")
criarBotaoArma("M9")
criarBotaoArma("Remington 870")
-- Basta repetir para outras armas, exemplo:
-- criarBotaoArma("NOME_DA_ARMA")

-- NOVO BOTÃO: Teleportar para o 5º filho do Crude Knife (SINGLE)
MainTab:CreateButton({
    Name = "Teleportar para o 5º filho do Crude Knife",
    Callback = function()
        local player = game.Players.LocalPlayer
        local char = player.Character or player.CharacterAdded:Wait()
        local crude = workspace:FindFirstChild("Prison_ITEMS")
            and workspace.Prison_ITEMS:FindFirstChild("single")
            and workspace.Prison_ITEMS.single:FindFirstChild("Crude Knife")
        if crude then
            local children = crude:GetChildren()
            if #children >= 5 and char and char:FindFirstChild("HumanoidRootPart") then
                local obj = children[5]
                if obj:IsA("BasePart") then
                    char.HumanoidRootPart.CFrame = obj.CFrame + Vector3.new(0, 2, 0)
                    Rayfield:Notify({
                        Title = "Rayfield Hub",
                        Content = "Você foi teleportado para o 5º filho do Crude Knife!",
                        Duration = 4
                    })
                else
                    Rayfield:Notify({
                        Title = "Rayfield Hub",
                        Content = "O 5º filho não é um BasePart.",
                        Duration = 4
                    })
                end
            else
                Rayfield:Notify({
                    Title = "Rayfield Hub",
                    Content = "Não foi possível encontrar o 5º filho.",
                    Duration = 4
                })
            end
        else
            Rayfield:Notify({
                Title = "Rayfield Hub",
                Content = "Não foi possível encontrar o Crude Knife.",
                Duration = 4
            })
        end
    end,
})

-- NOVO BOTÃO: Teleportar para o Hammer se prisonerOnly e ITEMPICKUP existirem
MainTab:CreateButton({
    Name = "Teleportar para o Hammer (prisonerOnly, ITEMPICKUP)",
    Callback = function()
        local player = game.Players.LocalPlayer
        local char = player.Character or player.CharacterAdded:Wait()
        local hammer = workspace:FindFirstChild("Prison_ITEMS")
            and workspace.Prison_ITEMS:FindFirstChild("single")
            and workspace.Prison_ITEMS.single:FindFirstChild("Hammer")
        if hammer
            and hammer:FindFirstChild("prisonerOnly")
            and hammer:FindFirstChild("ITEMPICKUP")
            and char
            and char:FindFirstChild("HumanoidRootPart")
        then
            local obj = hammer.ITEMPICKUP
            if obj:IsA("BasePart") then
                char.HumanoidRootPart.CFrame = obj.CFrame + Vector3.new(0, 2, 0)
                Rayfield:Notify({
                    Title = "Rayfield Hub",
                    Content = "Você foi teleportado para o Hammer (ITEMPICKUP)!",
                    Duration = 4
                })
            else
                Rayfield:Notify({
                    Title = "Rayfield Hub",
                    Content = "ITEMPICKUP não é um BasePart.",
                    Duration = 4
                })
            end
        else
            Rayfield:Notify({
                Title = "Rayfield Hub",
                Content = "Não foi possível encontrar Hammer com prisonerOnly e ITEMPICKUP.",
                Duration = 4
            })
        end
    end,
})
