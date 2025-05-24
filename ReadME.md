# CryzenHub UI Library v1.2.0

A powerful and feature-rich UI library for Roblox Luau scripts with smooth animations, modern design, and extensive customization options.

## What's New in v1.2.0

- **Acrylic Effect**: Modern blurred background effect for a premium look
- **Window Resizing**: Resize the UI window to your preferred size
- **Enhanced Search**: Global search functionality to find UI elements quickly
- **RGB Color Picker**: More precise color selection with RGB inputs
- **Collapsible Sections**: Organize your UI elements better with collapsible sections
- **Ripple Effects**: Beautiful material design-inspired ripple animations
- **Enhanced Notifications**: Different notification types (info, success, warning, error)
- **Keybind Support**: Add keyboard shortcuts to toggles and other elements
- **Configuration System**: Save and load UI settings
- **Rainbow Mode**: Animated color transitions for accent elements
- **List Element**: New element for managing collections of items
- **Checkbox Element**: Simpler alternative to toggles
- **Rich Text Labels**: Format text with colors and styles

## Installation

```lua
local CryzenHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/CryzenHub/CryzenUi/refs/heads/main/Source"))()
```

## Basic Usage

```lua
-- Load the library
local CryzenHub = loadstring(game:HttpGet("https://raw.githubusercontent.com/CryzenHub/CryzenUi/refs/heads/main/Source"))()

-- Create a window with custom configuration
local Window = CryzenHub:CreateWindow("CryzenHub Example", {
    MainColor = Color3.fromRGB(30, 30, 46),
    AccentColor = Color3.fromRGB(70, 130, 255),
    TextColor = Color3.fromRGB(240, 240, 240),
    Font = Enum.Font.Gotham,
    SmoothDragging = true,
    DefaultToggleKey = Enum.KeyCode.RightShift,
    UseAcrylic = true
})

-- Create tabs
local MainTab = Window:CreateTab("Main", "rbxassetid://6026568198") -- Icon is optional
local SettingsTab = Window:CreateTab("Settings")

-- Create sections
local FeaturesSection = MainTab:CreateSection("Features")
local MiscSection = MainTab:CreateSection("Miscellaneous")
local ConfigSection = SettingsTab:CreateSection("Configuration")

-- Add elements to sections
FeaturesSection:CreateButton("Click Me", function()
    Window:Notify("Button Clicked", "You clicked the button!", {
        type = "success", -- info, success, warning, error
        duration = 3
    })
end)

local toggle = FeaturesSection:CreateToggle("Toggle Feature", false, function(value)
    print("Toggle set to:", value)
end)

local slider = FeaturesSection:CreateSlider("Speed", 0, 100, 50, function(value)
    print("Slider value:", value)
end, {
    format = "%.1f", -- Custom format
    suffix = " studs/s" -- Add a unit
})

local dropdown = MiscSection:CreateDropdown("Select Option", {"Option 1", "Option 2", "Option 3"}, "Option 1", function(selected)
    print("Selected:", selected)
end)

local textbox = MiscSection:CreateTextbox("Enter Name", "Your name here...", function(text)
    print("Entered text:", text)
end)

local colorpicker = ConfigSection:CreateColorPicker("UI Color", Color3.fromRGB(255, 0, 0), function(color)
    print("Selected color:", color)
end)

local keybind = ConfigSection:CreateKeybind("Toggle UI", Enum.KeyCode.RightControl, function(key)
    print("Keybind pressed:", key.Name)
end)

local checkbox = ConfigSection:CreateCheckbox("Enable Feature", true, function(checked)
    print("Checkbox value:", checked)
end)

local list = ConfigSection:CreateList("Player Whitelist", {"Player1", "Player2"}, function(items)
    print("List updated:", table.concat(items, ", "))
end)

local label = ConfigSection:CreateLabel("<font color='rgb(70, 130, 255)'>Rich</font> <b>Text</b> <i>Support!</i>", {
    TextSize = 18,
    TextXAlignment = Enum.TextXAlignment.Center
})

-- Use theme presets
Window:SetTheme("Midnight") -- Available: Dark, Light, Discord, Midnight, Aqua

-- Save and load configurations
Window:SaveConfig("MyConfig")
Window:LoadConfig("MyConfig")

-- Enable rainbow mode
Window:SetRainbowMode(true)
```

## API Reference

### CryzenHub

#### `CryzenHub:CreateWindow(title, config)`
Creates a main window for your UI.
- `title`: The title displayed at the top of the window
- `config`: (Optional) Table with configuration options
- Returns: Window object

### Window

#### `Window:CreateTab(tabName, icon)`
Creates a new tab in the window.
- `tabName`: The name of the tab
- `icon`: (Optional) Asset ID for the tab icon
- Returns: Tab object

#### `Window:Notify(title, text, options)`
Shows a notification.
- `title`: Title of the notification
- `text`: Main text content
- `options`: Table with notification options:
  - `type`: "info", "success", "warning", "error"
  - `duration`: How long the notification stays visible (in seconds)
  - `position`: "bottom-right", "bottom-left", "top-right", "top-left"
  - `callback`: Function called when notification is closed
- Returns: Notification object

#### `Window:SetTheme(theme)`
Customizes the UI theme.
- `theme`: Either a preset name or a table with theme properties
  - Presets: "Dark", "Light", "Discord", "Midnight", "Aqua"
  - Custom: {MainColor, SecondaryColor, AccentColor, TextColor, Font}

#### `Window:SaveConfig(configName)`
Saves the current UI configuration.
- `configName`: Name to save the config under
- Returns: Configuration data or true if saved to file

#### `Window:LoadConfig(configName)`
Loads a UI configuration.
- `configName`: Name of the config to load, or a config table
- Returns: true if loaded successfully

#### `Window:SetRainbowMode(enabled)`
Enables or disables rainbow mode for accent colors.
- `enabled`: true to enable, false to disable

#### `Window:SetToggleKey(keyCode)`
Changes the key used to toggle the UI's visibility.
- `keyCode`: The Enum.KeyCode to use

### Tab

#### `Tab:CreateSection(sectionName)`
Creates a section within a tab.
- `sectionName`: The title of the section
- Returns: Section object

### Section

#### `Section:CreateButton(buttonText, callback)`
Creates a clickable button.
- `buttonText`: Text displayed on the button
- `callback`: Function called when button is clicked
- Returns: Button object

#### `Section:CreateToggle(toggleText, default, callback)`
Creates a toggle switch.
- `toggleText`: Text displayed next to the toggle
- `default`: Initial state (true/false)
- `callback`: Function called when toggle changes state
- Returns: Toggle object with SetValue(), GetValue(), SetKeybind(), GetKeybind() methods

#### `Section:CreateSlider(sliderText, min, max, default, callback, options)`
Creates a value slider.
- `sliderText`: Text displayed above the slider
- `min`: Minimum value
- `max`: Maximum value
- `default`: Initial value
- `callback`: Function called when slider value changes
- `options`: Table with additional options (format, prefix, suffix, decimal)
- Returns: Slider object with SetValue(), GetValue(), SetRange() methods

#### `Section:CreateDropdown(dropdownText, options, default, callback)`
Creates a dropdown selector with search.
- `dropdownText`: Text displayed above the dropdown
- `options`: Array of options
- `default`: Initially selected option
- `callback`: Function called when selection changes
- Returns: Dropdown object with SetValue(), GetValue(), Refresh() methods

#### `Section:CreateTextbox(boxText, placeholderText, callback, defaultText)`
Creates a text input field.
- `boxText`: Text displayed above the textbox
- `placeholderText`: Placeholder text when textbox is empty
- `callback`: Function called when text is submitted
- `defaultText`: Initial text in the textbox
- Returns: Textbox object with SetValue(), GetValue() methods

#### `Section:CreateLabel(labelText, options)`
Creates a text label with rich text support.
- `labelText`: Text to display (supports HTML-like tags)
- `options`: Table with label options (TextColor, TextSize, TextXAlignment)
- Returns: Label object with SetText(), SetColor() methods

#### `Section:CreateColorPicker(pickerText, default, callback)`
Creates a color picker with RGB inputs.
- `pickerText`: Text displayed next to the color display
- `default`: Initial color (Color3 value)
- `callback`: Function called when color changes
- Returns: ColorPicker object with SetValue(), GetValue() methods

#### `Section:CreateKeybind(bindText, defaultKey, callback)`
Creates a keybind input element.
- `bindText`: Text displayed next to the keybind
- `defaultKey`: Initial key (Enum.KeyCode)
- `callback`: Function called when keybind is pressed
- Returns: Keybind object with SetValue(), GetValue() methods

#### `Section:CreateCheckbox(checkText, default, callback)`
Creates a checkbox element.
- `checkText`: Text displayed next to the checkbox
- `default`: Initial state (true/false)
- `callback`: Function called when checkbox changes state
- Returns: Checkbox object with SetValue(), GetValue() methods

#### `Section:CreateList(listText, defaultItems, callback, options)`
Creates a list element with add/remove functionality.
- `listText`: Text displayed above the list
- `defaultItems`: Initial list items
- `callback`: Function called when list changes
- `options`: Additional options for the list
- Returns: List object with SetItems(), GetItems(), AddItem(), RemoveItem(), Clear() methods

## Examples

### Creating a player selector with the list element

```lua
local PlayersTab = Window:CreateTab("Players")
local PlayerSection = PlayersTab:CreateSection("Player Selection")

-- Get all player names
local playerNames = {}
for _, player in pairs(game.Players:GetPlayers()) do
    table.insert(playerNames, player.Name)
end

-- Create dropdown to select players
local playerDropdown = PlayerSection:CreateDropdown("Select Player", playerNames, nil, function(selected)
    Window:Notify("Player Selected", "You selected: " .. selected, {type = "info"})
end)

-- Create a list to track selected players
local selectedPlayers = PlayerSection:CreateList("Selected Players", {}, function(list)
    print("Selected players: " .. table.concat(list, ", "))
end)

-- Button to add selected player to the list
PlayerSection:CreateButton("Add Selected Player", function()
    local selected = playerDropdown:GetValue()
    if selected then
        -- Check if player is already in list
        local items = selectedPlayers:GetItems()
        for _, item in ipairs(items) do
            if item == selected then
                Window:Notify("Already Added", selected .. " is already in your list!", {type = "warning"})
                return
            end
        end
        
        selectedPlayers:AddItem(selected)
        Window:Notify("Player Added", selected .. " added to your list!", {type = "success"})
    end
end)

-- Update player list when players join/leave
game.Players.PlayerAdded:Connect(function(player)
    table.insert(playerNames, player.Name)
    playerDropdown:Refresh(playerNames, true)
end)

game.Players.PlayerRemoving:Connect(function(player)
    for i, name in ipairs(playerNames) do
        if name == player.Name then
            table.remove(playerNames, i)
            break
        end
    end
    playerDropdown:Refresh(playerNames, true)
end)
```

### Creating a theme customizer

```lua
local ThemesTab = Window:CreateTab("Themes")
local ThemeSection = ThemesTab:CreateSection("Theme Customization")

-- Preset themes
local presets = {"Dark", "Light", "Discord", "Midnight", "Aqua"}
ThemeSection:CreateDropdown("Theme Presets", presets, "Dark", function(selected)
    Window:SetTheme(selected)
    Window:Notify("Theme Applied", "Applied the " .. selected .. " theme!", {type = "success"})
end)

-- Custom theme colors
ThemeSection:CreateLabel("Custom Theme Colors")

local mainColor = ThemeSection:CreateColorPicker("Main Color", Config.MainColor, function(color)
    Window:SetTheme({MainColor = color})
end)

local accentColor = ThemeSection:CreateColorPicker("Accent Color", Config.AccentColor, function(color)
    Window:SetTheme({AccentColor = color})
end)

local textColor = ThemeSection:CreateColorPicker("Text Color", Config.TextColor, function(color)
    Window:SetTheme({TextColor = color})
end)

-- Font selection
local fonts = {"Gotham", "GothamBold", "GothamSemibold", "SourceSans", "SourceSansBold", "Arial", "ArialBold"}
local fontEnums = {
    Gotham = Enum.Font.Gotham,
    GothamBold = Enum.Font.GothamBold,
    GothamSemibold = Enum.Font.GothamSemibold,
    SourceSans = Enum.Font.SourceSans,
    SourceSansBold = Enum.Font.SourceSansBold,
    Arial = Enum.Font.Arial,
    ArialBold = Enum.Font.ArialBold
}

ThemeSection:CreateDropdown("Font", fonts, "Gotham", function(selected)
    Window:SetTheme({Font = fontEnums[selected]})
end)

-- Rainbow mode
ThemeSection:CreateToggle("Rainbow Mode", false, function(enabled)
    Window:SetRainbowMode(enabled)
end)

-- Save/load themes
ThemeSection:CreateTextbox("Theme Name", "Enter theme name...", function(text)
    if text and text ~= "" then
        -- Save current theme
        local themeConfig = {
            MainColor = Config.MainColor,
            AccentColor = Config.AccentColor,
            TextColor = Config.TextColor,
            Font = Config.Font
        }
        
        writefile("CryzenHub_Theme_" .. text .. ".json", game:GetService("HttpService"):JSONEncode(themeConfig))
        Window:Notify("Theme Saved", "Saved theme as: " .. text, {type = "success"})
    end
end)

-- Load saved themes
local function refreshThemes()
    if listfiles then
        local themeFiles = {}
        for _, file in ipairs(listfiles("")) do
            if file:match("CryzenHub_Theme_(.+).json") then
                local themeName = file:match("CryzenHub_Theme_(.+).json")
                table.insert(themeFiles, themeName)
            end
        end
        return themeFiles
    end
    return {}
end

local savedThemes = refreshThemes()
local themeDropdown = ThemeSection:CreateDropdown("Saved Themes", savedThemes, nil, function(selected)
    if selected and isfile("CryzenHub_Theme_" .. selected .. ".json") then
        local themeData = game:GetService("HttpService"):JSONDecode(readfile("CryzenHub_Theme_" .. selected .. ".json"))
        Window:SetTheme(themeData)
        Window:Notify("Theme Loaded", "Loaded theme: " .. selected, {type = "success"})
    end
end)

ThemeSection:CreateButton("Refresh Themes", function()
    local themes = refreshThemes()
    themeDropdown:Refresh(themes)
    Window:Notify("Themes Refreshed", "Updated the list of saved themes", {type = "info"})
end)
```

## License

This UI library is free to use for any purpose. Credit is appreciated but not required.
```

The v1.2.0 update adds numerous enhancements to the CryzenHub UI Library, making it more feature-rich and visually appealing. Key improvements include:

1. Acrylic blur effect for a modern look
2. Window resizing capability
3. Global search functionality for UI elements
4. Enhanced color picker with RGB inputs
5. Collapsible sections for better organization
6. Material design ripple effects
7. More notification types and positions
8. Keybind support for elements
9. Configuration save/load system
10. Rainbow mode for accent colors
11. New list element for collections
12. Checkbox element as a toggle alternative
13. Rich text support in labels
