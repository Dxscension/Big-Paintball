-- GUI --
if game.PlaceId == 155615604 then
    local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
    local Window = Library.CreateLib("Prison Life", "Sentinel")


    -- MAIN
    local Main = Window:NewTab("Main")
    local MainSection = Main:NewSection("Main")

    MainSection:NewDropdown("Give Gun:", "Gives the player the chosen gun", {"M9", "Remington 870", "AK-47"}, function(v)
        local A_1 = game:GetService("Workspace")["Prison_ITEMS"].giver[v].ITEMPICKUP
        local Event = game:GetService("Workspace").Remote.ItemHandler
        Event:InvokeServer(A_1)
        wait(0.5)
        Section:NewLabel("Give Gun:")
    end)

    MainSection:NewDropdown("Give Hand Item:", "Gives the player the chosen item", {"Crude Knife", "Hammer"}, function(v)
        local A_1 = game:GetService("Workspace")["Prison_ITEMS"].single[v].ITEMPICKUP
        local Event = game:GetService("Workspace").Remote.ItemHandler
        Event:InvokeServer(A_1)
        wait(0.5)
        Section:NewLabel("Give Hand Item:")
    end)


    MainSection:NewDropdown("Gun Modify: (laggy)", "This Will Modify The Firerate Of The Gun You Chose", {"M9", "Remington 870", "AK-47"}, function(v)
        local module = nil
        if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(v) then
            module = require(game:GetService("Players").LocalPlayer.Backpack[v].GunStates)
        elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild(v) then
            module = require(game:GetService("Players").LocalPlayer.Character[v].GunStates)
        end
        if module ~= nil then
            module["MaxAmmo"] = math.huge
            module["CurrentAmmo"] = math.huge
            module["StoredAmmo"] = math.huge
            module["FireRate"] = 0.001
            module["Spread"] = 0
            module["Range"] = math.huge
            module["Bullets"] = 10
            module["ReloadTime"] = 0.000001
            module["AutoFire"] = true
        end
        wait(0.5)
        Section:NewLabel("Gun Modify:")
    end)

    -- PLAYER
    local Player = Window:NewTab("Player")
    local PlayerSection = Player:NewSection("Player")

    PlayerSection:NewSlider("Walkspeed", "Changes the player walkspeed", 250, 16, function(v)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = v
    end)

    PlayerSection:NewSlider("Jumppower", "Changes the player jumppower", 250, 50, function(v)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = v
    end)

    PlayerSection:NewSlider("Gravity", "Changes the player gravity", 10, 196.2, function(v)
        game.Workspace.Gravity = v
    end)

    PlayerSection:NewButton("'E' To Noclip", "This Function Makes You Noclip", function()
        noclip = false
        game:GetService('RunService').Stepped:Connect(function()
            if noclip then
                game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                
            end
        end)
        
        local p = game.Players.LocalPlayer
        local mo = p:GetMouse()
        
        mo.KeyDown:Connect(function(k)
            if k == 'e' then
                noclip = not noclip
                p.Character.Humanoid:ChangeState(11)
            end
        end)
    end)



    PlayerSection:NewButton("'Q' To Fly", "This Function Makes You Fly", function()
        
    

repeat wait() until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("Torso") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid")
local mouse = game.Players.LocalPlayer:GetMouse()
repeat wait() until mouse
  local plr = game.Players.LocalPlayera
  local torso = plr.Character.Torso
  local flying = true
  local deb = true
  local ctrl = {f = 0, b = 0, l = 0, r = 0}
  local lastctrl = {f = 0, b = 0, l = 0, r = 0}
  local maxspeed = 50
  local speed = 0

  function Fly()
    local bg = Instance.new("BodyGyro", torso)
    bg.P = 9e4
    bg.maxTorque = Vector3.new(9e9, 9e9, 9e9)
    bg.cframe = torso.CFrame
    local bv = Instance.new("BodyVelocity", torso)
    bv.velocity = Vector3.new(0,0.1,0)
    bv.maxForce = Vector3.new(9e9, 9e9, 9e9)
    repeat wait()
      if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then
        speed = speed+.5+(speed/maxspeed)
        if speed > maxspeed then
          speed = maxspeed
        end
      elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then
        speed = speed-1
        if speed < 0 then
          speed = 0
        end
      end
      if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then
        bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
        lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r}
      elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then
        bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
      else
        bv.velocity = Vector3.new(0,0.1,0)
      end
      bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0)
    until not flying
    ctrl = {f = 0, b = 0, l = 0, r = 0}
    lastctrl = {f = 0, b = 0, l = 0, r = 0}
    speed = 0
    bg:Destroy()
    bv:Destroy()
  end
  mouse.KeyDown:connect(function(key)
  if key:lower() == "q" then
    if flying then flying = false
  else
    flying = true
    Fly()
  end
elseif key:lower() == "w" then
  ctrl.f = 1
elseif key:lower() == "s" then
  ctrl.b = -1
elseif key:lower() == "a" then
  ctrl.l = -1
elseif key:lower() == "d" then
  ctrl.r = 1
end
end)
mouse.KeyUp:connect(function(key)
if key:lower() == "w" then
  ctrl.f = 0
elseif key:lower() == "s" then
  ctrl.b = 0
elseif key:lower() == "a" then
  ctrl.l = 0
elseif key:lower() == "d" then
  ctrl.r = 0
end
end)
Fly()
         
 end)

-- Tems
local neutrale = false
function pee()
    local o = game.Players.LocalPlayer
    if neutrale == true then
        if o.Character.Health == 0 then
        o.TeamColor = BrickColor.new("Bright orange")
        o.Character.Humanoid.Health = 0
        neutrale = false
        else
            wait(0.3)
            pee()
        end

    end 
end
    local teams = Window:NewTab("Teams")
    local teamsSection = teams:NewSection("Teams")

    teamsSection:NewButton("Inmates", "This Functions Puts You On Inmates Team", function()
        local o = game.Players.LocalPlayer
        o.Character.HumanoidRootPart.CFrame = CFrame.new(888.399658, 97.1383057, 2388.50073, -1, 0, 0, 0, 1, 0, 0, 0, -1)
        o.TeamColor = BrickColor.new("Bright orange")
        o.Character.Humanoid.Health = 0
    end)

    teamsSection:NewButton("Guards", "This Functions Puts You On Inmates Team", function()
        local o = game.Players.LocalPlayer
        o.TeamColor = BrickColor.new("Bright blue")
        
    end)

    teamsSection:NewButton("Criminals", "This Functions Puts You On Criminals Team", function()
        local o = game.Players.LocalPlayer
        o.Character.HumanoidRootPart.CFrame = CFrame.new(-975.896118, 107.223793, 2044.90454, 0, 0, -1, 0, 1, 0, 1, 0, 0)
        o.TeamColor = BrickColor.new("Really red")
       
    end)


    teamsSection:NewButton("Neutral Team", "This Function Puts You On Neutral Team", function()
        neutrale = true
        local o = game.Players.LocalPlayer
        o.TeamColor = BrickColor.new("Medium stone grey")
        pee()
 
     end)

     teamsSection:NewButton("Fix Team Bugs", "This Functions Fix The Neutral Bug", function()
        local o = game.Players.LocalPlayer
        o.TeamColor = BrickColor.new("Bright orange")
        o.Character.Humanoid.Health = 0
    end)


  -- MISC
  local mesc = Window:NewTab("Teleports")
  local mescSection = mesc:NewSection("Teleports")
  local plr = game.Players.LocalPlayer

  mescSection:NewButton("Prision Yard", "This Teleports You To The Prision Yard", function()
    plr.Character.HumanoidRootPart.CFrame = CFrame.new(742.999756, 95.1383057, 2520.5, 1, 0, 0, 0, 1, 0, 0, 0, 1)
    wait(0.5)
end)

mescSection:NewButton("Criminal Base", "This Teleports You To The Criminal Base", function()
    plr.Character.HumanoidRootPart.CFrame = CFrame.new(-975.896118, 107.223793, 2044.90454, 0, 0, -1, 0, 1, 0, 1, 0, 0)
    wait(0.5)
  
end)

mescSection:NewButton("Nexus", "This Teleports You To The Local Spawn", function()
    plr.Character.HumanoidRootPart.CFrame = CFrame.new(888.399658, 97.1383057, 2388.50073, -1, 0, 0, 0, 1, 0, 0, 0, -1)
    wait(0.5)
end)

mescSection:NewButton("Cafeteria", "This Teleports You To The Cafeteria", function()
    plr.Character.HumanoidRootPart.CFrame = CFrame.new(875.049805, 96.9333496, 2287.5498, 0, 0, -1, 0, 1, 0, 1, 0, 0)
    wait(0.5)
end)


    -- NINJA LEGENDS
elseif game.PlaceId == 3956818381 then
    local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
    local Window = Library.CreateLib("Ninja Legends", "Sentinel")


    -- MAIN
    local Main = Window:NewTab("Main")
    local MainSection = Main:NewSection("Main")

    MainSection:NewToggle("Auto Swing", "Make your player autoswing", function(v)
        getgenv().autoswing = v
        while true do
            if not getgenv().autoswing then return end
            for _,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                if v:FindFirstChild("ninjitsuGain") then
                    game.Players.LocalPlayer.Character.Humanoid:EquipTool(v)
                    break
                end
            end
            local A_1 = "swingKatana"
            local Event = game:GetService("Players").LocalPlayer.ninjaEvent
            Event:FireServer(A_1)
            wait(0.1)
        end
    end)

    MainSection:NewToggle("Auto Sell", "Makes your player autosell", function(v)
        getgenv().autosell = v
        while true do
            if getgenv().autoswing == false then return end
            game:GetService("Workspace").sellAreaCircles["sellAreaCircle16"].circleInner.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
            wait(0.1)
            game:GetService("Workspace").sellAreaCircles["sellAreaCircle16"].circleInner.CFrame = CFrame.new(0,0,0)
            wait(0.1)
        end
    end)

    
    MainSection:NewToggle("Auto buy all swords", "Auto buys all swords", function(v)
        getgenv().buyswords = v
        while true do
            if not getgenv().buyswords then return end
            local A_1 = "buyAllSwords"
            local A_2 = "Blazing Vortex Island"
            local Event = game:GetService("Players").LocalPlayer.ninjaEvent
            Event:FireServer(A_1, A_2)
            wait(0.5)
        end
    end)


    MainSection:NewToggle("Auto buy all skills", "Auto buys all skills", function(v)
        getgenv().buyswords = v
        while true do
            if not getgenv().buyswords then return end
            local A_1 = "buyAllSkills"
            local A_2 = "Blazing Vortex Island"
            local Event = game:GetService("Players").LocalPlayer.ninjaEvent
            Event:FireServer(A_1, A_2)
            wait(0.5)
        end
    end)

    MainSection:NewToggle("Auto buy all belts", "Auto buys all belts", function(v)
        getgenv().buybelts = v
        while true do
            if not getgenv().buybelts then return end
            local A_1 = "buyAllBelts"
            local A_2 = "Blazing Vortex Island"
            local Event = game:GetService("Players").LocalPlayer.ninjaEvent
            Event:FireServer(A_1, A_2)
            wait(0.5)
        end
    end)


    MainSection:NewButton("Unlock all islands", "Unlocks all islands", function()
        local oldcframe = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        for _,v in pairs(game:GetService("Workspace").islandUnlockParts:GetChildren()) do
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame
            wait(0.1)
        end
        wait(0.1)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcframe
    end)

end
