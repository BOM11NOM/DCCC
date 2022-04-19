local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()

local Window = Library.CreateLib("MKXHUB", "DarkTheme")

local Tab = Window:NewTab("pvp")

local Section = Tab:NewSection("กด")

Section:NewButton("ButtonText", "กด", function()

    Combat:AddToggle("Auto Farm Player",false,function(value)

        _G.AutoFarmPlayer = value

    end)

    

    spawn(function()

        while wait() do 

            pcall(function()

                if _G.AutoFarmPlayer then

                    if game.Players:FindFirstChild(_G.SelectPly) and game.Players:FindFirstChild(_G.SelectPly).Character.Humanoid.Health > 0 then

                        repeat task.wait()

                            EquipWeapon(_G.SelectWeaponKill)

                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players:FindFirstChild(_G.SelectPly).Character.HumanoidRootPart.CFrame

                            game:GetService'VirtualUser':CaptureController()

                            game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))

                        until game.Players:FindFirstChild(_G.SelectPly).Character.Humanoid.Health <= 0 or not _G.AutoFarmPlayer or not game.Players:FindFirstChild(_G.SelectPly)

                    end

                end

            end)

        end

    end)

end)
