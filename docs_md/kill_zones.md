```luau
--!strict
local Zone = require("@game/ReplicatedStorage/SimplerZone")

-- Build zone from all parts inside workspace.KillZone
local shapeInstances = {}
for _, part in workspace.KillZone:GetChildren() do
    assert(part:IsA("BasePart"))
    table.insert(shapeInstances, Zone.shapeInstance.fromPart(part))
end

local killZone = Zone.new(shapeInstances)

local listener = Zone.listener.new({
    groups = {Zone.defaultGroups.players},
    zones = {killZone},
    precision = "Part", -- If any part of the player touches the killzone it should register
    queryShape = "Box", -- Detect the whole part, not just the center
})

listener:onEnter(function(item)
    local plr = item.player
    local character = item.model
    if not plr or not character then return end

    -- Kill the player immediately on entry
    local humanoid = character:FindFirstChildWhichIsA("Humanoid")
    if humanoid then
        humanoid.Health = 0
        print(`[KillZone] {plr.Name} was eliminated`)
    end
end)
```