local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("troll", "GrapeTheme")

--trolling
local Tab = Window:NewTab("trolling")


local Section = Tab:NewSection("troll")


Section:NewButton("endermen", "ButtonInfo", function()
    --Settings:
local ScriptStarted = false
local Keybind = "E" --Set to whatever you want, has to be the name of a KeyCode Enum.
local Transparency = true --Will make you slightly transparent when you are invisible. No reason to disable.
local NoClip = false --Will make your fake character no clip.

local Player = game:GetService("Players").LocalPlayer
local RealCharacter = Player.Character or Player.CharacterAdded:Wait()

local IsInvisible = false

RealCharacter.Archivable = true
local FakeCharacter = RealCharacter:Clone()
local Part
Part = Instance.new("Part", workspace)
Part.Anchored = true
Part.Size = Vector3.new(200, 1, 200)
Part.CFrame = CFrame.new(0, -500, 0) --Set this to whatever you want, just far away from the map.
Part.CanCollide = true
FakeCharacter.Parent = workspace
FakeCharacter.HumanoidRootPart.CFrame = Part.CFrame * CFrame.new(0, 5, 0)

for i, v in pairs(RealCharacter:GetChildren()) do
  if v:IsA("LocalScript") then
      local clone = v:Clone()
      clone.Disabled = true
      clone.Parent = FakeCharacter
  end
end
if Transparency then
  for i, v in pairs(FakeCharacter:GetDescendants()) do
      if v:IsA("BasePart") then
          v.Transparency = 0.7
      end
  end
end
local CanInvis = true
function RealCharacterDied()
  CanInvis = false
  RealCharacter:Destroy()
  RealCharacter = Player.Character
  CanInvis = true
  isinvisible = false
  FakeCharacter:Destroy()
  workspace.CurrentCamera.CameraSubject = RealCharacter.Humanoid

  RealCharacter.Archivable = true
  FakeCharacter = RealCharacter:Clone()
  Part:Destroy()
  Part = Instance.new("Part", workspace)
  Part.Anchored = true
  Part.Size = Vector3.new(200, 1, 200)
  Part.CFrame = CFrame.new(9999, 9999, 9999) --Set this to whatever you want, just far away from the map.
  Part.CanCollide = true
  FakeCharacter.Parent = workspace
  FakeCharacter.HumanoidRootPart.CFrame = Part.CFrame * CFrame.new(0, 5, 0)

  for i, v in pairs(RealCharacter:GetChildren()) do
      if v:IsA("LocalScript") then
          local clone = v:Clone()
          clone.Disabled = true
          clone.Parent = FakeCharacter
      end
  end
  if Transparency then
      for i, v in pairs(FakeCharacter:GetDescendants()) do
          if v:IsA("BasePart") then
              v.Transparency = 0.7
          end
      end
  end
 RealCharacter.Humanoid.Died:Connect(function()
 RealCharacter:Destroy()
 FakeCharacter:Destroy()
 end)
 Player.CharacterAppearanceLoaded:Connect(RealCharacterDied)
end
RealCharacter.Humanoid.Died:Connect(function()
 RealCharacter:Destroy()
 FakeCharacter:Destroy()
 end)
Player.CharacterAppearanceLoaded:Connect(RealCharacterDied)
local PseudoAnchor
game:GetService "RunService".RenderStepped:Connect(
  function()
      if PseudoAnchor ~= nil then
          PseudoAnchor.CFrame = Part.CFrame * CFrame.new(0, 5, 0)
      end
       if NoClip then
      FakeCharacter.Humanoid:ChangeState(11)
       end
  end
)

PseudoAnchor = FakeCharacter.HumanoidRootPart
local function Invisible()
  if IsInvisible == false then
      local StoredCF = RealCharacter.HumanoidRootPart.CFrame
      RealCharacter.HumanoidRootPart.CFrame = FakeCharacter.HumanoidRootPart.CFrame
      FakeCharacter.HumanoidRootPart.CFrame = StoredCF
      RealCharacter.Humanoid:UnequipTools()
      Player.Character = FakeCharacter
      workspace.CurrentCamera.CameraSubject = FakeCharacter.Humanoid
      PseudoAnchor = RealCharacter.HumanoidRootPart
      for i, v in pairs(FakeCharacter:GetChildren()) do
          if v:IsA("LocalScript") then
              v.Disabled = false
          end
      end

      IsInvisible = true
  else
      local StoredCF = FakeCharacter.HumanoidRootPart.CFrame
      FakeCharacter.HumanoidRootPart.CFrame = RealCharacter.HumanoidRootPart.CFrame
     
      RealCharacter.HumanoidRootPart.CFrame = StoredCF
     
      FakeCharacter.Humanoid:UnequipTools()
      Player.Character = RealCharacter
      workspace.CurrentCamera.CameraSubject = RealCharacter.Humanoid
      PseudoAnchor = FakeCharacter.HumanoidRootPart
      for i, v in pairs(FakeCharacter:GetChildren()) do
          if v:IsA("LocalScript") then
              v.Disabled = true
          end
      end
      IsInvisible = false
  end
end

game:GetService("UserInputService").InputBegan:Connect(
  function(key, gamep)
      if gamep then
          return
      end
      if key.KeyCode.Name:lower() == Keybind:lower() and CanInvis and RealCharacter and FakeCharacter then
          if RealCharacter:FindFirstChild("HumanoidRootPart") and FakeCharacter:FindFirstChild("HumanoidRootPart") then
              Invisible()
          end
      end
  end
)
local Sound = Instance.new("Sound",game:GetService("SoundService"))
Sound.SoundId = "rbxassetid://232127604"
Sound:Play()
game:GetService("StarterGui"):SetCore("SendNotification",{["Title"] = "Invisible Toggle Loaded",["Text"] = "Press "..Keybind.." to become change visibility.",["Duration"] = 20,["Button1"] = "Okay."})
end)


Section:NewButton("big boi", "be the man of the house unlike ur dad", function()
    local LocalPlayer = game:GetService("Players").LocalPlayer
local Character = LocalPlayer.Character
local Humanoid = Character:FindFirstChildOfClass("Humanoid")

function rm()
	for i,v in pairs(Character:GetDescendants()) do
		if v:IsA("BasePart") then
			if v.Name == "Handle" or v.Name == "Head" then
				if Character.Head:FindFirstChild("OriginalSize") then
					Character.Head.OriginalSize:Destroy()
				end
			else
				for i,cav in pairs(v:GetDescendants()) do
					if cav:IsA("Attachment") then
						if cav:FindFirstChild("OriginalPosition") then
							cav.OriginalPosition:Destroy()  
						end
					end
				end
				v:FindFirstChild("OriginalSize"):Destroy()
				if v:FindFirstChild("AvatarPartScaleType") then
					v:FindFirstChild("AvatarPartScaleType"):Destroy()
				end
			end
		end
	end
end

rm()
wait(0.5)
Humanoid:FindFirstChild("BodyProportionScale"):Destroy()
wait(1)

rm()
wait(0.5)
Humanoid:FindFirstChild("BodyHeightScale"):Destroy()
wait(1)

rm()
wait(0.5)
Humanoid:FindFirstChild("BodyWidthScale"):Destroy()
wait(1)

rm()
wait(0.5)
Humanoid:FindFirstChild("BodyDepthScale"):Destroy()
wait(1)

rm()
wait(0.5)
Humanoid:FindFirstChild("HeadScale"):Destroy()
wait(1)
end)


Section:NewSlider("speed", "run faster then ur dad", 500, 16, function(s) -- 500 (MaxValue) | 0 (MinValue)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = s
end)


Section:NewButton("fe fling", "make ppl die!", function()
    for i,v in next, game:GetService("Players").LocalPlayer.Character:GetDescendants() do
        if v:IsA("BasePart") and v.Name ~="HumanoidRootPart" then
        game:GetService("RunService").Heartbeat:connect(function()
        v.Velocity = Vector3.new(0,-30,0)
        wait(0.5)
        end)
        end
        end
        
        function rmesh(HatName)
        for _,mesh in next, workspace[game.Players.LocalPlayer.Name][HatName]:GetDescendants() do
        if mesh:IsA("Mesh") or mesh:IsA("SpecialMesh") then
        mesh:Remove()
        end
        end
        end
        
        function create(part, parent, position, rotation)
        part.AccessoryWeld:Remove()
        Instance.new("Attachment",part)
        Instance.new("AlignPosition",part)
        Instance.new("AlignOrientation",part)
        Instance.new("Attachment",parent)
        part.AlignPosition.Attachment0 = part.Attachment
        part.AlignOrientation.Attachment0 = part.Attachment
        part.AlignPosition.Attachment1 = parent.Attachment
        part.AlignOrientation.Attachment1 = parent.Attachment
        part.Attachment.Position = position
        part.Attachment.Orientation = rotation
        part.AlignPosition.Responsiveness = 200
        part.AlignOrientation.Responsiveness = 200
        part.AlignPosition.MaxForce = 9999999
        part.AlignPosition.RigidityEnabled = false
        part.AlignOrientation.MaxTorque = 9999999
        end
        
        local LocalPlayer = game.Players.LocalPlayer
        
        function eswait(num)
        if num == 0 or num == nil then
        game:service("RunService").Stepped:wait(0)
        else
        for i = 0, num do
        game:service("RunService").Stepped:wait(0)
        end
        end
        end
        
        function makepart(hat,part)
        Instance.new('Part',workspace[LocalPlayer.Name])
        workspace[LocalPlayer.Name].Part.Name = 'lerp'..hat
        workspace[LocalPlayer.Name]['lerp'..hat].CanCollide = false
        workspace[LocalPlayer.Name]['lerp'..hat].Size = workspace[LocalPlayer.Name][hat].Handle.Size
        workspace[LocalPlayer.Name]['lerp'..hat].Transparency = 1
        Instance.new('Weld',workspace[LocalPlayer.Name]['lerp'..hat])
        create(workspace[LocalPlayer.Name][hat].Handle,workspace[LocalPlayer.Name]['lerp'..hat],Vector3.new(),Vector3.new())
        workspace[LocalPlayer.Name]['lerp'..hat].Weld.Part0 = workspace[LocalPlayer.Name]['lerp'..hat]
        workspace[LocalPlayer.Name]['lerp'..hat].Weld.Part1 = workspace[LocalPlayer.Name][part]
        workspace[LocalPlayer.Name]['lerp'..hat].Weld.C0 = workspace[LocalPlayer.Name]['lerp'..hat].CFrame:inverse() * workspace[LocalPlayer.Name][part].CFrame * CFrame.new(0,0,0) * CFrame.Angles(math.rad(0),math.rad(0),0)
        end
        
        local hatsine = 0
        
        local hatchange = 1
        
        function clerp(hat,ppx,ppy,pppz,rrrx,rrry,rrz,lppx,lppy,lpppz,lrrrx,lrrry,lrrz,speed)
        coroutine.wrap(function()
        while true do
        hatsine = hatsine + speed
        workspace[game.Players.LocalPlayer.Name]['lerp'..hat].Weld.C0 = workspace[game.Players.LocalPlayer.Name]['lerp'..hat].Weld.C0:lerp(CFrame.new(ppx + lppx * math.sin(hatsine/11), ppy + lppy * math.sin(hatsine/11), pppz + lpppz * math.sin(hatsine/11)) * CFrame.Angles(math.rad(rrrx + lrrrx * math.sin(hatsine/11)), math.rad(rrry + lrrry * math.sin(hatsine/11)), math.rad(rrz + lrrz * math.sin(hatsine/11))),0.1)
        eswait()
        end
        end)()
        end
        
        local player = game.Players.LocalPlayer
        local character1 = player.Character
        local mouse = player:GetMouse()
        
        local fakebody = Instance.new("Part", character1)
        fakebody.Transparency = 1
        fakebody.Anchored = true
        fakebody.CanCollide = false
        fakebody.Position = character1.Head.Position
        fakebody.Name = "FPart"
        wait()
        _G.ReanimationType = "PDeath" --PDeath, Fling, Simple
        _G.Velocity = Vector3.new(36,0,0)
        _G.FlingBlock = true
        _G.FlingBlockTransparency = 1
        _G.HighlightFlingBlock = true
        _G.FlingBlockPosition = "FPart"
        _G.HighlightFlingBlockColor = Color3.fromRGB(255,0,0)
        
        loadstring(game:HttpGet("https://raw.githubusercontent.com/GelatekWasTaken/Reanimation.lua/main/Main/Main.lua"))()
        wait(1)
        
        mouse.KeyDown:connect(function(key)
            if key == "e" then
            character1.Reanimate.FPart.Position = mouse.Hit.p
            end
        end)
        
        rmesh('Pink Hair')
        rmesh('Kate Hair')
        
        makepart('Kate Hair','Right Arm')
        clerp('Kate Hair',0,1,0,0,0,0,0,0,0,0,0,0,1)
        
        makepart('Pink Hair','Right Arm')
        clerp('Pink Hair',0,0.5,-2,-90,0,0,0,0,0,0,0,0,1)
        
        local Scale = game.Players.LocalPlayer.Character.Torso.Size.X/2*(game.Players.LocalPlayer.Character.Torso:FindFirstChild("ScaleInserted") ~= nil and game.Players.LocalPlayer.Character.Torso:FindFirstChild("ScaleInserted").Scale.Z or 1)*0.8
        local Speed = 20*Scale
        local Gravity = 0.1
        
        local Player = game.Players.LocalPlayer
        local Character = Player.Character.Reanimate
        local Humanoid = Character.Humanoid
        Humanoid:SetStateEnabled(Enum.HumanoidStateType.Ragdoll,false)
        local Torso = Character.HumanoidRootPart
        local Mouse = game.Players.LocalPlayer:GetMouse()
        local RenderStepped = game:GetService("RunService").RenderStepped
        local Camera = Workspace.CurrentCamera
        Camera:ClearAllChildren()
        local Model = Instance.new("Model",Character)
        local IgnoreList = {Character,Workspace.Terrain}
        
        local Part0Joint = CFrame.new(Vector3.new(1,0.75,0)*Scale*1.25)
        local Part1Joint = CFrame.new(Vector3.new(-0.5,0.75,0)*Scale*1.25)
        local RotationOffset = CFrame.Angles(math.rad(90),math.rad(0),0)
        local Gangster = false
        
        local Part0JointHead = CFrame.new(Vector3.new(0,1,0)*Scale*1.25)
        local Part1JointHead = CFrame.new(Vector3.new(0,-0.5,0)*Scale*1.25)
        local RotationOffsetHead = CFrame.Angles(0,0,0)
        
        local Handle = Instance.new("Part",Model)
        Handle.CanCollide = false
        Handle.Name = "Handle"
        Handle.Position = Vector3.new(0,100,0)
        Handle:BreakJoints()
        Handle.FormFactor = "Custom"
        Handle.Size = Vector3.new(0.2,0.2,0.2)
        Handle.TopSurface = "SmoothNoOutlines"
        Handle.BottomSurface = "SmoothNoOutlines"
        Handle.FrontSurface = "SmoothNoOutlines"
        Handle.BackSurface = "SmoothNoOutlines"
        Handle.RightSurface = "SmoothNoOutlines"
        Handle.LeftSurface = "SmoothNoOutlines"
        Handle.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Handle)
        Mesh.Scale = Vector3.new(0.25,1,0.4) / 0.2 * Scale
        local HandleWeld = Instance.new("Motor6D")
        HandleWeld.Part0 = Character["Right Arm"]
        HandleWeld.Part1 = Handle
        HandleWeld.C0 = CFrame.new(Vector3.new(0,-1,0)*Scale) * CFrame.Angles(math.rad(-105),0,0)
        HandleWeld.Parent = Handle
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("CylinderMesh",Part)
        Mesh.Scale = Vector3.new(0.07,0.2,0.07) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(-0.115,-0.475,-0.190)*Scale) * CFrame.Angles(0,0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("CylinderMesh",Part)
        Mesh.Scale = Vector3.new(0.07,0.2,0.07) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0.115,-0.475,0.190)*Scale) * CFrame.Angles(0,0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("CylinderMesh",Part)
        Mesh.Scale = Vector3.new(0.07,0.2,0.07) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(-0.115,-0.475,0.190)*Scale) * CFrame.Angles(0,0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("CylinderMesh",Part)
        Mesh.Scale = Vector3.new(0.07,0.2,0.07) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0.115,-0.475,-0.190)*Scale) * CFrame.Angles(0,0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.23,0.2,0.1) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0,-0.475,-0.175)*Scale) * CFrame.Angles(0,0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.23,0.2,0.1) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0,-0.475,0.175)*Scale) * CFrame.Angles(0,0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.1,0.2,0.38) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(-0.1,-0.475,0)*Scale) * CFrame.Angles(0,0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.1,0.2,0.38) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0.1,-0.475,0)*Scale) * CFrame.Angles(0,0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.1,0.3,0.05) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.Angles(math.rad(15),0,0) * CFrame.new(Vector3.new(0,0.25,-0.75)*Scale) * CFrame.Angles(math.rad(-10),0,0)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.1,0.05,0.625) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.Angles(math.rad(15),0,0) * CFrame.new(Vector3.new(0,0.1,-0.435)*Scale)
        PartWeld.Parent = Part
        
        for i = 0,80,10 do
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.25,0.15,0.03555*2) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0,0.15,0.315)*Scale) * CFrame.Angles(math.rad(i-65),0,0) * CFrame.new(Vector3.new(0,0.2,0)*Scale)
        PartWeld.Parent = Part
        end
        
        local Barrel = Instance.new("Part",Model)
        Barrel.CanCollide = false
        Barrel.Position = Vector3.new(0,100,0)
        Barrel:BreakJoints()
        Barrel.FormFactor = "Custom"
        Barrel.Size = Vector3.new(0.2,0.2,0.2)
        Barrel.TopSurface = "SmoothNoOutlines"
        Barrel.BottomSurface = "SmoothNoOutlines"
        Barrel.FrontSurface = "SmoothNoOutlines"
        Barrel.BackSurface = "SmoothNoOutlines"
        Barrel.RightSurface = "SmoothNoOutlines"
        Barrel.LeftSurface = "SmoothNoOutlines"
        Barrel.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Barrel)
        Mesh.Scale = Vector3.new(0.25,0.2,2) / 0.2 * Scale
        local BarrelWeld = Instance.new("Motor6D")
        BarrelWeld.Part0 = Handle
        BarrelWeld.Part1 = Barrel
        BarrelWeld.C0 = CFrame.Angles(math.rad(15),0,0) * CFrame.new(Vector3.new(0,0.5,-0.7)*Scale)
        BarrelWeld.Parent = Barrel
        
        local Barrel1 = Barrel
        
        local Barrel2 = Instance.new("Part",Model)
        Barrel2.CanCollide = false
        Barrel2.Position = Vector3.new(0,100,0)
        Barrel2:BreakJoints()
        Barrel2.FormFactor = "Custom"
        Barrel2.Size = Vector3.new(0.2,0.2,0.2)
        Barrel2.TopSurface = "SmoothNoOutlines"
        Barrel2.BottomSurface = "SmoothNoOutlines"
        Barrel2.FrontSurface = "SmoothNoOutlines"
        Barrel2.BackSurface = "SmoothNoOutlines"
        Barrel2.RightSurface = "SmoothNoOutlines"
        Barrel2.LeftSurface = "SmoothNoOutlines"
        Barrel2.BrickColor = BrickColor.new("Really black")
        local Mesh = Instance.new("BlockMesh",Barrel2)
        Mesh.Scale = Vector3.new(0.25,0.25,2) / 0.2 * Scale
        local Barrel2Weld = Instance.new("Motor6D")
        Barrel2Weld.Part0 = Barrel
        Barrel2Weld.Part1 = Barrel2
        Barrel2Weld.C0 = CFrame.new(Vector3.new(0,0.225,0)*Scale)
        Barrel2Weld.Parent = Barrel2
        
        local RealBarrel = Instance.new("Part",Model)
        RealBarrel.CanCollide = false
        RealBarrel.Position = Vector3.new(0,100,0)
        RealBarrel:BreakJoints()
        RealBarrel.FormFactor = "Custom"
        RealBarrel.Size = Vector3.new(0.2,0.2,0.2)
        RealBarrel.TopSurface = "SmoothNoOutlines"
        RealBarrel.BottomSurface = "SmoothNoOutlines"
        RealBarrel.FrontSurface = "SmoothNoOutlines"
        RealBarrel.BackSurface = "SmoothNoOutlines"
        RealBarrel.RightSurface = "SmoothNoOutlines"
        RealBarrel.LeftSurface = "SmoothNoOutlines"
        RealBarrel.BrickColor = BrickColor.new("Dark grey metallic")
        local Mesh = Instance.new("CylinderMesh",RealBarrel)
        Mesh.Scale = Vector3.new(0.2,2,0.2) / 0.2 * Scale
        local RealBarrelWeld = Instance.new("Motor6D")
        RealBarrelWeld.Part0 = Barrel
        RealBarrelWeld.Part1 = RealBarrel
        RealBarrelWeld.C0 = CFrame.new(Vector3.new(0,0.1,-0.01)*Scale) * CFrame.Angles(math.rad(-90),0,0)
        RealBarrelWeld.Parent = RealBarrel
        
        for i = 1,75,15 do
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.05,0.065,0.05) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Handle
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0,0.525,-0.515)*Scale) * CFrame.Angles(math.rad(i),0,0) * CFrame.new(Vector3.new(0,0,0.2)*Scale)
        PartWeld.Parent = Part
        end
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Really black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.05,0.11,0.1) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Barrel2
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0.06,0.135,0.925)*Scale)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Really black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.05,0.11,0.1) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Barrel2
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(-0.06,0.135,0.925)*Scale)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Really black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.025,0.1,0.1) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Barrel2
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0,0.135,-0.925)*Scale)
        PartWeld.Parent = Part
        
        local Part = Instance.new("Part",Model)
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.Transparency = 1
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Really black")
        local Mesh = Instance.new("BlockMesh",Part)
        Mesh.Scale = Vector3.new(0.1,0.1,0.1) / 0.2 * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = Barrel
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0,0,-5)*Scale)
        PartWeld.Parent = Part
        
        local Light = Instance.new("PointLight",Part)
        Light.Color = BrickColor.new("Gold").Color
        Light.Enabled = true
        Light.Shadows = true
        Light.Brightness = 0
        Light.Range = 6
        
        local Part = Instance.new("Part",Model)
        Part.Material = "Neon"
        Part.CanCollide = false
        Part.Position = Vector3.new(0,100,0)
        Part:BreakJoints()
        Part.FormFactor = "Custom"
        Part.Size = Vector3.new(0.2,0.2,0.2)
        Part.TopSurface = "SmoothNoOutlines"
        Part.BottomSurface = "SmoothNoOutlines"
        Part.FrontSurface = "SmoothNoOutlines"
        Part.BackSurface = "SmoothNoOutlines"
        Part.RightSurface = "SmoothNoOutlines"
        Part.LeftSurface = "SmoothNoOutlines"
        Part.BrickColor = BrickColor.new("Bright yellow")
        Part.Transparency = 0.25
        local RecoilMesh = Instance.new("SpecialMesh",Part)
        RecoilMesh.MeshType = "FileMesh"
        RecoilMesh.MeshId = "http://www.roblox.com/Asset/?id=1323306"
        RecoilMesh.TextureId = "http://www.roblox.com/Asset/?id=98896228"
        RecoilMesh.Scale = Vector3.new(0.175,0,0.175) * Scale
        local PartWeld = Instance.new("Motor6D")
        PartWeld.Part0 = RealBarrel
        PartWeld.Part1 = Part
        PartWeld.C0 = CFrame.new(Vector3.new(0,0.95,0)*Scale)
        PartWeld.Parent = Part
        
        function ShootBullet(Target,barrel)
        local barrel = barrel or Barrel
        local Bullet = Instance.new("Part",Workspace)
        Barrel.CanCollide = false
        Bullet.FormFactor = "Custom"
        Bullet.Size = Vector3.new(0.2,0.2,5)*Scale
        Bullet.TopSurface = "Smooth"
        Bullet.BottomSurface = "Smooth"
        Bullet.Anchored = true
        Bullet.CanCollide = false
        Bullet.CFrame = CFrame.new((barrel.CFrame*CFrame.new(0,0,-barrel.Size.Z*barrel.Mesh.Scale.Z/2)).p,Target)*CFrame.new(0,0,-Bullet.Size.Z/2)
        Bullet.Transparency = 0.1
        Bullet.BrickColor = BrickColor.new("Gold")
        --[[local Mesh = Instance.new("SpecialMesh",Bullet)
        Mesh.MeshType = "FileMesh"
        Mesh.Scale = Vector3.new(0.5,0.5,0.2)
        Mesh.MeshId = "http://www.roblox.com/asset/?id=2697549"
        --Mesh.TextureId = "http://www.roblox.com/asset/?id=2697544"]]
        local Mesh = Instance.new("BlockMesh",Bullet)
        Mesh.Scale = Vector3.new(0.2,0.2,5)*Scale/Bullet.Size
        IgnoreList[#IgnoreList+1] = Bullet
        RenderStepped:wait()
        for i = Speed,1000,Speed do -- Loop to do the bullet movement and stuff.
        local ray,Hit,Pos,SurfaceNormal;
        ray = Ray.new(Bullet.Position,((Bullet.CFrame*CFrame.Angles(math.rad(-Gravity),0,0)*CFrame.new(0,0,-Speed)).p-Bullet.Position).unit*Speed)
        Hit,Pos,SurfaceNormal = Workspace:FindPartOnRayWithIgnoreList(ray,IgnoreList)
        Bullet.CFrame = Bullet.CFrame*CFrame.Angles(math.rad(-Gravity),0,0)*CFrame.new(0,0,-Speed)
        if Hit ~= nil then
        local Hum = Hit.Parent:FindFirstChild("Humanoid") or Hit.Parent.Parent:FindFirstChild("Humanoid") or (Hit.Parent.Parent.Parent ~= nil and Hit.Parent.Parent.Parent:FindFirstChild("Humanoid"))
        if Hum ~= nil then
        Hum:TakeDamage((((Gangster and math.random(0,0) or math.random(0,0))*Scale)/100)*Hum.MaxHealth)
        end
        break
        end
        RenderStepped:wait()
        end
        Bullet:Destroy()
        end
        
        Mouse.Button1Down:connect(function()
        if not Down and not DB then
        Down = true
        while Down do
        if Humanoid.Health == 0 then break end
        if not DB then
        DB = true
        local Sound = Instance.new("Sound",Barrel)
        Sound.SoundId = "http://www.roblox.com/Asset/?id=165946426" -- 132373574
        Sound.Volume = 5*Scale
        Sound.Pitch = (math.random(70,110)/100)/((Scale < 0.25 and 0.25) or (Scale > 4 and 4) or Scale)
        Sound:Play()
        Spawn(function()
        ShootBullet(Mouse.Hit.p,Barrel1)
        end)
        RecoilMesh.VertexColor = Vector3.new(1,math.random(160,245)/255,20/255)
        PartWeld.C0 = PartWeld.C0 * CFrame.Angles(0,math.rad(math.random(-40,40)),0)
        local Shell = Instance.new("Part",Workspace)
        Shell.FormFactor = "Custom"
        Shell.BrickColor = BrickColor.new("Bright yellow")
        Shell.Size = Vector3.new(0.2,0.5,0.2)*Scale
        Shell.CFrame = Barrel.CFrame*CFrame.new(0.5,0.5,0)*CFrame.Angles(math.rad(-90),0,0)
        Shell.Velocity = ((Barrel.CFrame*CFrame.new(5,0,math.random(-2,2))).p-Barrel.CFrame.p)*5*Scale
        local Mesh = Instance.new("CylinderMesh",Shell)
        Mesh.Scale = Vector3.new(0.2,0.5,0.2)*Scale/Shell.Size
        Spawn(function()
        wait(5)
        Shell:Destroy()
        end)
        for i = 1,20,7.5 do
        character1.Reanimate.FPart.Position = mouse.Hit.p
        RotationOffset = RotationOffset*CFrame.Angles(math.rad(7.5),0,0)
        Part1Joint = Part1Joint*CFrame.new(Vector3.new(0,-0.15,0)*Scale)
        Barrel2Weld.C0 = Barrel2Weld.C0*CFrame.new(Vector3.new(0,0,0.15)*Scale)
        Light.Brightness = Light.Brightness+38
        RecoilMesh.Scale = RecoilMesh.Scale+(Vector3.new(0,0.375,0)*Scale)
        RenderStepped:wait()
        end
        wait(0.02)
        for i = 1,20,3.75 do
        character1.Reanimate.FPart.Position = mouse.Hit.p
        RotationOffset = RotationOffset*CFrame.Angles(math.rad(-3.75),0,0)
        Part1Joint = Part1Joint*CFrame.new(Vector3.new(0,0.075,0)*Scale)
        Barrel2Weld.C0 = Barrel2Weld.C0*CFrame.new(Vector3.new(0,0,-0.075)*Scale)
        Light.Brightness = Light.Brightness-19
        RecoilMesh.Scale = RecoilMesh.Scale+(Vector3.new(0,-0.1875,0)*Scale)
        RenderStepped:wait()
        end
        wait(0.02)
        DB = false
        end
        end
        end
        end)
        
        Mouse.Button1Up:connect(function()
        Down = false
        end)
        
        Mouse.KeyDown:connect(function(Key)
        if Key:lower() == "g" and not DB then
        DB = true
        if Gangster == true then
        for i = 1,70,5 do
        RotationOffset = RotationOffset*CFrame.Angles(0,math.rad(-5),0)
        RenderStepped:wait()
        end
        Gangster = false
        else
        for i = 1,70,5 do
        RotationOffset = RotationOffset*CFrame.Angles(0,math.rad(5),0)
        RenderStepped:wait()
        end
        Gangster = true
        end
        DB = false
        end
        end)
        
        local Weld = Instance.new("Weld")
        Weld.Part0 = Torso
        Weld.Part1 = Character["Right Arm"]
        Weld.Parent = Torso
        
        local Weld2 = Instance.new("Weld")
        Weld2.Part0 = Torso
        Weld2.Part1 = Character.Head
        Weld2.Parent = Torso
        
        local RA = Character["Right Arm"]
        
        game:GetService("RunService"):BindToRenderStep("Pistol",Enum.RenderPriority.Character.Value,function()
        local Point = Torso.CFrame:vectorToObjectSpace(Mouse.Hit.p-Torso.CFrame.p)
        if Point.Z > 0 then
        if Point.X > 0 then
        Torso.CFrame = CFrame.new(Torso.Position,Vector3.new(Mouse.Hit.X,Torso.Position.Y,Mouse.Hit.Z))*CFrame.Angles(0,math.rad(90),0)
        elseif Point.X < 0 then
        Torso.CFrame = CFrame.new(Torso.Position,Vector3.new(Mouse.Hit.X,Torso.Position.Y,Mouse.Hit.Z))*CFrame.Angles(0,math.rad(-90),0)
        end
        end
        
        local CFr = (Torso.CFrame*Part0Joint):toObjectSpace(CFrame.new((Torso.CFrame*Part0Joint).p,Mouse.Hit.p))--RayEnd))
        Weld.C0 = Part0Joint * (CFr-CFr.p) * RotationOffset
        Weld.C1 = Part1Joint
        Weld.Part0 = Torso
        Weld.Part1 = RA
        local CFr = (Torso.CFrame*Part0JointHead):toObjectSpace(CFrame.new((Torso.CFrame*Part0JointHead).p,Mouse.Hit.p))--RayEnd))
        Weld2.C0 = Part0JointHead * (CFr-CFr.p) * RotationOffsetHead
        Weld2.C1 = Part1JointHead
        Weld2.Part0 = Torso
        Weld2.Part1 = Character.Head
        local Last = Scale
        Scale = game.Players.LocalPlayer.Character.Torso.Size.X/2*(game.Players.LocalPlayer.Character.Torso:FindFirstChild("ScaleInserted") ~= nil and game.Players.LocalPlayer.Character.Torso:FindFirstChild("ScaleInserted").Scale.Z or 1)*0.8
        Speed = 20*Scale
        if Scale ~= Last then
        Part0Joint = CFrame.new(Vector3.new(1,0.75,0)*Scale*1.25)
        Part1Joint = CFrame.new(Vector3.new(-0.5,0.75,0)*Scale*1.25)
        Part0JointHead = CFrame.new(Vector3.new(0,1,0)*Scale*1.25)
        Part1JointHead = CFrame.new(Vector3.new(0,-0.5,0)*Scale*1.25)
        end
        end)
end)


Section:NewButton("Telekinesis ", "use ur hands to umm work out hehehehe", function()
    local function a(b, c)
        local d = getfenv(c)
        local e =
            setmetatable(
            {},
            {__index = function(self, f)
                    if f == "script" then
                        return b
                    else
                        return d[f]
                    end
                end}
        )
        setfenv(c, e)
        return c
    end
    local g = {}
    local h = Instance.new("Model", game:GetService("Lighting"))
    local i = Instance.new("Tool")
    local j = Instance.new("Part")
    local k = Instance.new("Script")
    local l = Instance.new("LocalScript")
    local m = sethiddenproperty or set_hidden_property
    i.Name = "Telekinesis"
    i.Parent = h
    i.Grip = CFrame.new(0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 0, 0)
    i.GripForward = Vector3.new(-0, -1, -0)
    i.GripRight = Vector3.new(0, 0, 1)
    i.GripUp = Vector3.new(1, 0, 0)
    j.Name = "Handle"
    j.Parent = i
    j.CFrame = CFrame.new(-17.2635937, 15.4915619, 46, 0, 1, 0, 1, 0, 0, 0, 0, -1)
    j.Orientation = Vector3.new(0, 180, 90)
    j.Position = Vector3.new(-17.2635937, 15.4915619, 46)
    j.Rotation = Vector3.new(-180, 0, -90)
    j.Color = Color3.new(0.0666667, 0.0666667, 0.0666667)
    j.Transparency = 1
    j.Size = Vector3.new(1, 1.20000005, 1)
    j.BottomSurface = Enum.SurfaceType.Weld
    j.BrickColor = BrickColor.new("Really black")
    j.Material = Enum.Material.Metal
    j.TopSurface = Enum.SurfaceType.Smooth
    j.brickColor = BrickColor.new("Really black")
    k.Name = "LineConnect"
    k.Parent = i
    table.insert(
        g,
        a(
            k,
            function()
                wait()
                local n = script.Part2
                local o = script.Part1.Value
                local p = script.Part2.Value
                local q = script.Par.Value
                local color = script.Color
                local r = Instance.new("Part")
                r.TopSurface = 0
                r.BottomSurface = 0
                r.Reflectance = .5
                r.Name = "Laser"
                r.Locked = true
                r.CanCollide = false
                r.Anchored = true
                r.formFactor = 0
                r.Size = Vector3.new(1, 1, 1)
                local s = Instance.new("BlockMesh")
                s.Parent = r
                while true do
                    if n.Value == nil then
                        break
                    end
                    if o == nil or p == nil or q == nil then
                        break
                    end
                    if o.Parent == nil or p.Parent == nil then
                        break
                    end
                    if q.Parent == nil then
                        break
                    end
                    local t = CFrame.new(o.Position, p.Position)
                    local dist = (o.Position - p.Position).magnitude
                    r.Parent = q
                    r.BrickColor = color.Value.BrickColor
                    r.Reflectance = color.Value.Reflectance
                    r.Transparency = color.Value.Transparency
                    r.CFrame = CFrame.new(o.Position + t.lookVector * dist / 2)
                    r.CFrame = CFrame.new(r.Position, p.Position)
                    s.Scale = Vector3.new(.25, .25, dist)
                    wait()
                end
                r:remove()
                script:remove()
            end
        )
    )
    k.Disabled = true
    l.Name = "MainScript"
    l.Parent = i
    table.insert(
        g,
        a(
            l,
            function()
                wait()
                tool = script.Parent
                lineconnect = tool.LineConnect
                object = nil
                mousedown = false
                found = false
                BP = Instance.new("BodyPosition")
                BP.maxForce = Vector3.new(math.huge * math.huge, math.huge * math.huge, math.huge * math.huge)
                BP.P = BP.P * 1.1
                dist = nil
                point = Instance.new("Part")
                point.Locked = true
                point.Anchored = true
                point.formFactor = 0
                point.Shape = 0
                point.BrickColor = BrickColor.Black()
                point.Size = Vector3.new(1, 1, 1)
                point.CanCollide = false
                local s = Instance.new("SpecialMesh")
                s.MeshType = "Sphere"
                s.Scale = Vector3.new(.7, .7, .7)
                s.Parent = point
                handle = tool.Handle
                front = tool.Handle
                color = tool.Handle
                objval = nil
                local u = false
                local v = BP:clone()
                v.maxForce = Vector3.new(30000, 30000, 30000)
                function LineConnect(o, p, q)
                    local w = Instance.new("ObjectValue")
                    w.Value = o
                    w.Name = "Part1"
                    local x = Instance.new("ObjectValue")
                    x.Value = p
                    x.Name = "Part2"
                    local y = Instance.new("ObjectValue")
                    y.Value = q
                    y.Name = "Par"
                    local z = Instance.new("ObjectValue")
                    z.Value = color
                    z.Name = "Color"
                    local A = lineconnect:clone()
                    A.Disabled = false
                    w.Parent = A
                    x.Parent = A
                    y.Parent = A
                    z.Parent = A
                    A.Parent = workspace
                    if p == object then
                        objval = x
                    end
                end
                function onButton1Down(B)
                    if mousedown == true then
                        return
                    end
                    mousedown = true
                    coroutine.resume(
                        coroutine.create(
                            function()
                                local C = point:clone()
                                C.Parent = tool
                                LineConnect(front, C, workspace)
                                while mousedown == true do
                                    C.Parent = tool
                                    if object == nil then
                                        if B.Target == nil then
                                            local t = CFrame.new(front.Position, B.Hit.p)
                                            C.CFrame = CFrame.new(front.Position + t.lookVector * 1000)
                                        else
                                            C.CFrame = CFrame.new(B.Hit.p)
                                        end
                                    else
                                        LineConnect(front, object, workspace)
                                        break
                                    end
                                    wait()
                                end
                                C:remove()
                            end
                        )
                    )
                    while mousedown == true do
                        if B.Target ~= nil then
                            local D = B.Target
                            if D.Anchored == false then
                                object = D
                                dist = (object.Position - front.Position).magnitude
                                break
                            end
                        end
                        wait()
                    end
                    while mousedown == true do
                        if object.Parent == nil then
                            break
                        end
                        local t = CFrame.new(front.Position, B.Hit.p)
                        BP.Parent = object
                        BP.position = front.Position + t.lookVector * dist
                        wait()
                    end
                    BP:remove()
                    object = nil
                    objval.Value = nil
                end
                function onKeyDown(E, B)
                    local E = E:lower()
                    local F = false
                    if E == "q" then
                        if dist >= 5 then
                            dist = dist - 10
                        end
                    end
                    if E == "r" then
                        if object == nil then
                            return
                        end
                        for G, H in pairs(object:children()) do
                            if H.className == "BodyGyro" then
                                return nil
                            end
                        end
                        BG = Instance.new("BodyGyro")
                        BG.maxTorque = Vector3.new(math.huge, math.huge, math.huge)
                        BG.cframe = CFrame.new(object.CFrame.p)
                        BG.Parent = object
                        repeat
                            wait()
                        until object.CFrame == CFrame.new(object.CFrame.p)
                        BG.Parent = nil
                        if object == nil then
                            return
                        end
                        for G, H in pairs(object:children()) do
                            if H.className == "BodyGyro" then
                                H.Parent = nil
                            end
                        end
                        object.Velocity = Vector3.new(0, 0, 0)
                        object.RotVelocity = Vector3.new(0, 0, 0)
                        object.Orientation = Vector3.new(0, 0, 0)
                    end
                    if E == "e" then
                        dist = dist + 10
                    end
                    if E == "t" then
                        if dist ~= 10 then
                            dist = 10
                        end
                    end
                    if E == "y" then
                        if dist ~= 200 then
                            dist = 200
                        end
                    end
                    if E == "=" then
                        BP.P = BP.P * 1.5
                    end
                    if E == "-" then
                        BP.P = BP.P * 0.5
                    end
                end
                function onEquipped(B)
                    keymouse = B
                    local I = tool.Parent
                    human = I.Humanoid
                    human.Changed:connect(
                        function()
                            if human.Health == 0 then
                                mousedown = false
                                BP:remove()
                                point:remove()
                                tool:remove()
                            end
                        end
                    )
                    B.Button1Down:connect(
                        function()
                            onButton1Down(B)
                        end
                    )
                    B.Button1Up:connect(
                        function()
                            mousedown = false
                        end
                    )
                    B.KeyDown:connect(
                        function(E)
                            onKeyDown(E, B)
                        end
                    )
                    B.Icon = "rbxasset://textures\\GunCursor.png"
                end
                tool.Equipped:connect(onEquipped)
            end
        )
    )
    for J, H in pairs(h:GetChildren()) do
        H.Parent = game:GetService("Players").LocalPlayer.Backpack
        pcall(
            function()
                H:MakeJoints()
            end
        )
    end
    h:Destroy()
    for J, H in pairs(g) do
        spawn(
            function()
                pcall(H)
            end
        )
    end
end)


Section:NewButton("fake admin script", "fake kicking ppl", function()
    local Players = game.Players
Players.PlayerRemoving:Connect(function(player)
  -- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = ":kick "..player.Name,
    [2] = "All"
}

game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(unpack(args))


local args = {
    [1] = "[PENDULUM HUB ADMIN]: Player "..player.Name.. " has been kicked!",
    [2] = "All"
}

game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(unpack(args))
end)
print[[Made by xd_beaming]]
end)


Section:NewButton("tp tool", "pull out the item and click somwhere and then telaport", function()
    mouse = game.Players.LocalPlayer:GetMouse()
tool = Instance.new("Tool")
tool.RequiresHandle = false
tool.Name = "Click Teleport"
tool.Activated:connect(function()
local pos = mouse.Hit+Vector3.new(0,2.5,0)
pos = CFrame.new(pos.X,pos.Y,pos.Z)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = pos
end)
tool.Parent = game.Players.LocalPlayer.Backpack
end)


Section:NewButton("inf yeild", "be  a admin", function()
    loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
end)


Section:NewButton("FAKE ip logger", "make ppl shit there pants", function()
    local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("ImageLabel")
local TextLabel = Instance.new("TextLabel")
local TextLabel_2 = Instance.new("TextLabel")
local close = Instance.new("TextButton")
local TextLabel_3 = Instance.new("TextLabel")
local TextLabel_4 = Instance.new("TextLabel")
local username = Instance.new("TextBox")
local snatch = Instance.new("TextButton")
local TextButton_Roundify_12px = Instance.new("ImageLabel")
local miscbut = Instance.new("TextButton")
local MISC = Instance.new("ImageLabel")
local TextLabel_5 = Instance.new("TextLabel")
local TextLabel_6 = Instance.new("TextLabel")
local snatchall = Instance.new("TextButton")
local TextButton_Roundify_12px_2 = Instance.new("ImageLabel")
local TextLabel_7 = Instance.new("TextLabel")
Frame.Draggable = true
Frame.Active = true
Frame.Selectable = true
local sound = Instance.new("Sound")
sound.Parent = workspace
sound.SoundId = "rbxassetid://5292029547"
sound:Play()
 
--Properties:
 
ScreenGui.Parent = game.CoreGui
 
Frame.Name = "Frame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Frame.BackgroundTransparency = 1.000
Frame.Position = UDim2.new(0.152727276, 0, 0.277641267, 0)
Frame.Size = UDim2.new(0, 0, 0, 0)
Frame.ZIndex = 3
Frame.Image = "rbxassetid://3570695787"
Frame.ImageColor3 = Color3.fromRGB(20, 20, 20)
Frame.ScaleType = Enum.ScaleType.Slice
Frame.SliceCenter = Rect.new(100, 100, 100, 100)
Frame.SliceScale = 0.120
Frame.ClipsDescendants = true
 
TextLabel.Parent = Frame
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1.000
TextLabel.Position = UDim2.new(0.026143793, 0, 0.0232558139, 0)
TextLabel.Size = UDim2.new(0, 22, 0, 24)
TextLabel.ZIndex = 3
TextLabel.Font = Enum.Font.SourceSansBold
TextLabel.Text = "IP"
TextLabel.TextColor3 = Color3.fromRGB(255, 85, 0)
TextLabel.TextSize = 25.000
 
TextLabel_2.Parent = Frame
TextLabel_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_2.BackgroundTransparency = 1.000
TextLabel_2.Position = UDim2.new(0.0980392173, 0, 0.0232558139, 0)
TextLabel_2.Size = UDim2.new(0, 102, 0, 24)
TextLabel_2.ZIndex = 3
TextLabel_2.Font = Enum.Font.SourceSansBold
TextLabel_2.Text = "LOGGER"
TextLabel_2.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_2.TextSize = 25.000
 
close.Name = "close"
close.Parent = Frame
close.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
close.BackgroundTransparency = 1.010
close.Position = UDim2.new(0.934640527, 0, 0.0232558139, 0)
close.Size = UDim2.new(0, 20, 0, 20)
close.ZIndex = 3
close.Font = Enum.Font.SourceSansBold
close.Text = "X"
close.TextColor3 = Color3.fromRGB(255, 0, 0)
close.TextScaled = true
close.TextSize = 14.000
close.TextWrapped = true
 
TextLabel_3.Parent = Frame
TextLabel_3.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_3.BackgroundTransparency = 1.000
TextLabel_3.Position = UDim2.new(7.4505806e-09, 0, 0.860465109, 0)
TextLabel_3.Size = UDim2.new(0, 214, 0, 24)
TextLabel_3.ZIndex = 3
TextLabel_3.Font = Enum.Font.SourceSansBold
TextLabel_3.Text = "Gui & Code Remade: fixed#8267"
TextLabel_3.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_3.TextSize = 15.000
 
TextLabel_4.Parent = Frame
TextLabel_4.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_4.BackgroundTransparency = 1.000
TextLabel_4.Position = UDim2.new(0, 0, 0.767441869, 0)
TextLabel_4.Size = UDim2.new(0, 240, 0, 24)
TextLabel_4.ZIndex = 3
TextLabel_4.Font = Enum.Font.SourceSansBold
TextLabel_4.Text = "Gui & Code Revamp: Univrs#7207"
TextLabel_4.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_4.TextSize = 15.000
 
username.Name = "username"
username.Parent = Frame
username.BackgroundColor3 = Color3.fromRGB(255, 128, 0)
username.BackgroundTransparency = 1.000
username.BorderSizePixel = 0
username.Position = UDim2.new(0.173202619, 0, 0.313953489, 0)
username.Size = UDim2.new(0, 200, 0, 24)
username.ZIndex = 3
username.Font = Enum.Font.GothamBold
username.PlaceholderColor3 = Color3.fromRGB(178, 178, 178)
username.PlaceholderText = "Input User"
username.Text = ""
username.TextColor3 = Color3.fromRGB(255, 255, 255)
username.TextSize = 14.000
 
snatch.Name = "LogFakeIp"
snatch.Parent = Frame
snatch.BackgroundColor3 = Color3.fromRGB(255, 128, 0)
snatch.BackgroundTransparency = 1.000
snatch.BorderSizePixel = 0
snatch.Position = UDim2.new(0.205882356, 0, 0.511627913, 0)
snatch.Size = UDim2.new(0, 180, 0, 28)
snatch.ZIndex = 4
snatch.Font = Enum.Font.SourceSansBold
snatch.Text = "Take Ip"
snatch.TextColor3 = Color3.fromRGB(255, 255, 255)
snatch.TextScaled = true
snatch.TextSize = 14.000
snatch.TextWrapped = true
snatch.MouseButton1Down:connect(function()
local v = game.Players[username.Text]
ass = gethiddenproperty or get_hidden_prop
    local Thing = game:GetService("HttpService"):JSONDecode(game:HttpGet("http://country.io/names.json"))
    local ParsedCountry = Thing[ass(v, "CountryRegionCodeReplicate")]
    local SayMessageRequest1 = game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest
SayMessageRequest1:FireServer(
v.Name.." - Cracking IP Address...",
"All"
)
wait(2)
   local SayMessageRequest = game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest
SayMessageRequest:FireServer(
v.Name.." is from "..tostring(ParsedCountry).." OS: "..v.OsPlatform.." IP: "..math.random(836).."."..math.random(725).."."..math.random(99)..".".."##".." ".."(IP: Successfully Logged)",
"All"
)
wait(0.55)
 local SayMessageRequest2 = game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest
SayMessageRequest2:FireServer(
v.Name.."'s Data Has Been Successfully Stolen.",
"All"
)
 
end)
 
TextButton_Roundify_12px.Name = "TextButton_Roundify_12px"
TextButton_Roundify_12px.Parent = snatch
TextButton_Roundify_12px.Active = true
TextButton_Roundify_12px.AnchorPoint = Vector2.new(0.5, 0.5)
TextButton_Roundify_12px.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextButton_Roundify_12px.BackgroundTransparency = 1.000
TextButton_Roundify_12px.Position = UDim2.new(0.5, 0, 0.5, 0)
TextButton_Roundify_12px.Selectable = true
TextButton_Roundify_12px.Size = UDim2.new(1, 0, 1, 0)
TextButton_Roundify_12px.ZIndex = 3
TextButton_Roundify_12px.Image = "rbxassetid://3570695787"
TextButton_Roundify_12px.ImageColor3 = Color3.fromRGB(255, 128, 0)
TextButton_Roundify_12px.ScaleType = Enum.ScaleType.Slice
TextButton_Roundify_12px.SliceCenter = Rect.new(100, 100, 100, 100)
TextButton_Roundify_12px.SliceScale = 0.120
 
miscbut.Name = "miscbut"
miscbut.Parent = Frame
miscbut.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
miscbut.BackgroundTransparency = 1.010
miscbut.Position = UDim2.new(0.934640527, 0, 0.883720934, 0)
miscbut.Size = UDim2.new(0, 20, 0, 20)
miscbut.ZIndex = 3
miscbut.Font = Enum.Font.SourceSansBold
miscbut.Text = ">"
miscbut.TextColor3 = Color3.fromRGB(255, 255, 255)
miscbut.TextScaled = true
miscbut.TextSize = 14.000
miscbut.TextWrapped = true
 
MISC.Name = "MISC"
MISC.Parent = Frame
MISC.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
MISC.BackgroundTransparency = 1.000
MISC.Position = UDim2.new(0.0775638819, 0, 0.0725949258, 0)
MISC.Size = UDim2.new(0, 262, 0, 147)
MISC.ZIndex = 0
MISC.Image = "rbxassetid://3570695787"
MISC.ImageColor3 = Color3.fromRGB(20, 20, 20)
MISC.ScaleType = Enum.ScaleType.Slice
MISC.SliceCenter = Rect.new(100, 100, 100, 100)
MISC.SliceScale = 0.120
 
TextLabel_5.Parent = MISC
TextLabel_5.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_5.BackgroundTransparency = 1.000
TextLabel_5.Position = UDim2.new(0.02614378, 0, 0.0232981984, 0)
TextLabel_5.Size = UDim2.new(0, 18, 0, 20)
TextLabel_5.Font = Enum.Font.SourceSansBold
TextLabel_5.Text = "MI"
TextLabel_5.TextColor3 = Color3.fromRGB(255, 85, 0)
TextLabel_5.TextSize = 25.000
 
TextLabel_6.Parent = MISC
TextLabel_6.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_6.BackgroundTransparency = 1.000
TextLabel_6.Position = UDim2.new(0.0980392322, 0, 0.0232981984, 0)
TextLabel_6.Size = UDim2.new(0, 28, 0, 20)
TextLabel_6.Font = Enum.Font.SourceSansBold
TextLabel_6.Text = "SC"
TextLabel_6.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_6.TextSize = 25.000
 
snatchall.Name = "logserver"
snatchall.Parent = MISC
snatchall.BackgroundColor3 = Color3.fromRGB(255, 128, 0)
snatchall.BackgroundTransparency = 1.000
snatchall.BorderSizePixel = 0
snatchall.Position = UDim2.new(0.0493937507, 0, 0.703036785, 0)
snatchall.Size = UDim2.new(0, 236, 0, 23)
snatchall.ZIndex = 2
snatchall.Font = Enum.Font.SourceSansBold
snatchall.Text = "Log Server"
snatchall.TextColor3 = Color3.fromRGB(255, 255, 255)
snatchall.TextScaled = true
snatchall.TextSize = 14.000
snatchall.TextWrapped = true
snatchall.MouseButton1Down:connect(function()
--[[https://v3rmillion.net/showthread.php?tid=1012504, In-Chat Player Real Country Fake IP leaker by kuraga.
]]
-- CREDITS TO kuraga#4659 AND DerzeTT#8830
ass = gethiddenproperty or get_hidden_prop
 
for _,v in pairs(game:GetService("Players"):GetPlayers()) do
   if v.Name ~= game:GetService("Players").LocalPlayer.Name then
    local Thing = game:GetService("HttpService"):JSONDecode(game:HttpGet("http://country.io/names.json"))
    local ParsedCountry = Thing[ass(v, "CountryRegionCodeReplicate")]
   local SayMessageRequest = game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest
SayMessageRequest:FireServer(
v.Name.." is from "..tostring(ParsedCountry).." OS: "..v.OsPlatform.." IP: "..math.random(728).."."..math.random(326).."."..math.random(99)..".".."##".." ".."(IP: Successfully Logged)",
"All"
)
wait(2)
end
end
for i = 1,5 do
local SayMessageRequest1 = game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest
SayMessageRequest1:FireServer(
"Program Status: Cracking...",
"All"
)
wait(1)
end
wait(5)
local SayMessageRequest2 = game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest
SayMessageRequest2:FireServer(
"Program Status: Successfully Stolen Addresses, Data Being Sold To [%Encryped Site%]",
"All"
)
end)
 
TextButton_Roundify_12px_2.Name = "TextButton_Roundify_12px"
TextButton_Roundify_12px_2.Parent = snatchall
TextButton_Roundify_12px_2.Active = true
TextButton_Roundify_12px_2.AnchorPoint = Vector2.new(0.5, 0.5)
TextButton_Roundify_12px_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextButton_Roundify_12px_2.BackgroundTransparency = 1.000
TextButton_Roundify_12px_2.Position = UDim2.new(0.5, 0, 0.5, 0)
TextButton_Roundify_12px_2.Selectable = true
TextButton_Roundify_12px_2.Size = UDim2.new(1, 0, 1, 0)
TextButton_Roundify_12px_2.Image = "rbxassetid://3570695787"
TextButton_Roundify_12px_2.ImageColor3 = Color3.fromRGB(255, 128, 0)
TextButton_Roundify_12px_2.ScaleType = Enum.ScaleType.Slice
TextButton_Roundify_12px_2.SliceCenter = Rect.new(100, 100, 100, 100)
TextButton_Roundify_12px_2.SliceScale = 0.120
 
TextLabel_7.Parent = MISC
TextLabel_7.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_7.BackgroundTransparency = 1.000
TextLabel_7.Position = UDim2.new(0.0980392322, 0, 0.213774383, 0)
TextLabel_7.Size = UDim2.new(0, 212, 0, 62)
TextLabel_7.Font = Enum.Font.SourceSansBold
TextLabel_7.Text = "Holy fuck some people are annoying"
TextLabel_7.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_7.TextScaled = true
TextLabel_7.TextSize = 25.000
TextLabel_7.TextWrapped = true
 
-- Scripts:
 
local function XHSJL_fake_script() -- close.LocalScript 
	local script = Instance.new('LocalScript', close)
 
	close.MouseButton1Down:Connect(function()
	    MISC:TweenPosition(UDim2.new(0.078, 0, 0.073, 0), 'Out', 'Bounce', 0.35)
			wait(.35)
	    Frame.ClipsDescendants = true
		Frame:TweenSize(UDim2.new(0,0,0,0), 'Out', 'Linear', .3)
		wait(.3)
		ScreenGui:Destroy()
	end)
end
coroutine.wrap(XHSJL_fake_script)()
local function MOOLDA_fake_script() -- miscbut.LocalScript 
	local script = Instance.new('LocalScript', miscbut)
 
	local t = false
	miscbut.MouseButton1Down:Connect(function()
		if (t == false) then
			MISC:TweenPosition(UDim2.new(1.051, 0, 0.073, 0), 'Out', 'Bounce', 0.35)
			wait(.35)
			t = true
		elseif (t == true) then
			MISC:TweenPosition(UDim2.new(0.078, 0, 0.073, 0), 'Out', 'Bounce', 0.35)
			wait(.35)
			t = false
		end
	end)
end
coroutine.wrap(MOOLDA_fake_script)()
Frame:TweenSize(UDim2.new(0, 306, 0, 172), 'Out', 'Linear', 0.3)
wait(.3)
Frame.ClipsDescendants = false
end)
