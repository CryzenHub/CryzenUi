# CryzenHub UI Library v2.0.0

A premium UI library for Roblox scripts with a completely redesigned modern interface, enhanced features, and improved performance.

![CryzenHub v2.0.0 Banner](https://i.imgur.com/placeholder.png)

## What's New in v2.0.0

- **Complete Redesign**: Modern, sleek interface with a premium look and feel
- **Enhanced Performance**: Optimized rendering and interaction handling
- **Acrylic Effect**: Beautiful blur effect for a premium glass-like appearance
- **Improved Animations**: Smoother transitions and visual feedback
- **Gradient Support**: Customizable gradient backgrounds for UI elements
- **Advanced Color Picker**: More precise color selection with RGB inputs
- **Multi-Select Dropdowns**: Select multiple items from dropdowns
- **Improved Notifications**: Different notification types with icons
- **Section Management**: Collapsible sections for better organization
- **Flag System**: Easy value tracking across your UI
- **Config System**: Comprehensive save/load functionality
- **Tooltips**: Helpful hover tooltips for UI elements
- **Rich Search**: Find elements quickly with the built-in search functionality

## Installation

```lua
local CryzenHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/CryzenHub/CryzenUi/refs/heads/main/Source"))()
```

## Basic Usage

```lua
-- Create a window
local Window = CryzenHub:CreateWindow({
    Title = "CryzenHub Example",
    Theme = {
        Primary = Color3.fromRGB(20, 20, 30),
        Accent = Color3.fromRGB(100, 120, 255),
        TextSize = 14
    }
})

-- Create tabs with icons
local MainTab = Window:Tab("Main", "rbxassetid://7059346373")
local SettingsTab = Window:Tab("Settings", "rbxassetid://7059394039")

-- Create sections
local FeaturesSection = MainTab:Section("Features")
local VisualsSection = MainTab:Section("Visuals")
local ConfigSection = SettingsTab:Section("Configuration")

-- Add elements to sections
FeaturesSection:Label("Welcome to CryzenHub v2.0.0")

FeaturesSection:Button("Click Me", function()
    Window:Notify({
        Title = "Button Clicked",
        Message = "You clicked the button!",
        Duration = 3,
        Type = "Success"
    })
end)

local speedToggle = FeaturesSection:Toggle("Speed Hack", {
    Default = false,
    Flag = "SpeedEnabled"
}, function(value)
    print("Speed Hack:", value)
end)

local speedSlider = FeaturesSection:Slider("Speed Multiplier", {
    Min = 1,
    Max = 10,
    Default = 2,
    Decimals = 1,
    Suffix = "x",
    Flag = "SpeedMultiplier"
}, function(value)
    print("Speed multiplier set to:", value)
end)

local dropdown = FeaturesSection:Dropdown("Target", {
    Items = {"All Players", "Enemies", "Friends"},
    Default = "Enemies",
    Flag = "TargetOption"
}, function(selected)
    print("Target selected:", selected)
end)

local multiDropdown = FeaturesSection:Dropdown("Weapons", {
    Items = {"Assault Rifle", "Shotgun", "Sniper", "Pistol", "Knife"},
    MultiSelect = true,
    Default = {"Assault Rifle", "Pistol"},
    Flag = "SelectedWeapons"
}, function(selected)
    print("Weapons selected:", table.concat(selected, ", "))
end)

VisualsSection:Checkbox("ESP", true, function(value)
    print("ESP enabled:", value)
end)

local espColor = VisualsSection:ColorPicker("ESP Color", {
    Default = Color3.fromRGB(255, 0, 0),
    Flag = "ESPColor"
}, function(color)
    print("ESP color set to:", color)
end)

VisualsSection:Divider()

VisualsSection:Keybind("Toggle ESP", {
    Default = Enum.KeyCode.E,
    Flag = "ESPKeybind"
}, function(key)
    print("ESP toggled with key:", key.Name)
end)

VisualsSection:Textbox("Player Name", {
    Placeholder = "Enter player name...",
    ClearOnFocus = false,
    Flag = "TargetPlayer"
}, function(text)
    print("Player name set to:", text)
end)

-- Configuration section
ConfigSection:Label("Save and Load Configurations")

ConfigSection:Textbox("Config Name", {
    Placeholder = "Enter config name...",
    Default = "MyConfig"
}, function(text)
    -- Config name is stored for saving/loading
    ConfigName = text
end)

ConfigSection:Button("Save Config", function()
    local success = Window:SaveConfig(ConfigName or "Default")
    
    Window:Notify({
        Title = success and "Success" or "Error",
        Message = success and "Configuration saved!" or "Failed to save configuration",
        Type = success and "Success" or "Error"
    })
end)

ConfigSection:Button("Load Config", function()
    local success = Window:LoadConfig(ConfigName or "Default")
    
    Window:Notify({
        Title = success and "Success" or "Error",
        Message = success and "Configuration loaded!" or "Failed to load configuration",
        Type = success and "Success" or "Error"
    })
end)
```

## API Reference

### CryzenHub

#### `CryzenHub:CreateWindow(options)`
Creates a main window for your UI.
- `options`: Table with window configuration:
  - `Title`: Window title
  - `Theme`: Custom theme settings
  - `Size`: Window size (UDim2)
  - `Position`: Window position (UDim2)
  - `MinSize`: Minimum window size (Vector2)
- Returns: Window object

### Window

#### `Window:Tab(name, icon)`
Creates a new tab in the window.
- `name`: The name of the tab
- `icon`: (Optional) Asset ID for the tab icon
- Returns: Tab object

#### `Window:Notify(options)`
Shows a notification.
- `options`: Table with notification options:
  - `Title`: The title of the notification
  - `Message`: The notification content
  - `Duration`: How long to display the notification (in seconds)
  - `Type`: "Info", "Success", "Warning", or "Error"
- Returns: Notification object

#### `Window:SaveConfig(name)`
Saves the current UI configuration.
- `name`: Name to save the config under
- Returns: Success status and config data

#### `Window:LoadConfig(nameOrData)`
Loads a UI configuration.
- `nameOrData`: Name of the config to load or config data table
- Returns: Success status

#### `Window:SelectTab(tab)`
Selects a specific tab.
- `tab`: The tab object to select

#### `Window:GetElementByFlag(flag)`
Gets an element by its flag.
- `flag`: The flag name
- Returns: Element object if found, nil otherwise

### Tab

#### `Tab:Section(title)`
Creates a section within a tab.
- `title`: The title of the section
- Returns: Section object

### Section

#### `Section:Label(text, options)`
Creates a text label.
- `text`: The text to display (supports rich text)
- `options`: Additional options:
  - `Color`: Text color
  - `TextSize`: Font size
  - `Height`: Label height
  - `TextXAlignment`: Text alignment
- Returns: Label element

#### `Section:Button(text, callback, options)`
Creates a clickable button.
- `text`: Text displayed on the button
- `callback`: Function called when button is clicked
- `options`: Additional options:
  - `Flag`: Identifier for the element
- Returns: Button element

#### `Section:Toggle(text, options, callback)`
Creates a toggle switch.
- `text`: Text displayed next to the toggle
- `options`: Toggle options:
  - `Default`: Initial state (true/false)
  - `Flag`: Identifier for the element
- `callback`: Function called when toggle changes state
- Returns: Toggle element

#### `Section:Slider(text, options, callback)`
Creates a value slider.
- `text`: Text displayed above the slider
- `options`: Slider options:
  - `Min`: Minimum value
  - `Max`: Maximum value
  - `Default`: Initial value
  - `Decimals`: Number of decimal places
  - `Suffix`: Text to display after the value
  - `Flag`: Identifier for the element
- `callback`: Function called when slider value changes
- Returns: Slider element

#### `Section:Dropdown(text, options, callback)`
Creates a dropdown selector.
- `text`: Text displayed above the dropdown
- `options`: Dropdown options:
  - `Items`: Array of selectable items
  - `Default`: Initially selected item(s)
  - `MultiSelect`: Allow selecting multiple items
  - `Flag`: Identifier for the element
- `callback`: Function called when selection changes
- Returns: Dropdown element

#### `Section:Textbox(text, options, callback)`
Creates a text input field.
- `text`: Text displayed above the textbox
- `options`: Textbox options:
  - `Default`: Initial text
  - `Placeholder`: Placeholder text when empty
  - `ClearOnFocus`: Whether to clear text when focused
  - `Flag`: Identifier for the element
- `callback`: Function called when text is submitted
- Returns: Textbox element

#### `Section:ColorPicker(text, options, callback)`
Creates a color picker.
- `text`: Text displayed next to the color display
- `options`: ColorPicker options:
  - `Default`: Initial color (Color3)
  - `Flag`: Identifier for the element
- `callback`: Function called when color changes
- Returns: ColorPicker element

#### `Section:Keybind(text, options, callback)`
Creates a keybind input element.
- `text`: Text displayed next to the keybind
- `options`: Keybind options:
  - `Default`: Initial key (Enum.KeyCode)
  - `Flag`: Identifier for the element
- `callback`: Function called when keybind is pressed
- Returns: Keybind element

#### `Section:Checkbox(text, default, callback, options)`
Creates a checkbox element.
- `text`: Text displayed next to the checkbox
- `default`: Initial state (true/false)
- `callback`: Function called when checkbox changes state
- `options`: Additional options:
  - `Flag`: Identifier for the element
- Returns: Checkbox element

#### `Section:Divider(options)`
Creates a horizontal divider line.
- `options`: Divider options:
  - `Color`: Line color
  - `Transparency`: Line transparency
- Returns: Divider element

### Element Common Methods

Most elements share these common methods:

#### `Element:Update(value)`
Updates the element's value.
- `value`: The new value for the element

#### `Element:SetValue(value)`
Sets the element's value (same as Update).
- `value`: The new value for the element

### Dropdown-Specific Methods

#### `Dropdown:AddItem(item)`
Adds an item to the dropdown.
- `item`: The item to add

#### `Dropdown:RemoveItem(item)`
Removes an item from the dropdown.
- `item`: The item to remove

#### `Dropdown:Clear()`
Clears all items from the dropdown.

### Slider-Specific Methods

#### `Slider:SetMinMax(min, max)`
Changes the slider's minimum and maximum values.
- `min`: New minimum value
- `max`: New maximum value

## Customizing Themes

You can customize the UI appearance by providing theme options when creating a window:

```lua
local Window = CryzenHub:CreateWindow({
    Title = "Custom Theme Example",
    Theme = {
        -- Main colors
        Primary = Color3.fromRGB(20, 20, 30),      -- Main background
        Secondary = Color3.fromRGB(30, 30, 40),    -- Secondary background
        Tertiary = Color3.fromRGB(40, 40, 55),     -- Input fields
        Accent = Color3.fromRGB(100, 120, 255),    -- Accent color
        
        -- Text colors
        Text = Color3.fromRGB(240, 240, 255),      -- Primary text
        TextDark = Color3.fromRGB(180, 180, 195),  -- Secondary text
        
        -- Border colors
        Stroke = Color3.fromRGB(60, 60, 80),       -- Border color
        
        -- Status colors
        Success = Color3.fromRGB(70, 200, 120),    -- Success color
        Warning = Color3.fromRGB(255, 180, 70),    -- Warning color
        Error = Color3.fromRGB(255, 80, 80),       -- Error color
        Info = Color3.fromRGB(70, 160, 255),       -- Info color
        
        -- Typography
        Font = Enum.Font.Gotham,                   -- UI font
        HeaderSize = 18,                           -- Header text size
        TextSize = 14,                             -- Normal text size
        SubTextSize = 12,                          -- Smaller text size
        
        -- Effects
        Blur = true,                               -- Enable background blur
        BlurSize = 10,                             -- Blur intensity
        UseAcrylic = true,                         -- Enable acrylic effect
        EnableShadows = true,                      -- Enable drop shadows
        UseGradients = true                        -- Enable gradient backgrounds
    }
})
```

## Examples

### Player List with Multi-Select Dropdown

```lua
local PlayersTab = Window:Tab("Players", "rbxassetid://7072717958")
local PlayersSection = PlayersTab:Section("Player Selection")

-- Get all player names
local function GetAllPlayers()
    local playerNames = {}
    for _, player in pairs(game.Players:GetPlayers()) do
        table.insert(playerNames, player.Name)
    end
    return playerNames
end

-- Create multi-select dropdown for players
local selectedPlayers = PlayersSection:Dropdown("Select Players", {
    Items = GetAllPlayers(),
    MultiSelect = true,
    Flag = "SelectedPlayers"
}, function(selected)
    print("Selected players:", table.concat(selected, ", "))
end)

-- Refresh player list button
PlayersSection:Button("Refresh Player List", function()
    selectedPlayers:Update(GetAllPlayers())
    Window:Notify({
        Title = "Players Refreshed",
        Message = "Player list has been updated",
        Type = "Info"
    })
end)

-- Action buttons for selected players
PlayersSection:Button("Teleport to Selected", function()
    local selected = Window.Flags.SelectedPlayers
    if #selected == 0 then
        Window:Notify({
            Title = "No Selection",
            Message = "No players selected",
            Type = "Warning"
        })
        return
    end
    
    for _, playerName in ipairs(selected) do
        local player = game.Players:FindFirstChild(playerName)
        if player and player.Character then
            game.Players.LocalPlayer.Character:SetPrimaryPartCFrame(
                player.Character:GetPrimaryPartCFrame()
            )
            break -- Teleport to the first valid player
        end
    end
end)

-- Update when players join/leave
game.Players.PlayerAdded:Connect(function()
    selectedPlayers:Update(GetAllPlayers())
end)

game.Players.PlayerRemoving:Connect(function()
    selectedPlayers:Update(GetAllPlayers())
end)
```

### ESP Configuration with Color Picker

```lua
local VisualsTab = Window:Tab("Visuals", "rbxassetid://7072706108")
local ESPSection = VisualsTab:Section("ESP Settings")

-- ESP toggle
local espEnabled = ESPSection:Toggle("Enable ESP", {
    Default = false,
    Flag = "ESPEnabled"
}, function(value)
    -- ESP toggle logic here
end)

-- ESP options
ESPSection:Checkbox("Show Names", true, function(value)
    -- Names ESP logic
end)

ESPSection:Checkbox("Show Boxes", true, function(value)
    -- Box ESP logic
end)

ESPSection:Checkbox("Show Health", false, function(value)
    -- Health ESP logic
end)

ESPSection:Checkbox("Show Distance", true, function(value)
    -- Distance ESP logic
end)

-- ESP colors
local teamColorToggle = ESPSection:Toggle("Use Team Colors", {
    Default = true,
    Flag = "UseTeamColors"
}, function(value)
    -- Team color logic
end)

local espColor = ESPSection:ColorPicker("ESP Color", {
    Default = Color3.fromRGB(255, 0, 0),
    Flag = "ESPColor"
}, function(color)
    -- Color update logic
end)

-- ESP distance
local espDistance = ESPSection:Slider("ESP Distance", {
    Min = 50,
    Max = 5000,
    Default = 1000,
    Suffix = " studs"
}, function(value)
    -- Update ESP distance logic
end)

-- ESP keybind
ESPSection:Keybind("Toggle ESP", {
    Default = Enum.KeyCode.E,
    Flag = "ESPKeybind"
}, function()
    local newValue = not Window.Flags.ESPEnabled
    espEnabled:SetValue(newValue)
})

-- ESP target selection
ESPSection:Dropdown("ESP Targets", {
    Items = {"All Players", "Enemies", "Team", "Friends"},
    Default = "Enemies",
    Flag = "ESPTargets"
}, function(selected)
    -- Target selection logic
end)
```

### Configuration System

```lua
local SettingsTab = Window:Tab("Settings", "rbxassetid://7059394039")
local ConfigSection = SettingsTab:Section("Configuration")

local configName = "Default"

-- Config name input
ConfigSection:Textbox("Config Name", {
    Default = configName,
    Placeholder = "Enter config name..."
}, function(text)
    configName = text
end)

-- Save config
ConfigSection:Button("Save Configuration", function()
    local success, data = Window:SaveConfig(configName)
    
    if success then
        Window:Notify({
            Title = "Configuration Saved",
            Message = "Successfully saved as: " .. configName,
            Type = "Success"
        })
    else
        Window:Notify({
            Title = "Save Failed",
            Message = "Could not save configuration. Make sure your exploit supports file writing.",
            Type = "Error"
        })
    end
end)

-- Load config
ConfigSection:Button("Load Configuration", function()
    local success = Window:LoadConfig(configName)
    
    if success then
        Window:Notify({
            Title = "Configuration Loaded",
            Message = "Successfully loaded: " .. configName,
            Type = "Success"
        })
    else
        Window:Notify({
            Title = "Load Failed",
            Message = "Could not load configuration. The file may not exist.",
            Type = "Error"
        })
    end
end)

-- List available configs (if supported)
if listfiles then
    local configs = {}
    
    -- Refresh config list
    local function RefreshConfigs()
        configs = {}
        for _, file in ipairs(listfiles("")) do
            if file:match("CryzenHub_(.+)%.json") then
                local name = file:match("CryzenHub_(.+)%.json")
                table.insert(configs, name)
            end
        end
        return configs
    end
    
    -- Create dropdown with available configs
    local configDropdown = ConfigSection:Dropdown("Available Configs", {
        Items = RefreshConfigs(),
        Flag = "SelectedConfig"
    }, function(selected)
        configName = selected
    end)
    
    -- Refresh button
    ConfigSection:Button("Refresh Config List", function()
        configDropdown:Update(RefreshConfigs())
        Window:Notify({
            Title = "Config List Refreshed",
            Message = "Found " .. #configs .. " configurations",
            Type = "Info"
        })
    end)
end

-- Reset all settings
ConfigSection:Button("Reset All Settings", function()
    -- Prompt confirmation
    local confirmed = false
    
    -- Create a confirmation UI here or use your own method
    -- For this example, we'll just reset without confirmation
    
    -- Reset all values to defaults
    for flag, element in pairs(Window.Elements) do
        if element.SetValue and element.Default ~= nil then
            element:SetValue(element.Default)
        end
    end
    
    Window:Notify({
        Title = "Settings Reset",
        Message = "All settings have been reset to their default values",
        Type = "Info"
    })
end)
```

## License

This UI library is free to use for any purpose. Credit is appreciated but not required.
```

This v2.0.0 update represents a complete overhaul of the CryzenHub UI Library with a modern, premium design aesthetic. The new version includes:

1. A sleeker, more professional UI with acrylic effects and gradients
2. Improved element design with better visual feedback
3. Enhanced organization with collapsible sections
4. Advanced controls like multi-select dropdowns
5. Better notifications with different types and icons
6. Comprehensive configuration system
7. More intuitive tab navigation with icons
8. Improved tooltips and search functionality
9. Better performance through optimized rendering
