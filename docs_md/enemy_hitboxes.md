```luau
--!strict
local Zone = require("@game/ReplicatedStorage/SimplerZone")

local hitboxShape = Zone.shape.new("Box", CFrame.identity, vector.create(4, 6, 4))
local hitboxZone = Zone.new()

local listener = Zone.listener.new({
    groups = {Zone.defaultGroups.players},
    zones = {hitboxZone},
    precision = "BoundingBox",
    queryShape = "Point",
})

-- Tick damage while player overlaps the hitbox
listener:observe(function(item)
    local plr = item.player
    local character = item.model
    if not plr or not character then return end

    local humanoid = character:FindFirstChildWhichIsA("Humanoid")

    print(`[Hitbox] {plr.Name} entered {enemy.Name}'s attack range`)

    local connection = game:GetService("RunService").Heartbeat:Connect(function()
        if humanoid and humanoid.Health > 0 then
            humanoid:TakeDamage(damage)
        end
    end)

    return function()
        connection:Disconnect()
        print(`[Hitbox] {plr.Name} escaped {enemy.Name}'s attack range`)
    end
end)

-- Attach a damage hitbox to a single enemy NPC
local function attachEnemyHitbox(enemy: Model, damage: number)
    local rootAttach = assert(enemy:FindFirstChild("RootAttachment", true))

    local shapeInst = Zone.shapeInstance.new(hitboxShape)

    -- Keep the shape synced as the enemy moves
    shapeInst:syncWithAttachment(rootAttach)
    shapeInst:attach(hitboxZone)
    hitboxZone:rebuild()
end

-- Example: attach hitbox to every enemy in workspace.Enemies
for _, enemy in workspace.Enemies:GetChildren() do
    if enemy:IsA("Model") then
        attachEnemyHitbox(enemy, 5) -- 5 damage per heartbeat tick
    end
end
```