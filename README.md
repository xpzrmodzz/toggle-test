-- Variable pour suivre l'état du toggle
local toggleActif = false
local teleportationEffectuee = false

-- Fonction de téléportation au Dummy2
local function teleportToDummy()
    -- Vérification si le Dummy2 existe
    local dummy2 = workspace.MAP:FindFirstChild("5k_dummies").Dummy2
    if dummy2 then
        -- Téléportation au Dummy2
        game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(dummy2.HumanoidRootPart.CFrame)
    else
        -- Message d'erreur si le Dummy2 n'est pas trouvé
        print("Le Dummy2 n'existe pas.")
    end
end

-- Fonction pour envoyer des données au serveur
local function sendDataToServer()
    -- Vérification si le toggle est activé
    if toggleActif then
        -- Données à envoyer au serveur
        local args = {
            [1] = workspace.MAP:FindFirstChild("5k_dummies").Dummy2.Humanoid,
            [2] = 1
        }

        -- Envoi des données au serveur
        game:GetService("ReplicatedStorage").jdskhfsIIIllliiIIIdchgdIiIIIlIlIli:FireServer(unpack(args))
    end
end

-- Activer ou désactiver le toggle
local function toggle()
    if not toggleActif then
        toggleActif = true
        teleportToDummy() -- Téléporter uniquement lorsque le toggle est activé pour la première fois
    else
        toggleActif = false
    end
end

-- Boucle de mise à jour
while true do
    wait(0) -- Attendre 1 seconde entre chaque envoi de données
    sendDataToServer()
end
