local PlaceID = game.PlaceId
if PlaceID == 11606818992 then
if not _G.FlingStatus then
    spawn(function()
    _G.FlingStatus = false
    _G.SpinPower = 25
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
        elseif Key.KeyCode == Enum.KeyCode.R then
            if not game:GetService("Workspace").playerPlaced[tostring(game.Players.LocalPlayer.Name .. "_ladder")].Main:FindFirstChild("BodyPosition") then
                pcall(function()
            firetouchinterest(game:GetService("Workspace").Map.SpecialParts.lava , game:GetService("Workspace").playerPlaced[tostring(game.Players.LocalPlayer.Name .. "_ladder")].Main , 0)
                end)
            end
        elseif Key.KeyCode == Enum.KeyCode.T then
            if _G.SpinPower >= 1000 then
            _G.SpinPower = _G.SpinPower + 250
            else
                _G.SpinPower = _G.SpinPower + 25
            end
        elseif Key.KeyCode == Enum.KeyCode.Y then
            if _G.SpinPower >= 1000 then
            _G.SpinPower = _G.SpinPower - 250
            else
                _G.SpinPower = _G.SpinPower - 25
            end
        end
    end
end)

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
        Fling2.AngularVelocity = Vector3.new(0,_G.SpinPower,0)
        local BodyGyro = Instance.new("BodyGyro" , part.Main)
        BodyGyro.CFrame = BodyGyro.CFrame * CFrame.Angles(math.rad(180),math.rad(90),math.rad(90))
        BodyGyro.MaxTorque = Vector3.new(40000000,10000,40000000)
        BodyGyro.CFrame = BodyGyro.CFrame * CFrame.Angles(0,math.rad(90),0)
        end
    end
end)

while wait() do
    local OnOff = game:GetService("Players").LocalPlayer.PlayerGui.Menu.TA
    if _G.FlingStatus == true then
        OnOff.TextColor3 = Color3.fromRGB(0,255,0)
        if _G.SpinPower <= 9999 then
        OnOff.Text = "Status Fling : On".." "..tostring("Power :".._G.SpinPower)
        else
        OnOff.Text = "Status Fling : On".." "..tostring("Power :".._G.SpinPower).." Max"
        end
    elseif _G.FlingStatus == false then
        OnOff.TextColor3 = Color3.fromRGB(255,0,0)
        if _G.SpinPower <= 9999 then
        OnOff.Text = "Status Fling : Off".." "..tostring("Power :".._G.SpinPower)
        else
        OnOff.Text = "Status Fling : Off".." "..tostring("Power :".._G.SpinPower).." Max"
        end
    end
end
end)
spawn(function()
while wait() do
    pcall(function()
    if game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored == true then
        local OwnLadder = game:GetService("Workspace").playerPlaced[tostring(game.Players.LocalPlayer.Name .. "_ladder")]
        OwnLadder.Main.BodyPosition.Position = game.Players.LocalPlayer.Character.HumanoidRootPart.Position+Vector3.new(0,5000,0)
    end
    end)
end
end)

spawn(function()
while wait() do
    if _G.SpinPower >= 10001 then
        _G.SpinPower = 50
    elseif _G.SpinPower <= 0 then
        _G.SpinPower = 25
    end
end
end)
end
elseif PlaceID == 12004594806 then
local Mercury = loadstring(game:HttpGet("https://raw.githubusercontent.com/deeeity/mercury-lib/master/src.lua"))()

local GUI = Mercury:Create{
    Name = "GodY Hub",
    Size = UDim2.fromOffset(600, 400),
    Theme = Mercury.Themes.Dark,
    Link = ""
}

local Main = GUI:Tab{
	Name = "Main",
	Icon = "rbxassetid://8569322835"
}

Main:Textbox{
    Name = "Select Player : Beli",
    Callback = function(Name)
    if Name ~= "" then
local Target = tostring(Name)
local A = 0
for i,v in pairs(game:GetService("Players"):GetChildren()) do
    if string.find(v.Name , Target) then
        if A == 0 then
        game:GetService("ReplicatedStorage"):WaitForChild("GiveMoney"):FireServer(game:GetService("Players")[v.Name] , -game:GetService("Players")[v.Name].Data.Beli.Value)
        A = A + 1
        end
elseif string.find(string.lower(v.Name) , string.lower(Target)) then
    if A == 0 then
        game:GetService("ReplicatedStorage"):WaitForChild("GiveMoney"):FireServer(game:GetService("Players")[v.Name] , -game:GetService("Players")[v.Name].Data.Beli.Value)
        A = A + 1
    end
elseif string.find(v.DisplayName , Target) then
    if A == 0 then
        game:GetService("ReplicatedStorage"):WaitForChild("GiveMoney"):FireServer(game:GetService("Players")[v.Name] , -game:GetService("Players")[v.Name].Data.Beli.Value)
        A = A + 1
    end
elseif string.find(string.lower(v.DisplayName) , string.lower(Target)) then
    if A == 0 then
        game:GetService("ReplicatedStorage"):WaitForChild("GiveMoney"):FireServer(game:GetService("Players")[v.Name] , -game:GetService("Players")[v.Name].Data.Beli.Value)
        A = A + 1
    end
end
end
    end
    end
}

Main:Textbox{
    Name = "Select Player : Gem",
    Callback = function(Name)
    if Name ~= "" then
local Target = tostring(Name)
local A = 0
for i,v in pairs(game:GetService("Players"):GetChildren()) do
    if string.find(v.Name , Target) then
        if A == 0 then
        game:GetService("ReplicatedStorage"):WaitForChild("GiveGem"):FireServer(game:GetService("Players")[v.Name] , -game:GetService("Players")[v.Name].Data.Gem.Value)
        A = A + 1
        end
elseif string.find(string.lower(v.Name) , string.lower(Target)) then
    if A == 0 then
        game:GetService("ReplicatedStorage"):WaitForChild("GiveGem"):FireServer(game:GetService("Players")[v.Name] , -game:GetService("Players")[v.Name].Data.Gem.Value)
        A = A + 1
    end
elseif string.find(v.DisplayName , Target) then
    if A == 0 then
        game:GetService("ReplicatedStorage"):WaitForChild("GiveGem"):FireServer(game:GetService("Players")[v.Name] , -game:GetService("Players")[v.Name].Data.Gem.Value)
        A = A + 1
    end
elseif string.find(string.lower(v.DisplayName) , string.lower(Target)) then
    if A == 0 then
        game:GetService("ReplicatedStorage"):WaitForChild("GiveGem"):FireServer(game:GetService("Players")[v.Name] , -game:GetService("Players")[v.Name].Data.Gem.Value)
        A = A + 1
    end
end
end
    end
    end
}

Main:Button{
	Name = "Random DF : Free",
	Description = nil,
	Callback = function() 
	        local RarityTable = {
        [1] = "Common",
        [2] = "Uncommon",
        [3] = "Epic",
        [4] = "Legendary"
    }
    local Rarity = math.random(1,4)
    for i,v in pairs(RarityTable) do
        if i == Rarity then
    local args = {
    [1] = v
}

game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui"):WaitForChild("SpinGui"):WaitForChild("LOL"):WaitForChild("Spin"):WaitForChild("Spin"):WaitForChild("Reward"):FireServer(unpack(args))
        end
    end
	end
}
end
