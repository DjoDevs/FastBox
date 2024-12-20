# FastBox
a quick and easy way to make hitboxes in roblox
the documentation is really short so ill just go over it here
--FastBox is basically an easy way to makke hitboxes if you dont wanna do it yourself
--ik this can be made in like 30 minutes but i think its really nice for anyone whos lazy
--okay lets actually start with the documentation

--first of all you want to require the script which can be done by simply doing:
local FastBox = require(game:GetService("ReplicatedStorage"):WaitForChild("FastBox"):WaitForChild("FastBox"))
--after you have required the module make an attachement under the part you want to cast a hitbox on
--this can simply be done by doing:
game.Players.PlayerAdded:Connect(function(plr) -- also use this in serverscriptservice before anyone asks
	plr.CharacterAdded:Connect(function(Character)
		local attachement = Instance.new("Attachment")
		attachement.Name = "HitboxAttachement"  -- name it whatever it doesnt matter
		attachement.Parent = Character["Right Arm"]
	end)
end)
--congrats you have the basics setup nextup is actually using the module!!!!!
--first of all you want to create new hitboxdata for your hitbox and how do you do that?
local player = game.Players.LocalPlayer 
local character = player.Character or player.CharacterAdded:Wait() -- if you cant already tell this is a local script
local hitbox = FastBox.new({
	Attachment = character:WaitForChild("Right Arm"):WaitForChild("HitboxAttachement"), -- put the attachement which you wanna use here
	Size = Vector3.new(5,5,5), -- the size
	Params = OverlapParams.new(), -- just copy this line if you dont wanna do anything special
})
--
--next up were gonna show you how to start the hitbox!!!!!
--for that you wanna use the 
hitbox:HitStart() -- simple as that now the hitbox is detecting hits! dont worry it shouldnt hit the player whos casting the hitbox or anything other than the player (i think so)
hitbox:HitStop() -- stops the hit detection very self explanatory
hitbox.OnHitEvent:Connect(function(character, humanoid) -- this will detect when the player hitbox hits another player
	local event = Instance.new('RemoteEvent') -- random remote event i recommend using a networking library though
	event:FireServer(character, humanoid) -- fires to the server so thes erver cna do the logic damage other player etc etc etc etc
end)
hitbox:IsActive() -- this will return if the hitbox is still active not the most useful but it has its use cases
hitbox:Destroy() -- this will basically destroy the connection and stop the hitbox from detecting hits
-- if you made it this far i highly recommend you use a distance checker on the server lol cus exploiters are gonna uh oh kill everyone
