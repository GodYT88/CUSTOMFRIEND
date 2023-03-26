local PlaceID = game.PlaceId
if PlaceID == 11606818992 then
if not _G.FlingStatus then
    _G.FlingStatus = false
        game:GetService("Players").LocalPlayer.PlayerGui.Menu.TA.Visible = true
        game:GetService("Players").LocalPlayer.PlayerGui.Menu.TA.TextSize = 5
game:GetService("UserInputService").InputBegan:connect(function(Key,Chat)
    if not Chat then
        if Key.KeyCode == Enum.KeyCode.E then
            if _G.FlingStatus == true then
                _G.FlingStatus = false
            elseif _G.FlingStatus == false then
                _G.FlingStatus = true
            end
        elseif Key.KeyCode == Enum.KeyCode.F then
            if _G.FlingStatus == true then
                if game.Players.LocalPlayer.Character.Torso.CanCollide == false then
                    local OwnLadder = game:GetService("Workspace").playerPlaced[tostring(game.Players.LocalPlayer.Name .. "_ladder")]
                    OwnLadder.Main.BodyPosition.Position = game.Players.LocalPlayer.Character.HumanoidRootPart.Position+Vector3.new(0,1,0)
                end
            end
        end
    end
end)

while wait() do
    if game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored == true then
        local OwnLadder = game:GetService("Workspace").playerPlaced[tostring(game.Players.LocalPlayer.Name .. "_ladder")]
        OwnLadder.Main.BodyPosition.Position = game.Players.LocalPlayer.Character.HumanoidRootPart.Position+Vector3.new(0,-5000,0)
    end
end

game:GetService("Workspace").playerPlaced.ChildAdded:connect(function(part)
    if part.Name == tostring(game.Players.LocalPlayer.Name .. "_ladder") then
        if _G.FlingStatus == true then
            wait(0.25)
        local PartPosition = part.Main.Position
        local Fling = Instance.new("BodyPosition" , part.Main)
        Fling.Position = PartPosition
        Fling.MaxForce = Vector3.new(9e99,9e99,9e99)
        Fling.P = 100000
        local Fling2 = Instance.new("BodyAngularVelocity" , part.Main)
        Fling2.P = 9e99
        Fling2.MaxTorque = Vector3.new(0,9e99,0)
        Fling2.AngularVelocity = Vector3.new(0,75,0)
        local BodyGyro = Instance.new("BodyGyro" , part.Main)
        BodyGyro.CFrame = BodyGyro.CFrame * CFrame.Angles(math.rad(180),math.rad(90),math.rad(90))
        BodyGyro.MaxTorque = Vector3.new(40000,1000,40000)
        BodyGyro.CFrame = BodyGyro.CFrame * CFrame.Angles(0,math.rad(90),0)
        end
    end
end)

while wait() do
    local OnOff = game:GetService("Players").LocalPlayer.PlayerGui.Menu.TA
    if _G.FlingStatus == true then
        OnOff.TextColor3 = Color3.fromRGB(0,255,0)
        OnOff.Text = "Status Fling : On"
    elseif _G.FlingStatus == false then
        OnOff.TextColor3 = Color3.fromRGB(255,0,0)
        OnOff.Text = "Status Fling : Off"
    end
end

end
end
