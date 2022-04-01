
--[[Local Whitelist.]]--
game.StarterGui:SetCore("SendNotification", {
    Title = "WHITELIST";
    Text = "Checking if player is whitelisted...";
    Icon = "";
    Duration = 4;
        })
wait(2)
local LPR = game:GetService("Players").LocalPlayer
local Whitelisted = {
    [496721656] = true; -- crpyt
    [340544469] = true; -- csu
    [710195933] = true; --kos
    [193003759] = true; cory

}
    if Whitelisted[LPR.UserId] then
        game.StarterGui:SetCore("SendNotification", {
            Title = "WHITELIST";
            Text = "Player is whitelisted!";
            Icon = "";
            Duration = 2;
                })
    else
    LPR:Kick("You not whitelist kid")
    end

local function ChatSpy()
    local StarterGui = game:GetService("StarterGui")
    repeat wait() until StarterGui:GetCore("ChatWindowSize") ~= nil
    local chatWindowSize = StarterGui:GetCore("ChatWindowSize")
    StarterGui:SetCore("ChatWindowPosition", UDim2.new(0, 0, 0.414965987, 0))
    enabled = true
	spyOnMyself = true
	public = false
	publicItalics = false
	privateProperties = {
		Color = Color3.fromRGB(87, 198, 235); 
		Font = Enum.Font.SourceSansBold;
		TextSize = 18;
	}
	local StarterGui = game:GetService("StarterGui")
	local Players = game:GetService("Players")
	local player = Players.LocalPlayer or Players:GetPropertyChangedSignal("LocalPlayer"):Wait() or Players.LocalPlayer
	local saymsg = game:GetService("ReplicatedStorage"):WaitForChild("DefaultChatSystemChatEvents"):WaitForChild("SayMessageRequest")
	local getmsg = game:GetService("ReplicatedStorage"):WaitForChild("DefaultChatSystemChatEvents"):WaitForChild("OnMessageDoneFiltering")
	local instance = (_G.chatSpyInstance or 0) + 1
	_G.chatSpyInstance = instance

	local function onChatted(p,msg)
		if _G.chatSpyInstance == instance then
			if p==player and msg:lower():sub(1,4)=="/spy" then
				enabled = not enabled
				wait()
				privateProperties.Text = "{SPY "..(enabled and "EN" or "DIS").."ABLED}"
				StarterGui:SetCore("ChatMakeSystemMessage",privateProperties)
			elseif enabled and (spyOnMyself==true or p~=player) then
				msg = msg:gsub("[\n\r]",''):gsub("\t",' '):gsub("[ ]+",' ')
				local hidden = true
				local conn = getmsg.OnClientEvent:Connect(function(packet,channel)
					if packet.SpeakerUserId==p.UserId and packet.Message==msg:sub(#msg-#packet.Message+1) and (channel=="All" or (channel=="Team" and public==false and Players[packet.FromSpeaker].Team==player.Team)) then
						hidden = false
					end
				end)
				wait(1)
				conn:Disconnect()
				if hidden and enabled then
					if public then
						saymsg:FireServer((publicItalics and "/me " or '').."{SPY} [".. p.Name .."]: "..msg,"All")
					else
						privateProperties.Text = "{SPY} [".. p.Name .."]: "..msg
						StarterGui:SetCore("ChatMakeSystemMessage",privateProperties)
					end
				end
			end
		end
	end

	for _,p in ipairs(Players:GetPlayers()) do
		p.Chatted:Connect(function(msg) onChatted(p,msg) end)
	end
	Players.PlayerAdded:Connect(function(p)
		p.Chatted:Connect(function(msg) onChatted(p,msg) end)
	end)
	privateProperties.Text = "{SPY "..(enabled and "EN" or "DIS").."ABLED}"
	StarterGui:SetCore("ChatMakeSystemMessage",privateProperties)
	if not player.PlayerGui:FindFirstChild("Chat") then wait(3) end
	local chatFrame = player.PlayerGui.Chat.Frame
	chatFrame.ChatChannelParentFrame.Visible = true
	chatFrame.ChatBarParentFrame.Position = chatFrame.ChatChannelParentFrame.Position+UDim2.new(UDim.new(),chatFrame.ChatChannelParentFrame.Size.Y)
end
ChatSpy()

game.Players:Chat("CSU ADMIN")

print([[

Prison Admin

Version 2.0

Prefix = "!"

CSU GANG's ADMIN
-------------------------------------------------------------------------
Locals:
[1] Ws/WalkSpeed/Speed, - Chnages the players walkspeed
[2] Noclip, - Allows you to walk through walls
[3] Jp/JumpPower, - Changes the players JumpPower
[4] Reset/Re/Res, - Resets player
[5] Goto, - Teleport to a players
[6] BlinkSpeed/Bs, - Sets runspeed
=========================================================================
Combat:
[7] Camlock/Cl/Cml/Cam, - Locks camera onto target 
[8] Aimlock/Target/Shoot/Al/Aim/Aimbot, - Locks bullets onto target
[9] UnCamlock/UnCl/UnCml/UnCam, - Turns off camlock 
[10] UnAimlock/UnTarget/UnShoot/UnAl/UnAim/UnAimbot, - Turns off aimlock
[11] Hvh, - Makes your hitbox smaller
[12] UnHvh, - Turns off hvh
[13] Kill, - Beta for testing but kills target
[14] Kill all, - Kills everyone in the server
[15] SpinCam, - Sometimes breaks other peoples camlock
[16] UnSpinCam, - Turns off spincam
[17] Esp/Find, - Toggles esp 
[18] UnEsp/Unfind, - Turns off esp
[19] GunAnims, - Chnages the gun animation
[20] GodMode/UnGodMode, - Makes you invincible
[21] FlySpeed/Fs, - Sets flyspeed
=========================================================================
Extra:
[22] AntiFe, - Makes you immune to fe bots or feloopers
[23] Bypass, - Can go as fast as you want permanently
[24] Sit, - Useless just makes you sit
[25] Droptools/dt, - Drops equipped tool
[26] AntiGrab, - Breaks feloopers grab fling
[27] OgRun, - Gives you old run animation
[28] Sky1, - Changes sky Background
[29] Sky2, - Changes sky Background
[30] View/Unview, - View/Unviews a player
[31] RemoveSeats/Rs/NoSeats/Ns, - Stops you from sitting permanently
[32] NoDoors/RemoveDoors/Nds/rds, - Remove doors
[33] AutoReset/AutoRe/Ar, - Resets you when ko'd
[34] Fov, - Changes your fieldofview
[35] Wg/WeldGun, - Enables bfg
[35] InvisGun/Ivg, - Makes gun invisible
=========================================================================
Coming soon:
Infinte Ammo, - Alt account with guns needed
Triggerbot, - Working on
Gui Settings, - Gui with toggable commands
GunSkins Gui, - Gui with gun colors
=========================================================================
KeyBinds:
Fly - "F"
Noclip - "X"
HitBox - "H"
TrashTalk - "T"
Reset - "R"
AntiAim - "G"
AutoShoot - "E"
-------------------------------------------------------------------------

Made by Cryptid_God
]])



	local LoadingTime = tick();
local Commands, Prefix = {}, ""
getgenv().Notify = function(title, text, icon, time)
    game:GetService("StarterGui"):SetCore("SendNotification",{
        Title = title;
        Text = text;
        Icon = "";
        Duration = time;
    }) 
end

getgenv().SearchPlayers = function(Name)
    local Inserted = {}
        for _, p in pairs(game:GetService("Players"):GetPlayers()) do 
        if string.lower(string.sub(p.Name, 1, string.len(Name))) == string.lower(Name) then 
            table.insert(Inserted, p);return p
        end
    end
end


getgenv().GetInit = function(CName)
    for _, v in next, Commands do 
        if v.Name == CName or table.find(v.Aliases, CName) then 
            return v.Function 
        end 
    end
end

getgenv().RunCommand = function(Cmd)
    Cmd = string.lower(Cmd)
    pcall(function()
        if Cmd:sub(1, #Prefix) == Prefix then 
            local Args = string.split(Cmd:sub(#Prefix + 1), " ")
            local CmdName = GetInit(table.remove(Args, 1))
            if CmdName and Args then
                return CmdName(Args)
            end
        end
    end)
end

local HealthBarGui = Instance.new("ScreenGui")
local HealthBar = Instance.new("Frame")
local GreenFrame = Instance.new("Frame")
local HealthStatus = Instance.new("TextLabel")
local lol = Instance.new("TextLabel")

--Properties:

HealthBarGui.Name = "HealthBarGui"
HealthBarGui.Parent = game.CoreGui
HealthBarGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

HealthBar.Name = "HealthBar"
HealthBar.Parent = HealthBarGui
HealthBar.AnchorPoint = Vector2.new(0, 0.5)
HealthBar.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
HealthBar.BackgroundTransparency = 1.000
HealthBar.BorderColor3 = Color3.fromRGB(255, 255, 255)
HealthBar.BorderSizePixel = 2
HealthBar.Position = UDim2.new(0.550999999, 0, 0.736999989, 0)
HealthBar.Size = UDim2.new(0.200000003, 0, 0.0500000007, 0)

GreenFrame.Name = "GreenFrame"
GreenFrame.Parent = HealthBar
GreenFrame.AnchorPoint = Vector2.new(0, 0.5)
GreenFrame.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
GreenFrame.BackgroundTransparency = 1.000
GreenFrame.BorderSizePixel = 0
GreenFrame.Position = UDim2.new(0, 0, 0.5, 0)
GreenFrame.Size = UDim2.new(1, 0, 1, 0)

HealthStatus.Name = "HealthStatus"
HealthStatus.Parent = HealthBar
HealthStatus.AnchorPoint = Vector2.new(0.5, 0.5)
HealthStatus.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
HealthStatus.BackgroundTransparency = 1.000
HealthStatus.BorderSizePixel = 0
HealthStatus.Position = UDim2.new(-0.846, 0,1.082, 0)
HealthStatus.Size = UDim2.new(0, 235,0, 32)
HealthStatus.Font = Enum.Font.Gotham
HealthStatus.Text = "100"
HealthStatus.TextColor3 = Color3.fromRGB(255, 255, 0)
HealthStatus.TextSize = 59.000
HealthStatus.TextWrapped = true

lol.Name = "lol"
lol.Parent = HealthBar
lol.AnchorPoint = Vector2.new(0.5, 0.5)
lol.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
lol.BackgroundTransparency = 1.000
lol.BorderSizePixel = 0
lol.Position = UDim2.new(-1.293, 0,1.069, 0)
lol.Size = UDim2.new(0, 235,0, 45)
lol.Font = Enum.Font.Gotham
lol.Text = "Health:"
lol.TextColor3 = Color3.fromRGB(255, 255, 0)
lol.TextSize = 59.000
lol.TextWrapped = true

-- Scripts:

local function AUFLIT_fake_script() -- HealthBarGui.LocalScript 
	local script = Instance.new('LocalScript', HealthBarGui)

	-- Disable the healthbar
	game.StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Health,false)
	
	--Variables
	local player = game.Players.LocalPlayer
	local char = player.Character or player.CharacterAdded:Wait()
	
	local healthbar = script.Parent:WaitForChild("HealthBar")
	
	-- Updating the healthbar
	game:GetService("RunService").RenderStepped:Connect(function()
		local humanoid = char:FindFirstChild("Humanoid")
		healthbar.GreenFrame.Size = UDim2.new(humanoid.Health/humanoid.MaxHealth,0,1,0)
		healthbar.HealthStatus.Text = math.floor(game.Players.LocalPlayer.Character.Humanoid.Health)
	end)
end
coroutine.wrap(AUFLIT_fake_script)()

local ScreenGui = Instance.new("ScreenGui")
local TextLabel = Instance.new("TextLabel")

--Properties:



ScreenGui.Parent = game.CoreGui

TextLabel.Parent = ScreenGui
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1.000
TextLabel.Position = UDim2.new(0.550999999, 0, 0.736999989, 0)
TextLabel.Size = UDim2.new(0, 235,0, 50)
TextLabel.Font = Enum.Font.Gotham
TextLabel.Text = "Ammo: "
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 0)
TextLabel.TextSize = 59.000

local ScreenGui = Instance.new("ScreenGui")
local ClipsTxt = Instance.new("TextLabel")
local BulletsTxt = Instance.new("TextLabel")
ScreenGui.Parent = game.CoreGui
ClipsTxt.Name = "ClipsTxt"
ClipsTxt.Parent = ScreenGui
ClipsTxt.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ClipsTxt.BackgroundTransparency = 1.000
ClipsTxt.Position = UDim2.new(0, 0, 0.10211359, 0)
ClipsTxt.Size = UDim2.new(0, 200, 0, 50)
ClipsTxt.Font = Enum.Font.Gotham
ClipsTxt.Text = "Clips:"
ClipsTxt.TextColor3 = Color3.fromRGB(255,255,0)
ClipsTxt.TextSize = 24.000
ClipsTxt.Visible = false

BulletsTxt.Name = "BulletsTxt"
BulletsTxt.Parent = ScreenGui
BulletsTxt.BackgroundColor3 = Color3.fromRGB(255,255,0)
BulletsTxt.BackgroundTransparency = 1.000
BulletsTxt.Position = UDim2.new(0.551, 0,0.737, 0)
BulletsTxt.Size = UDim2.new(0, 235,0, 50)
BulletsTxt.Font = Enum.Font.Gotham
BulletsTxt.Text = "             "
BulletsTxt.TextColor3 = Color3.fromRGB(255,255,0)
BulletsTxt.TextSize = 59.000
BulletsTxt.Visible = false
game.Players.LocalPlayer.PlayerGui.HUD:FindFirstChild("Ammo"):Destroy()

function CustomAmmoUI()
local gunequipped = false
for _,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
	if v:IsA("Tool") then
        if v ~= nil then	
v.Equipped:Connect(function()
if v:FindFirstChild("Clips") and v:FindFirstChild("Ammo") then		
wait(.3)
ClipsTxt.Text = "Clips:"
BulletsTxt.Text = "              "		
gunequipped = true	
BulletsTxt.Visible = true
ClipsTxt.Visible = true
repeat	
BulletsTxt.Text = "             "..v:FindFirstChild("Ammo").Value..""
ClipsTxt.Text = "Clips: "..v:FindFirstChild("Clips").Value..""
game:GetService("RunService").Heartbeat:Wait()	
until gunequipped == false
else
return nil			
end				
end)
v.Unequipped:Connect(function()
ClipsTxt.Text = "Clips:"
BulletsTxt.Text = "             "
gunequipped = false	
BulletsTxt.Visible = false
ClipsTxt.Visible = false
end)
end			
end	
end	
end
CustomAmmoUI()
game.Players.LocalPlayer.Character.Humanoid.Died:Connect(function()
game.Players.LocalPlayer.Character.Humanoid:UnequipTools()
end)
game.Players.LocalPlayer.CharacterAdded:Connect(function()	
local hud = game.Players.LocalPlayer.PlayerGui:WaitForChild("HUD")
hud.Ammo:Destroy()
wait(1)
CustomAmmoUI()	
end)

local ScreenGui = Instance.new("ScreenGui")
local Cmdbar = Instance.new("TextBox")
local CmdbarARC = Instance.new("TextLabel")
local Frame = Instance.new("Frame")
local UIGradient = Instance.new("UIGradient")

coroutine.resume(coroutine.create(function()
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ResetOnSpawn = false

Cmdbar.Name = "Cmdbar"
Cmdbar.Parent = ScreenGui
Cmdbar.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Cmdbar.BorderColor3 = Color3.fromRGB(255,255,0)
Cmdbar.BorderSizePixel = 3
Cmdbar.Position = UDim2.new(0, 0,0.481, 0)
Cmdbar.Size = UDim2.new(0, 300,0, 20)
Cmdbar.SizeConstraint = Enum.SizeConstraint.RelativeYY
Cmdbar.Font = Enum.Font.SourceSansSemibold
Cmdbar.PlaceholderColor3 = Color3.fromRGB(255,255,0)
Cmdbar.Text = "!"
Cmdbar.TextColor3 = Color3.fromRGB(255,255,0)
Cmdbar.TextSize = 31.000
Cmdbar.TextWrapped = true
Cmdbar.TextXAlignment = Enum.TextXAlignment.Center
Cmdbar.Visible = false

CmdbarARC.Name = "CmdbarARC"
CmdbarARC.Parent = Cmdbar
CmdbarARC.BackgroundColor3 = Color3.fromRGB(255, 170, 255)
CmdbarARC.BorderColor3 = Color3.fromRGB(255, 255, 255)
CmdbarARC.BorderSizePixel = 3
CmdbarARC.Position = UDim2.new(-0.123076916, 0, 0, 0)
CmdbarARC.Size = UDim2.new({0, 12},{0, 32})
CmdbarARC.Font = Enum.Font.Code
CmdbarARC.Text = "!"
CmdbarARC.TextColor3 = Color3.fromRGB(255,255,0)
CmdbarARC.TextSize = 19.000
CmdbarARC.TextWrapped = true
CmdbarARC.Visible = true

Frame.Parent = Cmdbar
Frame.BackgroundColor3 = Color3.fromRGB(0,0,0)
Frame.BorderColor3 = Color3.fromRGB(255,255,0)
Frame.BorderSizePixel = 3
Frame.Position = UDim2.new(-0.123076923, 0, 0.972426474, 0)
Frame.Size = UDim2.new(0, 292, 0, 2)
Frame.Visible = false

UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(100,225,200)), ColorSequenceKeypoint.new(0.52, Color3.fromRGB(100,225,200)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(128,0,128))}
UIGradient.Parent = Frame
end))


local Uis = game:GetService("UserInputService")
Uis.InputBegan:Connect(function(Key, Typing)
    if Typing then return end
    if Key.KeyCode == Enum.KeyCode.Semicolon then
        Cmdbar.Visible = true
        Cmdbar.Text = "!"
        wait()
        Cmdbar:CaptureFocus()
        --Cmdbar:TweenSize(UDim2.new(0, 419, 0, 20), "Out", "Quad", 0.1, true)
    end
end)
Cmdbar.FocusLost:Connect(function(Foc)
    if Foc == true then
        Cmdbar.Visible = false
            RunCommand(Cmdbar.Text)
    end
end)
Uis.InputEnded:Connect(function(Key)
    if Key.KeyCode.Name == "LeftAlt" then
        Cmdbar.Visible = false
    end
end)

-- [[ locals ]] -- 
local Players, RService, RStorage, VUser, SGui, TPService = game:GetService("Players"), game:GetService("RunService"), game:GetService("ReplicatedStorage"), game:GetService("VirtualUser"), game:GetService("StarterGui"), game:GetService("TeleportService")
local Client, Mouse, Camera, CF, INew, Vec3, Vec2, UD2, UD = Players.LocalPlayer, Players.LocalPlayer:GetMouse(), workspace.CurrentCamera, CFrame.new, Instance.new, Vector3.new, Vector2.new, UDim2.new, UDim.new;
local Noclip, Blink, Esp, Flying, Noseats, GunAnims, AntiFe, TpBypass, Hitbox, WSpeed, JumpPower = false, false, false, false, false, false, false, false, false, false, false;
local Aimbot, Viewing, Camlock = false, false, false;
local AimbotTarget, ViewTarget, CamlockTarget, EspTarget = nil, nil, nil, nil;
local Flyspeed, Aimvelocity, Blinkspeed = 5, 10, 2;
local AimPart, CamPart = "Torso", "Torso";
local StreetsID, PrisonID = 8046624339, 4669040;
local Sit, Sort, DropTool, Gunanim2, Goto, NoDoors, Airwalk = false, false, false, false, false, false, false;
local antife2 = false;

-- [[ functions ]] -- 
local AimPartTable = {
    ["torso"] = "Torso";
    ["head"] = "Head";
}
local KeysTable = {
    ["W"] = false;["A"] = false;
    ["S"] = false;["D"] = false;
    ["LeftControl"] = false;["LeftShift"] = false;
}



local function ConfirmCallbacks()
    wait()
    SGui:SetCore("ResetButtonCallback", true)
end
ConfirmCallbacks()

getgenv().ResetCharacter = function()
    if Client and Client.Character and Client.Character:FindFirstChild("Humanoid") then 
        Client.Character.Humanoid:ChangeState(15)
    end
end


getgenv().EspPlayer = function(Dude)
    


	local bgui = Instance.new("BillboardGui", Dude.Character.Head)
	local tlabel = Instance.new("TextLabel", bgui)

	bgui.Name = "ESP"
	bgui.Adornee = part
	bgui.AlwaysOnTop = true
	bgui.ExtentsOffset = Vector3.new(0, 3, 0)
	bgui.Size = UDim2.new(0, 5, 0, 5)
	bgui.ResetOnSpawn = false

	tlabel.Name = "espTarget"
	tlabel.BackgroundColor3 = Color3.new(255, 255, 255)
	tlabel.BackgroundTransparency = 1
	tlabel.BorderSizePixel = 0
	tlabel.Position = UDim2.new(0, 0, 0, -30)
	tlabel.Size = UDim2.new(1, 0, 7, 0)
	tlabel.Visible = true
	tlabel.ZIndex = 10
	tlabel.Font = "SourceSansSemibold"
	tlabel.FontSize = "Size28"
	RService.RenderStepped:Connect(function()
		if Dude and Dude.Character and Dude.Character:FindFirstChildOfClass("Humanoid") then 
		    
			tlabel.Text = Dude.Name
			.." ("..math.floor(Dude.Character.Humanoid.Health)
			..")"
		end
	end)
	tlabel.TextColor3 = Color3.fromRGB(255,0,0)
	tlabel.TextStrokeTransparency = 0.5
end

local plr = game.Players.LocalPlayer
repeat wait() until plr.Character
local char = plr.Character

local garbage = {
    "Dog shct";
    "I own you";
    "Ez!";
    "Gg = Get Good";
    "How you lose?";
    "L";
    "So bad";
    "CSU gang on top";
    "Get looped skid";
    "Dont fold now";

}


function TrashTalk(inputObject, gameProcessedEvent)
    if inputObject.KeyCode == Enum.KeyCode.P and gameProcessedEvent == false then        
game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(
        garbage[math.random(1,#garbage)],
        "All"
    )
    end
end
 
game:GetService("UserInputService").InputBegan:connect(TrashTalk)

getgenv().togglefly = function()
    Flying = not Flying
    Notify("CSU GANG", "Flying: "..tostring(Flying), "", 3)
    local T = Client.Character:FindFirstChild("HumanoidRootPart") or Client.Character:FindFirstChild("Torso")
    local BV, BG = INew("BodyVelocity", T), INew("BodyGyro", T)
    BV.Velocity = Vec3(0, 0.1, 0);BV.MaxForce = Vec3(math.huge, math.huge, math.huge)
    BG.CFrame = T.CFrame;BG.P = 9e9;BG.MaxTorque = Vec3(9e9, 9e9, 9e9)
    local FlyPart = INew("Part", workspace)
    FlyPart.Anchored = true;FlyPart.Size = Vec3(6, 1, 6);FlyPart.Transparency = 1 
    
    while Flying == true and Client and Client.Character and Client.Character:FindFirstChild("Humanoid") and Client.Character.Humanoid.Health ~= 0 and RService.Heartbeat:Wait() and T do 
        local Front, Back, Left, Right = 0, 0, 0, 0
        if KeysTable["W"] == true then 
            Front = Flyspeed 
        elseif not KeysTable["W"] == true then
            Front = 0 
        end
        if KeysTable["A"] == true then 
            Right = -Flyspeed
        elseif not KeysTable["A"] == true then 
            Right = 0 
        end
        if KeysTable["S"] == true then 
            Back = -Flyspeed 
        elseif not KeysTable["S"] == true then 
            Back = 0
        end
        if KeysTable["D"] == true then 
            Left = Flyspeed
        elseif not KeysTable["D"] == true then 
            Left = 0
        end
        if tonumber(Front + Back) ~= 0 or tonumber(Left + Right) ~= 0 then 
            BV.Velocity = ((Camera.CoordinateFrame.lookVector * (Front + Back)) + ((Camera.CoordinateFrame * CF(Left + Right, (Front + Back) * 0.2, 0).p) - Camera.CoordinateFrame.p)) * 50
        else 
            BV.Velocity = Vec3(0, 0.1, 0)
        end
        BG.CFrame = Camera.CoordinateFrame
    end
    FlyPart:Destroy();BG:Remove();BV:Remove()
end

Uis.InputBegan:Connect(function(Key)
    if not (Uis:GetFocusedTextBox()) then
        if Key.KeyCode == Enum.KeyCode.W then 
            KeysTable["W"] = true 
        end 
        if Key.KeyCode == Enum.KeyCode.A then 
            KeysTable["A"] = true 
        end
        if Key.KeyCode == Enum.KeyCode.S then 
            KeysTable["S"] = true 
        end
        if Key.KeyCode == Enum.KeyCode.D then 
            KeysTable["D"] = true 
        end
        if Key.KeyCode == Enum.KeyCode.F then 
            if FirstFly == true then 
                Notify("CSU GANG v1", "You can now fly, like a bird.", "", 3)
                FirstFly = false 
            end
            togglefly()
        end
        if Key.KeyCode == Enum.KeyCode.X then 
            Noclip = not Noclip 
            Notify("CSU GANG", "Noclip: "..tostring(Noclip), "", 3)
        end
        if Key.KeyCode == Enum.KeyCode.LeftShift then
            KeysTable["LeftShift"] = true
            while Blink == true and KeysTable["LeftShift"] == true and Client and Client.Character and RService.Heartbeat:Wait() do
                local ClientRF = Client.Character:FindFirstChild("HumanoidRootPart") or Client.Character:FindFirstChild("Torso")
                local Hum = Client.Character:FindFirstChild("Humanoid")
                ClientRF.CFrame = ClientRF.CFrame + Vec3(Hum.MoveDirection.X * Blinkspeed, Hum.MoveDirection.Y * Blinkspeed, Hum.MoveDirection.Z * Blinkspeed)
            end 
        end
    end
end)
Uis.InputEnded:Connect(function(Key --[[Typing]])
    if not (Uis:GetFocusedTextBox()) then
        if Key.KeyCode == Enum.KeyCode.W then 
            KeysTable["W"] = false 
        end
        if Key.KeyCode == Enum.KeyCode.A then 
            KeysTable["A"] = false 
        end
        if Key.KeyCode == Enum.KeyCode.S then 
            KeysTable["S"] = false 
        end
        if Key.KeyCode == Enum.KeyCode.D then 
            KeysTable["D"] = false
        end
        if Key.KeyCode == Enum.KeyCode.LeftShift then
            KeysTable["LeftShift"] = false
        end
    end
end)

-- [[ Bypass ]] --
local rm = getrawmetatable(game) or debug.getrawmetatable(game) or getmetatable(game)
if setreadonly then setreadonly(rm, false) else make_writeable(rm, true) end
local caller, cscript = checkcaller or is_protosmasher_caller, getcallingscript or get_calling_script;
local rindex, nindex, ncall, closure = rm.__index, rm.__newindex, rm.__namecall, newcclosure or read_me;

rm.__newindex = closure(function(self, Meme, Val)
    if caller() then return nindex(self, Meme, Val) end 
    if game.PlaceId ~= (StreetsID) then 
        if Meme == "WalkSpeed" then 
            return 16
        end
        if Meme == "JumpPower" then 
            return 37.5 
        end
        if Meme == "HipHeight" then 
            return 0 
        end
        if Meme == "Health" then 
            return 100 
        end
    end
    if self:IsDescendantOf(Client.Character) and self.Name == "HumanoidRootPart" or self.Name == "Torso" then 
        if Meme == "CFrame" or Meme == "Position" or Meme == "Anchored" then 
            return nil 
        end
    end
    return nindex(self, Meme, Val) 
end)
rm.__namecall = closure(function(self, ...)
    local Args, Method = {...}, getnamecallmethod() or get_namecall_method();
    if Method == "BreakJoints" then 
        return wait(9e9)
    end
    if game.PlaceId ~= (StreetsID) then
        if Method == "FireServer" and not self.Name == "SayMessageRequest" then
            if tostring(self.Parent) == "ReplicatedStorage" or self.Name == "lIII" then 
                return wait(9e9) 
            end
            if Args[1] == "hey" then 
                return wait(9e9) 
            end
        end
        if Method == "FireServer" and self.Name == "Fire" and AimbotTarget ~= nil and Aimbot == true  then
            return ncall(self, AimbotTarget.Character[AimPart].CFrame + AimbotTarget.Character[AimPart].Velocity/Aimvelocity)
        end
    end
    if game.PlaceId == (StreetsID) then
        if Method == "FireServer" and Args[1] == "WalkSpeed" or Args[1] == "JumpPower" or Args[1] == "HipHeight" then 
            return nil 
        end
        if Method == "FireServer" and self.Name == "Input" then 
            if Args[1] == "bv" or Args[1] == "hb" or Args[1] == "ws" then 
                return wait(9e9)
            end
        end
        if Method == "FireServer" and self.Name == "Input" and AimbotTarget ~= nil and Aimbot == true then 
            Args[2].mousehit = AimbotTarget.Character[AimPart].CFrame + AimbotTarget.Character[AimPart].Velocity/Aimvelocity 
            Args[2].velo = math.huge
            return ncall(self, unpack(Args))
        end
    end
    return ncall(self, unpack(Args))
end)
if setreadonly then setreadonly(rm, true) else make_writeable(rm, false) end

-- [[ CharacterAdded/Died ]] --
Client.Character.Humanoid.Died:Connect(function()
    if Flying then togglefly() end
end)
Client.CharacterAdded:Connect(function()
    repeat wait() until Client.Character:FindFirstChild("Humanoid")
    Client.Character.Humanoid.Died:Connect(function()
        if Flying then togglefly() end
    end)
end)

local godmode = false
game:GetService('RunService').Stepped:connect(function()
    if godmode == true then
        if game.Players.LocalPlayer.Character ~= nil then
            if game.Players.LocalPlayer.Character:FindFirstChild("Right Leg") then
                game.Players.LocalPlayer.Character:FindFirstChild("Right Leg"):Destroy()
            end
        end
    end
end)


local hvh = false
game:GetService('RunService').Stepped:connect(function()
    if hvh == true then
        if game.Players.LocalPlayer.Character ~= nil then
            if game.Players.LocalPlayer.Character:FindFirstChild("Right Leg") then
                game.Players.LocalPlayer.Character:FindFirstChild("Right Leg"):Destroy()
                end
                if game.Players.LocalPlayer.Character:FindFirstChild("Left Leg") then
                game.Players.LocalPlayer.Character:FindFirstChild("Left Leg"):Destroy()
                end
                if game.Players.LocalPlayer.Character:FindFirstChild("Left Arm") then
                game.Players.LocalPlayer.Character:FindFirstChild("Left Arm"):Destroy()
            end
        end
    end
end)

-- [[ Commands ]] --

    Commands["Sets Walkspeed"] = {
    ["Aliases"] = {"!ws", "!walkspeed", "!speed"};
    ["Function"] = function(Args)
getgenv().WalkSpeedValue = tonumber(Args[1]) --set your desired walkspeed here
local Player = game:service'Players'.LocalPlayer;
Player.Character.Humanoid:GetPropertyChangedSignal'WalkSpeed':Connect(function()
Player.Character.Humanoid.WalkSpeed = getgenv().WalkSpeedValue
end)
Player.Character.Humanoid.WalkSpeed = getgenv().WalkSpeedValue
        Notify("CSU GANG", "Walkspeed: "..tonumber(Args[1]), "", 3)
    end
}
        Commands["Sets JumpPower"] = {
    ["Aliases"] = {"!jp", "!jumppower"};
    ["Function"] = function(Args)
getgenv().JumpPowerValue = tonumber(Args[1]) --set your desired walkspeed here
local Player = game:service'Players'.LocalPlayer;
Player.Character.Humanoid:GetPropertyChangedSignal'JumpPower':Connect(function()
Player.Character.Humanoid.JumpPower = getgenv().JumpPowerValue
end)
Player.Character.Humanoid.JumpPower = getgenv().JumpPowerValue
        Notify("CSU GANG", "JumpPower: "..tonumber(Args[1]), "", 3)
    end
}
Commands["AntiFe"] = {
    ["Aliases"] = {"!antife"};
    ["Function"] = function(Args)
workspace.FallenPartsDestroyHeight = math.huge - math.huge
game.Players.LocalPlayer.Character.Humanoid.Sit = true
game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
end
}
Commands["OgRun"] = {
    ["Aliases"] = {"!ogrun"};
    ["Function"] = function(Args)
game.Players.LocalPlayer.Character.Humanoid.Health = 0
if not game:IsLoaded() then game.Loaded:Wait() end
local RunReplacementAnimation = Instance.new("Animation")
RunReplacementAnimation.AnimationId = "rbxassetid://1357408709"

local NameCall
function OnNameCall(self, ...)
    local Arguments = {...}
    local Caller, Method = checkcaller(), getnamecallmethod()
    if not Caller then
        if Method == "LoadAnimation" then
            local A = Arguments[1]
            if tostring(A) == "Run" then
                Arguments[1] = RunReplacementAnimation
            end
        end
    end
    return NameCall(self, unpack(Arguments))
end
NameCall = hookmetamethod(game, "__namecall", OnNameCall)
end
}
Commands["AntiGrab"] = {
    ["Aliases"] = {"!antigrab"};
    ["Function"] = function(Args)
local plr = game:GetService("Players").LocalPlayer
local function run()
   local wltools = {}

   for _,v in pairs(plr.Backpack:GetChildren()) do
       if v:IsA("Tool") then
           table.insert(wltools,v)
       end
   end
   for _,v in pairs(plr.Character:GetChildren()) do
       if v:IsA("Tool") then
           table.insert(wltools,v)
       end
   end
   
   plr.Character.ChildAdded:Connect(function(child)
       if child:IsA("Tool") and not table.find(wltools, child) then
           child:Destroy()
       end
   end)
end

plr.CharacterAdded:Connect(function(char)
   char:WaitForChild("HumanoidRootPart")
   run()
end)

run()
end
}
Commands["instantre"] = {
    ["Aliases"] = {"!ff"};
    ["Function"] = function(Args)
instantre = true
Notify("CSU GANG", "Instant Respawn: true")
end
}
Commands["UnInstantre"] = {
    ["Aliases"] = {"!unff"};
    ["Function"] = function(Args)
instantre = false 
        Notify("CSU GANG", "Instant Respawn: False")
end
}
Commands["kill everyone"] = {
    ["Aliases"] = {"!kill all"};
    ["Function"] = function(Args)
local Players = game:GetService('Players')
local RunService = game:GetService('RunService')

local LP = Players.LocalPlayer
local Backpack = LP:WaitForChild('Backpack')
local Char = LP.Character
local Humanoid = Char:WaitForChild('Humanoid')
local Root = Char:WaitForChild('HumanoidRootPart')

local CanCloneHumanoid = true

local Whitelist = {'xcz', 'CSU', 'okugettheidea'} -- shortened names work.

local GetWhitelistedUsers = function()
    local Whitelisted = {}
    for K,V in next, Whitelist do
        for K2,V2 in next, Players:GetPlayers() do
            if V2.Name:lower():find(V) then
                table.insert(Whitelisted, V2)
            end
        end
    end
    return Whitelisted
end

local ReplaceHumanoid = function()
    if CanCloneHumanoid then
        CanCloneHumanoid = false;
        local Clone = Humanoid:Clone(); Humanoid:Destroy(); Clone.Parent = Char
    end
end

local onCharacterAppearanceLoaded = function(Character)
    Backpack, Char = LP:WaitForChild('Backpack'), Character
    Root, Humanoid = Char:WaitForChild('HumanoidRootPart'), Char:WaitForChild('Humanoid')
    CanCloneHumanoid = true;
end

RunService.Heartbeat:Connect(function()
    local Tool = Backpack:FindFirstChildOfClass('Tool'); ReplaceHumanoid()
    for K,V in next, Players:GetPlayers() do
        if V ~= LP and V.Character and not table.find(GetWhitelistedUsers(), V) then
            local TargetChar = V.Character
            if Tool and Root and TargetChar:FindFirstChildOfClass('Humanoid') and TargetChar:FindFirstChild('Torso') and not TargetChar:FindFirstChildOfClass('Humanoid').Sit then
                Tool.Parent = Char; Char:FindFirstChildOfClass('Humanoid'):ChangeState(15); firetouchinterest(TargetChar.Torso, Tool.Handle, 0)
                Root.CFrame = TargetChar:FindFirstChild('Torso').CFrame; task.wait() -- roblox go fuck urself
            end
        end
    end
end)

LP.CharacterAppearanceLoaded:Connect(onCharacterAppearanceLoaded)
ait(1)
 
-- Get LocalPlayer
local p = game.Players.LocalPlayer
Notify("CSU GANG", "Kill: True")
end
}
Commands["unhvh"] = {
    ["Aliases"] = {"!unhvh"};
    ["Function"] = function(Args)
hvh = false 
      game.Players.LocalPlayer.Character.Humanoid.Health = 0
        Notify("CSU GANG", "HvhMode: False")
end
}
Commands["unhvh"] = {
    ["Aliases"] = {"!unhvh"};
    ["Function"] = function(Args)
hvh = false 
      game.Players.LocalPlayer.Character.Humanoid.Health = 0
        Notify("CSU GANG", "HvhMode: False")
end
}
Commands["invis"] = {
    ["Aliases"] = {"!god", "!godmode"};
    ["Function"] = function(Args)
        
godmode = true
game.Players.LocalPlayer.Character.Humanoid.Health = 0
        game.Players.LocalPlayer.Character:BreakJoints()
        Notify("CSU GANG", "GodMode: True")
end
}
Commands["wg2"] = {
    ["Aliases"] = {"!weldgun2", "!wg2"};
    ["Function"] = function(Args)
game.Players.LocalPlayer:findFirstChildOfClass('Backpack')['Shotty'].Parent = game.Players.LocalPlayer.Character
wait(1)
		    local AnimationTracks = game.Players.LocalPlayer.Character.Humanoid:GetPlayingAnimationTracks()
    for i, track in pairs (AnimationTracks) do
        if track then 
            track:Stop()
        end
    end

    
local char = game.Players.LocalPlayer.Character
local torso = char.Torso

torso_att = Instance.new("Attachment", torso)

torso_att.Rotation = Vector3.new(0,0,0)
torso_att.Position = Vector3.new(0,0,0)

rarm = char["Right Arm"]
torso["Right Shoulder"]:Destroy()
rarm.RightShoulderAttachment:Destroy()

r = Instance.new("Attachment",rarm)
r.Rotation = Vector3.new(-100, -0, 0) 
r.Position = Vector3.new(-0.00007, 1.3255, -1.400333)

t = Instance.new("Attachment",torso)

rap = Instance.new("AlignPosition",rarm)
rap.ApplyAtCenterOfMass = false
rap.MaxVelocity = 0/0
rap.ReactionForceEnabled = false
rap.Attachment0 = r
rap.Attachment1 = t
rap.RigidityEnabled = true;
rap.MaxForce = 0/0;
rap.RigidityEnabled = true;
rap.Responsiveness = 10000;
rarm.CanCollide = false

rao = Instance.new("AlignOrientation",rarm)
rao.MaxAngularVelocity = 0/0
rao.MaxTorque = 0/0
rao.PrimaryAxisOnly = false
rao.ReactionTorqueEnabled = false
rao.Attachment0 = r
rao.Attachment1 = t
rao.RigidityEnabled = true

game:GetService("RunService").Heartbeat:Connect(function()
rarm.Velocity = Vector3.new(100,100,100)
end)

wait(2)
print(rarm.Velocity)
for i,v in next, game:GetService("Players").LocalPlayer.Character:GetDescendants() do
if v.Name == "Right Arm" then 
game:GetService("RunService").RenderStepped:connect(function()
v.Velocity = Vector3.new(1e1,2e2,3e3)
end)
end
end
wait(1)
 local Shot = game.Players.LocalPlayer.Character.Shotty.Handle
    local rar = game.Players.LocalPlayer.Character["Right Arm"]
    local LocalPlayer = game.Players.LocalPlayer

    LocalPlayer.Character["Right Arm"]:FindFirstChild("RightGrip")
    LocalPlayer.Character["Right Arm"]:FindFirstChild("RightGrip"):Remove()
    rar.Touched:Connect(function(hit)
        if hit.Parent:FindFirstChild("Humanoid") then
            local Shotty = hit.Parent.Shotty
            RightArm.CFrame = Shotty.CFrame
            local weld = Instance.new("Weld")
            weld.RightArm = Shotty.CFrame
        end
    end)
    function InsertGrips()
        for i, v in pairs(grips) do
            grips(i).Parent = l.Character("Right Arm")
        end
    end


    s = Instance.new("Attachment",Shot)
    s.Rotation = Vector3.new(90, -1, 0)
    s.Position = Vector3.new(-1.5 ,-0.5 ,1.6)

    r = Instance.new("Attachment",rar)
    r.Rotation = Vector3.new(0, 0, 0)
    r.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shp = Instance.new("AlignPosition",Shot)
    shp.ApplyAtCenterOfMass = false
    shp.MaxVelocity = 0/0
    shp.ReactionForceEnabled = false
    shp.Attachment0 = s
    shp.Attachment1 = r
    shp.RigidityEnabled = true;
    shp.MaxForce = 0/0;
    shp.RigidityEnabled = true;
    shp.Responsiveness = 10000;

    sho = Instance.new("AlignOrientation",Shot)
    sho.MaxAngularVelocity = 0/0
    sho.MaxTorque = 0/0
    sho.PrimaryAxisOnly = false
    sho.ReactionTorqueEnabled = false
    sho.Attachment0 = s
    sho.Attachment1 = r
    sho.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = s
    weld.Part1 = rar

    s.Position =  Vector3.new(-1.5,0.4,0.6)
    
    sa = Instance.new("Attachment",Shot)
    sa.Rotation = Vector3.new(0, 0, 0)
    sa.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    ra = Instance.new("Attachment",rar)
    ra.Rotation = Vector3.new(0, 0, 0)
    ra.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shap = Instance.new("AlignPosition",Shot)
    shap.ApplyAtCenterOfMass = false
    shap.MaxVelocity = 0/0
    shap.ReactionForceEnabled = false
    shap.Attachment0 = s
    shap.Attachment1 = r
    shap.RigidityEnabled = true;
    shap.MaxForce = 0/0;
    shap.RigidityEnabled = true;
    shap.Responsiveness = 10000;

    shao = Instance.new("AlignOrientation",Shot)
    shao.MaxAngularVelocity = 0/0
    shao.MaxTorque = 0/0
    shao.PrimaryAxisOnly = false
    shao.ReactionTorqueEnabled = false
    shao.Attachment0 = s
    shao.Attachment1 = r
    shao.RigidityEnabled = true

        local weld = Instance.new("WeldConstraint")
        weld.Parent = l.Character["Right Arm"]
        weld.Part0 = sa
        weld.Part1 = rar

        sa.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shbp = Instance.new("AlignPosition",Shot)
    shbp.ApplyAtCenterOfMass = false
    shbp.MaxVelocity = 0/0
    shbp.ReactionForceEnabled = false
    shbp.Attachment0 = s
    shbp.Attachment1 = r
    shbp.RigidityEnabled = true;
    shbp.MaxForce = 0/0;
    shbp.RigidityEnabled = true;
    shbp.Responsiveness = 10000;

    shbo = Instance.new("AlignOrientation",Shot)
    shbo.MaxAngularVelocity = 0/0
    shbo.MaxTorque = 0/0
    shbo.PrimaryAxisOnly = false
    shbo.ReactionTorqueEnabled = false
    shbo.Attachment0 = s
    shbo.Attachment1 = r
    shbo.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sb
    weld.Part1 = rar

    sb.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shcp = Instance.new("AlignPosition",Shot)
    shcp.ApplyAtCenterOfMass = false
    shcp.MaxVelocity = 0/0
    shcp.ReactionForceEnabled = false
    shcp.Attachment0 = s
    shcp.Attachment1 = r
    shcp.RigidityEnabled = true;
    shcp.MaxForce = 0/0;
    shcp.RigidityEnabled = true;
    shcp.Responsiveness = 10000;

    shco = Instance.new("AlignOrientation",Shot)
    shco.MaxAngularVelocity = 0/0
    shco.MaxTorque = 0/0
    shco.PrimaryAxisOnly = false
    shco.ReactionTorqueEnabled = false
    shco.Attachment0 = s
    shco.Attachment1 = r
    shco.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sc
    weld.Part1 = rar

    sc.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shdp = Instance.new("AlignPosition",Shot)
    shdp.ApplyAtCenterOfMass = false
    shdp.MaxVelocity = 0/0
    shdp.ReactionForceEnabled = false
    shdp.Attachment0 = s
    shdp.Attachment1 = r
    shdp.RigidityEnabled = true;
    shdp.MaxForce = 0/0;
    shdp.RigidityEnabled = true;
    shdp.Responsiveness = 10000;

    shdo = Instance.new("AlignOrientation",Shot)
    shdo.MaxAngularVelocity = 0/0
    shdo.MaxTorque = 0/0
    shdo.PrimaryAxisOnly = false
    shdo.ReactionTorqueEnabled = false
    shdo.Attachment0 = s
    shdo.Attachment1 = r
    shdo.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sd
    weld.Part1 = rar

    sd.Position =  Vector3.new(-1.5,0.4,0.6)



    for a,b in ipairs(guns) do
        b.GripPos = Vector3.new(-1.5,0.4,0.6)
    end
    
         Notify("CSU GANG", "BFG2 On")
end
}
Commands["invisiblegun"] = {
    ["Aliases"] = {"!invisgun", "!ivg"};
    ["Function"] = function(Args)
        local function invis(instance) 
    for i,v in pairs(instance:GetChildren()) do
	if v.Name == "Weld" and v.Parent.Name ~= "Heh" and v.Parent.Name ~= "Barrel" then
	    v:Destroy()
	end
    invis(v)
    end
end
invis(game.Players.LocalPlayer.Character.Shotty)

        Notify("CSU GANG", "Invisible Gun: True")
end
}
Commands["Bfg"] = {
    ["Aliases"] = {"!wg"};
    ["Function"] = function(Args)
game.Players.LocalPlayer:findFirstChildOfClass('Backpack')['Shotty'].Parent = game.Players.LocalPlayer.Character
wait(1)
local AnimationTracks = game.Players.LocalPlayer.Character.Humanoid:GetPlayingAnimationTracks()
    for i, track in pairs (AnimationTracks) do
        if track then 
            track:Stop()
        end
    end
    
    local char = game.Players.LocalPlayer.Character
local torso = char.Torso

torso_att = Instance.new("Attachment", torso)

torso_att.Rotation = Vector3.new(0,0,0)
torso_att.Position = Vector3.new(0,0,0)

rarm = char["Right Arm"]
torso["Right Shoulder"]:Destroy()
rarm.RightShoulderAttachment:Destroy()

r = Instance.new("Attachment",rarm)
r.Rotation = Vector3.new(-90, 0, 0) 
r.Position = Vector3.new(-1.40007, 0.0255, -0.000333)

t = Instance.new("Attachment",torso)

rap = Instance.new("AlignPosition",rarm)
rap.ApplyAtCenterOfMass = false
rap.MaxVelocity = 0/0
rap.ReactionForceEnabled = false
rap.Attachment0 = r
rap.Attachment1 = t
rap.RigidityEnabled = true;
rap.MaxForce = 0/0;
rap.RigidityEnabled = true;
rap.Responsiveness = 10000;
rarm.CanCollide = false

rao = Instance.new("AlignOrientation",rarm)
rao.MaxAngularVelocity = 0/0
rao.MaxTorque = 0/0
rao.PrimaryAxisOnly = false
rao.ReactionTorqueEnabled = false
rao.Attachment0 = r
rao.Attachment1 = t
rao.RigidityEnabled = true

game:GetService("RunService").Heartbeat:Connect(function()
rarm.Velocity = Vector3.new(100,100,100)
end)

wait(2)
print(rarm.Velocity)
for i,v in next, game:GetService("Players").LocalPlayer.Character:GetDescendants() do
if v.Name == "Right Arm" then 
game:GetService("RunService").RenderStepped:connect(function()
v.Velocity = Vector3.new(1e1,2e2,3e3)
end)
end
end
 local Shot = game.Players.LocalPlayer.Character.Shotty.Handle
    local rar = game.Players.LocalPlayer.Character["Right Arm"]
    local LocalPlayer = game.Players.LocalPlayer

    LocalPlayer.Character["Right Arm"]:FindFirstChild("RightGrip")
    LocalPlayer.Character["Right Arm"]:FindFirstChild("RightGrip"):Remove()
    rar.Touched:Connect(function(hit)
        if hit.Parent:FindFirstChild("Humanoid") then
            local Shotty = hit.Parent.Shotty
            RightArm.CFrame = Shotty.CFrame
            local weld = Instance.new("Weld")
            weld.RightArm = Shotty.CFrame
        end
    end)
    function InsertGrips()
        for i, v in pairs(grips) do
            grips(i).Parent = l.Character("Right Arm")
        end
    end


    s = Instance.new("Attachment",Shot)
    s.Rotation = Vector3.new(90, -1, 0)
    s.Position = Vector3.new(-1.5 ,-0.5 ,1.6)

    r = Instance.new("Attachment",rar)
    r.Rotation = Vector3.new(0, 0, 0)
    r.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shp = Instance.new("AlignPosition",Shot)
    shp.ApplyAtCenterOfMass = false
    shp.MaxVelocity = 0/0
    shp.ReactionForceEnabled = false
    shp.Attachment0 = s
    shp.Attachment1 = r
    shp.RigidityEnabled = true;
    shp.MaxForce = 0/0;
    shp.RigidityEnabled = true;
    shp.Responsiveness = 10000;

    sho = Instance.new("AlignOrientation",Shot)
    sho.MaxAngularVelocity = 0/0
    sho.MaxTorque = 0/0
    sho.PrimaryAxisOnly = false
    sho.ReactionTorqueEnabled = false
    sho.Attachment0 = s
    sho.Attachment1 = r
    sho.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = s
    weld.Part1 = rar

    s.Position =  Vector3.new(-1.5,0.4,0.6)
    
    sa = Instance.new("Attachment",Shot)
    sa.Rotation = Vector3.new(0, 0, 0)
    sa.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    ra = Instance.new("Attachment",rar)
    ra.Rotation = Vector3.new(0, 0, 0)
    ra.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shap = Instance.new("AlignPosition",Shot)
    shap.ApplyAtCenterOfMass = false
    shap.MaxVelocity = 0/0
    shap.ReactionForceEnabled = false
    shap.Attachment0 = s
    shap.Attachment1 = r
    shap.RigidityEnabled = true;
    shap.MaxForce = 0/0;
    shap.RigidityEnabled = true;
    shap.Responsiveness = 10000;

    shao = Instance.new("AlignOrientation",Shot)
    shao.MaxAngularVelocity = 0/0
    shao.MaxTorque = 0/0
    shao.PrimaryAxisOnly = false
    shao.ReactionTorqueEnabled = false
    shao.Attachment0 = s
    shao.Attachment1 = r
    shao.RigidityEnabled = true

        local weld = Instance.new("WeldConstraint")
        weld.Parent = l.Character["Right Arm"]
        weld.Part0 = sa
        weld.Part1 = rar

        sa.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shbp = Instance.new("AlignPosition",Shot)
    shbp.ApplyAtCenterOfMass = false
    shbp.MaxVelocity = 0/0
    shbp.ReactionForceEnabled = false
    shbp.Attachment0 = s
    shbp.Attachment1 = r
    shbp.RigidityEnabled = true;
    shbp.MaxForce = 0/0;
    shbp.RigidityEnabled = true;
    shbp.Responsiveness = 10000;

    shbo = Instance.new("AlignOrientation",Shot)
    shbo.MaxAngularVelocity = 0/0
    shbo.MaxTorque = 0/0
    shbo.PrimaryAxisOnly = false
    shbo.ReactionTorqueEnabled = false
    shbo.Attachment0 = s
    shbo.Attachment1 = r
    shbo.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sb
    weld.Part1 = rar

    sb.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shcp = Instance.new("AlignPosition",Shot)
    shcp.ApplyAtCenterOfMass = false
    shcp.MaxVelocity = 0/0
    shcp.ReactionForceEnabled = false
    shcp.Attachment0 = s
    shcp.Attachment1 = r
    shcp.RigidityEnabled = true;
    shcp.MaxForce = 0/0;
    shcp.RigidityEnabled = true;
    shcp.Responsiveness = 10000;

    shco = Instance.new("AlignOrientation",Shot)
    shco.MaxAngularVelocity = 0/0
    shco.MaxTorque = 0/0
    shco.PrimaryAxisOnly = false
    shco.ReactionTorqueEnabled = false
    shco.Attachment0 = s
    shco.Attachment1 = r
    shco.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sc
    weld.Part1 = rar

    sc.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shdp = Instance.new("AlignPosition",Shot)
    shdp.ApplyAtCenterOfMass = false
    shdp.MaxVelocity = 0/0
    shdp.ReactionForceEnabled = false
    shdp.Attachment0 = s
    shdp.Attachment1 = r
    shdp.RigidityEnabled = true;
    shdp.MaxForce = 0/0;
    shdp.RigidityEnabled = true;
    shdp.Responsiveness = 10000;

    shdo = Instance.new("AlignOrientation",Shot)
    shdo.MaxAngularVelocity = 0/0
    shdo.MaxTorque = 0/0
    shdo.PrimaryAxisOnly = false
    shdo.ReactionTorqueEnabled = false
    shdo.Attachment0 = s
    shdo.Attachment1 = r
    shdo.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sd
    weld.Part1 = rar

    sd.Position =  Vector3.new(-1.5,0.4,0.6)



    for a,b in ipairs(guns) do
        b.GripPos = Vector3.new(-1.5,0.4,0.6)
    end
    
    local char = game.Players.LocalPlayer.Character
local torso = char.Torso

torso_att = Instance.new("Attachment", torso)

torso_att.Rotation = Vector3.new(0,0,0)
torso_att.Position = Vector3.new(0,0,0)

rarm = char["Right Arm"]
torso["Right Shoulder"]:Destroy()
rarm.RightShoulderAttachment:Destroy()

r = Instance.new("Attachment",rarm)
r.Rotation = Vector3.new(-90, 0, 0) 
r.Position = Vector3.new(-1.40007, 0.0255, -0.000333)

t = Instance.new("Attachment",torso)

rap = Instance.new("AlignPosition",rarm)
rap.ApplyAtCenterOfMass = false
rap.MaxVelocity = 0/0
rap.ReactionForceEnabled = false
rap.Attachment0 = r
rap.Attachment1 = t
rap.RigidityEnabled = true;
rap.MaxForce = 0/0;
rap.RigidityEnabled = true;
rap.Responsiveness = 10000;
rarm.CanCollide = false

rao = Instance.new("AlignOrientation",rarm)
rao.MaxAngularVelocity = 0/0
rao.MaxTorque = 0/0
rao.PrimaryAxisOnly = false
rao.ReactionTorqueEnabled = false
rao.Attachment0 = r
rao.Attachment1 = t
rao.RigidityEnabled = true

game:GetService("RunService").Heartbeat:Connect(function()
rarm.Velocity = Vector3.new(100,100,100)
end)

wait(2)
print(rarm.Velocity)
for i,v in next, game:GetService("Players").LocalPlayer.Character:GetDescendants() do
if v.Name == "Right Arm" then 
game:GetService("RunService").RenderStepped:connect(function()
v.Velocity = Vector3.new(1e1,2e2,3e3)
end)
end
end
         Notify("CSU GANG", "BFG On")
end
}
Commands["Bfg"] = {
    ["Aliases"] = {"!wg"};
    ["Function"] = function(Args)
game.Players.LocalPlayer:findFirstChildOfClass('Backpack')['Shotty'].Parent = game.Players.LocalPlayer.Character
wait(1)
local AnimationTracks = game.Players.LocalPlayer.Character.Humanoid:GetPlayingAnimationTracks()
    for i, track in pairs (AnimationTracks) do
        if track then 
            track:Stop()
        end
    end
    
    local char = game.Players.LocalPlayer.Character
local torso = char.Torso

torso_att = Instance.new("Attachment", torso)

torso_att.Rotation = Vector3.new(0,0,0)
torso_att.Position = Vector3.new(0,0,0)

rarm = char["Right Arm"]
torso["Right Shoulder"]:Destroy()
rarm.RightShoulderAttachment:Destroy()

r = Instance.new("Attachment",rarm)
r.Rotation = Vector3.new(-90, 0, 0) 
r.Position = Vector3.new(-1.40007, 0.0255, -0.000333)

t = Instance.new("Attachment",torso)

rap = Instance.new("AlignPosition",rarm)
rap.ApplyAtCenterOfMass = false
rap.MaxVelocity = 0/0
rap.ReactionForceEnabled = false
rap.Attachment0 = r
rap.Attachment1 = t
rap.RigidityEnabled = true;
rap.MaxForce = 0/0;
rap.RigidityEnabled = true;
rap.Responsiveness = 10000;
rarm.CanCollide = false

rao = Instance.new("AlignOrientation",rarm)
rao.MaxAngularVelocity = 0/0
rao.MaxTorque = 0/0
rao.PrimaryAxisOnly = false
rao.ReactionTorqueEnabled = false
rao.Attachment0 = r
rao.Attachment1 = t
rao.RigidityEnabled = true

game:GetService("RunService").Heartbeat:Connect(function()
rarm.Velocity = Vector3.new(100,100,100)
end)

wait(2)
print(rarm.Velocity)
for i,v in next, game:GetService("Players").LocalPlayer.Character:GetDescendants() do
if v.Name == "Right Arm" then 
game:GetService("RunService").RenderStepped:connect(function()
v.Velocity = Vector3.new(1e1,2e2,3e3)
end)
end
end
 local Shot = game.Players.LocalPlayer.Character.Shotty.Handle
    local rar = game.Players.LocalPlayer.Character["Right Arm"]
    local LocalPlayer = game.Players.LocalPlayer

    LocalPlayer.Character["Right Arm"]:FindFirstChild("RightGrip")
    LocalPlayer.Character["Right Arm"]:FindFirstChild("RightGrip"):Remove()
    rar.Touched:Connect(function(hit)
        if hit.Parent:FindFirstChild("Humanoid") then
            local Shotty = hit.Parent.Shotty
            RightArm.CFrame = Shotty.CFrame
            local weld = Instance.new("Weld")
            weld.RightArm = Shotty.CFrame
        end
    end)
    function InsertGrips()
        for i, v in pairs(grips) do
            grips(i).Parent = l.Character("Right Arm")
        end
    end


    s = Instance.new("Attachment",Shot)
    s.Rotation = Vector3.new(90, -1, 0)
    s.Position = Vector3.new(-1.5 ,-0.5 ,1.6)

    r = Instance.new("Attachment",rar)
    r.Rotation = Vector3.new(0, 0, 0)
    r.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shp = Instance.new("AlignPosition",Shot)
    shp.ApplyAtCenterOfMass = false
    shp.MaxVelocity = 0/0
    shp.ReactionForceEnabled = false
    shp.Attachment0 = s
    shp.Attachment1 = r
    shp.RigidityEnabled = true;
    shp.MaxForce = 0/0;
    shp.RigidityEnabled = true;
    shp.Responsiveness = 10000;

    sho = Instance.new("AlignOrientation",Shot)
    sho.MaxAngularVelocity = 0/0
    sho.MaxTorque = 0/0
    sho.PrimaryAxisOnly = false
    sho.ReactionTorqueEnabled = false
    sho.Attachment0 = s
    sho.Attachment1 = r
    sho.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = s
    weld.Part1 = rar

    s.Position =  Vector3.new(-1.5,0.4,0.6)
    
    sa = Instance.new("Attachment",Shot)
    sa.Rotation = Vector3.new(0, 0, 0)
    sa.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    ra = Instance.new("Attachment",rar)
    ra.Rotation = Vector3.new(0, 0, 0)
    ra.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shap = Instance.new("AlignPosition",Shot)
    shap.ApplyAtCenterOfMass = false
    shap.MaxVelocity = 0/0
    shap.ReactionForceEnabled = false
    shap.Attachment0 = s
    shap.Attachment1 = r
    shap.RigidityEnabled = true;
    shap.MaxForce = 0/0;
    shap.RigidityEnabled = true;
    shap.Responsiveness = 10000;

    shao = Instance.new("AlignOrientation",Shot)
    shao.MaxAngularVelocity = 0/0
    shao.MaxTorque = 0/0
    shao.PrimaryAxisOnly = false
    shao.ReactionTorqueEnabled = false
    shao.Attachment0 = s
    shao.Attachment1 = r
    shao.RigidityEnabled = true

        local weld = Instance.new("WeldConstraint")
        weld.Parent = l.Character["Right Arm"]
        weld.Part0 = sa
        weld.Part1 = rar

        sa.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shbp = Instance.new("AlignPosition",Shot)
    shbp.ApplyAtCenterOfMass = false
    shbp.MaxVelocity = 0/0
    shbp.ReactionForceEnabled = false
    shbp.Attachment0 = s
    shbp.Attachment1 = r
    shbp.RigidityEnabled = true;
    shbp.MaxForce = 0/0;
    shbp.RigidityEnabled = true;
    shbp.Responsiveness = 10000;

    shbo = Instance.new("AlignOrientation",Shot)
    shbo.MaxAngularVelocity = 0/0
    shbo.MaxTorque = 0/0
    shbo.PrimaryAxisOnly = false
    shbo.ReactionTorqueEnabled = false
    shbo.Attachment0 = s
    shbo.Attachment1 = r
    shbo.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sb
    weld.Part1 = rar

    sb.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shcp = Instance.new("AlignPosition",Shot)
    shcp.ApplyAtCenterOfMass = false
    shcp.MaxVelocity = 0/0
    shcp.ReactionForceEnabled = false
    shcp.Attachment0 = s
    shcp.Attachment1 = r
    shcp.RigidityEnabled = true;
    shcp.MaxForce = 0/0;
    shcp.RigidityEnabled = true;
    shcp.Responsiveness = 10000;

    shco = Instance.new("AlignOrientation",Shot)
    shco.MaxAngularVelocity = 0/0
    shco.MaxTorque = 0/0
    shco.PrimaryAxisOnly = false
    shco.ReactionTorqueEnabled = false
    shco.Attachment0 = s
    shco.Attachment1 = r
    shco.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sc
    weld.Part1 = rar

    sc.Position =  Vector3.new(-1.5,0.4,0.6)

    sb = Instance.new("Attachment",Shot)
    sb.Rotation = Vector3.new(0, 0, 0)
    sb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    rb = Instance.new("Attachment",rar)
    rb.Rotation = Vector3.new(0, 0, 0)
    rb.Position = Vector3.new(-1.5 ,0.4 ,0.6)

    shdp = Instance.new("AlignPosition",Shot)
    shdp.ApplyAtCenterOfMass = false
    shdp.MaxVelocity = 0/0
    shdp.ReactionForceEnabled = false
    shdp.Attachment0 = s
    shdp.Attachment1 = r
    shdp.RigidityEnabled = true;
    shdp.MaxForce = 0/0;
    shdp.RigidityEnabled = true;
    shdp.Responsiveness = 10000;

    shdo = Instance.new("AlignOrientation",Shot)
    shdo.MaxAngularVelocity = 0/0
    shdo.MaxTorque = 0/0
    shdo.PrimaryAxisOnly = false
    shdo.ReactionTorqueEnabled = false
    shdo.Attachment0 = s
    shdo.Attachment1 = r
    shdo.RigidityEnabled = true

    local weld = Instance.new("WeldConstraint")
    weld.Parent = l.Character["Right Arm"]
    weld.Part0 = sd
    weld.Part1 = rar

    sd.Position =  Vector3.new(-1.5,0.4,0.6)



    for a,b in ipairs(guns) do
        b.GripPos = Vector3.new(-1.5,0.4,0.6)
    end
         Notify("CSU GANG", "BFG On")
end
}
Commands["ungod"] = {
    ["Aliases"] = {"!ungod", "!ungodmode"};
    ["Function"] = function(Args)
godmode = false 
game.Players.LocalPlayer.Character.Humanoid.Health = 0
        game.Players.LocalPlayer.Character:BreakJoints()
         Notify("CSU GANG", "GodMode: False")
end
}
Commands["Goto"] = {
    ["Aliases"] = {"!goto"};
    ["Function"] = function(Args)
local player
		for i, plr in ipairs(game.Players:GetPlayers()) do
			if string.lower(plr.Name):sub(1, string.len(msg:sub(7))) == string.lower(msg:sub(7)) then
				player = plr.Name
			end
		end
		local tweenService = game:GetService("TweenService")
		local info = TweenInfo.new()
		local function tweenPlayer(player, CF)
			local CFrameValue = Instance.new("CFrameValue")
			CFrameValue.Value = player:GetPrimaryPartCFrame()
			CFrameValue:GetPropertyChangedSignal("Value"):Connect(function()
				player:SetPrimaryPartCFrame(CFrameValue.Value)
			end)
			local tween = tweenService:Create(CFrameValue, info, {
				Value = CF
			})
			tween:Play()
			tween.Completed:Connect(function()
				CFrameValue:Destroy()
			end)
		end
		tweenPlayer(game:GetService("Players").LocalPlayer.Character, workspace[player].HumanoidRootPart.CFrame + Vector3.new(3,0, 2))
	end

}
Commands["SpinSpeed"] = {
    ["Aliases"] = {"!sky1"};
    ["Function"] = function(Args)
local id = 92464172
local skybox = Instance.new("Sky")
skybox.Parent = game.Lighting
skybox.SkyboxBk = "rbxassetid://" .. id
skybox.SkyboxDn = "rbxassetid://" .. id
skybox.SkyboxFt = "rbxassetid://" .. id
skybox.SkyboxLf = "rbxassetid://" .. id
skybox.SkyboxRt = "rbxassetid://" .. id
skybox.SkyboxUp = "rbxassetid://" .. id
Notify("CSU GANG", "SkyBox1")
end
}
Commands["DropTools"] = {
    ["Aliases"] = {"!dt", "!droptool"};
    ["Function"] = function(Args)
local plr = game.Players.LocalPlayer
local humanoid = plr.Character.Humanoid
wait(0.1)
humanoid:Destroy()
plr.Character["Torso"]:Destroy()
plr.Character["Left Arm"]:Destroy()
plr.Character["Right Arm"]:Destroy()
plr.Character["Left Leg"]:Destroy()
plr.Character["Right Leg"]:Destroy()
plr.Character["Head"]:Destroy()
wait(5.25)
end
}

Commands["Sit"] = {
    ["Aliases"] = {"!sit"};
    ["Function"] = function(Args)
game.Players.LocalPlayer.Character.Humanoid.Sit = true
end
}
Commands["GunAnims"] = {
    ["Aliases"] = {"!gunanims", "!gunanim"};
    ["Function"] = function(Args)
game.StarterGui:SetCore("SendNotification", {
Title = "CSU GANG";
Text = "Gunanims On";
Duration = 5;
})

local lplr = game:GetService("Players").LocalPlayer
local shotty = lplr.Backpack:FindFirstChild("Shotty")
local Animation = Instance.new("Animation")
Animation.AnimationId = "rbxassetid://889968874"
local plr = game:GetService('Players').LocalPlayer
local HUM = plr.Character.Humanoid:LoadAnimation(Animation)
shotty.Equipped:connect(function()
    wait(.1)
    HUM:Play()
    HUM:AdjustSpeed(0.0)
end)
shotty.Unequipped:connect(function()
    HUM:Stop()
end)
local lplr = game:GetService("Players").LocalPlayer
local Glock = lplr.Backpack:FindFirstChild("Glock")
local Animation = Instance.new("Animation")
Animation.AnimationId = "rbxassetid://889968874"
local plr = game:GetService('Players').LocalPlayer
local HUM = plr.Character.Humanoid:LoadAnimation(Animation)
Glock.Equipped:connect(function()
    wait(.1)
    HUM:Play()
    HUM:AdjustSpeed(0.0)
end)
Glock.Unequipped:connect(function()
    HUM:Stop()
end)
end
}
Commands["NoDoors"] = {
    ["Aliases"] = {"!nodoors", "!doors"};
    ["Function"] = function(Args)
local doors = game.Workspace:GetChildren()
for i,v in pairs (doors)do 
    if v.Name == "Door" then
        v:Destroy()
        
     
    end    
    end
end
}
Commands["Sets your Flyspeed"] = {
    ["Aliases"] = {"!flyspeed", "!fs"};
    ["Function"] = function(Args)
        if Args[1] then 
            Flyspeed = tonumber(Args[1])
            Notify("CSU GANG", "Flyspeed: "..tonumber(Flyspeed), "", 3)
        end
    end
}
Commands["TpBypass"] = {
    ["Aliases"] = {"!bypass"};
    ["Function"] = function(Args)
        game.StarterGui:SetCore("SendNotification", {
Title = "CSU GANG";
Text = "Bypass On";
Duration = 5;
})
getgenv().bypass = true

while wait() do
  if bypass then
local l = game.Players.LocalPlayer
local rs = game['RunService'].RenderStepped
local storage = Instance.new('Folder', game);storage.Name = 'HumStorage'

rs:connect(function()
    if l.Character:FindFirstChild('HumanoidRootPart') then
        l.Character.HumanoidRootPart.Parent = nil
        l.Character.Humanoid.Parent = storage
        storage.Humanoid.Parent = l.Character
    end
end)

GetChar():BreakJoints()
end
end
end
}
Commands["Toggles Fly"] = {
    ["Aliases"] = {"!fly", "!togglefly"};
    ["Function"] = function(Args)
        togglefly()
    end
}
Commands["SkyBox1"] = {
    ["Aliases"] = {"!sky1"};
    ["Function"] = function(Args)
local lighting = game.Lighting
        if lighting:FindFirstChild("ColorCorrection") then
            lighting:FindFirstChild("ColorCorrection"):Remove()
        end
        if lighting:FindFirstChild("Correction") then
            lighting:FindFirstChild("Correction"):Remove()
        end

        local sunray = Instance.new("SunRaysEffect", lighting)
        local sky = lighting.Sky
        sky.SkyboxBk = "http://www.roblox.com/asset/?id=92464172"
        sky.SkyboxDn = "http://www.roblox.com/asset/?id=92464250"
        sky.SkyboxFt = "http://www.roblox.com/asset/?id=92464217"
        sky.SkyboxLf = "http://www.roblox.com/asset/?id=92464234"
        sky.SkyboxRt = "http://www.roblox.com/asset/?id=92464189"
        sky.SkyboxUp = "http://www.roblox.com/asset/?id=92464157"

        sky.StarCount = 3000
        sky.SunAngularSize = 21
        sky.MoonAngularSize = 11

        local correction = Instance.new("ColorCorrectionEffect", lighting)
        correction.Name = "Correction"
        correction.Saturation = -0.4
        correction.TintColor = Color3.fromRGB(255, 197, 197)
end
}
Commands["Sets your FieldOfView"] = {
    ["Aliases"] = {"!fieldofview", "!fov"};
    ["Function"] = function(Args)
        if Args[1] then 
            Camera.FieldOfView = tonumber(Args[1])
        end
        Notify("CSU GANG", "FieldOfView: "..tonumber(Args[1]), "", 3)
    end
}
Commands["Toggles Blink"] = {
    ["Aliases"] = {"!blink", "!blinkspeed"};
    ["Function"] = function(Args)
        Blink = not Blink 
        Notify("CSU GANG", "Blink: "..tostring(Blink), "", 3)
    end
}
Commands["Esp a Player"] = {
    ["Aliases"] = {"!esp", "!find"};
    ["Function"] = function(Args)
        if Args[1] then
            EspTarget = SearchPlayers(Args[1])
            if EspTarget then
                EspPlayer(EspTarget)
            end
        end
        Notify("CSU GANG", "Esp Target: "..tostring(EspTarget), "", 3)
    end
}
Commands["UnEsp Esp'd Player"] = {
    ["Aliases"] = {"!unesp", "!unfind"};
    ["Function"] = function(Args)
        if Args[1] then 
			local UnEspPlayer;UnEspPlayer = SearchPlayers(Args[1])
			if UnEspPlayer then 
				for _, v in next, UnEspPlayer.Character:GetDescendants() do 
					if v:IsA("BillboardGui") or v:IsA("TextLabel") then 
						v:Destroy() --[[if staircase(s) go brrrRRR]]
					end
				end
			end
		end
	end
}
Commands["Rejoins Current Game"] = {
    ["Aliases"] = {"!rejoin", "!rj"};
    ["Function"] = function()
        TPService:Teleport(game.PlaceId, Client)
    end
}
Commands["Resets Your Character"] = {
    ["Aliases"] = {"!r", "!reset", "!re", "!res"};
    ["Function"] = function()
       game.Players.LocalPlayer.Character.Humanoid.Health = 0
    end
}
Commands["Sets Camlock Target"] = {
    ["Aliases"] = {"!camlock", "!cam", "!cl", "!cml"};
    ["Function"] = function(Args)
        if Args[1] then 
            CamlockTarget = SearchPlayers(Args[1]);Camlock = true
        end
        Notify("CSU GANG", "Camlock Target: "..tostring(CamlockTarget), "", 3)
    end
}
Commands["UnCamlocks Camlocked Target"] = {
    ["Aliases"] = {"!uncamlock", "!uncam", "!uncl", "!uncml"};
    ["Function"] = function()
        CamlockTarget = nil;Camlock = false 
        Notify("CSU GANG", "Camlock: "..tostring(Camlock), "", 3)
    end
}
Commands["Sets Aimbot Target"] = {
    ["Aliases"] = {"!aim", "!al", "!target", "!aimlock", "!aimbot", "!shoot"};
    ["Function"] = function(Args)
        if Args[1] then 
            AimbotTarget = SearchPlayers(Args[1]);Aimbot = true
        end
        Notify("CSU GANG", "Aimbot Target: "..tostring(AimbotTarget), "", 3)
    end
}
Commands["UnAimbots Aimbotted Target"] = {
    ["Aliases"] = {"!unaim", "!unal", "!untarget", "!uns", "!unaimbot", "!unshoot"};
    ["Function"] = function()
        AimbotTarget = nil;Aimbot = false
        Notify("CSU GANG", "Aimbot: "..tostring(Aimbot), "", 3)
    end
}
Commands["View a Player"] = {
    ["Aliases"] = {"!view"};
    ["Function"] = function(Args)
        if Args[1] then 
            ViewTarget = SearchPlayers(Args[1]);Viewing = true 
        end
        Notify("CSU GANG", "View Target: "..tostring(ViewTarget), "", 3)
    end
}
Commands["UnView Viewed Target"] = {
    ["Aliases"] = {"!unview"};
    ["Function"] = function()
        ViewTarget = nil;Viewing = false
        Camera.CameraSubject = Client.Character
        Notify("CSU GANG", "Viewing: "..tostring(Viewing), "", 3)
    end
}
Commands["Sets Aimvelocity"] = {
    ["Aliases"] = {"!aimvelocity", "!av"};
    ["Function"] = function(Args)
        if Args[1] then 
            Aimvelocity = tonumber(Args[1])
        end
        Notify("CSU GANG", "Aimvelocity: "..tonumber(Args[1]), "", 3)
    end
}
Commands["Toggles Noclip"] = {
    ["Aliases"] = {"!noclip", "!nc", "!nclip"};
    ["Function"] = function()
        Noclip = not Noclip 
        Notify("CSU GANG", "Noclip: "..tostring(Noclip), "", 3)
    end
}
Commands["Sets Blinkspeed"] = {
    ["Aliases"] = {"!bs", "!blinkspeed"};
    ["Function"] = function(Args)
        if Args[1] then 
            Blinkspeed = tonumber(Args[1])
        end
        Notify("CSU GANG", "Blinkspeed: "..tonumber(Args[1]), "", 3)
    end
}
Commands["Sets Aimbot Part"] = {
    ["Aliases"] = {"!aimpart"};
    ["Function"] = function(Args)
        AimPart = Args[1]
        if AimPartTable[Args[1]] then 
            AimPart = AimPartTable[Args[1]] 
        end
        Notify("CSU GANG", "AimPart: "..tostring(AimPart), "", 3)
    end
}
Commands["Removes Chairs"] = {
    ["Aliases"] = { "!removeseats", "!rs", "!noseats", "!ns"};
    ["Function"] = function()
        
for i,v in next, workspace:GetDescendants() do
    if v:IsA'Seat' then
        v:Destroy()
    end
        end
Notify("CSU GANG", "Removed Seats")
    end
}
Commands["AutoReset"] = {
    ["Aliases"] = { "!autore", "!ar"};
    ["Function"] = function()
         game.StarterGui:SetCore("SendNotification", {
Title = "CSU GANG";
Text = "AutoReset Looped";
Duration = 5;
})
while wait() do
        pcall(function()
        if game.Players.LocalPlayer.Character.Head:FindFirstChild("Bone") then
        game.Players.LocalPlayer.Character.Humanoid.Health = 0
        end
        end)
        end
    end
}

RService.Stepped:Connect(function()
    if Camlock == true and CamlockTarget and CamlockTarget.Character and CamlockTarget.Character:FindFirstChild(CamPart) then 
        Camera.CoordinateFrame = CF(Camera.CoordinateFrame.p, CF(CamlockTarget.Character[CamPart].Position).p)
    end
    if Noclip == true then 
        for i = 1, #Client.Character:GetChildren() do
            local CG = Client.Character:GetChildren()[i]
            if CG:IsA("BasePart") then 
                CG.CanCollide = false 
            end
        end
        pcall(function()
            if Client and Client.Backpack then 
                Client.Backpack:FindFirstChild("Glock").Barrel.CanCollide = false 
            else
                Client.Character:FindFirstChild("Glock").Barrel.CanCollide = false
            end
        end)
    end
    if Viewing == true and ViewTarget ~= nil then 
        Camera.CameraSubject = ViewTarget.Character
    end
    if Flying and Client.Character then
        if Client.Character and Client.Character:FindFirstChild("Humanoid") then
            RService.Heartbeat:Wait()
            Client.Character.Humanoid.PlatformStand = false;Client.Character.Humanoid.Sit = false
            Client.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Running)
        end
	end
    if Client.Character:FindFirstChild("FlyPart") then
        Client.Character:FindFirstChild("FlyPart").CFrame = Client.Character.HumanoidRootPart.CFrame * CF(0, -3.5, 0)
    end
end)


print([[


]])
getgenv().Night = false
getgenv().Day = true 

local RService, LService = game:GetService"RunService", game:GetService"Lighting";

RService.RenderStepped:Connect(function()
    if LService and LService.ClockTime then
        if Night == true then 
            LService.ClockTime = 3;
        elseif Day == true then 
            LService.ClockTime = 14; 
        end
    end
end)
Client.Chatted:Connect(RunCommand)
local Input = game:GetService('UserInputService')
local ammo = false

game:GetService('RunService').Stepped:connect(
    function()
        if ammo then
                 if game.Workspace:FindFirstChild("Buy Ammo | $25") then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame =
                    game.Workspace["Buy Ammo | $25"].Head.CFrame
            end
           end
        game.Players.Localplayer.Backpack.ServerTraits.Stann.Value = 100
    end
)


Input.InputBegan:Connect(
    function(hotkey)
        if hotkey.KeyCode == Enum.KeyCode.Q then
            if Input:GetFocusedTextBox() == nil then
                 local SavePos = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                ammo = true
            end
        end
    end
)

Input.InputEnded:Connect(
    function(hotkey)
        if hotkey.KeyCode == Enum.KeyCode.G then
            if Input:GetFocusedTextBox() == nil then
                ammo = false
                  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = SavePos
            end
        end
    end
)
game:GetService("Workspace").FallenPartsDestroyHeight = math.huge-math.huge
Notify("CSU GANG", "Took "..string.format("%.3f", tick() - LoadingTime).." seconds to load", "" , 3)


local EspTable = {

[496721656] = {
        ['Name'] = "Cryptid_God (Owner)";
        ['Colour'] = Color3.fromRGB(255,255,0)
    };
[340544469] = {
        ['Name'] = "CSUowner (Owner/Admin)";
        ['Colour'] = Color3.fromRGB(255,0,0)
    };
[478979011] = {
        ['Name'] = "Scott/Admin";
        ['Colour'] = Color3.fromRGB(255,249,123)
    };
[710195933] = {
        ['Name'] = "KOS/Admin";
        ['Colour'] = Color3.fromRGB(255, 166, 184)
    };
[193003759] = {
        ['Name'] = "SPACEDGODS [Admin]";
        ['Colour'] = Color3.fromRGB(255, 128, 0)
    };
[2291506324] = {
        ['Name'] = "SPACEDGODS [Admin]";
        ['Colour'] = Color3.fromRGB(128, 0 ,128)
    };
}
local function EspNoteablePerson(Plr)
    local B = Instance.new('BillboardGui',Plr.Character.Head)
    B.Adornee = Plr.Character.Head
    B.Size = UDim2.new(0,100,0,100)
    B.StudsOffset = Vector3.new(0,1,0)
    B.AlwaysOnTop = true 
    local C = Instance.new('TextLabel',B)
    C.BackgroundTransparency = 1
    C.Position = UDim2.new(0,0,0,0)
    C.Size = UDim2.new(1,0,0,40)
    C.TextStrokeTransparency = 0.5
    C.TextSize = 13.8
    C.TextStrokeColor3 = EspTable[Plr.UserId].Colour
    C.TextColor3 = EspTable[Plr.UserId].Colour
    C.Text = EspTable[Plr.UserId].Name
end

local PlayersC = game:GetService'Players':GetPlayers()
for i = 1,#PlayersC do 
    local Plr = PlayersC[i]
    if EspTable[Plr.UserId] then
        local Head = Plr.Character:WaitForChild('Head',10)
        if Head then 
            EspNoteablePerson(Plr)
        end 
        Plr.CharacterAdded:Connect(function()
            Plr.Character:WaitForChild('Head',10)
            EspNoteablePerson(Plr)
        end)
    end
end 

game:GetService'Players'.PlayerAdded:Connect(function(Plr)
    if EspTable[Plr.UserId] then 
        Plr.CharacterAdded:Connect(function()
            EspNoteablePerson(Plr)
        end)
    end
end)
game:GetService'Players'.ChildAdded:Connect(function(Plr)
    if EspTable[Plr.UserId] then 
        Plr.CharacterAdded:Connect(function()
            EspNoteablePerson(Plr)
        end)
    end
end)


local RunService = game:GetService("RunService")

RunService.RenderStepped:Connect(function()
    if game.Players.LocalPlayer.Character.Humanoid then
        if game.Players.LocalPlayer.Character.Humanoid:findFirstChild("Bullet") then
            if game.Players.LocalPlayer.Character.Humanoid.Bullet:findFirstChild("Trail") then
                if game.Players.LocalPlayer.Character.Humanoid:findFirstChild("Bullet").Name == "BulletDone" then
                end
                if game.Players.LocalPlayer.Character.Humanoid:findFirstChild("Bullet"):findFirstChild("Trail").Lifetime < 0.21 then
                    game.Players.LocalPlayer.Character.Humanoid:findFirstChild("Bullet").Trail.Lifetime = 0.21
                    game.Players.LocalPlayer.Character.Humanoid:findFirstChild("Bullet").Trail.Transparency = NumberSequence.new(0)
                    game.Players.LocalPlayer.Character.Humanoid:findFirstChild("Bullet").Trail.Color = ColorSequence.new(Color3.fromRGB(255,0,0),Color3.fromRGB(255,0,0))
                    game.Players.LocalPlayer.Character.Humanoid:findFirstChild("Bullet").Name = "BulletDone"
                end
            end
        end
    end
end)

local P = game:GetService("Players")
local LP = P.LocalPlayer
local mouse = LP:GetMouse()

mouse.Button1Down:Connect(function()
	for _,a in pairs(LP.Character:GetChildren()) do
		if a:IsA("Tool") and a.Name == "Shotty" or a.Name == "Glock" then


			a.Fire:FireServer(mouse.Hit)



		end
	end
end)


game.Players.LocalPlayer:GetMouse().KeyDown:Connect(function(key)
 if key == "h" then
game.Players.LocalPlayer.Character.Humanoid.HipHeight = 1.7
game.Players.LocalPlayer.Character["Left Arm"]:Remove()
game.Players.LocalPlayer.Character["Left Leg"]:Remove()
game.Players.LocalPlayer.Character["Right Leg"]:Remove()
 end
end)

game.Players.LocalPlayer:GetMouse().KeyDown:Connect(function(key)
 if key == "r" then
     game.Players.LocalPlayer.Character.Humanoid.Health = 0
 end
end)

	
local ScreenGui = Instance.new("ScreenGui")
local TextLabel = Instance.new("TextLabel")



ScreenGui.Parent = game.CoreGui

TextLabel.Parent = ScreenGui
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1.000
TextLabel.Position = UDim2.new(0.00374999992, 0, 0.16312997, 0)
TextLabel.Size = UDim2.new(0, 200, 0, 50)
TextLabel.Font = Enum.Font.Gotham
TextLabel.Text = "C.S.U Gang"
TextLabel.TextColor3 = Color3.fromRGB(0, 0, 0)
TextLabel.TextSize = 32.000

-- Scripts:

local function HOUSK_fake_script() -- TextLabel.Script 
	local script = Instance.new('Script', TextLabel)

	local text = script.Parent
	local add = 10
	wait(1)
	local k = 1
	while k <= 255 do
		text.TextColor3 = Color3.new(k/255,0/255,0/255)
		k = k + add
		wait()
	end
	while true do
		k = 1
		while k <= 255 do
			text.TextColor3 = Color3.new(255/255,k/255,0/255)
			k = k + add
			wait()
		end
		k = 1
		while k <= 255 do
			text.TextColor3 = Color3.new(255/255 - k/255,255/255,0/255)
			k = k + add
			wait()
		end
		k = 1
		while k <= 255 do
			text.TextColor3 = Color3.new(0/255,255/255,k/255)
			k = k + add
			wait()
		end
		k = 1
		while k <= 255 do
			text.TextColor3 = Color3.new(0/255,255/255 - k/255,255/255)
			k = k + add
			wait()
		end
		k = 1
		while k <= 255 do
			text.TextColor3 = Color3.new(k/255,0/255,255/255)
			k = k + add
			wait()
		end
		k = 1
		while k <= 255 do
			text.TextColor3 = Color3.new(255/255,0/255,255/255 - k/255)
			k = k + add
			wait()
		end
		while k <= 255 do
			text.TextColor3 = Color3.new(255/255 - k/255,0/255,0/255)
			k = k + add
			wait()
		end
	end
end
coroutine.wrap(HOUSK_fake_script)()


local Key = "G"
local Toggle = false
--[[

    For symbols, put the name of the symbol, with uppercase starting letters.
    So for example, Semicolon, LessThan, Equals, Minus, Underscore, RightBracket, LeftControl
    all those would work
    Check out https://developer.roblox.com/en-us/api-reference/enum/KeyCode for a list of names that'll work

--]]

game:GetService("UserInputService").InputBegan:Connect(function(keyobject, stuffhappening)
    if keyobject.KeyCode == Enum.KeyCode[Key] and not stuffhappening then 
        Toggle = true
    end
end)

game:GetService("UserInputService").InputEnded:Connect(function(keyobject, stuffhappening)
    if keyobject.KeyCode == Enum.KeyCode[Key] and not stuffhappening then 
        Toggle = false
    end
end)


game:GetService('RunService').Stepped:connect(function()
    if Toggle then
power = 99999999

game:GetService('RunService').Stepped:connect(function()
game.Players.LocalPlayer.Character.Head.CanCollide = false
game.Players.LocalPlayer.Character.Torso.CanCollide = false
game.Players.LocalPlayer.Character["Left Leg"].CanCollide = false
game.Players.LocalPlayer.Character["Right Leg"].CanCollide = false
end)

wait(.1)
local bambam = Instance.new("BodyThrust")
bambam.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
bambam.Force = Vector3.new(power,111,power)
bambam.Location = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
    end
end)

game:GetService("RunService").RenderStepped:Connect(function()
local LService = game:GetService("Lighting")
LService.ClockTime = 14
end)

for i, v in pairs(game:GetService("Lighting"):GetDescendants()) do
    if v.Parent == game:GetService("Lighting") then
        v:Destroy()
    end
end

local Mouse = game:GetService("Players").LocalPlayer:GetMouse()
local Toggled = false
local Keybind = "e"

Mouse.KeyDown:Connect(function(Key)
   if Key == Keybind then
       if Toggled then
           Toggled = false
       else
           Toggled = true
           while Toggled and wait() do
               mouse1click()
           end
       end
   end
end)
