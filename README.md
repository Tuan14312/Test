Config = {
namescript "test,

logoscript "210869654"

tacgia "sadas''

lua
local characters = {all player}
local function addCharacter(character)
table.insert(characters, character)
end
local function startPvP()
for i, v in pairs(characters) do
v:FireServer("PvP")
end
end
local function updateHealth(character, health)
character:FireServer("UpdateHealth", health)
end
local function attack(character, attacker, damage)
character:FireServer("Attack", attacker, damage)
end
game.Players.LocalPlayer.CharacterAdded:Connect(function()
if #characters >= 2 then
startPvP()
end
end)
game.Players.LocalPlayer.CharacterAdded:Connect(function()
local character = game.Players.LocalPlayer.Character
local health = character:FireServer("GetHealth")
updateHealth(character, health)
end)
game:GetService("UserInputService").InputBegan:Connect(function(input)
if input.KeyCode == Enum.KeyCode.E then
local character = game.Players.LocalPlayer.Character
local attacker = character
local target = game.Players:GetPlayerFromCharacter(game.Workspace:FindFirstChild("Target"))
if target then
attack(target, attacker, 10)
end
end
end)
