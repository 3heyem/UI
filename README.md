# prodordie UI Library

macOS style UI framework built for matcha.

## Features

- Custom Drawing: Uses the Drawing API for vector rendering and shapes.
- Animations: Smooth transitions for tabs, pills, dropdowns, and buttons.
- Configs: Saves and loads profiles locally in JSON.
- Elements: Toggles, sliders, dropdowns, textboxes, and buttons.
- Search: Global search across tabs and sections.
- Themes: Built-in color themes.

## API Reference

### Window

- prodordie:Tab(name): Makes a new tab.
- prodordie:CreateSettingsTab(customName): Makes the settings tab with themes and config options.
- prodordie:SetMenuTitle(title): Sets the title.
- prodordie:SetMenuSize(vector2): Sets window size.
- prodordie:SetMenuKey(keyName): Changes the toggle key (default f5).
- prodordie:CenterMenu(): Centers the window.
- prodordie:Notification(text, time): Shows a toast alert.
- prodordie:Unload(): Closes everything and removes drawings.

### Elements

#### Toggles
section:Toggle({
    Label = "Toggle Name",
    Value = false,
    Callback = function(v) print(v) end,
    IsNew = false
})

- AddKeybind(key, callback): Binds a hotkey.
- AddColorpicker(label, defaultColor, overwrite, callback): Adds a color picker.

#### Sliders
section:Slider({
    Label = "Slider Name",
    Value = 50,
    Step = 1,
    Min = 0,
    Max = 100,
    Suffix = "%",
    IsNew = false,
    Callback = function(v) print(v) end
})

#### Dropdowns
section:Dropdown({
    Label = "Dropdown Name",
    Value = {"Option 1"},
    Choices = {"Option 1", "Option 2"},
    Multi = false,
    IsNew = false,
    Callback = function(v) print(v) end
})

#### Textboxes
section:Textbox({
    Label = "Textbox Name",
    Value = "Default text",
    Callback = function(v) print(v) end
})

#### Buttons
section:Button({
    Label = "Button Name",
    IsNew = false,
    Callback = function() print("Clicked") end
})

## Render Loop

local RunService = game:GetService("RunService")

local connection
connection = RunService.RenderStepped:Connect(function()
    if prodordie._unloaded then
        connection:Disconnect()
        return
    end
    prodordie:Step()
end)
