-- 🔥 TRX HUB FINAL COMPLETO 🔥
-- feito por wsy | ajustado para Rich

---------------- SERVICES ----------------
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")
local lp = Players.LocalPlayer
local cam = workspace.CurrentCamera

---------------- GUI ROOT ----------------
local gui = Instance.new("ScreenGui", lp.PlayerGui)
gui.Name = "TRX_HUB_GUI"
gui.ResetOnSpawn = false

---------------- LOADING FULLSCREEN ----------------
local loading = Instance.new("Frame", gui)
loading.Size = UDim2.fromScale(1,1)
loading.BackgroundColor3 = Color3.new(0,0,0)

local title = Instance.new("TextLabel", loading)
title.Size = UDim2.new(1,0,0,60)
title.Position = UDim2.new(0,0,0.42,0)
title.BackgroundTransparency = 1
title.Text = "🔥 TRX HUB 🔥"
title.Font = Enum.Font.GothamBold
title.TextSize = 32
title.TextColor3 = Color3.new(1,1,1)

local barBG = Instance.new("Frame", loading)
barBG.Size = UDim2.new(0.6,0,0,18)
barBG.Position = UDim2.new(0.2,0,0.52,0)
barBG.BackgroundColor3 = Color3.fromRGB(30,30,30)
Instance.new("UICorner", barBG)

local bar = Instance.new("Frame", barBG)
bar.Size = UDim2.new(0,0,1,0)
bar.BackgroundColor3 = Color3.fromRGB(170,0,255)
Instance.new("UICorner", bar)

TweenService:Create(bar, TweenInfo.new(3), {Size = UDim2.new(1,0,1,0)}):Play()
task.wait(3)
loading:Destroy()

---------------- HUB BASE ----------------
local hub = Instance.new("Frame", gui)
hub.Size = UDim2.new(0,560,0,360)
hub.Position = UDim2.new(0.5,-280,0.5,-180)
hub.BackgroundColor3 = Color3.fromRGB(10,10,10)
hub.Active = true
hub.Draggable = true
Instance.new("UICorner", hub)

---------------- MINIMIZAR ----------------
local minimized=false
local mini

local minBtn = Instance.new("TextButton", hub)
minBtn.Size = UDim2.new(0,30,0,24)
minBtn.Position = UDim2.new(1,-36,0,8)
minBtn.Text = "-"
minBtn.Font = Enum.Font.GothamBold
minBtn.TextSize = 20
minBtn.BackgroundColor3 = Color3.new(1,1,1)
Instance.new("UICorner", minBtn)

minBtn.MouseButton1Click:Connect(function()
	if minimized then return end
	minimized=true
	hub.Visible=false

	mini = Instance.new("TextButton", gui)
	mini.Size = UDim2.new(0,70,0,70)
	mini.Position = UDim2.new(0.02,0,0.3,0)
	mini.Text="🔥T🔥"
	mini.Font=Enum.Font.GothamBold
	mini.TextSize=22
	mini.TextColor3=Color3.new(1,1,1)
	mini.BackgroundColor3=Color3.new(0,0,0)
	mini.BorderSizePixel=3
	mini.BorderColor3=Color3.fromRGB(170,0,255)
	mini.Active=true
	mini.Draggable=true
	Instance.new("UICorner", mini)

	mini.MouseButton1Click:Connect(function()
		mini:Destroy()
		hub.Visible=true
		minimized=false
	end)
end)

---------------- MENU ----------------
local menu = Instance.new("Frame", hub)
menu.Size = UDim2.new(0,150,1,0)
menu.BackgroundColor3 = Color3.fromRGB(20,0,30)
Instance.new("UICorner", menu)

local function menuBtn(txt,y)
	local b=Instance.new("TextButton", menu)
	b.Size=UDim2.new(1,-16,0,34)
	b.Position=UDim2.new(0,8,0,y)
	b.Text=txt
	b.Font=Enum.Font.GothamBold
	b.TextSize=14
	b.TextColor3=Color3.new(1,1,1)
	b.BackgroundColor3=Color3.fromRGB(140,0,200)
	Instance.new("UICorner", b)
	return b
end

local bMain=menuBtn("MAIN",20)
local bAim=menuBtn("AIMBOT",60)
local bESP=menuBtn("ESP",100)
local bMirar=menuBtn("MIRAR",140)
local bBypass=menuBtn("BYPASS",180)
local bCfg=menuBtn("CONFIG",220)

---------------- PAINÉIS ----------------
local function panel()
	local f=Instance.new("Frame", hub)
	f.Position=UDim2.new(0,150,0,0)
	f.Size=UDim2.new(1,-150,1,0)
	f.BackgroundColor3=Color3.fromRGB(12,12,12)
	Instance.new("UICorner", f)
	return f
end

local pMain,pAim,pESP,pMirar,pBypass,pCfg=panel(),panel(),panel(),panel(),panel(),panel()
pAim.Visible=false;pESP.Visible=false;pMirar.Visible=false;pBypass.Visible=false;pCfg.Visible=false

local function show(p)
	for _,v in pairs({pMain,pAim,pESP,pMirar,pBypass,pCfg}) do v.Visible=false end
	p.Visible=true
end

bMain.MouseButton1Click:Connect(function()show(pMain)end)
bAim.MouseButton1Click:Connect(function()show(pAim)end)
bESP.MouseButton1Click:Connect(function()show(pESP)end)
bMirar.MouseButton1Click:Connect(function()show(pMirar)end)
bBypass.MouseButton1Click:Connect(function()show(pBypass)end)
bCfg.MouseButton1Click:Connect(function()show(pCfg)end)

---------------- MAIN ----------------
local txt=Instance.new("TextLabel", pMain)
txt.Size=UDim2.new(1,-20,1,-20)
txt.Position=UDim2.new(0,10,0,10)
txt.BackgroundTransparency=1
txt.TextWrapped=true
txt.Text="feito por wsy caso vc tenha se endereçado cada vez teremos atualizações adiante se gostarem avaliem no site"
txt.Font=Enum.Font.Gotham
txt.TextSize=16
txt.TextColor3=Color3.new(1,1,1)

------------------------------------------------
-- AIMBOT + BONECO
------------------------------------------------
local aimbotOn=false
local selectedAim="Head"
local aimSmooth=0.15

local doll=Instance.new("Frame", pAim)
doll.Size=UDim2.new(0,140,0,200)
doll.Position=UDim2.new(0.6,0,0.08,0)
doll.BackgroundTransparency=1

local function part(sz,pos)
	local f=Instance.new("Frame", doll)
	f.Size=sz;f.Position=pos
	f.BackgroundColor3=Color3.fromRGB(245,245,245)
	f.BorderSizePixel=0
	Instance.new("UICorner", f)
	return f
end

local head=part(UDim2.new(0,50,0,50),UDim2.new(0.32,0,0.02,0))
local chest=part(UDim2.new(0,80,0,70),UDim2.new(0.22,0,0.32,0))
local armL=part(UDim2.new(0,22,0,80),UDim2.new(0.05,0,0.32,0))
local armR=part(UDim2.new(0,22,0,80),UDim2.new(0.73,0,0.32,0))

local function highlight(w)
	for _,v in pairs({head,chest,armL,armR})do v.BorderSizePixel=0 end
	local c=Color3.fromRGB(170,0,255)
	if w=="Head" then head.BorderSizePixel=4;head.BorderColor3=c end
	if w=="Chest" then chest.BorderSizePixel=4;chest.BorderColor3=c end
	if w=="Arm" then
		armL.BorderSizePixel=4;armR.BorderSizePixel=4
		armL.BorderColor3=c;armR.BorderColor3=c
	end
end
highlight(selectedAim)

local function aimBtn(txt,y,mode)
	local b=Instance.new("TextButton", pAim)
	b.Size=UDim2.new(0,200,0,30)
	b.Position=UDim2.new(0.06,0,0,y)
	b.Text=txt
	b.BackgroundColor3=Color3.fromRGB(140,0,200)
	b.TextColor3=Color3.new(1,1,1)
	Instance.new("UICorner", b)
	b.MouseButton1Click:Connect(function()
		selectedAim=mode
		highlight(mode)
	end)
end

aimBtn("Cabeça",40,"Head")
aimBtn("Peito",75,"Chest")
aimBtn("Braço",110,"Arm")

local toggleAim=Instance.new("TextButton", pAim)
toggleAim.Size=UDim2.new(0,220,0,36)
toggleAim.Position=UDim2.new(0.06,0,0,160)
toggleAim.Text="ATIVAR AIMBOT"
toggleAim.BackgroundColor3=Color3.fromRGB(170,0,255)
toggleAim.TextColor3=Color3.new(1,1,1)
Instance.new("UICorner", toggleAim)

toggleAim.MouseButton1Click:Connect(function()
	aimbotOn=not aimbotOn
	toggleAim.Text=aimbotOn and "AIMBOT ATIVO" or "ATIVAR AIMBOT"
end)

local function getClosest()
	if not lp.Character or not lp.Character:FindFirstChild("HumanoidRootPart") then return end
	local best,dist
	for _,p in pairs(Players:GetPlayers()) do
		if p~=lp and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
			local h=p.Character:FindFirstChild("Humanoid")
			if h and h.Health>0 then
				local d=(p.Character.HumanoidRootPart.Position-lp.Character.HumanoidRootPart.Position).Magnitude
				if not dist or d<dist then dist=d;best=p end
			end
		end
	end
	return best
end

local function getPart(c)
	if selectedAim=="Head" then return c:FindFirstChild("Head") end
	if selectedAim=="Chest" then return c:FindFirstChild("UpperTorso") or c:FindFirstChild("Torso") end
	if selectedAim=="Arm" then return c:FindFirstChild("RightUpperArm") or c:FindFirstChild("Right Arm") end
end

RunService.RenderStepped:Connect(function()
	if not aimbotOn then return end
	local t=getClosest()
	if t and t.Character then
		local p=getPart(t.Character)
		if p then
			cam.CFrame=cam.CFrame:Lerp(CFrame.new(cam.CFrame.Position,p.Position),aimSmooth)
		end
	end
end)

------------------------------------------------
-- MIRAR (SLIDER + SHADER)
------------------------------------------------
local sliderBG=Instance.new("Frame", pMirar)
sliderBG.Size=UDim2.new(0,260,0,14)
sliderBG.Position=UDim2.new(0.1,0,0.35,0)
sliderBG.BackgroundColor3=Color3.fromRGB(40,40,40)
Instance.new("UICorner", sliderBG)

local slider=Instance.new("Frame", sliderBG)
slider.Size=UDim2.new(0.2,0,1,0)
slider.BackgroundColor3=Color3.fromRGB(255,0,0)
Instance.new("UICorner", slider)

sliderBG.InputBegan:Connect(function(i)
	if i.UserInputType==Enum.UserInputType.MouseButton1 then
		local x=math.clamp((i.Position.X-sliderBG.AbsolutePosition.X)/sliderBG.AbsoluteSize.X,0,1)
		slider.Size=UDim2.new(x,0,1,0)
		aimSmooth=0.02+(1-x)*0.3
	end
end)

local visionOn=false
local cc=Instance.new("ColorCorrectionEffect", Lighting)
cc.Enabled=false

local visionBtn=Instance.new("TextButton", pMirar)
visionBtn.Size=UDim2.new(0,220,0,36)
visionBtn.Position=UDim2.new(0.1,0,0.5,0)
visionBtn.Text="VISION RXZ"
visionBtn.BackgroundColor3=Color3.fromRGB(140,0,200)
visionBtn.TextColor3=Color3.new(1,1,1)
Instance.new("UICorner", visionBtn)

visionBtn.MouseButton1Click:Connect(function()
	visionOn=not visionOn
	cc.Enabled=visionOn
	cc.Contrast=0.2
	cc.Saturation=0.3
	cc.Brightness=0.05
end)

------------------------------------------------
-- ESP + VEICULAR (PERSISTENTE)
------------------------------------------------
local espOn=false
local vehOn=false

local function applyESP(c)
	if c:FindFirstChild("TRX_ESP") then return end
	local h=Instance.new("Highlight", c)
	h.Name="TRX_ESP"
	h.OutlineColor=Color3.fromRGB(170,0,255)
	h.FillTransparency=1
end

local function applyVeh(c)
	if c:FindFirstChild("TRX_VEH") then return end
	local hum=c:WaitForChild("Humanoid")
	local root=c:WaitForChild("HumanoidRootPart")

	local g=Instance.new("BillboardGui", c)
	g.Name="TRX_VEH"
	g.Adornee=root
	g.Size=UDim2.new(4,0,0.4,0)
	g.StudsOffset=Vector3.new(0,-3,0)
	g.AlwaysOnTop=true

	local bg=Instance.new("Frame", g)
	bg.Size=UDim2.new(1,0,1,0)
	bg.BackgroundColor3=Color3.fromRGB(40,40,40)
	Instance.new("UICorner", bg)

	local bar=Instance.new("Frame", bg)
	bar.Size=UDim2.new(1,0,1,0)
	bar.BackgroundColor3=Color3.fromRGB(170,0,255)
	Instance.new("UICorner", bar)

	hum.HealthChanged:Connect(function(hp)
		bar.Size=UDim2.new(math.clamp(hp/hum.MaxHealth,0,1),0,1,0)
	end)
end

local function updateAll()
	for _,p in pairs(Players:GetPlayers()) do
		if p~=lp and p.Character then
			if espOn then applyESP(p.Character) end
			if vehOn then applyVeh(p.Character) end
		end
	end
end

Players.PlayerAdded:Connect(function(p)
	p.CharacterAdded:Connect(function(c)
		task.wait(1)
		if espOn then applyESP(c) end
		if vehOn then applyVeh(c) end
	end)
end)

local espBtn=menuBtn("ESP ON/OFF",260)
espBtn.Parent=pESP
espBtn.Position=UDim2.new(0.06,0,0.2,0)
espBtn.MouseButton1Click:Connect(function()
	espOn=not espOn
	updateAll()
end)

local vehBtn=menuBtn("VEICULAR",300)
vehBtn.Parent=pESP
vehBtn.Position=UDim2.new(0.06,0,0.35,0)
vehBtn.MouseButton1Click:Connect(function()
	vehOn=not vehOn
	updateAll()
end)

------------------------------------------------
-- BYPASS
------------------------------------------------
local des=menuBtn("🔥DESATIVAR🔥",40)
des.Parent=pBypass
des.MouseButton1Click:Connect(function()
	aimbotOn=false
	espOn=false
	vehOn=false
end)

local hide=menuBtn("🔥ESCONDER🔥",90)
hide.Parent=pBypass
hide.MouseButton1Click:Connect(function()
	hub.Visible=false
end)

lp.Chatted:Connect(function(msg)
	if msg=="bv" then hub.Visible=true end
end)

------------------------------------------------
-- CONFIG
------------------------------------------------
local cfgTxt=Instance.new("TextLabel", pCfg)
cfgTxt.Size=UDim2.new(1,-20,1,-20)
cfgTxt.Position=UDim2.new(0,10,0,10)
cfgTxt.BackgroundTransparency=1
cfgTxt.Text="estou trabalhando nisso embreve esta pronto"
cfgTxt.Font=Enum.Font.Gotham
cfgTxt.TextSize=16
cfgTxt.TextColor3=Color3.new(1,1,1)

print("🔥 TRX HUB COMPLETO CARREGADO 🔥")
