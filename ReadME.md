# CryzenHub UI Library v1.0.0 - Orion Inspired

A premium UI library for Roblox scripts inspired by the elegant design of Orion UI Library, enhanced with CryzenHub's advanced features and performance optimizations.

![CryzenHub Orion](https://i.imgur.com/placeholder.png)

## 🌟 Features

### 🎨 Orion-Inspired Design
- **Modern Card Interface**: Clean, card-based design with smooth corners
- **Professional Typography**: Gotham font family for crisp, readable text
- **Consistent Spacing**: Carefully designed padding and margins
- **Elegant Animations**: Smooth transitions and hover effects
- **Material Ripple Effects**: Interactive feedback on button clicks

### 🎭 Multiple Themes
- **Default Theme**: Professional dark theme with blue accents
- **Ocean Theme**: Cool blue tones for a calming experience
- **Dark Theme**: Deep black theme with purple accents
- **Custom Themes**: Easy theme creation and customization

### 📱 Modern Components
- **Smart Tabs**: Icon-supported tabs with smooth selection
- **Interactive Buttons**: Ripple effects and hover animations
- **Advanced Toggles**: Visual feedback with checkmark indicators
- **Smooth Sliders**: Real-time value display and smooth dragging
- **Enhanced Dropdowns**: Searchable options with smooth animations
- **Modern Textboxes**: Focus effects and placeholder support
- **Color Pickers**: Intuitive color selection interface

### 🔔 Advanced Notifications
- **Multiple Types**: Info, success, warning, and error notifications
- **Rich Content**: Support for icons, titles, and detailed messages
- **Auto Dismiss**: Configurable auto-close timers
- **Progress Indicators**: Visual progress bars for timed notifications
- **Smooth Animations**: Elegant slide-in and slide-out effects

### ⚡ Performance Optimized
- **Efficient Rendering**: Optimized for smooth 60fps performance
- **Memory Management**: Automatic cleanup and garbage collection
- **Error Handling**: Comprehensive error catching and logging
- **Mobile Support**: Responsive design for all screen sizes

## 🚀 Installation

```lua
local CryzenHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/CryzenHub/CryzenUi/refs/heads/main/Source"))()
```

## 💡 Basic Usage

### Creating a Window
```lua
local Window = CryzenHub:MakeWindow({
    Name = "CryzenHub Orion",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "MyScript",
    IntroEnabled = true,
    IntroText = "Welcome to CryzenHub!",
    IntroIcon = "rbxassetid://4483345998",
    Icon = "rbxassetid://4483345998"
})
```

### Creating Tabs and Sections
```lua
-- Create a tab
local MainTab = Window:MakeTab({
    Name = "Main Features",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Create a section
local Section = MainTab:AddSection({
    Name = "Player Features"
})
```

### Adding Elements

#### Labels
```lua
Section:AddLabel({
    Text = "Welcome to CryzenHub Orion!"
})

-- Rich text support
Section:AddLabel({
    Text = "<b>Bold</b> and <i>italic</i> text supported!"
})
```

#### Buttons
```lua
Section:AddButton({
    Name = "Click Me!",
    Callback = function()
        print("Button clicked!")
        CryzenHub:CreateNotification({
            Title = "Success!",
            Content = "Button was clicked successfully!",
            Image = "rbxassetid://4483345998",
            Time = 3
        })
    end
})
```

#### Toggles
```lua
local speedToggle = Section:AddToggle({
    Name = "Speed Hack",
    Default = false,
    Flag = "SpeedHack",
    Callback = function(value)
        print("Speed hack:", value)
        
        if value then
            -- Enable speed hack
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 50
        else
            -- Disable speed hack
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
        end
    end
})

-- Update toggle programmatically
speedToggle:Set(true)
```

#### Sliders
```lua
local speedSlider = Section:AddSlider({
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
local weaponDropdown = Section:AddDropdown({
    Name = "Select Weapon",
    Options = {"Sword", "Gun", "Bow", "Magic Staff"},
    Default = "Sword",
    Flag = "SelectedWeapon",
    Callback = function(selected)
        print("Selected weapon:", selected)
        CryzenHub:CreateNotification({
            Title = "Weapon Changed",
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
local playerTextbox = Section:AddTextbox({
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
local colorPicker = Section:AddColorpicker({
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
-- Change theme
CryzenHub:SetTheme("Ocean")  -- Ocean, Dark, Default

-- Get available themes
local themes = CryzenHub:GetThemes()
for _, theme in pairs(themes) do
    print("Available theme:", theme)
end
```

### Creating Custom Themes
```lua
-- Define custom theme
local myTheme = {
    Name = "Custom",
    Main = Color3.fromRGB(30, 30, 35),
    Second = Color3.fromRGB(40, 40, 45),
    Stroke = Color3.fromRGB(60, 60, 65),
    Divider = Color3.fromRGB(60, 60, 65),
    Text = Color3.fromRGB(255, 255, 255),
    TextDark = Color3.fromRGB(180, 180, 180),
    SchemeColor = Color3.fromRGB(255, 100, 100),
    Background = Color3.fromRGB(35, 35, 40),
    Header = Color3.fromRGB(45, 45, 50),
    Success = Color3.fromRGB(100, 255, 100),
    Warning = Color3.fromRGB(255, 255, 100),
    Error = Color3.fromRGB(255, 100, 100),
    Info = Color3.fromRGB(100, 100, 255),
    DropShadow = Color3.fromRGB(0, 0, 0),
    CornerRadius = 8,
    StrokeThickness = 1,
    Font = Enum.Font.Gotham,
    FontSemiBold = Enum.Font.GothamSemibold,
    FontBold = Enum.Font.GothamBold,
    TextSize = {
        Small = 12,
        Medium = 14,
        Large = 16,
        XLarge = 18
    }
}

-- Add custom theme
CryzenHub.Themes.Custom = myTheme

-- Use custom theme
CryzenHub:SetTheme("Custom")
```

## 🔔 Advanced Notifications

### Basic Notifications
```lua
CryzenHub:CreateNotification({
    Title = "Information",
    Content = "This is an info notification",
    Time = 5
})
```

### Rich Notifications
```lua
CryzenHub:CreateNotification({
    Title = "Achievement Unlocked!",
    Content = "You have successfully completed the tutorial!",
    Image = "rbxassetid://4483345998",
    Time = 10
})
```

### Persistent Notifications
```lua
-- Notification that doesn't auto-close
local notification = CryzenHub:CreateNotification({
    Title = "Important Notice",
    Content = "This notification will stay until manually closed",
    Time = 0 -- 0 = no auto-close
})

-- Close manually later
task.wait(5)
notification.Close()
```

## 🎮 Complete Script Examples

### Jailbreak Script
```lua
local CryzenHub = loadstring(game:HttpGet("YOUR_URL_HERE"))()

-- Set theme for Jailbreak
CryzenHub:SetTheme("Ocean")

local Window = CryzenHub:MakeWindow({
    Name = "Jailbreak Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "JailbreakHub",
    IntroEnabled = true,
    IntroText = "Welcome to Jailbreak Hub!",
    IntroIcon = "rbxassetid://4483345998"
})

-- Main Tab
local MainTab = Window:MakeTab({
    Name = "Main",
    Icon = "rbxassetid://4483345998"
})

local PlayerSection = MainTab:AddSection({Name = "Player"})

-- Speed hack
PlayerSection:AddToggle({
    Name = "Speed Hack",
    Default = false,
    Callback = function(value)
        if value then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 50
        else
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
        end
    end
})

-- Jump power
PlayerSection:AddSlider({
    Name = "Jump Power",
    Min = 50,
    Max = 200,
    Default = 50,
    Increment = 10,
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
    end
})

-- Teleport Section
local TeleportSection = MainTab:AddSection({Name = "Teleport"})

local locations = {
    "Bank", "Prison", "Criminal Base", "Police Station", 
    "Gun Shop", "Garage", "Jewelry Store"
}

TeleportSection:AddDropdown({
    Name = "Location",
    Options = locations,
    Default = "Bank",
    Callback = function(selected)
        print("Selected location:", selected)
        
        -- Teleport logic here
        CryzenHub:CreateNotification({
            Title = "Teleported!",
            Content = "Teleported to " .. selected,
            Time = 3
        })
    end
})

-- Vehicle Tab
local VehicleTab = Window:MakeTab({
    Name = "Vehicle",
    Icon = "rbxassetid://4483345998"
})

local VehicleSection = VehicleTab:AddSection({Name = "Vehicle Settings"})

VehicleSection:AddToggle({
    Name = "Vehicle Speed",
    Default = false,
    Callback = function(value)
        -- Vehicle speed logic here
    end
})

VehicleSection:AddSlider({
    Name = "Speed Multiplier",
    Min = 1,
    Max = 10,
    Default = 1,
    Increment = 0.5,
    ValueName = "x",
    Callback = function(value)
        -- Apply speed multiplier
    end
})

-- Settings Tab
local SettingsTab = Window:MakeTab({
    Name = "Settings",
    Icon = "rbxassetid://4483345998"
})

local ThemeSection = SettingsTab:AddSection({Name = "Theme"})

ThemeSection:AddDropdown({
    Name = "Select Theme",
    Options = CryzenHub:GetThemes(),
    Default = "Ocean",
    Callback = function(selected)
        CryzenHub:SetTheme(selected)
        CryzenHub:CreateNotification({
            Title = "Theme Changed",
            Content = "Theme changed to " .. selected,
            Time = 2
        })
    end
})
```

### Arsenal Script
```lua
local CryzenHub = loadstring(game:HttpGet("YOUR_URL_HERE"))()

CryzenHub:SetTheme("Dark")

local Window = CryzenHub:MakeWindow({
    Name = "Arsenal Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "ArsenalHub"
})

-- Combat Tab
local CombatTab = Window:MakeTab({
    Name = "Combat",
    Icon = "rbxassetid://4483345998"
})

local AimbotSection = CombatTab:AddSection({Name = "Aimbot"})

AimbotSection:AddToggle({
    Name = "Enable Aimbot",
    Default = false,
    Callback = function(value)
        -- Aimbot logic here
        CryzenHub:CreateNotification({
            Title = "Aimbot " .. (value and "Enabled" or "Disabled"),
            Content = "Aimbot has been " .. (value and "enabled" or "disabled"),
            Time = 2
        })
    end
})

AimbotSection:AddSlider({
    Name = "Aimbot FOV",
    Min = 10,
    Max = 500,
    Default = 100,
    Increment = 10,
    ValueName = " pixels",
    Callback = function(value)
        -- Set aimbot FOV
    end
})

AimbotSection:AddDropdown({
    Name = "Target Part",
    Options = {"Head", "Torso", "Random"},
    Default = "Head",
    Callback = function(selected)
        -- Set target part
    end
})

-- Visual Tab
local VisualTab = Window:MakeTab({
    Name = "Visuals",
    Icon = "rbxassetid://4483345998"
})

local ESPSection = VisualTab:AddSection({Name = "ESP"})

ESPSection:AddToggle({
    Name = "Player ESP",
    Default = false,
    Callback = function(value)
        -- ESP logic here
    end
})

ESPSection:AddColorpicker({
    Name = "ESP Color",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(color)
        -- Apply ESP color
    end
})

-- Misc Tab
local MiscTab = Window:MakeTab({
    Name = "Misc",
    Icon = "rbxassetid://4483345998"
})

local MiscSection = MiscTab:AddSection({Name = "Miscellaneous"})

MiscSection:AddTextbox({
    Name = "Walkspeed",
    Default = "16",
    TextDisappear = false,
    Callback = function(text)
        local speed = tonumber(text)
        if speed then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed
        end
    end
})

MiscSection:AddButton({
    Name = "Respawn",
    Callback = function()
        game.Players.LocalPlayer.Character:BreakJoints()
        CryzenHub:CreateNotification({
            Title = "Respawned",
            Content = "Character has been respawned",
            Time = 2
        })
    end
})
```

## 🔧 Advanced Features

### Flag System
```lua
-- Access flag values
local Window = CryzenHub:MakeWindow({Name = "Test"})
local Tab = Window:MakeTab({Name = "Test"})
local Section = Tab:AddSection({Name = "Test"})

Section:AddToggle({
    Name = "Test Toggle",
    Flag = "TestFlag",
    Default = false,
    Callback = function(value) end
})

-- Access flag value
print(Window.Flags.TestFlag) -- false

-- Update flag value
Window.Flags.TestFlag = true
```

### Debug Mode
```lua
-- Enable debug logging
CryzenHub.Debug.Enabled = true

-- View debug logs
for _, log in pairs(CryzenHub.Debug.Logs) do
    print(log)
end
```

### Performance Optimization
```lua
-- The library automatically optimizes performance based on:
-- - Number of elements
-- - Device capabilities
-- - Frame rate monitoring
-- - Memory usage tracking
```

## 📱 Mobile Support

The library is fully responsive and works seamlessly on mobile devices:

- **Touch-friendly buttons**: Larger hit areas for easier tapping
- **Responsive layout**: Adapts to different screen sizes
- **Smooth scrolling**: Optimized for touch scrolling
- **Mobile gestures**: Support for swipe and pinch gestures

## 🎯 Best Practices

### Performance
```lua
-- Minimize frequent updates
local slider = Section:AddSlider({
    Name = "Example",
    Callback = function(value)
        -- Avoid expensive operations here
        -- Use task.spawn for heavy operations
        task.spawn(function()
            heavyOperation(value)
        end)
    end
})
```

### User Experience
```lua
-- Provide feedback for all actions
Section:AddButton({
    Name = "Action Button",
    Callback = function()
        -- Show loading state
        CryzenHub:CreateNotification({
            Title = "Processing...",
            Content = "Please wait while the action completes",
            Time = 2
        })
        
        -- Perform action
        performAction()
        
        -- Show completion
        CryzenHub:CreateNotification({
            Title = "Complete!",
            Content = "Action completed successfully",
            Time = 3
        })
    end
})
```

### Organization
```lua
-- Group related features in sections
local PlayerSection = Tab:AddSection({Name = "Player Features"})
local CombatSection = Tab:AddSection({Name = "Combat Features"})
local VisualSection = Tab:AddSection({Name = "Visual Features"})

-- Use descriptive names and flags
Section:AddToggle({
    Name = "Enable Player ESP",
    Flag = "PlayerESPEnabled",
    Callback = function(value) end
})
```

## 🔧 Troubleshooting

### Common Issues

**UI not appearing:**
```lua
-- Check if ScreenGui was created successfully
if not CryzenHub.ScreenGui then
    warn("Failed to create ScreenGui - check CoreGui access")
end
```

**Elements not responding:**
```lua
-- Ensure callbacks are functions
Section:AddButton({
    Name = "Test",
    Callback = function()  -- Make sure this is a function
        print("Button clicked")
    end
})
```

**Performance issues:**
```lua
-- Enable debug mode to monitor performance
CryzenHub.Debug.Enabled = true

-- Check debug logs for performance warnings
```

## 📄 License

This library is free to use for any purpose. Attribution is appreciated but not required.

---

**CryzenHub v1.0.0 Orion Inspired** - Modern, elegant, and powerful UI library for Roblox.
```

This v1.0.0 Orion-inspired version provides:

1. **Complete Redesign**: New modern card-based interface inspired by Orion UI
2. **Enhanced Themes**: Multiple built-in themes with easy customization
3. **Improved Components**: All elements redesigned with better UX
4. **Advanced Notifications**: Rich notification system with animations
5. **Better Performance**: Optimized rendering and memory management
6. **Mobile Support**: Responsive design for all devices
7. **Professional Design**: Clean, modern aesthetics with consistent styling
8. **Easy Integration**: Simple API similar to Orion but with CryzenHub enhancements
9. **Error Handling**: Comprehensive error catching and logging
10. **Rich Documentation**: Complete examples and best practices

