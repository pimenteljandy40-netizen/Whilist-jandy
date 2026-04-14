-- [[ ACUSADO HUB // SOUTH BRONX THE TRENCHER // FINAL VERSION FIX ✅ ]]
local Players = game:GetService("Players")
local L_Plr = Players.LocalPlayer
local HttpService = game:GetService("HttpService")

-- CONFIGURACIÓN DE SEGURIDAD (Whitelist desde tu GitHub)
local URL_WHITELIST = "https://raw.githubusercontent.com/mateoyandi02-droid/Script/refs/heads/main/Whitelist.pimenteljandy40-netizen=" .. math.random(1, 9999)

local function CheckWhitelist()
    local success, result = pcall(function()
        return game:HttpGet(URL_WHITELIST)
    end)

    if success then
        local ok, ids = pcall(function() return HttpService:JSONDecode(result) end)
        if ok and type(ids) == "table" then
            for _, id in pairs(ids) do
                if tonumber(id) == L_Plr.UserId then
                    return true
                end
            end
        end
    end
    
    L_Plr:Kick("\n❌ ID NO AUTORIZADO: " .. L_Plr.UserId .. "\nAcceso denegado por ivancaba29-max")
    return false
end

-- Ejecutar validación de Whitelist antes de cargar nada
if not CheckWhitelist() then return end

-- [[ INICIO DEL HUB ]]
local k1, k2 = "BA", "CK01"
local CLAVE_CORRECTA = k1..k2
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera
local Mouse = L_Plr:GetMouse()

local function ExecuteHub()
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "ACUSADO_SAFE_V5"
    ScreenGui.ResetOnSpawn = false
    ScreenGui.Parent = (gethui and gethui()) or game:GetService("CoreGui")

    -- [[ INTRO ]]
    local Intro = Instance.new("Frame", ScreenGui)
    Intro.Size = UDim2.new(0, 400, 0, 100); Intro.Position = UDim2.new(0.5, -200, 0.5, -50); Intro.BackgroundColor3 = Color3.fromRGB(15, 15, 25); Intro.ZIndex = 100
    Instance.new("UICorner", Intro); Instance.new("UIStroke", Intro).Color = Color3.fromRGB(60, 60, 220)
    local IT = Instance.new("TextLabel", Intro); IT.Size = UDim2.new(1, 0, 1, 0); IT.Text = "ACUSADO SCRIPT EXECUTED ✅"; IT.TextColor3 = Color3.new(1,1,1); IT.Font = Enum.Font.GothamBold; IT.TextSize = 20; IT.BackgroundTransparency = 1
    task.wait(2.5); Intro:Destroy()

    -- // VARIABLES //
    _G.Hitbox_Size = 15
    _G.Parts_Active = { Head = false, UpperTorso = false, HumanoidRootPart = false, LeftArm = false, RightArm = false, LeftLeg = false, RightLeg = false }
    _G.Visuals = { Box = true, Names = true, Dist = true, Weapon = true, HealthBar = true, Tracers = true }
    _G.Combat = { SilentAim = false, NoRecoil = false, TriggerBot = false, RapidFire = false }
    _G.Misc = { Speed_On = false, SpeedVal = 16, FullBright = false }
    local DeletedObjects = {}

    -- [[ INTERFAZ + PORTADA ]]
    local MainFrame = Instance.new("Frame", ScreenGui)
    MainFrame.Size = UDim2.new(0, 580, 0, 450); MainFrame.Position = UDim2.new(0.5, -290, 0.5, -225); MainFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 18); MainFrame.Visible = false; MainFrame.Active = true; MainFrame.Draggable = true
    Instance.new("UICorner", MainFrame); Instance.new("UIStroke", MainFrame).Color = Color3.fromRGB(60, 60, 220)
    local MenuTitle = Instance.new("TextLabel", MainFrame); MenuTitle.Size = UDim2.new(1, 0, 0, 40); MenuTitle.Position = UDim2.new(0, 160, 0, 5); MenuTitle.Text = "Acusado Hub // South Bronx The Treach Best Script"; MenuTitle.TextColor3 = Color3.fromRGB(80, 80, 255); MenuTitle.Font = Enum.Font.GothamBold; MenuTitle.TextSize = 14; MenuTitle.BackgroundTransparency = 1; MenuTitle.TextXAlignment = 0

    local MiniBar = Instance.new("Frame", ScreenGui); MiniBar.Size = UDim2.new(0, 450, 0, 35); MiniBar.Position = UDim2.new(0.5, -225, 0, 10); MiniBar.BackgroundColor3 = Color3.fromRGB(15, 15, 20); MiniBar.Visible = false; MiniBar.Active = true; MiniBar.Draggable = true; Instance.new("UICorner", MiniBar); Instance.new("UIStroke", MiniBar).Color = Color3.fromRGB(60, 60, 220)
    local MiniTitle = Instance.new("TextLabel", MiniBar); MiniTitle.Size = UDim2.new(1, -40, 1, 0); MiniTitle.Position = UDim2.new(0, 15, 0, 0); MiniTitle.Text = "Acusado Hub // South Bronx The Treach Best Script"; MiniTitle.TextColor3 = Color3.fromRGB(80, 80, 255); MiniTitle.Font = Enum.Font.GothamBold; MiniTitle.TextSize = 11; MiniTitle.BackgroundTransparency = 1; MiniTitle.TextXAlignment = 0
    local MaxBtn = Instance.new("TextButton", MiniBar); MaxBtn.Size = UDim2.new(0, 30, 0, 30); MaxBtn.Position = UDim2.new(1, -35, 0, 2.5); MaxBtn.Text = "+"; MaxBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 220); MaxBtn.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", MaxBtn)
    local MinBtn = Instance.new("TextButton", MainFrame); MinBtn.Size = UDim2.new(0, 30, 0, 30); MinBtn.Position = UDim2.new(1, -40, 0, 10); MinBtn.Text = "-"; MinBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 220); MinBtn.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", MinBtn)
    MinBtn.MouseButton1Click:Connect(function() MainFrame.Visible = false; MiniBar.Visible = true end); MaxBtn.MouseButton1Click:Connect(function() MainFrame.Visible = true; MiniBar.Visible = false end)

    local Sidebar = Instance.new("Frame", MainFrame); Sidebar.Size = UDim2.new(0, 140, 1, -60); Sidebar.Position = UDim2.new(0, 10, 0, 50); Sidebar.BackgroundTransparency = 1; Instance.new("UIListLayout", Sidebar).Padding = UDim.new(0, 5)
    local Container = Instance.new("Frame", MainFrame); Container.Position = UDim2.new(0, 160, 0, 50); Container.Size = UDim2.new(1, -170, 1, -70); Container.BackgroundColor3 = Color3.fromRGB(18, 18, 25); Instance.new("UICorner", Container)

    local Tabs = {}
    local function CreateTab(name) local f = Instance.new("ScrollingFrame", Container); f.Size = UDim2.new(1, -10, 1, -10); f.BackgroundTransparency = 1; f.Visible = false; f.ScrollBarThickness = 2; Instance.new("UIListLayout", f).Padding = UDim.new(0, 8); Tabs[name] = f; return f end
    local CombatTab = CreateTab("Combat"); local VisualsTab = CreateTab("Visuals"); local FarmTab = CreateTab("Farm"); local MiscTab = CreateTab("Misc")
    local function AddTabBtn(txt, target) local b = Instance.new("TextButton", Sidebar); b.Size = UDim2.new(1, 0, 0, 38); b.BackgroundColor3 = Color3.fromRGB(25, 25, 35); b.Text = "  "..txt; b.TextColor3 = Color3.new(1,1,1); b.Font = Enum.Font.GothamBold; b.TextSize = 12; b.TextXAlignment = 0; Instance.new("UICorner", b); b.MouseButton1Click:Connect(function() for _, t in pairs(Tabs) do t.Visible = false end Tabs[target].Visible = true end) end
    AddTabBtn("⚔️ COMBAT", "Combat"); AddTabBtn("👁️ VISUALS", "Visuals"); AddTabBtn("🚜 FARM", "Farm"); AddTabBtn("⚙️ MISC", "Misc")

    local function AddToggle(parent, text, tab, var)
        local b = Instance.new("TextButton", parent); b.Size = UDim2.new(1, -5, 0, 35); b.BackgroundColor3 = tab[var] and Color3.fromRGB(60, 60, 220) or Color3.fromRGB(30, 30, 45); b.Text = "  "..text; b.TextColor3 = Color3.new(1,1,1); b.Font = Enum.Font.Gotham; b.TextSize = 11; b.TextXAlignment = 0; Instance.new("UICorner", b)
        b.MouseButton1Click:Connect(function() tab[var] = not tab[var] b.BackgroundColor3 = tab[var] and Color3.fromRGB(60, 60, 220) or Color3.fromRGB(30, 30, 45) end)
    end

    -- [[ COMBATE ]]
    local hbS = Instance.new("TextBox", CombatTab); hbS.Size = UDim2.new(1,-5,0,32); hbS.Text = "15"; hbS.BackgroundColor3 = Color3.fromRGB(35,35,50); hbS.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", hbS); hbS.FocusLost:Connect(function() _G.Hitbox_Size = tonumber(hbS.Text) or 15 end)
    AddToggle(CombatTab, "SILENT AIM", _G.Combat, "SilentAim"); AddToggle(CombatTab, "TRIGGER BOT", _G.Combat, "TriggerBot"); AddToggle(CombatTab, "RAPID FIRE", _G.Combat, "RapidFire"); AddToggle(CombatTab, "NO RECOIL", _G.Combat, "NoRecoil")
    for k,_ in pairs(_G.Parts_Active) do AddToggle(CombatTab, "ACTIVATE "..k, _G.Parts_Active, k) end

    -- [[ VISUALES ]]
    AddToggle(VisualsTab, "BOX ESP", _G.Visuals, "Box"); AddToggle(VisualsTab, "NAMES", _G.Visuals, "Names"); AddToggle(VisualsTab, "DISTANCE", _G.Visuals, "Dist"); AddToggle(VisualsTab, "WEAPON ESP", _G.Visuals, "Weapon"); AddToggle(VisualsTab, "HEALTH BAR", _G.Visuals, "HealthBar"); AddToggle(VisualsTab, "TOP LINE", _G.Visuals, "Tracers")

    -- [[ AUTOFARM ]]
    local function CreateFarmBtn(txt, url) local b = Instance.new("TextButton", FarmTab); b.Size = UDim2.new(1,-5,0,40); b.Text = txt; b.BackgroundColor3 = Color3.fromRGB(60,60,200); b.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", b); b.MouseButton1Click:Connect(function() loadstring(game:HttpGet(url))() end) end
    CreateFarmBtn("AUTOFARM 2K", "https://raw.githubusercontent.com/ivancaba29-max/ACUSADO-SCRIPT/main/2k"); CreateFarmBtn("AUTOFARM LEVEL", "https://raw.githubusercontent.com/ivancaba29-max/ACUSADO-SCRIPT/main/level"); CreateFarmBtn("AUTO-ROB ATM", "https://raw.githubusercontent.com/ivancaba29-max/ACUSADO-SCRIPT/main/atm")

    -- [[ MISC ]]
    AddToggle(MiscTab, "SPEED HACK", _G.Misc, "Speed_On")
    local sVal = Instance.new("TextBox", MiscTab); sVal.Size = UDim2.new(1,-5,0,32); sVal.Text = "16"; sVal.BackgroundColor3 = Color3.fromRGB(35,35,50); sVal.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", sVal); sVal.FocusLost:Connect(function() _G.Misc.SpeedVal = tonumber(sVal.Text) or 16 end)
    AddToggle(MiscTab, "FULL BRIGHT", _G.Misc, "FullBright")
    local DelT = Instance.new("TextButton", MiscTab); DelT.Size = UDim2.new(1,-5,0,35); DelT.Text = "CLICK DELETE TOOL"; DelT.BackgroundColor3 = Color3.fromRGB(60, 200, 60); Instance.new("UICorner", DelT); DelT.MouseButton1Click:Connect(function() local T = Instance.new("Tool"); T.Name = "Click Delete"; T.RequiresHandle = false; T.Parent = L_Plr.Backpack; T.Activated:Connect(function() if Mouse.Target then table.insert(DeletedObjects, {o = Mouse.Target, p = Mouse.Target.Parent}) Mouse.Target.Parent = nil end end) end)
    local ResT = Instance.new("TextButton", MiscTab); ResT.Size = UDim2.new(1,-5,0,35); ResT.Text = "RESET MAP"; ResT.BackgroundColor3 = Color3.fromRGB(200, 50, 50); Instance.new("UICorner", ResT); ResT.MouseButton1Click:Connect(function() for _, v in pairs(DeletedObjects) do if v.o then v.o.Parent = v.p end end DeletedObjects = {} end)

    -- [[ ESP DRAWING LOGIC ]]
    local function CreateESP(plr)
        local Box = Drawing.new("Square"); Box.Thickness = 1; Box.Filled = false; Box.Color = Color3.new(1,1,1); Box.Visible = false
        local Name = Drawing.new("Text"); Name.Size = 13; Name.Center = true; Name.Outline = true; Name.Color = Color3.new(1,1,1); Name.Visible = false
        local Dist = Drawing.new("Text"); Dist.Size = 13; Dist.Center = true; Dist.Outline = true; Dist.Color = Color3.new(1,1,1); Dist.Visible = false
        local Weap = Drawing.new("Text"); Weap.Size = 13; Weap.Center = true; Weap.Outline = true; Weap.Color = Color3.new(1, 1, 1); Weap.Visible = false
        local Line = Drawing.new("Line"); Line.Thickness = 1; Line.Color = Color3.new(1,1,1); Line.Visible = false
        local HealthBar = Drawing.new("Square"); HealthBar.Thickness = 1; HealthBar.Filled = true; HealthBar.Visible = false

        RunService.RenderStepped:Connect(function()
            if plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") and plr.Character:FindFirstChild("Humanoid") and plr ~= L_Plr then
                local HRP = plr.Character.HumanoidRootPart
                local Hum = plr.Character.Humanoid
                local Pos, OnScreen = Camera:WorldToViewportPoint(HRP.Position)

                if OnScreen then
                    local Size = (Camera:WorldToViewportPoint(HRP.Position - Vector3.new(0, 3, 0)).Y - Camera:WorldToViewportPoint(HRP.Position + Vector3.new(0, 2.6, 0)).Y)
                    local BoxSize = Vector2.new(Size / 1.5, Size)
                    local BoxPos = Vector2.new(Pos.X - BoxSize.X / 2, Pos.Y - BoxSize.Y / 2)

                    Box.Visible = _G.Visuals.Box; Box.Size = BoxSize; Box.Position = BoxPos
                    Name.Visible = _G.Visuals.Names; Name.Text = plr.Name; Name.Position = Vector2.new(Pos.X, BoxPos.Y - 15)
                    local d = math.floor((L_Plr.Character.HumanoidRootPart.Position - HRP.Position).Magnitude)
                    Dist.Visible = _G.Visuals.Dist; Dist.Text = "["..d.."m]"; Dist.Position = Vector2.new(Pos.X, BoxPos.Y + BoxSize.Y + 5)
                    local tool = plr.Character:FindFirstChildOfClass("Tool")
                    Weap.Visible = _G.Visuals.Weapon; Weap.Text = tool and tool.Name or "Hands"; Weap.Position = Vector2.new(Pos.X, BoxPos.Y + BoxSize.Y + 18)
                    Line.Visible = _G.Visuals.Tracers; Line.From = Vector2.new(Camera.ViewportSize.X / 2, 0); Line.To = Vector2.new(Pos.X, BoxPos.Y)
                    HealthBar.Visible = _G.Visuals.HealthBar; HealthBar.Size = Vector2.new(2, (Hum.Health / Hum.MaxHealth) * BoxSize.Y); HealthBar.Position = Vector2.new(BoxPos.X - 5, BoxPos.Y + (BoxSize.Y - HealthBar.Size.Y)); HealthBar.Color = Color3.fromHSV(Hum.Health/Hum.MaxHealth * 0.3, 1, 1)
                else
                    Box.Visible = false; Name.Visible = false; Dist.Visible = false; Weap.Visible = false; Line.Visible = false; HealthBar.Visible = false
                end
            else
                Box.Visible = false; Name.Visible = false; Dist.Visible = false; Weap.Visible = false; Line.Visible = false; HealthBar.Visible = false
            end
        end)
    end
    for _, p in pairs(Players:GetPlayers()) do CreateESP(p) end
    Players.PlayerAdded:Connect(CreateESP)

    -- [[ CORE LOGIC: HITBOX INVISIBLE + ANTI-FREEZE ]]
    RunService.Heartbeat:Connect(function()
        if _G.Misc.Speed_On and L_Plr.Character and L_Plr.Character:FindFirstChild("Humanoid") then L_Plr.Character.Humanoid.WalkSpeed = _G.Misc.SpeedVal end
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= L_Plr and p.Character then
                for n, act in pairs(_G.Parts_Active) do
                    local part = p.Character:FindFirstChild(n)
                    if part and part:IsA("BasePart") then
                        if act then 
                            part.Size = Vector3.new(_G.Hitbox_Size, _G.Hitbox_Size, _G.Hitbox_Size)
                            part.CanCollide = false
                            part.Massless = true
                            part.Transparency = 1 
                        else 
                            if part.Transparency == 1 then part.Size = (n == "Head" and Vector3.new(2,1,1) or Vector3.new(2,2,1)); part.Transparency = 0; part.CanCollide = true end 
                        end
                    end
                end
            end
        end
    end)

    -- [[ KEY SYSTEM ]]
    local KeyFrame = Instance.new("Frame", ScreenGui); KeyFrame.Size = UDim2.new(0, 320, 0, 220); KeyFrame.Position = UDim2.new(0.5,-160,0.5,-110); KeyFrame.BackgroundColor3 = Color3.fromRGB(15,15,20); Instance.new("UICorner", KeyFrame); Instance.new("UIStroke", KeyFrame).Color = Color3.fromRGB(60, 60, 220)
    local KeyT = Instance.new("TextLabel", KeyFrame); KeyT.Size = UDim2.new(1,0,0,60); KeyT.Text = "ACUSADO NINJA HUB\nIngresa la contra"; KeyT.TextColor3 = Color3.new(1,1,1); KeyT.Font = Enum.Font.GothamBold; KeyT.TextSize = 16; KeyT.BackgroundTransparency = 1
    local KeyInp = Instance.new("TextBox", KeyFrame); KeyInp.Size = UDim2.new(0,250,0,45); KeyInp.Position = UDim2.new(0.5,-125,0,80); KeyInp.PlaceholderText = "CONTRASEÑA"; KeyInp.BackgroundColor3 = Color3.fromRGB(25,25,35); KeyInp.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", KeyInp)
    local KeyBtn = Instance.new("TextButton", KeyFrame); KeyBtn.Size = UDim2.new(0,160,0,45); KeyBtn.Position = UDim2.new(0.5,-80,0,145); KeyBtn.Text = "ENTRAR"; KeyBtn.BackgroundColor3 = Color3.fromRGB(60,60,200); KeyBtn.TextColor3 = Color3.new(1,1,1); Instance.new("UICorner", KeyBtn)
    KeyBtn.MouseButton1Click:Connect(function() if KeyInp.Text == CLAVE_CORRECTA then KeyFrame:Destroy(); MainFrame.Visible = true; Tabs.Combat.Visible = true end end)
end

-- Ejecutar el Hub de forma segura
pcall(ExecuteHub)
