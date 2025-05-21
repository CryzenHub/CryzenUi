# CryzenHub UI Library v1.2.0

A modern, powerful, and customizable UI library for Roblox Luau scripts with a comprehensive key system, sleek design, and extensive features.

## What's New in v1.2.0

- **Key System**: Secure authentication with multiple verification methods
  - Online verification via API
  - Offline verification with predefined keys
  - Linkvertise key generation
  - Hardware ID binding
  - Auto-login support
  - Discord webhook integration for key logging
- **Configuration System**: Save and load UI configurations
  - Save element states between sessions
  - UI state persistence (position, size, theme, etc.)
  - Export/import configurations
- **Loading Screen**: Customizable loading screens with animations
- **UI Sounds**: Sound effects for interactions and haptic feedback
- **Enhanced Mobile Support**: Improved touch controls and adaptive layouts
- **Performance Improvements**: Optimized rendering and memory usage
- **Element Grouping**: Organize elements in grid layouts
- **New UI Elements**: Progress bars, charts, and more
- **Custom Window Shapes**: Choose from different window styles
- **Bug Fixes**: Various stability improvements and fixes

## Getting Started

### Installation

```lua
local CryzenHub = loadstring(game:HttpGet('https://raw.githubusercontent.com/YourUsername/CryzenHub/main/Source.lua'))()
```

## Key System

### Creating a Key System

```lua
local keySystem = CryzenHub:CreateKeySystem({
    Title = "My Script", -- Title of the key system
    Subtitle = "Authentication", -- Subtitle text
    Logo = "rbxassetid://7733765398", -- Optional logo
    Note = "Enter your key to access the script", -- Note to display
    KeyLinkURL = "https://example.com/getkey", -- URL for obtaining a key
    AutoLogin = true, -- Enable auto-login
    
    -- Key verification settings
    KeyData = {
        verificationMethod = "offline", -- "offline", "online", or "linkvertise"
        
        -- For online verification
        verificationURL = "https://yourapi.com/verify",
        
        -- For offline verification
        keys = {
            {key = "EXAMPLE-KEY-123", expiresAt = os.time() + 86400, userId = nil, hwid = nil}
        },
        
        -- For linkvertise method
        secretKey = "yoursecretkey",
        keyExpiration = 86400, -- 24 hours
        
        -- Common settings
        webhookURL = "https://discord.com/api/webhooks/your-webhook-url", -- Discord webhook for logging
        saveKeys = true, -- Save keys to file (offline mode)
        allowHWIDUpdate = true -- Allow HWID to be updated (offline mode)
    },
    
    -- Optional callback when authentication is successful
    onAuthenticated = function()
        print("Key verified successfully!")
    end
})
```

### Key System Verification Methods

#### 1. Online Verification

Uses an external API to verify keys. Your API should accept:
- `key`: The key to verify
- `hwid`: Hardware ID of the user
- `username`: Roblox username
- `userid`: Roblox user ID
- `game`: Roblox place ID

And return JSON with:
```json
{
    "success": true/false,
    "message": "Optional message"
}
```

#### 2. Offline Verification

Verifies keys against a predefined list. Each key can have:
- `key`: The key string
- `expiresAt`: Expiration timestamp
- `userId`: Optional user ID binding
- `hwid`: Optional hardware ID binding

#### 3. Linkvertise Verification

Generates keys based on user ID, timestamp, and a secret key. Perfect for integration with linkvertise or other ad-based key systems.

## Main UI

### Creating a Window

```lua
local window = CryzenHub:CreateWindow({
    Title = "My Script",
    Size = UDim2.new(0, 600, 0, 400),
    Theme = "Default", -- Theme preset (Default, Light, Dark, Oceanic, Midnight)
    DefaultTab = "Main", -- Tab to be selected by default
    TabBarMode = false, -- Use vertical tabs (true for horizontal tabs)
    AutoScale = true, -- Automatically scale UI based on screen size
    SaveConfig = true, -- Save UI state
    WindowName = "MyScript", -- Used for saving UI state
    WindowShape = "Rounded", -- "Rectangle", "Rounded", or "Circular"
    UseKeySystem = true -- Require key authentication
})
```

### Tabs and Sections

```lua
local mainTab = window:CreateTab("Main", "rbxassetid://7733765398") -- With icon
local settingsTab = window:CreateTab("Settings")

-- Create a section with collapsible header
local generalSection = mainTab:CreateSection("General", true)
local visualsSection = mainTab:CreateSection("Visuals", true)

-- Create a grid layout (2 columns)
local gridContainer = generalSection:CreateGridLayout(2)
```

### UI Elements

#### Button

```lua
local button = generalSection:CreateButton({
    Text = "Click Me",
    Tooltip = "This is a button with a tooltip",
    Callback = function()
        window:Notify({
            Title = "Button Clicked",
            Content = "You clicked the button!",
            Duration = 3,
            Type = "Success"
        })
    end
})
```

#### Toggle

```lua
local toggle = generalSection:CreateToggle({
    Text = "Enable Feature",
    Tooltip = "Toggles the feature on/off",
    Default = false,
    Callback = function(value)
        print("Toggle state:", value)
    end
})

-- API methods
toggle:Set(true) -- Set toggle state
local state = toggle:Get() -- Get current state
```

#### Slider

```lua
local slider = generalSection:CreateSlider({
    Text = "Walkspeed",
    Tooltip = "Adjust your character's walk speed",
    Min = 16,
    Max = 100,
    Default = 16,
    Precise = false, -- Use integers
    Unit = " studs/s", -- Display unit
    Callback = function(value)
        if game.Players.LocalPlayer.Character then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
        end
    end
})
```

#### Dropdown

```lua
local dropdown = generalSection:CreateDropdown({
    Text = "Select Option",
    Tooltip = "Choose from the list",
    Options = {"Option 1", "Option 2", "Option 3"},
    Default = "Option 1",
    MultiSelect = false, -- Single selection
    Callback = function(option)
        print("Selected:", option)
    end
})

-- Multi-select dropdown
local multiDropdown = generalSection:CreateDropdown({
    Text = "Select Options",
    Options = {"Option 1", "Option 2", "Option 3"},
    Default = {"Option 1"}, -- Can be a table for multi-select
    MultiSelect = true,
    Callback = function(options)
        print("Selected options:", table.concat(options, ", "))
    end
})
```

#### Text Input

```lua
local input = generalSection:CreateInput({
    Text = "Username",
    Tooltip = "Enter your username",
    Placeholder = "Type here...",
    Default = "",
    ClearOnFocus = true,
    Callback = function(text, enterPressed)
        print("Input:", text, "Enter pressed:", enterPressed)
    end
})
```

#### Color Picker

```lua
local colorPicker = visualsSection:CreateColorPicker({
    Text = "ESP Color",
    Tooltip = "Choose the ESP color",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(color)
        print("Selected color:", color)
    end
})
```

#### Key Bind

```lua
local keyBind = settingsTab:CreateKeyBind({
    Text = "Toggle UI",
    Tooltip = "Set the key to toggle the UI",
    Default = Enum.KeyCode.RightShift,
    AllowMouse = true, -- Allow mouse buttons
    Callback = function(key)
        print("Key set to:", key.Name)
    end
})
```

#### Label

```lua
local label = generalSection:CreateLabel({
    Text = "Welcome to <font color='rgb(88, 101, 242)'>CryzenHub</font> v1.2.0!",
    Tooltip = "Rich text is supported",
    Centered = true,
    TextColor = Color3.fromRGB(255, 255, 255)
})
```

#### Progress Bar

```lua
local progressBar = generalSection:CreateProgressBar({
    Text = "Loading...",
    Tooltip = "Shows the loading progress",
    Min = 0,
    Max = 100,
    Value = 50,
    Color = Color3.fromRGB(67, 181, 129),
    Unit = "%",
    Callback = function(value)
        print("Progress:", value)
    end
})

-- Update progress with animation
progressBar:Set(75, true)
```

#### Image

```lua
local image = visualsSection:CreateImage({
    Image = "rbxassetid://7072718362",
    Tooltip = "Click to enlarge",
    Size = UDim2.new(1, 0, 0, 100),
    AspectRatio = 16/9,
    Callback = function()
        print("Image clicked")
    end
})
```

### Notifications

```lua
window:Notify({
    Title = "Notification Title",
    Content = "This is a notification message with a longer text that might wrap to multiple lines.",
    Duration = 5, -- Seconds
    Type = "Info", -- "Success", "Warning", "Error", "Info"
    Buttons = { -- Optional buttons
        {
            Text = "Confirm",
            Primary = true, -- Uses accent color
            Callback = function()
                print("Confirmed")
            end
        },
        {
            Text = "Cancel",
            Callback = function()
                print("Canceled")
            end
        }
    }
})
```

### Context Menus

```lua
window:ShowContextMenu(
    {X = mouse.X, Y = mouse.Y}, -- Position
    {
        {
            Text = "Copy Text",
            Icon = "rbxassetid://7733774602", -- Optional icon
            Callback = function()
                setclipboard("Text copied!")
            end
        },
        {
            Text = "Reset Settings",
            Callback = function()
                -- Reset logic here
            end
        },
        {
            Text = "Disabled Option",
            Disabled = true -- Disabled option
        }
    }
)
```

### Configuration System

```lua
-- Save the current configuration
SaveConfigButton.MouseButton1Click:Connect(function()
    local configName = "MyConfig"
    -- The library automatically collects all element states
    -- You can access this through the window API
})

-- Load a saved configuration
LoadConfigButton.MouseButton1Click:Connect(function()
    local configName = "MyConfig"
    -- The library handles loading and applying the configuration
})
```

## Advanced Usage

### Window Control

```lua
-- Change the window size
window:SetSize(UDim2.new(0, 700, 0, 500))

-- Change the window position
window:SetPosition(UDim2.new(0.5, 0, 0.5, 0))

-- Minimize the window
window:Minimize(true)

-- Hide/show the window
window:Hide()
window:Show()

-- Change theme
window:ChangeTheme("Dark")
```

### Handling UI State

The library automatically saves:
- Window position and size
- Minimized state
- Selected theme
- Element states (toggles, sliders, etc.)

This data persists between sessions if SaveConfig is enabled.

## Comprehensive Example

```lua
local CryzenHub = loadstring(game:HttpGet('https://raw.githubusercontent.com/YourUsername/CryzenHub/main/Source.lua'))()

-- Create key system
local keySystem = CryzenHub:CreateKeySystem({
    Title = "My Amazing Script",
    Subtitle = "Key System",
    Logo = "rbxassetid://7733765398",
    Note = "Enter your key to access the script. Get a key at discord.gg/example",
    KeyLinkURL = "https://example.com/getkey",
    AutoLogin = true,
    KeyData = {
        verificationMethod = "offline",
        keys = {
            {key = "EXAMPLE-KEY-123", expiresAt = os.time() + 86400}
        },
        webhookURL = "https://discord.com/api/webhooks/your-webhook-url",
    }
})

-- Once authenticated, create the main UI
local window = CryzenHub:CreateWindow({
    Title = "My Amazing Script v1.0",
    Size = UDim2.new(0, 600, 0, 400),
    Theme = "Default",
    DefaultTab = "Main",
    TabBarMode = false,
    AutoScale = true,
    SaveConfig = true,
    WindowName = "MyScript",
    WindowShape = "Rounded",
    UseKeySystem = true
})

-- Create tabs
local mainTab = window:CreateTab("Main", "rbxassetid://7733765398")
local visualsTab = window:CreateTab("Visuals", "rbxassetid://7733774602")
local settingsTab = window:CreateTab("Settings", "rbxassetid://7072721682")

-- Create sections
local generalSection = mainTab:CreateSection("General")
local characterSection = mainTab:CreateSection("Character")
local visualsSection = visualsTab:CreateSection("ESP Settings")
local configSection = settingsTab:CreateSection("Configuration")
local creditSection = settingsTab:CreateSection("Credits")

-- General section elements
generalSection:CreateLabel({
    Text = "Welcome to <font color='rgb(88, 101, 242)'>My Amazing Script</font>!",
    Centered = true
})

generalSection:CreateButton({
    Text = "Start Script",
    Tooltip = "Initializes the main functionality",
    Callback = function()
        window:Notify({
            Title = "Script Started",
            Content = "The script has been initialized successfully!",
            Type = "Success"
        })
    end
})

local autoFarm = generalSection:CreateToggle({
    Text = "Auto Farm",
    Tooltip = "Automatically farms resources",
    Default = false,
    Callback = function(state)
        print("Auto Farm:", state)
    end
})

-- Character section elements
local walkspeedSlider = characterSection:CreateSlider({
    Text = "Walk Speed",
    Tooltip = "Adjust your character's walk speed",
    Min = 16,
    Max = 100,
    Default = 16,
    Unit = " studs/s",
    Callback = function(value)
        if game.Players.LocalPlayer.Character then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
        end
    end
})

local jumpPowerSlider = characterSection:CreateSlider({
    Text = "Jump Power",
    Tooltip = "Adjust your character's jump height",
    Min = 50,
    Max = 200,
    Default = 50,
    Unit = " studs",
    Callback = function(value)
        if game.Players.LocalPlayer.Character then
            game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
        end
    end
})

-- Create a grid for character mods (2 columns)
local characterMods = characterSection:CreateGridLayout(2)

-- Add elements to the grid
local noClip = characterSection:CreateToggle({
    Text = "No-Clip",
    Parent = characterMods,
    Callback = function(state)
        print("No-Clip:", state)
    end
})

local infiniteJump = characterSection:CreateToggle({
    Text = "Infinite Jump",
    Parent = characterMods,
    Callback = function(state)
        print("Infinite Jump:", state)
    end
})

local godMode = characterSection:CreateToggle({
    Text = "God Mode",
    Parent = characterMods,
    Callback = function(state)
        print("God Mode:", state)
    end
})

local invisibility = characterSection:CreateToggle({
    Text = "Invisibility",
    Parent = characterMods,
    Callback = function(state)
        print("Invisibility:", state)
    end
})

-- Visuals section elements
local espEnabled = visualsSection:CreateToggle({
    Text = "Enable ESP",
    Default = false,
    Callback = function(state)
        print("ESP:", state)
    end
})

local espColor = visualsSection:CreateColorPicker({
    Text = "ESP Color",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(color)
        print("ESP Color:", color)
    end
})

local espOptions = visualsSection:CreateDropdown({
    Text = "ESP Features",
    Options = {"Names", "Boxes", "Health", "Distance", "Tracers"},
    MultiSelect = true,
    Default = {"Names", "Boxes"},
    Callback = function(selected)
        print("ESP Features:", table.concat(selected, ", "))
    end
})

-- Config section elements
local configDropdown = configSection:CreateDropdown({
    Text = "Config",
    Options = listConfigs() or {"Default"}, -- Function from the library
    Default = "Default",
    Callback = function(config)
        print("Selected config:", config)
    end
})

local saveConfigButton = configSection:CreateButton({
    Text = "Save Config",
    Callback = function()
        -- Library handles the dialog and saving process
        print("Config saved")
    end
})

local loadConfigButton = configSection:CreateButton({
    Text = "Load Config",
    Callback = function()
        -- Library handles the dialog and loading process
        print("Config loaded")
    end
})

-- Theme selector
local themeDropdown = configSection:CreateDropdown({
    Text = "Theme",
    Options = {"Default", "Light", "Dark", "Oceanic", "Midnight"},
    Default = "Default",
    Callback = function(theme)
        window:ChangeTheme(theme)
    end
})

-- Keybind for toggling UI
local uiToggle = configSection:CreateKeyBind({
    Text = "Toggle UI",
    Default = Enum.KeyCode.RightShift,
    Callback = function(key)
        print("UI Toggle Key:", key.Name)
    end
})

-- Credits section
creditSection:CreateLabel({
    Text = "Created by: YourName",
    Centered = true
})

creditSection:CreateLabel({
    Text = "UI Library: CryzenHub v1.2.0",
    Centered = true
})

creditSection:CreateButton({
    Text = "Join Discord",
    Callback = function()
        setclipboard("https://discord.gg/example")
        window:Notify({
            Title = "Discord Invite",
            Content = "Discord invite copied to clipboard!",
            Type = "Info",
            Duration = 3
        })
    end
})

-- Setup context menu for the window
UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 then
        window:ShowContextMenu(
            {X = input.Position.X, Y = input.Position.Y},
            {
                {
                    Text = "Copy Script Version",
                    Icon = "rbxassetid://7733774602",
                    Callback = function()
                        setclipboard("v1.0")
                        window:Notify({
                            Title = "Copied",
                            Content = "Script version copied to clipboard",
                            Type = "Success",
                            Duration = 2
                        })
                    end
                },
                {
                    Text = "Reset All Settings",
                    Icon = "rbxassetid://7072714839",
                    Callback = function()
                        window:Notify({
                            Title = "Reset Settings",
                            Content = "Are you sure you want to reset all settings?",
                            Type = "Warning",
                            Buttons = {
                                {
                                    Text = "Yes",
                                    Primary = true,
                                    Callback = function()
                                        -- Reset logic here
                                        print("Settings reset")
                                    end
                                },
                                {
                                    Text = "No"
                                }
                            }
                        })
                    end
                }
            }
        )
    end
end)

-- Show a welcome notification
window:Notify({
    Title = "Welcome!",
    Content = "Thanks for using My Amazing Script. If you have any questions, join our Discord server.",
    Type = "Info",
    Duration = 5
})
```

## Mobile Support

CryzenHub v1.2.0 includes enhanced mobile support:

- Touch-friendly UI elements with appropriate sizing
- Adaptive layouts that work well on phones and tablets
- Haptic feedback for interactions
- Responsive design that scales based on screen size
- Mobile-friendly buttons and controls

## Security Features

The key system includes several security measures:

- Hardware ID binding to prevent key sharing
- User ID binding for user-specific keys
- Key expiration timestamps
- Encrypted key verification
- Rate limiting (when using online verification)
- Discord webhook logging for monitoring key usage

## License

This library is free to use for any purpose. Credit is appreciated but not required.

## Credits

Created by CryzenHub Team - v1.2.0
```

In this v1.2.0 update, I've implemented a comprehensive key system with multiple verification methods (online API, offline predefined keys, and linkvertise key generation). The key system includes features like hardware ID binding, auto-login support, and webhook integration for logging key usage to Discord.

The UI has been enhanced with configuration saving/loading capabilities, UI state persistence between sessions, customizable window shapes, UI sounds with haptic feedback for mobile devices, and various new UI elements including progress bars and image elements.

I've also improved the mobile support with better touch controls, adaptive layouts, and haptic feedback. The performance has been optimized with element pooling and memory usage improvements.