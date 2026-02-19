```luau
--!strict
local Zone = require("@game/ReplicatedStorage/SimplerZone")
local Players = game:GetService("Players")

-- Build zone from all parts inside workspace.SafeZone
local shapeInstances = {}
for _, part in workspace.SafeZone:GetChildren() do
    assert(part:IsA("BasePart"))
    table.insert(shapeInstances, Zone.shapeInstance.fromPart(part))
end

local safeZone = Zone.new(shapeInstances)

local listener = Zone.listener.new({
    groups = { Zone.defaultGroups.players },
    zones = { safeZone },
    precision = "BoundingBox",
    queryShape = "Point",
})

listener:observe(function(item)
    local plr = item.player
    if not plr then return end

    -- Grant invincibility on enter
    plr:SetAttribute("InSafeZone", true)
    print(`[SafeZone] {plr.Name} is now protected`)

    return function()
        -- Revoke invincibility on exit
        plr:SetAttribute("InSafeZone", false)
        print(`[SafeZone] {plr.Name} left protection`)
    end
end)
```