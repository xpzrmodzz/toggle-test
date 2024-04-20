local teleportEnabled = false -- Initialisation de l'état du basculement

local function teleportToDummy()
    local dummy2 = workspace.MAP:FindFirstChild("5k_dummies").Dummy2
    if dummy2 then
        game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(dummy2.HumanoidRootPart.CFrame)
    else
        print("Le Dummy2 n'existe pas.")
    end
end

local function toggleTeleport()
    teleportEnabled = not teleportEnabled -- Inversion de l'état du basculement
    if teleportEnabled then
        print("Téléportation activée.")
    else
        print("Téléportation désactivée.")
    end
end

local function sendToServer()
    while teleportEnabled do -- Exécuter seulement si la téléportation est activée
        wait()
        local dummy2 = workspace.MAP:FindFirstChild("5k_dummies").Dummy2
        if dummy2 then
            local args = {
                [1] = dummy2.Humanoid,
                [2] = 1
            }
            game:GetService("ReplicatedStorage").jdskhfsIIIllliiIIIdchgdIiIIIlIlIli:FireServer(unpack(args))
        else
            print("Le Dummy2 n'existe pas.")
        end
    end
end

-- Commande pour basculer l'état de la téléportation
toggleTeleport()

-- Exécuter la fonction d'envoi au serveur dans un thread séparé
coroutine.wrap(sendToServer)()
