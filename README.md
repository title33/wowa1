local args = {
    [1] = "Melee",
    [2] = 1
}

local player = game.Players.LocalPlayer
if player then
    local remote = game:GetService("ReplicatedStorage").Remote.Other.upstats
    if remote then
        remote:FireServer(unpack(args))
    end
end

-- ServerScript

game:GetService("ReplicatedStorage").Remote.Other.upstats.OnServerEvent:Connect(function(targetPlayer, args)
    -- เพิ่มค่า IntValue ของผู้เล่น
    local IntValue = targetPlayer:FindFirstChild("IntValue")
    if IntValue then
        if targetPlayer:HasPermission("upstats") then
            IntValue.Value = IntValue.Value + args[2]
        end
    end
end)
