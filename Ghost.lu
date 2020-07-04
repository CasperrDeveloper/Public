local startTick=tick()
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local HttpService = game:GetService("HttpService")
local TPS = game:GetService("TeleportService")
local Client = Players.LocalPlayer
local Character = Client.Character or Client.CharacterAdded:Wait()
local Toggle={}
local Data={}

local gameMeta = getrawmetatable(game)

local Index,Namecall,Newindex = gameMeta.__index,gameMeta.__namecall,gameMeta.__newindex

local a={}_G.commands=a;local b=';'local c=game:GetService("ReplicatedStorage")handler={}setmetatable(handler,{__index=function(d)return handler[d]end})function handler:addcommand(e,f)if not a[e]then a[e]=f end end;function handler:parsecommand(e,g)if a[e]then local f=a[e]return f(g or{})end end;function handler:initiate(h)h.Chatted:connect(function(i)if i:sub(1,#b)==b then i=i:lower():sub(#b+1)for e,j in next,a do if i:sub(1,#e)==e:lower()then local g=string.split(i," ")table.remove(g,1)local k=handler:parsecommand(e,g)if k then wait(0.5) game.StarterGui:SetCore("SendNotification",{Title="Ghost Admin",Text=k,Icon="",Duration=5}) end end end else return false end end)end

local function newInstance(class,Extra) --extra args
	local object = Instance.new(class)
	for idx,ti in next,Extra do
		object[idx]=ti
	end
	return object
end

local function getState(gay)
    if gay then
        return "enabled"
    else
        return "disabled"
    end
end

local function Notify(msg)
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = "Ghost Admin";
        Text = msg;
        Icon = ""; 
        Duration = 5;
    })
end

local function cacheTable(t)
    local cached={}
    for i,v in next,t do
        cached[i]=v
    end
    return cached
end

KeyDown=setmetatable({},{
    __index=function(t,k)
        if UserInputService:IsKeyDown(Enum.KeyCode[k]) then
            return true
        else
            return false;
        end
    end
})

local function findplayer(String)
    local Found = {}
    local strl = String:lower()
    for i,v in pairs(Players:GetPlayers()) do
    	if v.Name:lower():sub(1, #String) == String:lower() then
    		table.insert(Found,v)
    	end
   	end 
	return Found[1]
end

setreadonly(gameMeta,false)

gameMeta.__index=function(self,k)
    if not checkcaller() then
        if k=="WalkSpeed" then
            return 15.9;
        end
        if k=="HipHeight" then
            return 2;
        end
        if k=="JumpPower" then
            return 0;
        end
        if k=="StateChanged" then
            return Instance.new("Part").Touched;
        end
        if k=="FireServer" then
            return newcclosure(function(...)
                local args={...}
                if args[2]=="hey" then
                    return wait(9e9)
                end
                return Index(self,k)(...)
            end)
        end
        if k=="HumanoidRootPart" then
            k="Head"
        end
        if k=="Anchored" then
            return false
        end
        if k=="Hit" and Toggle.aimlock then
            if Players:GetPlayerFromCharacter(Client:GetMouse().Target.Parent) then
                if Data.aimlocktarget~=Client:GetMouse().Target.Parent then
                    rawset(Data,"aimlocktarget",Client:GetMouse().Target.Parent)
                    Notify(string.format("Aimlock target set to %s.",tostring(Data.aimlocktarget)));
                    spawn(function()
                        wait(10)
                        rawset(Data,"aimlocktarget",nil)
                    end)
                end
            end
            -- if Data.aimlocktarget and (Client.Character.Torso.Position-Data.aimlocktarget.Torso.Position).magnitude<90 and Data.aimlocktarget:FindFirstChild("KO").Value>5 then
            --     return (Data.aimlocktarget.Torso.CFrame + Data.aimlocktarget.Torso.Velocity / 5)
            -- else
            --     return Index(self,k)
            -- end
        end
    end
    return Index(self,k)
end

gameMeta.__newindex=function(self,k,v)
    if not checkcaller() then
        if k=="WalkSpeed" and UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) then
            return Newindex(self,k,Data.speed or 80)
        end
        if k=="WalkSpeed" and v==0 and Toggle.noslow then
            return nil;
        end
        if k=="Anchored" then
            return nil;
        end
        if k=="Health" and v==0 then
            return nil;
        end
        if k=="JumpPower" and v==0 then
            return nil;
        end
        if k=="CFrame" and tostring(self)=="HumanoidRootPart" then
            return nil;
        end
        if k=="CFrame" and tostring(self)=="Torso" then
            return nil;
        end
        if k=="JumpPower" and Toggle.superjump then
            v=100;
        end
    end
    return Newindex(self,k,v)
end

gameMeta.__namecall=newcclosure(function(self,...)
    local args={...}
    if not checkcaller() then
        if getnamecallmethod()=="BreakJoints" then
            return newcclosure(function() end)
        end
        if getnamecallmethod()=="SetStateEnabled" then
            return newcclosure(function() end)
        end
        if getnamecallmethod()=="GetDescendants" then
            return wait(9e9)
        end
        if getnamecallmethod()=="ClearAllChildren" then
            return function() return {} end
        end
        if getnamecallmethod()=="WaitForChild" then
            if args[1]=="HumanoidRootPart" then
                args[1]="Torso"
                return Namecall(self,unpack(args))
            end
        end
        if getnamecallmethod()=="Destroy" and tostring(self)=="Head" then
            return nil
        end
        if getnamecallmethod()=="FireServer" and (args[1]=="m1" or args[1]=="moff1") and Data.aimlocktarget then
            local copy=cacheTable(args[2])
            if Data.aimlocktarget and (Client.Character.Torso.Position-Data.aimlocktarget.Torso.Position).magnitude<200 then
                rawset(copy,"mousehit",(Data.aimlocktarget.Torso.CFrame + Data.aimlocktarget.Torso.Velocity / 5))
                rawset(copy,"velo",0)
                args[2]=copy;
                return Namecall(self,unpack(args))
            end
        end
        if getnamecallmethod()=="FireServer" and args[1]=="play" then
            args[2]=string.rep('\n',450)..args[2]-- adding better anti logger next --
            spawn(function()
                Notify("audio is being protected...")
            end)
            return Namecall(self,unpack(args))
        end
    end
    return Namecall(self,...)
end)

for i,v in next,getgc() do
    if type(v)=="function" then        
        for idx,val in next,debug.getupvalues(v) do
            if type(val)=="function" and val==Instance.new("RemoteEvent").FireServer then
                local backup=val;
                debug.setupvalue(v,idx,newcclosure(function(...)
                    local args={...}
                    if args[2]=="hey" then
                        return wait(9e9)
                    end
                    return val(unpack(args))
                end))
            end
        end
    end
end

handler:addcommand("noslow",function()
    Toggle.noslow=not Toggle.noslow
    return string.format("noslow has been %s", getState(Toggle.noslow))
end)

handler:addcommand("sword",function()
    local idx=0;
    for _,obj in next,Client.Character:GetDescendants() do
        if obj:IsA("Accessory") and obj:FindFirstChild("Handle") and obj.Handle:FindFirstChildWhichIsA("DataModelMesh").MeshId=="rbxassetid://4315410540" then
            local Handle=obj.Handle;
            Handle.Massless=true
    
            Handle:FindFirstChildWhichIsA("Attachment"):Destroy()
            Handle:FindFirstChildWhichIsA("Weld"):Destroy()
    
            newInstance("AlignPosition",{
                Parent=Handle,
                Attachment0=newInstance("Attachment",{
                    Parent=Handle,
                    Orientation=Vector3.new(0,90,0)
                }),
                Attachment1=newInstance("Attachment",{Parent=Client.Character:FindFirstChildWhichIsA("Tool").Handle,Position=Vector3.new(0,1.5,0)}),
                RigidityEnabled=true,
                Responsiveness=200
            })
            Client.Character:FindFirstChildWhichIsA("Tool").Grip=CFrame.new()
            newInstance("AlignOrientation",{
                Parent=Handle,
                Attachment0=newInstance("Attachment",{Parent=Handle}),
                Attachment1=newInstance("Attachment",{Parent=Client.Character:FindFirstChildWhichIsA("Tool").Handle,Orientation=Vector3.new(0, 25, -135)}),
                RigidityEnabled=true,
                Responsiveness=150
            })
            idx=idx+1
        end
    end
    if idx<1 then
        return string.format("you need the sword...")
    else
        return string.format("attempted to get sword...")
    end
end)

handler:addcommand("noanim",function()
    Toggle.noanim=not Toggle.noanim
    coroutine.wrap(function()
        while Toggle.noanim and RunService.Heartbeat:Wait() do
            for _,anim in next,Client.Character.Humanoid:GetPlayingAnimationTracks() do
                if tostring(anim)=="WalkAnim" then
                 anim:Stop()
                end
             end
        end
    end)()
    return string.format("noanim has been %s", getState(Toggle.noanim))
end)

handler:addcommand("fly",function()
    Toggle.fly=not Toggle.fly
    coroutine.wrap(function()
        while Toggle.fly and RunService.RenderStepped:Wait() do
            Client.Character.Humanoid:ChangeState(3)
        end
    end)()
    return string.format("fly has been %s", getState(Toggle.fly))
end)

handler:addcommand("setpov",function(args)
    if #args~=1 then return "Please specify number..." end
    workspace.CurrentCamera.FieldOfView=tonumber(args[1])
    return string.format("pov has been set to %s.", tostring(args[1]))
end)

handler:addcommand("aimlock",function()
    Toggle.aimlock=not Toggle.aimlock
    return string.format("aimlock has been %s", getState(Toggle.aimlock))
end)

handler:addcommand("superjump",function()
    Toggle.superjump=not Toggle.superjump
    return string.format("superjump has been %s", getState(Toggle.superjump))
end)

handler:addcommand("airwalk",function()
    Toggle.airwalk=not Toggle.airwalk
    coroutine.wrap(function()
        while Toggle.airwalk and RunService.RenderStepped:Wait() do
            Client.Character.Humanoid.JumpPower=1
            Client.Character.Humanoid:ChangeState(3)
            wait()
            Client.Character.Humanoid:ChangeState(11)
        end
    end)()
    return string.format("airwalk has been %s", getState(Toggle.airwalk))
end)

handler:addcommand("stealaudio",function(args)
    if #args~=1 then return "Please specify player..." end
    local target=findplayer(args[1])
    if target then
        for _,obj in next,target.Character:GetDescendants() do
            if tostring(obj)=="SoundX" then
                local soundId=obj.SoundId:sub(obj.SoundId:find('://')+3)
                setclipboard(soundId)
                return string.format("Audio: %s",tostring(soundId))
            end
        end
    else
        return "player not found..."
    end
end)

handler:addcommand("serverhop",function()
    local function fetchServers(filter)
        local rawText = game:HttpGet(string.format("https://www.roblox.com/games/getgameinstancesjson?placeId=%s&startIndex=0",game.PlaceId))
        local jsonData = HttpService:JSONDecode(rawText).Collection

        for i,v in next,jsonData do
            if #v.CurrentPlayers<v.Capacity then
                table.remove(jsonData,i)
            end
        end
        
        if filter then
            for i,v in next,jsonData do
                if v.Ping>=90 then
                    table.remove(jsonData,i)
                end
            end  
        end
        return jsonData
    end
    local serverCollection = fetchServers(true)
    local randomServer = serverCollection[math.random(#serverCollection)]
    TPS:TeleportToPlaceInstance(game.PlaceId,randomServer.Guid,Client)
end)

handler:addcommand("cmds",function()
    warn("command list")
    for name,func in next,_G.commands do
        print(name)
    end
    return string.format("%s commands in console.", tostring(#_G.commands))
end)

handler:addcommand("goto",function(args)
    if #args~=1 then return "Please specify player..." end
    local target=findplayer(args[1])
    if target then
        Toggle.noclip=true
        if Toggle.tpbypass then
            Client.Character.Torso.CFrame=target.Character.Torso.CFrame
        else
            coroutine.wrap(function()
                local tween=game:GetService("TweenService"):Create(Client.Character.HumanoidRootPart,TweenInfo.new(2.5,Enum.EasingStyle.Quad),{CFrame=target.Character.Torso.CFrame});
                tween:Play();
                Toggle.noclip=false
            end)()
        end
    else
        return "player not found..."
    end
    return string.format("teleporting to %s", tostring(target))
end)

handler:addcommand("tpbypass",function()
    Toggle.tpbypass=not Toggle.tpbypass
    coroutine.wrap(function()
        while RunService.Stepped:Wait() and Toggle.tpbypass do
            if Client.Character and Client.Character:FindFirstChild("HumanoidRootPart") then
                Client.Character.HumanoidRootPart.Parent=nil
            end
        end
    end)()
    Client.Character:BreakJoints()
    return string.format("teleport bypass %s.",getState(Toggle.tpbypass))
end)

handler:addcommand("setspeed",function(args)
    if #args~=1 then return "Please specify speed..." end
    if tonumber(args[1])==nil then return "Invalid speed..." end
    rawset(Data,"speed",tonumber(args[1]))
    return string.format("speed has been set to %s.", tostring(args[1]))
end)

handler:addcommand("god",function(args)
    Toggle.god=not Toggle.god;
    coroutine.wrap(function()
        while RunService.Stepped:Wait() and Toggle.god do
            if game.PlaceId==455366377 then
                if Client.Character and Client.Character:FindFirstChild("HumanoidRootPart") then
                    Client.Character["HumanoidRootPart"].Parent=nil
                end
            else
                if Client.Character and Client.Character:FindFirstChild("Right Leg") then
                    Client.Character["Right Leg"].Parent=nil
                end
            end
        end
    end)()
    Client.Character:BreakJoints();
    return string.format("god has been %s.",getState(Toggle.god))
end)

handler:addcommand("rejoin",function(args)
    coroutine.wrap(function()
        wait(1.5)
        game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId,game.JobId)
    end)()
    return string.format("Please wait... rejoining.")
end)

handler:addcommand("triggerbot",function()
    Toggle.triggerbot=not Toggle.triggerbot
    coroutine.wrap(function()
        while Toggle.triggerbot and RunService.RenderStepped:Wait() do
            if Client:GetMouse().Target~=nil and Players:GetPlayerFromCharacter(Client:GetMouse().Target.Parent) then
                if Client:GetMouse().Target.Parent:FindFirstChild("KO") and Client:GetMouse().Target.Parent:FindFirstChild("KO").Value>3 then
                    mouse1click();
                end
            end
        end
    end)()
    return string.format("triggerbot has been %s", getState(Toggle.triggerbot))
end)

handler:addcommand("camlock",function()
    Toggle.camlock=not Toggle.camlock
    coroutine.wrap(function()
        while RunService.RenderStepped:Wait() and Toggle.camlock do
            
        end
    end)()
    return string.format("camlock has been %s", getState(Toggle.camlock))
end)

handler:addcommand("swimfly",function()
    Toggle.swimfly=not Toggle.swimfly
    coroutine.wrap(function()
        while RunService.RenderStepped:Wait() and Toggle.swimfly do
            if Client.Character then
                Client.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Swimming)
            end
        end
    end)()
    return string.format("swimfly has been %s", getState(Toggle.swimfly))
end)

handler:addcommand("noclip",function()
    Toggle.noclip = not Toggle.noclip;
    coroutine.wrap(function()
        while RunService.Stepped:Wait() and Toggle.noclip do
            if Client.Character then
                for _,obj in next,Client.Character:GetDescendants() do
                    if obj:IsA("BasePart") and obj.CanCollide then
                        obj.CanCollide=false
                    end
                end
            end
        end
    end)()
    return string.format("noclip has been %s.",getState(Toggle.noclip))
end)

handler:addcommand("heal",function()
    local origPos=Client.Character.Torso.CFrame
    for idx,obj in next,workspace:GetChildren() do
        if obj:IsA("Model") and tostring(obj):find("|") then
            local itemData={
                name=obj.Name:sub(1,obj.Name:find("|")-2),
                price=tonumber(obj.Name:sub(obj.Name:find("|")+3)),
                CFrame=obj.Head.CFrame
            }
            if itemData.name:lower()=="burger" or itemData.name:lower()=="drink" then
                if tonumber(Client.PlayerGui.HUD.Cash.Text:sub(2))>=itemData.price then
                    if not Toggle.tpbypass then
                        repeat 
                            Client.Character.Humanoid.Jump=true
                            Client.Character.Humanoid.AutoRotate=false
                            Client.Character.Humanoid.Sit=true
                            Client.Character.Humanoid.PlatformStand=true
                            Client.Character.HumanoidRootPart.CFrame=itemData.CFrame;
                            RunService.RenderStepped:Wait()
                        until Client.Backpack:FindFirstChild(itemData.name)
                        
                        Client.Character.HumanoidRootPart.CFrame=origPos
                        Client.Character.Humanoid.AutoRotate=true
                        Client.Character.Humanoid.Sit=false
                        Client.Character.Humanoid.PlatformStand=false
                    else
                        local origCFrame=Client.Character.Torso.CFrame
                        repeat 
                            Client.Character.Humanoid.AutoRotate=false
                            Client.Character.Humanoid.Sit=true
                            Client.Character.Humanoid.PlatformStand=true
                            Client.Character.Torso.CFrame=itemData.CFrame
                            RunService.RenderStepped:Wait()
                        until Client.Backpack:FindFirstChild(itemData.name)

                        Client.Character.Torso.CFrame=origPos
                        Client.Character.Humanoid.AutoRotate=true
                        Client.Character.Humanoid.Sit=false
                        Client.Character.Humanoid.PlatformStand=false
                    end
                    for _,k in next,Client.Backpack:GetChildren() do
                        if k:IsA("Tool") and ({["Burger"]=true,["Drink"]=true})[tostring(k)] then
                            k.Parent=Client.Character
                            k:Activate()
                        end
                    end
                end
            end
        end
    end
end)

handler:addcommand("buy",function(args)
    if #args~=1 then return "Please specify item..." end
    local foundItem;

    for idx,obj in next,workspace:GetChildren() do
        if obj:IsA("Model") and tostring(obj):find("|") then
            local itemData={
                name=obj.Name:sub(1,obj.Name:find("|")-2),
                price=tonumber(obj.Name:sub(obj.Name:find("|")+3)),
                CFrame=obj.Head.CFrame
            }
            if itemData.name:lower():find(args[1]:lower()) then
                foundItem=itemData;
                break;
            end
        end
    end

    if foundItem then
        if tonumber(Client.PlayerGui.HUD.Cash.Text:sub(2))>=foundItem.price then
            if not Toggle.tpbypass then
            repeat 
                Client.Character.Humanoid.Jump=true
                Client.Character.Humanoid.AutoRotate=false
                Client.Character.Humanoid.Sit=true
                Client.Character.Humanoid.PlatformStand=true
                Client.Character.HumanoidRootPart.CFrame=foundItem.CFrame;
                RunService.RenderStepped:Wait()
            until Client.Backpack:FindFirstChild(foundItem.name)
                Client.Character.Humanoid.AutoRotate=true
                Client.Character.Humanoid.Sit=false
                Client.Character.Humanoid.PlatformStand=false
            else
                local origCFrame=Client.Character.Torso.CFrame
                repeat 
                    Client.Character.Humanoid.AutoRotate=false
                    Client.Character.Humanoid.Sit=true
                    Client.Character.Humanoid.PlatformStand=true
                    Client.Character.Torso.CFrame=foundItem.CFrame
                    RunService.RenderStepped:Wait()
                until Client.Backpack:FindFirstChild(foundItem.name)
                Client.Character.Humanoid.AutoRotate=true
                Client.Character.Humanoid.Sit=false
                Client.Character.Humanoid.PlatformStand=false
                Client.Character.Torso.CFrame=origCFrame
            end
        
            return string.format("Got %s.", foundItem.name)
        else
            return "Could not afford item...";
        end
    end
end)

handler:addcommand("reset",function()
    Client.Character:BreakJoints()
end)

handler:initiate(Client);

setreadonly(gameMeta,true)

local rdMove=coroutine.create(function()
    while RunService.RenderStepped:Wait() do
        if Client.Character and Client.Character:FindFirstChild("KO") then
            if Client.Character:FindFirstChild("KO").Value<=3 then
                Client.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Swimming)
            end
        end
    end
end)

local detectThread=coroutine.create(function()
    local lastDetected;
    while wait(0.25) do
        for _,plr in next,game:GetService("Players"):GetPlayers() do
            if plr~=Client and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                local rootPart=plr.Character:FindFirstChild("HumanoidRootPart")
                local Velocity=math.floor(rootPart.Velocity.magnitude)

                if plr.Character.Humanoid:GetState()==Enum.HumanoidStateType.Running and not plr.Character.Humanoid.PlatformStand and not plr.Character.Humanoid.Sit  then
                    if Velocity>50 and plr.Character:FindFirstChild("KO").Value>4.5 then
                        warn(plr.Character.Humanoid:GetState())
                        lastDetected=plr;
                        Notify(string.format("Strange Velocity detected: %s",tostring(plr)))
                    end
                end
                
                if not plr.Character:FindFirstChild("Right Leg") then
                    lastDetected=plr;
                    Notify(string.format("Godmode detected: %s",tostring(plr)))
                end
            end
        end
    end
end)

local characterThread=coroutine.create(function()
    while RunService.Heartbeat:Wait() do
        for i,v in next,workspace:FindFirstChild("Live"):GetChildren() do
            if Players:FindFirstChild(tostring(v)) then
                v.Parent=workspace
            end
        end
    end
end)

if workspace:FindFirstChild'Armoured Truck' then 
    local Part = Instance.new("Part", workspace)
    Part.Name,Part.Color,Part.CFrame,Part.Size,Part.Material,Part.Anchored = "TP Region",Color3.fromRGB(196,40,28),CFrame.new(-136.858002,0,-523.700012),Vector3.new(9.93,1,20.31),"ForceField",true
    workspace:FindFirstChild'Armoured Truck':Destroy()
elseif workspace:FindFirstChild'TPer' then
    local Part = Instance.new("Part", workspace)
    Part.Name,Part.Color,Part.CFrame,Part.Size,Part.Material,Part.Anchored = "TP Region",Color3.fromRGB(196,40,28),CFrame.new(-31,-0.2,221),Vector3.new(12,1,6),"ForceField",true
    workspace:FindFirstChild'TPer':Destroy()
end

coroutine.resume(rdMove)
coroutine.resume(detectThread)
coroutine.resume(characterThread)

Notify(string.format("Loaded\nTook %s seconds to load.",tostring(tick()-startTick)))