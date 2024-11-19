
local player = game.Players.LocalPlayer
local c3 = Color3.fromHex("FF00F3") 
local connections = {}

local function hawk_tuah(pe)

    if pe:IsA("ParticleEmitter") or pe:IsA("Trail") then
        pe.Color = ColorSequence.new(c3)
        if not pe.LightEmission then
            pe.LightEmission = 1 
        end

    elseif pe:IsA("Decal") then
        pe.Color3 = Color3.new(c3.R + 0.33, c3.G + 0.33, c3.B + 0.33)

    elseif pe:IsA("Light") then
        pe.Color = c3
    end
end

local function rizz(char)
   
    local weapons = {
        "#KATANAWEAPON",
        "#NinjaKATANA",
        "#BATWEAPON"
    }
    
    for _, weaponName in ipairs(weapons) do
        local weapon = char:FindFirstChild(weaponName)
        if weapon then
            for _, pe in weapon:GetDescendants() do
                hawk_tuah(pe)
            end
            table.insert(connections, weapon.DescendantAdded:Connect(hawk_tuah))
        end
    end

 
    for _, pe in char:GetDescendants() do
        hawk_tuah(pe)
    end

    table.insert(connections, char.DescendantAdded:Connect(hawk_tuah))
end

local function onPlayerAdded(player)
    if player:IsA("Model") then
        rizz(player)
    else
        rizz(player.Character or player.CharacterAdded:Wait())
        table.insert(connections, player.CharacterAdded:Connect(rizz))
    end
end


onPlayerAdded(player)
