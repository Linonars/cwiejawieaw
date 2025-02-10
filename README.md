
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local leftArm = character:WaitForChild("LeftLowerArm")
local rightArm = character:WaitForChild("RightLowerArm")
local leftLeg = character:WaitForChild("LeftLowerLeg")
local rightLeg = character:WaitForChild("RightLowerLeg")
local gui = player:WaitForChild("PlayerGui"):WaitForChild("ScreenGui")  
local armSlider = gui:WaitForChild("ArmSlider")  
local legSlider = gui:WaitForChild("LegSlider")  
local armButton = gui:WaitForChild("ArmButton")  
local legButton = gui:WaitForChild("LegButton") 
local armResizeFactor = 1  
local legResizeFactor = 1  


    leftArm.Size = Vector3.new(leftArm.Size.X, leftArm.Size.Y * armResizeFactor, leftArm.Size.Z)
    rightArm.Size = Vector3.new(rightArm.Size.X, rightArm.Size.Y * armResizeFactor, rightArm.Size.Z)
    leftLeg.Size = Vector3.new(leftLeg.Size.X, leftLeg.Size.Y * legResizeFactor, leftLeg.Size.Z)
    rightLeg.Size = Vector3.new(rightLeg.Size.X, rightLeg.Size.Y * legResizeFactor, rightLeg.Size.Z)

    
    local reachFactor = 10 * armResizeFactor 

    
    local function checkForBall()
        local rayOrigin = character:WaitForChild("HumanoidRootPart").Position
        local rayDirection = character:WaitForChild("RightHand").CFrame.LookVector * reachFactor
        local ray = workspace:Raycast(rayOrigin, rayDirection)

        if ray and ray.Instance and ray.Instance.Name == "Ball" then
            print("Piłka wykryta! Możesz ją uderzyć.")
        end
    end

    
    checkForBall()
end


armButton.MouseButton1Click:Connect(function()
    armResizeFactor = armSlider.Value  
    resizeAndAlterReach()
end)


legButton.MouseButton1Click:Connect(function()
    legResizeFactor = legSlider.Value  
    resizeAndAlterReach()
end)


resizeAndAlterReach()
