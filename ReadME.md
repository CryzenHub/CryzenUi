# CryzenHub UI Library v1.0.0

A simple yet powerful UI library for Roblox scripts.

## Installation

```lua
local CryzenHub = loadstring(game:HttpGet("YOUR_RAW_GITHUB_URL_HERE"))()
```

## Features

- Easy-to-use API for creating professional UIs
- Tab system for organizing your UI elements
- Section containers for grouping related elements
- Various UI elements: buttons, toggles, sliders, dropdowns, textboxes, and more
- Color picker with HSV support
- Notification system
- Theme customization
- Smooth animations and transitions

## Basic Usage

```lua
-- Load the library
local CryzenHub = loadstring(game:HttpGet("YOUR_RAW_GITHUB_URL_HERE"))()

-- Create a window
local Window = CryzenHub:CreateWindow("CryzenHub Example")

-- Create tabs
local MainTab = Window:CreateTab("Main", "rbxassetid://6026568198") -- Icon is optional
local SettingsTab = Window:CreateTab("Settings")

-- Create sections
local FeaturesSection = MainTab:CreateSection("Features")
local MiscSection = MainTab:CreateSection("Miscellaneous")
local ConfigSection = SettingsTab:CreateSection("Configuration")

-- Add elements to sections
FeaturesSection:CreateButton("Click Me", function()
    print("Button clicked!")
end)

local toggle = FeaturesSection:CreateToggle("Toggle Feature", false, function(value)
    print("Toggle set to:", value)
end)

local slider = FeaturesSection:CreateSlider("Speed", 0, 100, 50, function(value)
    print("Slider value:", value)
end)

local dropdown = MiscSection:CreateDropdown("Select Option", {"Option 1", "Option 2", "Option 3"}, "Option 1", function(selected)
    print("Selected:", selected)
end)

local textbox = MiscSection:CreateTextbox("Enter Name", "Your name here...", function(text)
    print("Entered text:", text)
end)

local colorpicker = ConfigSection:CreateColorPicker("UI Color", Color3.fromRGB(255, 0, 0), function(color)
    print("Selected color:", color)
end)

-- Add a notification
Window:Notify("Hello!", "Welcome to CryzenHub UI Library", 5)
```

## API Reference

### CryzenHub

#### `CryzenHub:CreateWindow(title)`
Creates a main window for your UI.
- `title`: The title displayed at the top of the window
- Returns: Window object

### Window

#### `Window:CreateTab(tabName, icon)`
Creates a new tab in the window.
- `tabName`: The name of the tab
- `icon`: (Optional) Asset ID for the tab icon
- Returns: Tab object

#### `Window:Notify(title, text, duration)`
Shows a notification.
- `title`: Title of the notification
- `text`: Main text content
- `duration`: How long the notification stays visible (in seconds)
- Returns: Notification object

#### `Window:SetTheme(theme)`
Customizes the UI theme.
- `theme`: Table with theme properties (MainColor, AccentColor, TextColor, Font)

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
- `callback`: Function called when toggle changes state, receives the new state
- Returns: Toggle object with SetValue() and GetValue() methods

#### `Section:CreateSlider(sliderText, min, max, default, callback)`
Creates a value slider.
- `sliderText`: Text displayed above the slider
- `min`: Minimum value
- `max`: Maximum value
- `default`: Initial value
- `callback`: Function called when slider value changes
- Returns: Slider object with SetValue() and GetValue() methods

#### `Section:CreateDropdown(dropdownText, options, default, callback)`
Creates a dropdown selector.
- `dropdownText`: Text displayed above the dropdown
- `options`: Array of options
- `default`: Initially selected option
- `callback`: Function called when selection changes
- Returns: Dropdown object with SetValue(), GetValue() and Refresh() methods

#### `Section:CreateTextbox(boxText, placeholderText, callback)`
Creates a text input field.
- `boxText`: Text displayed above the textbox
- `placeholderText`: Placeholder text when textbox is empty
- `callback`: Function called when text is submitted (enter key)
- Returns: Textbox object with SetValue() and GetValue() methods

#### `Section:CreateLabel(labelText)`
Creates a text label.
- `labelText`: Text to display
- Returns: Label object with SetText() method

#### `Section:CreateColorPicker(pickerText, default, callback)`
Creates a color picker.
- `pickerText`: Text displayed next to the color display
- `default`: Initial color (Color3 value)
- `callback`: Function called when color changes
- Returns: ColorPicker object with SetValue() and GetValue() methods

## Examples

### Creating a simple ESP script UI

```lua
local CryzenHub = loadstring(game:HttpGet("YOUR_RAW_GITHUB_URL_HERE"))()
local Window = CryzenHub:CreateWindow("CryzenHub ESP")

local ESPTab = Window:CreateTab("ESP")
local ESPSection = ESPTab:CreateSection("ESP Settings")

local espEnabled = ESPSection:CreateToggle("Enable ESP", false, function(value)
    -- ESP toggle logic here
end)

local boxESP = ESPSection:CreateToggle("Box ESP", true, function(value)
    -- Box ESP logic here
end)

local nameESP = ESPSection:CreateToggle("Name ESP", true, function(value)
    -- Name ESP logic here
end)

local distanceESP = ESPSection:CreateToggle("Distance ESP", false, function(value)
    -- Distance ESP logic here
end)

local espDistance = ESPSection:CreateSlider("ESP Distance", 50, 2000, 1000, function(value)
    -- Update ESP distance logic here
end)

local espColor = ESPSection:CreateColorPicker("ESP Color", Color3.fromRGB(255, 0, 0), function(color)
    -- Update ESP color logic here
end)

-- Notification when loaded
Window:Notify("ESP Loaded", "Press Right Shift to toggle the UI", 5)
```

## License

This UI library is free to use for any purpose. Credit is appreciated but not required.
```

This UI library provides a comprehensive set of tools for creating professional-looking user interfaces for Roblox exploits. The code includes a main window system with tabs, sections, and various interactive elements like buttons, toggles, sliders, dropdowns, textboxes, and a color picker.
