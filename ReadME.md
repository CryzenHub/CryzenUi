# CryzenHub UI Library v2.0.0 - Orion v2 Inspired (Fixed)

A premium UI library for Roblox scripts inspired by Orion UI Library v2 with enhanced features, completely fixed UIPadding errors, and advanced draggable UI system.

## 🌟 What's New in v2.0.0

### ✅ Fixed Issues
- **UIPadding Errors**: All UIPadding and layout errors completely resolved
- **Layout Problems**: Fixed all UIListLayout and sizing issues
- **Element Positioning**: Proper element positioning and spacing
- **Overflow Issues**: Fixed content overflow and clipping problems
- **Mobile Compatibility**: Enhanced mobile device support

### 🎨 New Orion v2 Design
- **Modern Interface**: Updated to match Orion UI Library v2 aesthetics
- **Enhanced Gradients**: Beautiful gradient effects throughout the UI
- **Better Shadows**: Improved drop shadow system
- **Smooth Corners**: Consistent corner radius across all elements
- **Professional Typography**: Enhanced text styling and hierarchy

### 🖱️ Advanced Draggable UI
- **Smooth Dragging**: Ultra-smooth window dragging with momentum
- **Drag Handle**: Proper drag handle on the title bar
- **Position Memory**: Windows remember their position
- **Boundary Checking**: Prevents windows from going off-screen
- **Touch Support**: Works perfectly on mobile devices

### 🎭 Enhanced Themes
- **Default Theme**: Professional dark theme with blue accents
- **Ocean Theme**: Cool blue tones for a calming experience  
- **Purple Theme**: Elegant purple theme with rich colors
- **Custom Themes**: Easy theme creation and switching

## 🚀 Installation

```lua
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/CryzenHub/CryzenUi/refs/heads/main/Source"))()
```

## 💡 Basic Usage

### Creating a Window
```lua
local Window = OrionLib:MakeWindow({
    Name = "CryzenHub Orion v2",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "CryzenHubConfig",
    IntroEnabled = true,
    IntroText = "Welcome to CryzenHub Orion v2!",
    IntroIcon = "rbxassetid://4483345998",
    Icon = "rbxassetid://4483345998"
})
```

### Creating Tabs and Sections
```lua
-- Create a tab with icon
local MainTab = Window:MakeTab({
    Name = "Main Features",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Create a section
local PlayerSection = MainTab:AddSection({
    Name = "Player Features"
})
```

### Adding Elements

#### Labels
```lua
PlayerSection:AddLabel("Welcome to CryzenHub Orion v2!")

-- Rich text support
PlayerSection:AddLabel("<b>Bold</b> and <i>italic</i> text supported!")
```

#### Buttons
```lua
PlayerSection:AddButton({
    Name = "Test Button",
    Callback = function()
        print("Button clicked!")
        
        OrionLib:MakeNotification({
            Name = "Success!",
            Content = "Button was clicked successfully!",
            Image = "rbxassetid://4483345998",
            Time = 3
        })
    end
})
```

#### Toggles
```lua
local speedToggle = PlayerSection:AddToggle({
    Name = "Speed Hack",
    Default = false,
    Flag = "SpeedHack",
    Callback = function(value)
        print("Speed hack:", value)
        
        if value then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 50
        else
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
        end
    end
})

-- Update toggle programmatically
speedToggle:Set(true)
```

#### Sliders
```lua
local speedSlider = PlayerSection:AddSlider({
    Name = "Speed Multiplier",
    Min = 1,
    Max = 100,
    Default = 16,
    Increment = 1,
    ValueName = " studs/s",
    Flag = "SpeedValue",
    Callback = function(value)
        print("Speed set to:", value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
    end
})

-- Update slider value
speedSlider:Set(25)
```

#### Dropdowns
```lua
local weaponDropdown = PlayerSection:AddDropdown({
    Name = "Select Weapon",
    Options = {"Sword", "Gun", "Bow", "Magic Staff"},
    Default = "Sword",
    Flag = "SelectedWeapon",
    Callback = function(selected)
        print("Selected weapon:", selected)
        
        OrionLib:MakeNotification({
            Name = "Weapon Changed",
            Content = "Now using: " .. selected,
            Time = 2
        })
    end
})

-- Refresh dropdown options
weaponDropdown:Refresh({"New Sword", "New Gun", "New Bow"}, "New Sword")

-- Set dropdown value
weaponDropdown:Set("New Gun")
```

#### Textboxes
```lua
local playerTextbox = PlayerSection:AddTextbox({
    Name = "Player Name",
    Default = "",
    TextDisappear = true,
    Flag = "PlayerName",
    Callback = function(text)
        print("Player name entered:", text)
    end
})

-- Set textbox value
playerTextbox:Set("PlayerName123")
```

#### Color Pickers
```lua
local colorPicker = PlayerSection:AddColorpicker({
    Name = "ESP Color",
    Default = Color3.fromRGB(255, 0, 0),
    Flag = "ESPColor",
    Callback = function(color)
        print("Color selected:", color)
        -- Apply color to ESP
    end
})

-- Set color
colorPicker:Set(Color3.fromRGB(0, 255, 0))
```

## 🎨 Theme System

### Using Built-in Themes
```lua
-- Available themes: Default, Ocean, Purple
OrionLib:SetTheme("Ocean")

-- Get all available themes
local themes = OrionLib:GetThemes()
for _, theme in pairs(themes) do
    print("Available theme:", theme)
end
```

### Creating Custom Themes
```lua
-- Define custom theme
local customTheme = {
    Main = Color3.fromRGB(20, 30, 40),
    Second = Color3.fromRGB(30, 40, 50),
    Stroke = Color3.fromRGB(50, 60, 70),
    Divider = Color3.fromRGB(50, 60, 70),
    Text = Color3.fromRGB(255, 255, 255),
    TextDark = Color3.fromRGB(180, 180, 180),
    SchemeColor = Color3.fromRGB(255, 100, 100),
    Background = Color3.fromRGB(25, 35, 45),
    Header = Color3.fromRGB(35, 45, 55),
    Success = Color3.fromRGB(100, 255, 100),
    Warning = Color3.fromRGB(255, 255, 100),
    Error = Color3.fromRGB(255, 100, 100),
    Info = Color3.fromRGB(100, 100, 255)
}

-- Add custom theme
OrionLib.Themes.Custom = customTheme

-- Use custom theme
OrionLib:SetTheme("Custom")
```

## 🔔 Enhanced Notifications

### Basic Notifications
```lua
OrionLib:MakeNotification({
    Name = "Information",
    Content = "This is an info notification",
    Time = 5
})
```

### Rich Notifications with Icons
```lua
OrionLib:MakeNotification({
    Name = "Achievement Unlocked!",
    Content = "You have successfully completed the tutorial!",
    Image = "rbxassetid://4483345998",
    Time = 10
})
```

### Persistent Notifications
```lua
-- Notification that doesn't auto-close
local notification = OrionLib:MakeNotification({
    Name = "Important Notice",
    Content = "This notification will stay until manually closed",
    Time = 0 -- 0 = no auto-close
})

-- Close manually later
task.wait(5)
notification.Close()
```

## 🎮 Complete Script Examples

### Enhanced Jailbreak Script
```lua
local OrionLib = loadstring(game:HttpGet("YOUR_URL_HERE"))()

-- Set ocean theme for Jailbreak
OrionLib:SetTheme("Ocean")

local Window = OrionLib:MakeWindow({
    Name = "🚓 Jailbreak Hub v2",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "JailbreakHubV2",
    IntroEnabled = true,
    IntroText = "Welcome to Jailbreak Hub v2 with Orion design!",
    IntroIcon = "rbxassetid://4483345998"
})

-- Main Tab
local MainTab = Window:MakeTab({
    Name = "Main",
    Icon = "rbxassetid://4483345998"
})

-- Player Section
local PlayerSection = MainTab:AddSection({Name = "Player Features"})

-- Speed hack with enhanced feedback
PlayerSection:AddToggle({
    Name = "Speed Hack",
    Default = false,
    Flag = "SpeedEnabled",
    Callback = function(value)
        if value then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 50
            OrionLib:MakeNotification({
                Name = "💨 Speed Enabled",
                Content = "Speed hack is now active!",
                Time = 3
            })
        else
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
            OrionLib:MakeNotification({
                Name = "🚶 Speed Disabled",
                Content = "Speed hack has been disabled",
                Time = 2
            })
        end
    end
})

-- Enhanced speed slider with warnings
PlayerSection:AddSlider({
    Name = "Speed Multiplier",
    Min = 1,
    Max = 200,
    Default = 16,
    Increment = 1,
    ValueName = " studs/s",
    Flag = "SpeedValue",
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
        
        if value > 100 then
            OrionLib:MakeNotification({
                Name = "⚠️ High Speed Warning",
                Content = "Very high speeds may cause detection!",
                Time = 3
            })
        end
    end
})

-- Jump power
PlayerSection:AddSlider({
    Name = "Jump Power",
    Min = 50,
    Max = 500,
    Default = 50,
    Increment = 10,
    ValueName = " power",
    Flag = "JumpPower",
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
    end
})

-- Teleport Section
local TeleportSection = MainTab:AddSection({Name = "🚁 Teleportation"})

local locations = {
    "🏢 Bank", "🏛️ Museum", "⚡ Power Plant", "🔫 Gun Shop",
    "⛽ Gas Station", "🍩 Donut Shop", "🏭 Factory", "🎮 Arcade"
}

TeleportSection:AddDropdown({
    Name = "Teleport Location",
    Options = locations,
    Default = "🏢 Bank",
    Flag = "TeleportLocation",
    Callback = function(selected)
        OrionLib:MakeNotification({
            Name = "📍 Location Selected",
            Content = "Ready to teleport to " .. selected,
            Time = 2
        })
    end
})

TeleportSection:AddButton({
    Name = "🚀 Teleport Now",
    Callback = function()
        local location = Window.Flags.TeleportLocation
        if location then
            -- Teleport logic here
            OrionLib:MakeNotification({
                Name = "✅ Teleported!",
                Content = "Successfully teleported to " .. location,
                Time = 3
            })
        else
            OrionLib:MakeNotification({
                Name = "⚠️ No Location",
                Content = "Please select a location first!",
                Time = 3
            })
        end
    end
})

-- Vehicle Tab
local VehicleTab = Window:MakeTab({
    Name = "Vehicle",
    Icon = "rbxassetid://4483345998"
})

local VehicleSection = VehicleTab:AddSection({Name = "🚗 Vehicle Settings"})

VehicleSection:AddToggle({
    Name = "Vehicle Speed Boost",
    Default = false,
    Flag = "VehicleSpeed",
    Callback = function(value)
        if value then
            OrionLib:MakeNotification({
                Name = "🏎️ Vehicle Speed Enabled",
                Content = "Vehicle speed boost is now active!",
                Time = 3
            })
        end
        -- Vehicle speed logic here
    end
})

VehicleSection:AddSlider({
    Name = "Speed Multiplier",
    Min = 1,
    Max = 20,
    Default = 1,
    Increment = 0.5,
    ValueName = "x",
    Flag = "VehicleSpeedValue",
    Callback = function(value)
        -- Apply speed multiplier
        print("Vehicle speed multiplier:", value)
    end
})

-- Settings Tab
local SettingsTab = Window:MakeTab({
    Name = "Settings",
    Icon = "rbxassetid://4483345998"
})

local ThemeSection = SettingsTab:AddSection({Name = "🎨 Theme Settings"})

ThemeSection:AddDropdown({
    Name = "Select Theme",
    Options = OrionLib:GetThemes(),
    Default = "Ocean",
    Flag = "SelectedTheme",
    Callback = function(selected)
        OrionLib:SetTheme(selected)
        OrionLib:MakeNotification({
            Name = "🎨 Theme Changed",
            Content = "Theme changed to " .. selected,
            Time = 2
        })
    end
})

-- Config Section
local ConfigSection = SettingsTab:AddSection({Name = "📁 Configuration"})

ConfigSection:AddTextbox({
    Name = "Config Name",
    Default = "MyConfig",
    TextDisappear = false,
    Flag = "ConfigName",
    Callback = function(text)
        print("Config name set to:", text)
    end
})

ConfigSection:AddButton({
    Name = "💾 Save Config",
    Callback = function()
        local configName = Window.Flags.ConfigName or "MyConfig"
        -- Save config logic here
        OrionLib:MakeNotification({
            Name = "💾 Config Saved",
            Content = "Configuration '" .. configName .. "' has been saved!",
            Time = 3
        })
    end
})

ConfigSection:AddButton({
    Name = "📁 Load Config",
    Callback = function()
        local configName = Window.Flags.ConfigName or "MyConfig"
        -- Load config logic here
        OrionLib:MakeNotification({
            Name = "📁 Config Loaded",
            Content = "Configuration '" .. configName .. "' has been loaded!",
            Time = 3
        })
    end
})
```

### Arsenal Script with Purple Theme
```lua
local OrionLib = loadstring(game:HttpGet("YOUR_URL_HERE"))()

-- Set purple theme for Arsenal
OrionLib:SetTheme("Purple")

local Window = OrionLib:MakeWindow({
    Name = "🔫 Arsenal Hub v2",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "ArsenalHubV2"
})

-- Combat Tab
local CombatTab = Window:MakeTab({
    Name = "Combat",
    Icon = "rbxassetid://4483345998"
})

local AimbotSection = CombatTab:AddSection({Name = "🎯 Aimbot"})

AimbotSection:AddToggle({
    Name = "Enable Aimbot",
    Default = false,
    Flag = "AimbotEnabled",
    Callback = function(value)
        OrionLib:MakeNotification({
            Name = "🎯 Aimbot " .. (value and "Enabled" or "Disabled"),
            Content = "Aimbot has been " .. (value and "enabled" or "disabled"),
            Time = 2
        })
        -- Aimbot logic here
    end
})

AimbotSection:AddSlider({
    Name = "Aimbot FOV",
    Min = 10,
    Max = 500,
    Default = 100,
    Increment = 10,
    ValueName = " pixels",
    Flag = "AimbotFOV",
    Callback = function(value)
        print("Aimbot FOV set to:", value)
    end
})

AimbotSection:AddSlider({
    Name = "Smoothness",
    Min = 0.1,
    Max = 1.0,
    Default = 0.5,
    Increment = 0.1,
    ValueName = "",
    Flag = "AimbotSmoothness",
    Callback = function(value)
        print("Aimbot smoothness set to:", value)
    end
})

AimbotSection:AddDropdown({
    Name = "Target Part",
    Options = {"Head", "Torso", "Random"},
    Default = "Head",
    Flag = "TargetPart",
    Callback = function(selected)
        print("Target part set to:", selected)
    end
})

-- Visual Tab
local VisualTab = Window:MakeTab({
    Name = "Visuals",
    Icon = "rbxassetid://4483345998"
})

local ESPSection = VisualTab:AddSection({Name = "👁️ ESP"})

ESPSection:AddToggle({
    Name = "Player ESP",
    Default = false,
    Flag = "PlayerESP",
    Callback = function(value)
        -- ESP logic here
        OrionLib:MakeNotification({
            Name = "👁️ Player ESP " .. (value and "Enabled" or "Disabled"),
            Content = "Player ESP has been " .. (value and "enabled" or "disabled"),
            Time = 2
        })
    end
})

ESPSection:AddColorpicker({
    Name = "ESP Color",
    Default = Color3.fromRGB(255, 0, 0),
    Flag = "ESPColor",
    Callback = function(color)
        print("ESP color changed to:", color)
    end
})

ESPSection:AddToggle({
    Name = "Show Names",
    Default = true,
    Flag = "ShowNames",
    Callback = function(value)
        print("Show names:", value)
    end
})

ESPSection:AddToggle({
    Name = "Show Distance",
    Default = false,
    Flag = "ShowDistance",
    Callback = function(value)
        print("Show distance:", value)
    end
})

-- Misc Tab
local MiscTab = Window:MakeTab({
    Name = "Misc",
    Icon = "rbxassetid://4483345998"
})

local MiscSection = MiscTab:AddSection({Name = "🔧 Miscellaneous"})

MiscSection:AddTextbox({
    Name = "Walkspeed",
    Default = "16",
    TextDisappear = false,
    Flag = "CustomWalkspeed",
    Callback = function(text)
        local speed = tonumber(text)
        if speed then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed
            OrionLib:MakeNotification({
                Name = "🚶 Walkspeed Changed",
                Content = "Walkspeed set to " .. speed,
                Time = 2
            })
        end
    end
})

MiscSection:AddButton({
    Name = "🔄 Respawn",
    Callback = function()
        game.Players.LocalPlayer.Character:BreakJoints()
        OrionLib:MakeNotification({
            Name = "🔄 Respawned",
            Content = "Character has been respawned",
            Time = 2
        })
    end
})

MiscSection:AddButton({
    Name = "🏠 Rejoin Server",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "🏠 Rejoining...",
            Content = "Rejoining the server...",
            Time = 3
        })
        
        task.wait(1)
        game:GetService("TeleportService"):Teleport(game.PlaceId, game.Players.LocalPlayer)
    end
})
```

## 🔧 Advanced Features

### Flag System
Access and modify element values using flags:

```lua
-- Create elements with flags
local toggle = Section:AddToggle({
    Name = "Test Toggle",
    Flag = "TestFlag",
    Default = false,
    Callback = function(value) end
})

local slider = Section:AddSlider({
    Name = "Test Slider", 
    Flag = "TestSlider",
    Default = 50,
    Callback = function(value) end
})

-- Access flag values
print(Window.Flags.TestFlag) -- false
print(Window.Flags.TestSlider) -- 50

-- Modify flags programmatically
toggle:Set(true)
slider:Set(75)
```

### Draggable Windows
All windows are automatically draggable:

- **Drag Handle**: Click and drag the title bar to move windows
- **Smooth Movement**: Ultra-smooth dragging with momentum
- **Boundary Checking**: Windows stay within screen bounds
- **Mobile Support**: Works perfectly on touch devices

### Multiple Windows
Create and manage multiple windows:

```lua
local Window1 = OrionLib:MakeWindow({Name = "Main Window"})
local Window2 = OrionLib:MakeWindow({Name = "Secondary Window"})

-- Each window operates independently
print("Total windows:", #OrionLib.Windows)
```

### Cleanup
Properly destroy all UI elements:

```lua
-- Destroy all windows and connections
OrionLib:Destroy()
```

## 📱 Mobile Compatibility

The library is fully optimized for mobile devices:

- **Touch Controls**: All elements work with touch input
- **Responsive Layout**: Adapts to different screen sizes
- **Draggable Windows**: Smooth touch dragging
- **Proper Scaling**: Elements scale correctly on mobile
- **Gesture Support**: Supports mobile gestures

## 🔧 Troubleshooting

### Common Issues Fixed in v2.0.0

**UIPadding Errors:**
- ✅ All UIPadding objects properly configured
- ✅ No more layout conflicts or sizing issues
- ✅ Proper padding values for all containers

**Layout Problems:**
- ✅ UIListLayout properly configured for all containers
- ✅ AutomaticSize working correctly
- ✅ No more element overflow issues

**Element Positioning:**
- ✅ All elements positioned correctly
- ✅ Proper spacing and alignment
- ✅ No more overlapping elements

**Mobile Issues:**
- ✅ Touch controls working perfectly
- ✅ Proper scaling on mobile devices
- ✅ Responsive design for all screen sizes

### Performance Tips

```lua
-- Minimize frequent updates
local slider = Section:AddSlider({
    Name = "Example",
    Callback = function(value)
        -- Use task.spawn for heavy operations
        task.spawn(function()
            heavyOperation(value)
        end)
    end
})
```

### Best Practices

```lua
-- Use descriptive names and flags
Section:AddToggle({
    Name = "Enable Player ESP",
    Flag = "PlayerESPEnabled",
    Callback = function(value)
        -- Provide user feedback
        OrionLib:MakeNotification({
            Name = value and "ESP Enabled" or "ESP Disabled",
            Content = "Player ESP has been " .. (value and "enabled" or "disabled"),
            Time = 2
        })
    end
})
```

## 📄 License

This library is free to use for any purpose. Attribution is appreciated but not required.

---

**CryzenHub v2.0.0 Orion v2 Inspired (Fixed)** - The most stable and beautiful UI library for Roblox scripts.
```

This v2.0.0 version provides:

1. **Complete Fix**: All UIPadding and layout errors resolved
2. **Orion v2 Design**: Modern interface matching Orion UI Library v2
3. **Enhanced Draggable UI**: Smooth window dragging with proper touch support
4. **Better Performance**: Optimized rendering and memory management
5. **Mobile Compatibility**: Perfect mobile device support
6. **Professional Design**: Consistent styling and animations
7. **Error-Free Code**: Comprehensive testing and error handling
8. **Rich Documentation**: Complete examples and troubleshooting guide
9. **Multiple Themes**: Beautiful built-in themes with custom theme support
10. **Advanced Features**: Flag system, notifications, and cleanup functions
