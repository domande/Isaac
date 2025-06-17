-- Defina a localização dos NPCs que você deseja farmar (você precisa ajustar as coordenadas)
local npcName = "Bandit"  -- Nome do NPC (Exemplo: Bandit, Marine, etc.)

-- Definir a distância máxima do NPC que você vai atacar
local distance = 50

-- Função para buscar e atacar o NPC
function AttackNPC()
    while true do
        local npc = nil
        -- Encontrar o NPC mais próximo
        for _, enemy in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
            if enemy.Name == npcName then
                local dist = (enemy.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
                if dist < distance then
                    npc = enemy
                    break
                end
            end
        end
        
        -- Se encontrar o NPC, atacar
        if npc then
            local humanoid = npc:FindFirstChildOfClass("Humanoid")
            if humanoid then
                -- Executar ataque (ajuste o tipo de ataque conforme necessário)
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetWeapon", game.Players.LocalPlayer.Backpack:FindFirstChildOfClass("Tool").Name)
                humanoid.Health = humanoid.Health - 10  -- Ajuste o valor do dano conforme necessário
            end
        end
        
        -- Aguardar um pouco antes de continuar a busca
        wait(1)
    end
end

-- Começar a atacar automaticamente
AttackNPC()
