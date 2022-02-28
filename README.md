getgenv().key = ""


function script()
    print("A")
end



local key = getgenv().key or ""

local http_request = http_request
if syn then 
    http_request = syn.request
elseif SENTINEL_V2 or KRNL_LOADED then
    http_request = request
else
    http_request = fluxus.request
end

function kick(msg)
    game.Players.LocalPlayer:Kick(msg)
end


if getgenv().key == nil then
    return kick("Use key")
end


local getservice = game.GetService
local httpservice = getservice(game, "HttpService")

local function http_request_get(url, headers) 
    return http_request({Url=url,Method="GET",Headers=headers or nil}).Body 
end

local function jsondecode(json)
    local jsonTable = {}
     pcall(function() jsonTable = httpservice.JSONDecode(httpservice,json) end)
    return jsonTable
end

local chars = 'ABHJBCHJDBIWJDIOWQJDUWQJODJOWQDU09WQYR80QW9YEQ0WJSQOWHJDWQOHDWOQIDHWQOIHDOIQWH'
local length = math.random(250,9999)
local randomString = ''

charTable = {}
for c in chars:gmatch"." do
    table.insert(charTable, c)
end

for i = 1, length do
    randomString = randomString .. charTable[math.random(1, #charTable)]
end

local body = http_request_get('https://httpbin.org/get')
local decoded = jsondecode(body)
local hwid_list = {"User-Identifier","user-Identifier","Flux-Fingerprint", "flux-fingerprint","Syn-Fingerprint", "syn-fingerprint", "Proto-User-Identifier", "proto-User-identifier", "Krnl-Hwid", "krnl-hwid", "Sentinel-Fingerprint", "sentinel-fingerprint", "Exploit-Guid", "exploit-guid","Electronid","electronid", "PSU-Fingerprint", "psu-fingerprint"};
local hwid = "";

for i, v in next, hwid_list do
    if decoded.headers[v] then
        hwid = decoded.headers[v];
        break
    end
end

local randoms = randomString

local data = jsondecode(http_request_get("http://103.141.69.249/raw/Server.php?key=".. key .."&random="..randoms))

if data.Hwid == "Unknown" then
    http_request_get("http://103.141.69.249/raw/Changehwid.php?key=".. key .."&hwid="..hwid)
    game.Players.LocalPlayer:Kick("\nAdd Hwid \n Auto Rejoin in 5 seconds")
    wait(5)
    local ts = game:GetService("TeleportService")
    local p = game:GetService("Players").LocalPlayer
    ts:Teleport(game.PlaceId, p)
    else
    if data.Key == key then
        if data.Blacklist == "False" then
            if data.Hwid == hwid then
                script()
            else
                print("Invalid Hwid")
                game.Players.LocalPlayer:Kick("Invalid Hwid")
            end
        else
            print("Blacklist Reason : "..data.Reason)
            game.Players.LocalPlayer:Kick("Blacklist Reason : "..data.Reason)
        end
    else
        warn("Invalid Key")
        game.Players.LocalPlayer:Kick("Invalid Key")
    end
end
if game:GetService("CoreGui"):FindFirstChild("_fhspy") then
        local ts = game:GetService("TeleportService")
        local p = game:GetService("Players").LocalPlayer
        ts:Teleport(4888224079, p)
end

    local old;old=hookfunction(string.len, newcclosure(function(t, ...)
   if (not t) then return old(t, ...) end;
  
   if (rawequal(old(t), 16)) then
       return false
   end;
   return old(t, ...)
end))
