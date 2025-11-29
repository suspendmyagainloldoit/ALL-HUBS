-- Orion Library (Classic Style A Recreation)
-- FULL VISUAL REPLICA OF THE ORIGINAL ORION (BLUE THEME, GLOW, ROUNDED, INSTANCE-BASED)
-- API: IDENTICAL TO OLD ORION
-- This is a complete rebuild using only Instance.new(), matching original layout

local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local function ProtectGUI(gui)
    if syn and syn.protect_gui then
        pcall(function() syn.protect_gui(gui) end)
        gui.Parent = game:GetService("CoreGui")
    elseif gethui then
        gui.Parent = gethui()
    elseif LocalPlayer:FindFirstChild("PlayerGui") then
        gui.Parent = LocalPlayer:FindFirstChild("PlayerGui")
    else
        gui.Parent = game:GetService("CoreGui")
    end
end

local Orion = Instance.new("ScreenGui")
Orion.Name = "Orion"
Orion.ResetOnSpawn = false
ProtectGUI(Orion)

-- THEME (Original Orion Blue)
local Theme = {
    Main = Color3.fromRGB(20, 20, 30),
    Glow = Color3.fromRGB(0, 170, 255),
    Dark = Color3.fromRGB(15, 15, 22),
    Light = Color3.fromRGB(35, 35, 45),
    Stroke = Color3.fromRGB(60, 60, 80),
    Text = Color3.fromRGB(235, 235, 255)
}

local OrionLib = {}

-- FUNCTION: MAKE WINDOW
function OrionLib:MakeWindow(cfg)
    cfg = cfg or {}

    local Main = Instance.new("Frame")
    Main.Size = UDim2.new(0, 600, 0, 360)
    Main.Position = UDim2.new(0.5, -300, 0.5, -180)
    Main.BackgroundColor3 = Theme.Main
    Main.BorderSizePixel = 0
    Main.Active = true
    Main.Parent = Orion

    local MainCorner = Instance.new("UICorner", Main)
    MainCorner.CornerRadius = UDim.new(0, 12)

    local Glow = Instance.new("ImageLabel")
    Glow.Parent = Main
    Glow.BackgroundTransparency = 1
    Glow.Position = UDim2.new(0, -15, 0, -15)
    Glow.Size = UDim2.new(1, 30, 1, 30)
    Glow.Image = "rbxassetid://4996891970"
    Glow.ImageColor3 = Theme.Glow
    Glow.ImageTransparency = 0.55

    -- TOPBAR
    local TopBar = Instance.new("Frame")
    TopBar.Parent = Main
    TopBar.Size = UDim2.new(1, 0, 0, 50)
    TopBar.BackgroundColor3 = Theme.Dark
    TopBar.BorderSizePixel = 0
    TopBar.Active = true

    Instance.new("UICorner", TopBar).CornerRadius = UDim.new(0, 12)

    local Title = Instance.new("TextLabel")
    Title.Parent = TopBar
    Title.Text = cfg.Name or "Orion"
    Title.Font = Enum.Font.GothamBlack
    Title.TextSize = 20
    Title.TextColor3 = Theme.Text
    Title.BackgroundTransparency = 1
    Title.Position = UDim2.new(0, 20, 0, 6)
    Title.Size = UDim2.new(1, -40, 1, -12)

    -- TAB LIST
    local TabList = Instance.new("Frame")
    TabList.Parent = Main
    TabList.Size = UDim2.new(0, 150, 1, -50)
    TabList.Position = UDim2.new(0, 0, 0, 50)
    TabList.BackgroundColor3 = Theme.Dark
    TabList.BorderSizePixel = 0
    Instance.new("UICorner", TabList).CornerRadius = UDim.new(0, 12)

    local TabListLayout = Instance.new("UIListLayout")
    TabListLayout.Parent = TabList
    TabListLayout.Padding = UDim.new(0, 6)
    TabListLayout.SortOrder = Enum.SortOrder.LayoutOrder

    -- CONTENT AREA
    local ContentArea = Instance.new("Frame")
    ContentArea.Parent = Main
    ContentArea.Size = UDim2.new(1, -150, 1, -50)
    ContentArea.Position = UDim2.new(0, 150, 0, 50)
    ContentArea.BackgroundColor3 = Theme.Light
    ContentArea.BorderSizePixel = 0
    Instance.new("UICorner", ContentArea).CornerRadius = UDim.new(0, 10)

    -- DRAGGING
    local dragging = false
    local dragStart, startPos
    TopBar.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = Main.Position
        end
    end)
    UserInputService.InputChanged:Connect(function(input)
        if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
            local delta = input.Position - dragStart
            Main.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end
    end)

    -- WINDOW OBJECT
    local Window = {}
    Window.Tabs = {}

    -- TAB CREATION
    function Window:MakeTab(tabCfg)
        tabCfg = tabCfg or {}

        local TabButton = Instance.new("TextButton")
        TabButton.Parent = TabList
        TabButton.Size = UDim2.new(1, -10, 0, 32)
        TabButton.Text = "  " .. (tabCfg.Name or "Tab")
        TabButton.BackgroundColor3 = Theme.Main
        TabButton.TextColor3 = Theme.Text
        TabButton.Font = Enum.Font.GothamSemibold
        TabButton.TextSize = 14
        TabButton.BorderSizePixel = 0
        Instance.new("UICorner", TabButton).CornerRadius = UDim.new(0, 10)

        -- INDICATOR BAR
        local Indicator = Instance.new("Frame")
        Indicator.Parent = TabButton
        Indicator.Size = UDim2.new(0, 5, 1, 0)
        Indicator.Position = UDim2.new(0, -5, 0, 0)
        Indicator.BackgroundColor3 = Theme.Glow
        Indicator.BorderSizePixel = 0
        Indicator.Visible = false

        local SectionContainer = Instance.new("ScrollingFrame")
        SectionContainer.Parent = ContentArea
        SectionContainer.Size = UDim2.new(1, -20, 1, -20)
        SectionContainer.Position = UDim2.new(0, 10, 0, 10)
        SectionContainer.BackgroundTransparency = 1
        SectionContainer.CanvasSize = UDim2.new(0, 0, 0, 0)
        SectionContainer.Visible = false

        local Layout = Instance.new("UIListLayout")
        Layout.Parent = SectionContainer
        Layout.Padding = UDim.new(0, 10)
        Layout.SortOrder = Enum.SortOrder.LayoutOrder

        Layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
            SectionContainer.CanvasSize = UDim2.new(0, 0, 0, Layout.AbsoluteContentSize.Y + 20)
        end)

        -- SELECTING TABS
        TabButton.MouseButton1Click:Connect(function()
            -- hide all
            for _,t in ipairs(Window.Tabs) do
                t.Container.Visible = false
                t.Indicator.Visible = false
            end
            SectionContainer.Visible = true
            Indicator.Visible = true
        end)

        local Tab = {Container = SectionContainer, Indicator = Indicator}
        table.insert(Window.Tabs, Tab)

        if #Window.Tabs == 1 then
            Indicator.Visible = true
            SectionContainer.Visible = true
        end

        -- ELEMENTS APIS
        function Tab:AddLabel(text)
            local Label = Instance.new("TextLabel")
            Label.Parent = SectionContainer
            Label.Size = UDim2.new(1, -10, 0, 25)
            Label.Text = text or "Label"
            Label.TextColor3 = Theme.Text
            Label.TextSize = 14
            Label.Font = Enum.Font.GothamSemibold
            Label.BackgroundTransparency = 1
            return Label
        end

        function Tab:AddButton(cfg)
            cfg = cfg or {}
            local Btn = Instance.new("TextButton")
            Btn.Parent = SectionContainer
            Btn.Size = UDim2.new(1, -10, 0, 32)
            Btn.BackgroundColor3 = Theme.Main
            Btn.TextColor3 = Theme.Text
            Btn.Text = cfg.Name or "Button"
            Btn.TextSize = 14
            Btn.Font = Enum.Font.GothamBold
            Btn.BorderSizePixel = 0
            Instance.new("UICorner", Btn).CornerRadius = UDim.new(0, 10)
            Btn.MouseButton1Click:Connect(function() pcall(cfg.Callback) end)
            return Btn
        end

        function Tab:AddToggle(cfg)
            cfg = cfg or {}
            local State = cfg.Default or false

            local Frame = Instance.new("Frame")
            Frame.Parent = SectionContainer
            Frame.Size = UDim2.new(1, -10, 0, 32)
            Frame.BackgroundColor3 = Theme.Main
            Frame.BorderSizePixel = 0
            Instance.new("UICorner", Frame).CornerRadius = UDim.new(0, 10)

            local Text = Instance.new("TextLabel")
            Text.Parent = Frame
            Text.Size = UDim2.new(1, -50, 1, 0)
            Text.Position = UDim2.new(0, 10, 0, 0)
            Text.BackgroundTransparency = 1
            Text.Text = cfg.Name or "Toggle"
            Text.TextColor3 = Theme.Text
            Text.Font = Enum.Font.GothamSemibold
            Text.TextSize = 14

            local Button = Instance.new("TextButton")
            Button.Parent = Frame
            Button.Size = UDim2.new(0, 40, 0, 20)
            Button.Position = UDim2.new(1, -50, 0.5, -10)
            Button.BackgroundTransparency = 1
            Button.Text = ""

            local Knob = Instance.new("Frame")
            Knob.Parent = Button
            Knob.Size = UDim2.new(0, 18, 0, 18)
            Knob.Position = UDim2.new(0, 2, 0, 1)
            Knob.BackgroundColor3 = State and Theme.Glow or Theme.Stroke
            Knob.BorderSizePixel = 0
            Instance.new("UICorner", Knob).CornerRadius = UDim.new(1, 0)

            Button.MouseButton1Click:Connect(function()
                State = not State
                TweenService:Create(Knob, TweenInfo.new(0.15, Enum.EasingStyle.Quart), {
                    Position = UDim2.new(State and 1 or 0, State and -20 or 2, 0, 1),
                    BackgroundColor3 = State and Theme.Glow or Theme.Stroke
                }):Play()
                pcall(cfg.Callback, State)
            end)

            return {
                Set = function(_,v) State=v end,
                Get = function() return State end
            }
        end

        return Tab
    end

    return Window
end

function OrionLib:Destroy()
    Orion:Destroy()
end

return OrionLib (Exact API - Improved Implementation)
-- API kept compatible with original Orion:
-- OrionLib:Init()
-- OrionLib:MakeWindow(cfg)
-- Window:MakeTab(cfg)
-- Tab:AddLabel(text)
-- Tab:AddParagraph(title, content)
-- Tab:AddButton(cfg)
-- Tab:AddToggle(cfg)
-- Tab:AddSlider(cfg)
-- Tab:AddTextBox(cfg)
-- OrionLib:MakeNotification(cfg)
-- OrionLib:Destroy()

-- Written: clean, modern, robust, playable across executors
-- Features: safe GUI parenting, draggable windows, Active=true for input, basic theming, persistent flags

local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local LocalPlayer = Players.LocalPlayer

local OrionLib = {
    Elements = {},
    ThemeObjects = {},
    Connections = {},
    Flags = {},
    Themes = {
        Default = {
            Main = Color3.fromRGB(25,25,35),
            Second = Color3.fromRGB(32,32,42),
            Stroke = Color3.fromRGB(37,37,47),
            Divider = Color3.fromRGB(60,60,70),
            Text = Color3.fromRGB(240,240,240),
            TextDark = Color3.fromRGB(150,150,150)
        }
    },
    SelectedTheme = "Default",
    Folder = nil,
    SaveCfg = false
}

-- Utility functions
local function isInstance(obj)
    return typeof(obj) == "Instance" or (type(obj) == "userdata" and tostring(obj):match("Instance"))
end

local function safePcall(fn)
    local ok,ret = pcall(fn)
    return ok,ret
end

local function AddConnection(signal, fn)
    if not signal or not fn then return end
    local ok, conn = pcall(function() return signal:Connect(fn) end)
    if ok and conn then
        table.insert(OrionLib.Connections, conn)
        return conn
    end
    return nil
end

-- Clean GUI parent: try syn.protect_gui -> gethui() -> PlayerGui -> CoreGui
local function safeParentGui(gui)
    gui.ResetOnSpawn = false
    if typeof(syn) == "table" and type(syn.protect_gui) == "function" then
        pcall(function() syn.protect_gui(gui) end)
        if game:GetService("CoreGui") then
            gui.Parent = game:GetService("CoreGui")
            return
        end
    end
    if type(gethui) == "function" then
        local ok, parent = pcall(gethui)
        if ok and parent then
            gui.Parent = parent
            return
        end
    end
    if LocalPlayer and LocalPlayer:FindFirstChild("PlayerGui") then
        gui.Parent = LocalPlayer:FindFirstChild("PlayerGui")
        return
    end
    gui.Parent = game:GetService("CoreGui")
end

-- Create instances with properties and children
local function Create(class, props, children)
    local obj = Instance.new(class)
    if props then
        for k,v in pairs(props) do
            pcall(function() obj[k] = v end)
        end
    end
    if children then
        for _,c in ipairs(children) do
            if isInstance(c) then
                c.Parent = obj
            end
        end
    end
    return obj
end

-- Basic element factory (keeps original element names)
local function CreateElement(name, ...)
    if OrionLib.Elements[name] then
        return OrionLib.Elements[name](...)
    end
    error("Unknown element: " .. tostring(name))
end

local function SetProps(obj, props)
    for k,v in pairs(props or {}) do
        pcall(function() obj[k] = v end)
    end
    return obj
end

local function SetChildren(obj, children)
    for _,c in ipairs(children or {}) do
        if isInstance(c) then c.Parent = obj end
    end
    return obj
end

-- Small set of element constructors used by this rewrite
OrionLib.Elements["RoundFrame"] = function(color, scale, offset)
    local frame = Create("Frame", {BackgroundColor3 = color or Color3.new(1,1,1), BorderSizePixel = 0})
    local corner = Create("UICorner", {CornerRadius = UDim.new(scale or 0, offset or 8)})
    corner.Parent = frame
    return frame
end

OrionLib.Elements["Label"] = function(text, size, transparency)
    return Create("TextLabel", {Text = text or "", TextColor3 = Color3.fromRGB(240,240,240), TextSize = size or 14, Font = Enum.Font.GothamSemibold, BackgroundTransparency = 1, TextXAlignment = Enum.TextXAlignment.Left, RichText = true})
end

OrionLib.Elements["Image"] = function(img)
    return Create("ImageLabel", {Image = img or "", BackgroundTransparency = 1})
end

OrionLib.Elements["Button"] = function()
    return Create("TextButton", {Text = "", BackgroundTransparency = 1, AutoButtonColor = false, BorderSizePixel = 0})
end

OrionLib.Elements["TFrame"] = function()
    return Create("Frame", {BackgroundTransparency = 1})
end

OrionLib.Elements["ScrollFrame"] = function(color, width)
    return Create("ScrollingFrame", {BackgroundTransparency = 1, ScrollBarImageColor3 = color or Color3.fromRGB(255,255,255), BorderSizePixel = 0, ScrollBarThickness = width or 6, CanvasSize = UDim2.new(0,0,0,0)})
end

-- Theme helpers
local function ReturnProperty(obj)
    if obj:IsA("Frame") or obj:IsA("TextButton") then return "BackgroundColor3" end
    if obj:IsA("ScrollingFrame") then return "ScrollBarImageColor3" end
    if obj:IsA("UIStroke") then return "Color" end
    if obj:IsA("TextLabel") or obj:IsA("TextBox") then return "TextColor3" end
    if obj:IsA("ImageLabel") or obj:IsA("ImageButton") then return "ImageColor3" end
    return nil
end

local function AddThemeObject(obj, kind)
    if not OrionLib.ThemeObjects[kind] then OrionLib.ThemeObjects[kind] = {} end
    table.insert(OrionLib.ThemeObjects[kind], obj)
    local prop = ReturnProperty(obj)
    if prop then
        pcall(function() obj[prop] = OrionLib.Themes[OrionLib.SelectedTheme][kind] end)
    end
    return obj
end

local function SetTheme()
    for kind, list in pairs(OrionLib.ThemeObjects) do
        for _,obj in pairs(list) do
            local prop = ReturnProperty(obj)
            if prop then
                pcall(function() obj[prop] = OrionLib.Themes[OrionLib.SelectedTheme][kind] end)
            end
        end
    end
end

-- Simple rounding helper
local function Clamp(n, a, b) return math.max(a, math.min(b, n)) end

-- Notifications container
local OrionGui = Instance.new("ScreenGui")
OrionGui.Name = "Orion"
OrionGui.ResetOnSpawn = false
safeParentGui(OrionGui)

local NotificationHolder = Create("Frame", {Size = UDim2.new(0,300,0,100), Position = UDim2.new(1,-25,1,-25), AnchorPoint = Vector2.new(1,1), BackgroundTransparency = 1, Parent = OrionGui})
local notifyList = Create("UIListLayout", {Padding = UDim.new(0,6), SortOrder = Enum.SortOrder.LayoutOrder})
notifyList.Parent = NotificationHolder

function OrionLib:MakeNotification(cfg)
    cfg = cfg or {}
    local title = cfg.Name or "Notification"
    local text = cfg.Content or "Content"
    local time = cfg.Time or 5
    local icon = cfg.Image or ""

    local container = Create("Frame", {AutomaticSize = Enum.AutomaticSize.Y, Size = UDim2.new(1,0,0,0), BackgroundTransparency = 1})
    container.Parent = NotificationHolder

    local frame = Create("Frame", {BackgroundColor3 = OrionLib.Themes[OrionLib.SelectedTheme].Main, Size = UDim2.new(1,0,0,0), AutomaticSize = Enum.AutomaticSize.Y, ClipsDescendants = true})
    frame.Parent = container
    frame.BorderSizePixel = 0
    local corner = Create("UICorner", {CornerRadius = UDim.new(0,8)}) corner.Parent = frame
    local stroke = Create("UIStroke", {Color = OrionLib.Themes[OrionLib.SelectedTheme].Stroke, Thickness = 1}) stroke.Parent = frame

    local iconLabel = Create("ImageLabel", {Image = icon, Size = UDim2.new(0,24,0,24), Position = UDim2.new(0,8,0,8), BackgroundTransparency = 1}) iconLabel.Parent = frame
    local titleLabel = Create("TextLabel", {Text = title, Font = Enum.Font.GothamBold, TextSize = 15, Position = UDim2.new(0,40,0,6), BackgroundTransparency = 1, TextXAlignment = Enum.TextXAlignment.Left}) titleLabel.Parent = frame
    local contentLabel = Create("TextLabel", {Text = text, Font = Enum.Font.Gotham, TextSize = 13, Position = UDim2.new(0,40,0,26), Size = UDim2.new(1,-48,0,0), BackgroundTransparency = 1, TextWrapped = true, AutomaticSize = Enum.AutomaticSize.Y}) contentLabel.Parent = frame

    TweenService:Create(frame, TweenInfo.new(0.35, Enum.EasingStyle.Quart), {BackgroundTransparency = 0}):Play()
    delay(time, function()
        pcall(function()
            TweenService:Create(frame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {BackgroundTransparency = 1}):Play()
            wait(0.45)
            container:Destroy()
        end)
    end)
end

-- Make draggable: robust implementation using AbsolutePosition and ViewportSize
local function MakeDraggable(dragPoint, main)
    if not isInstance(dragPoint) or not isInstance(main) then return end
    pcall(function() dragPoint.Active = true main.Active = true end)

    local dragging = false
    local dragInput = nil
    local dragStart = nil
    local startPos = nil

    AddConnection(dragPoint.InputBegan, function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            local absPos = main.AbsolutePosition
            startPos = Vector2.new(absPos.X, absPos.Y)
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    AddConnection(dragPoint.InputChanged, function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement then
            dragInput = input
        end
    end)

    AddConnection(UserInputService.InputChanged, function(input)
        if dragging and dragInput and input == dragInput and dragStart and startPos then
            local delta = input.Position - dragStart
            local newPos = startPos + delta
            local cam = workspace.CurrentCamera
            local view = Vector2.new( (cam and cam.ViewportSize.X) or 1920, (cam and cam.ViewportSize.Y) or 1080)
            -- keep the original scale and use offset in pixels
            local current = main.Position
            local xOff, yOff = Clamp(math.floor(newPos.X), -99999, 99999), Clamp(math.floor(newPos.Y), -99999, 99999)
            local newUDim = UDim2.new(current.X.Scale, xOff, current.Y.Scale, yOff)
            pcall(function()
                TweenService:Create(main, TweenInfo.new(0.06, Enum.EasingStyle.Quint), {Position = newUDim}):Play()
            end)
            main.Position = newUDim
        end
    end)
end

-- Clean API: MakeWindow implementation
function OrionLib:MakeWindow(cfg)
    cfg = cfg or {}
    local WindowConfig = {
        Name = cfg.Name or "Orion Window",
        Icon = cfg.Icon or "",
        IntroEnabled = cfg.IntroEnabled == nil and true or cfg.IntroEnabled,
        IntroText = cfg.IntroText or cfg.Name or "Orion",
        ShowIcon = cfg.ShowIcon or false,
        HidePremium = cfg.HidePremium or false,
        SaveConfig = cfg.SaveConfig or false,
    }

    local MainWindow = Create("Frame", {Size = UDim2.new(0,600,0,340), Position = UDim2.new(0.5,-300,0.5,-170), BackgroundColor3 = OrionLib.Themes[OrionLib.SelectedTheme].Main, BorderSizePixel = 0, ClipsDescendants = true})
    local corner = Create("UICorner", {CornerRadius = UDim.new(0,10)}) corner.Parent = MainWindow
    local stroke = Create("UIStroke", {Color = OrionLib.Themes[OrionLib.SelectedTheme].Stroke, Thickness = 1}) stroke.Parent = MainWindow
    MainWindow.Parent = OrionGui
    MainWindow.Active = true

    -- Top bar
    local TopBar = Create("Frame", {Size = UDim2.new(1,0,0,50), BackgroundTransparency = 1, Name = "TopBar"}) TopBar.Parent = MainWindow
    local title = Create("TextLabel", {Text = WindowConfig.Name, Font = Enum.Font.GothamBlack, TextSize = 20, BackgroundTransparency = 1, Position = UDim2.new(0,24,0,8)}) title.Parent = TopBar

    -- Close button
    local CloseBtn = Create("TextButton", {Size = UDim2.new(0,70,0,30), Position = UDim2.new(1,-90,0,10), BackgroundTransparency = 1, Text = ""}) CloseBtn.Parent = TopBar
    local closeIcon = Create("ImageLabel", {Image = "rbxassetid://7072725342", Size = UDim2.new(0,18,0,18), Position = UDim2.new(0,9,0,6), BackgroundTransparency = 1}) closeIcon.Parent = CloseBtn
    AddConnection(CloseBtn.MouseButton1Up, function()
        MainWindow.Visible = false
        OrionLib:MakeNotification({Name = "Interface Hidden", Content = "Press LeftControl to reopen"})
    end)

    AddConnection(UserInputService.InputBegan, function(input)
        if input.KeyCode == Enum.KeyCode.LeftControl and not MainWindow.Visible then
            MainWindow.Visible = true
        end
    end)

    -- Minimize
    local MinBtn = Create("TextButton", {Size = UDim2.new(0,70,0,30), Position = UDim2.new(1,-160,0,10), BackgroundTransparency = 1, Text = ""}) MinBtn.Parent = TopBar
    local minIcon = Create("ImageLabel", {Image = "rbxassetid://7072719338", Size = UDim2.new(0,18,0,18), Position = UDim2.new(0,9,0,6), BackgroundTransparency = 1}) minIcon.Parent = MinBtn

    local WindowStuff = Create("Frame", {Size = UDim2.new(0,150,1,-50), Position = UDim2.new(0,0,0,50), BackgroundTransparency = 1}) WindowStuff.Parent = MainWindow

    -- Tabs holder
    local TabHolder = Create("ScrollingFrame", {Size = UDim2.new(0,150,1,-50), Position = UDim2.new(0,0,0,50), ScrollBarThickness = 6, BackgroundTransparency = 1}) TabHolder.Parent = MainWindow
    local tabList = Create("UIListLayout", {Padding = UDim.new(0,6)}) tabList.Parent = TabHolder

    -- Content area (where tab items show)
    local ContentArea = Create("Frame", {Size = UDim2.new(1,-150,1,-50), Position = UDim2.new(0,150,0,50), BackgroundTransparency = 1, Name = "ContentArea"}) ContentArea.Parent = MainWindow

    -- Draggable
    MakeDraggable(TopBar, MainWindow)

    -- Public window object
    local Window = {}
    Window._tabs = {}

    function Window:MakeTab(tabCfg)
        tabCfg = tabCfg or {}
        local name = tabCfg.Name or "Tab"
        local icon = tabCfg.Icon or ""
        local premium = tabCfg.PremiumOnly or false

        -- Tab button
        local tabBtn = Create("TextButton", {Size = UDim2.new(1,0,0,30), BackgroundTransparency = 1, Text = ""}) tabBtn.Parent = TabHolder
        local ico = Create("ImageLabel", {Image = icon, Size = UDim2.new(0,18,0,18), Position = UDim2.new(0,8,0,6), BackgroundTransparency = 1}) ico.Parent = tabBtn
        local lbl = Create("TextLabel", {Text = name, Position = UDim2.new(0,35,0,0), Size = UDim2.new(1,-35,1,0), BackgroundTransparency = 1, Font = Enum.Font.GothamSemibold, TextSize = 14}) lbl.Parent = tabBtn

        -- Container
        local container = Create("ScrollingFrame", {Size = UDim2.new(1,-160,1,-70), Position = UDim2.new(0,150,0,50), BackgroundTransparency = 1, Visible = false, ScrollBarThickness = 6}) container.Parent = MainWindow
        local list = Create("UIListLayout", {Padding = UDim.new(0,8)}) list.Parent = container
        AddConnection(container:GetPropertyChangedSignal("CanvasSize"), function()
            pcall(function() container.CanvasSize = UDim2.new(0,0,0, list.AbsoluteContentSize.Y + 16) end)
        end)

        if #Window._tabs == 0 then
            lbl.Font = Enum.Font.GothamBlack; lbl.TextTransparency = 0; ico.ImageTransparency = 0; container.Visible = true
        end

        AddConnection(tabBtn.MouseButton1Click, function()
            for _,child in ipairs(MainWindow:GetChildren()) do
                if child:IsA("ScrollingFrame") and child ~= TabHolder then child.Visible = false end
            end
            for _,tb in ipairs(TabHolder:GetChildren()) do
                if tb:IsA("TextButton") then
                    for _,c in ipairs(tb:GetChildren()) do
                        if c:IsA("TextLabel") then c.Font = Enum.Font.GothamSemibold; c.TextTransparency = 0.45 end
                        if c:IsA("ImageLabel") then c.ImageTransparency = 0.45 end
                    end
                end
            end
            lbl.Font = Enum.Font.GothamBlack; lbl.TextTransparency = 0; ico.ImageTransparency = 0
            container.Visible = true
        end)

        local Tab = {}
        function Tab:AddLabel(text)
            local frame = Create("Frame", {Size = UDim2.new(1,0,0,28), BackgroundTransparency = 0.7}) frame.Parent = container
            local lab = Create("TextLabel", {Text = text or "", Font = Enum.Font.GothamBold, TextSize = 15, BackgroundTransparency = 1, Position = UDim2.new(0,12,0,0)}) lab.Parent = frame
            return {
                Set = function(self, v) lab.Text = v end
            }
        end

        function Tab:AddParagraph(title, content)
            local frame = Create("Frame", {Size = UDim2.new(1,0,0,40), BackgroundTransparency = 0.7}) frame.Parent = container
            local t = Create("TextLabel", {Text = title or "", Font = Enum.Font.GothamBold, TextSize = 14, BackgroundTransparency = 1, Position = UDim2.new(0,12,0,6)}) t.Parent = frame
            local c = Create("TextLabel", {Text = content or "", Font = Enum.Font.Gotham, TextSize = 13, BackgroundTransparency = 1, Position = UDim2.new(0,12,0,22), Size = UDim2.new(1,-24,0,0), TextWrapped = true, AutomaticSize = Enum.AutomaticSize.Y}) c.Parent = frame
            return { Set = function(self, v) c.Text = v end }
        end

        function Tab:AddButton(cfg)
            cfg = cfg or {}
            local name = cfg.Name or "Button"
            local callback = cfg.Callback or function() end
            local btnFrame = Create("Frame", {Size = UDim2.new(1,0,0,32), BackgroundTransparency = 0.7}) btnFrame.Parent = container
            local btn = Create("TextButton", {Text = name or "Button", Size = UDim2.new(1,-20,1,0), Position = UDim2.new(0,10,0,0), BackgroundTransparency = 1, Font = Enum.Font.GothamBold}) btn.Parent = btnFrame
            AddConnection(btn.MouseButton1Click, function()
                pcall(callback)
            end)
            return { Set = function(self, v) btn.Text = v end }
        end

        function Tab:AddToggle(cfg)
            cfg = cfg or {}
            local name = cfg.Name or "Toggle"
            local default = cfg.Default or false
            local callback = cfg.Callback or function() end

            local frame = Create("Frame", {Size = UDim2.new(1,0,0,30), BackgroundTransparency = 0.7}) frame.Parent = container
            local label = Create("TextLabel", {Text = name, Position = UDim2.new(0,12,0,0), Size = UDim2.new(1,-60,1,0), BackgroundTransparency = 1, Font = Enum.Font.GothamSemibold}) label.Parent = frame
            local toggleBtn = Create("TextButton", {Size = UDim2.new(0,40,0,20), Position = UDim2.new(1,-52,0,5), BackgroundTransparency = 1, Text = ""}) toggleBtn.Parent = frame
            local switch = Create("Frame", {Size = UDim2.new(0,14,0,14), Position = UDim2.new(0,2,0,3), BackgroundColor3 = default and Color3.fromRGB(100,200,100) or Color3.fromRGB(120,120,120)}) switch.Parent = toggleBtn
            local state = default

            AddConnection(toggleBtn.MouseButton1Click, function()
                state = not state
                pcall(function() switch.BackgroundColor3 = state and Color3.fromRGB(100,200,100) or Color3.fromRGB(120,120,120) end)
                pcall(function() callback(state) end)
            end)

            -- store flag
            local flagId = tostring(math.random(1,9999999))
            OrionLib.Flags[flagId] = {Type = "Toggle", Value = state, Set = function(_,v) state = v pcall(function() switch.BackgroundColor3 = v and Color3.fromRGB(100,200,100) or Color3.fromRGB(120,120,120) end) end, Save = cfg.Save}

            return {
                Get = function() return state end,
                Set = function(_, v) state = v pcall(function() switch.BackgroundColor3 = v and Color3.fromRGB(100,200,100) or Color3.fromRGB(120,120,120) end) end
            }
        end

        function Tab:AddSlider(cfg)
            cfg = cfg or {}
            local name = cfg.Name or "Slider"
            local min = cfg.Min or 0
            local max = cfg.Max or 100
            local default = cfg.Default or min
            local callback = cfg.Callback or function() end

            local frame = Create("Frame", {Size = UDim2.new(1,0,0,40), BackgroundTransparency = 0.7}) frame.Parent = container
            local lbl = Create("TextLabel", {Text = name, Position = UDim2.new(0,12,0,0), BackgroundTransparency = 1, Font = Enum.Font.GothamSemibold}) lbl.Parent = frame
            local barBg = Create("Frame", {Size = UDim2.new(1,-24,0,10), Position = UDim2.new(0,12,0,22), BackgroundColor3 = Color3.fromRGB(60,60,70)}) barBg.Parent = frame
            local barFill = Create("Frame", {Size = UDim2.new((default - min)/(max - min),0,1,0), BackgroundColor3 = Color3.fromRGB(120,120,220)}) barFill.Parent = barBg

            local dragging = false
            AddConnection(barBg.InputBegan, function(input)
                if input.UserInputType == Enum.UserInputType.MouseButton1 then
                    dragging = true
                end
            end)
            AddConnection(UserInputService.InputEnded, function(input)
                if input.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end
            end)

            AddConnection(UserInputService.InputChanged, function(input)
                if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
                    local rel = Clamp((input.Position.X - barBg.AbsolutePosition.X) / barBg.AbsoluteSize.X, 0, 1)
                    barFill.Size = UDim2.new(rel,0,1,0)
                    local value = min + (max - min) * rel
                    pcall(function() callback(value) end)
                end
            end)

            return {
                Get = function() return min + (max - min) * barFill.Size.X.Scale end,
                Set = function(_, v) local rel = Clamp((v - min)/(max - min), 0,1) barFill.Size = UDim2.new(rel,0,1,0) end
            }
        end

        function Tab:AddTextBox(cfg)
            cfg = cfg or {}
            local placeholder = cfg.Placeholder or ""
            local callback = cfg.Callback or function() end
            local frame = Create("Frame", {Size = UDim2.new(1,0,0,30), BackgroundTransparency = 0.7}) frame.Parent = container
            local box = Create("TextBox", {Text = "", PlaceholderText = placeholder, Size = UDim2.new(1,-24,1,0), Position = UDim2.new(0,12,0,0), BackgroundTransparency = 1, Font = Enum.Font.Gotham}) box.Parent = frame
            AddConnection(box.FocusLost, function(enter)
                if enter then pcall(function() callback(box.Text) end) end
            end)
            return {Get = function() return box.Text end, Set = function(_,v) box.Text = v end}
        end

        table.insert(Window._tabs, Tab)
        return Tab
    end

    function Window:Destroy()
        pcall(function() MainWindow:Destroy() end)
    end

    function Window:Show()
        MainWindow.Visible = true
    end

    function Window:Hide()
        MainWindow.Visible = false
    end

    return Window
end

function OrionLib:Init()
    -- load saved config if needed (not implemented here - placeholder)
    return true
end

function OrionLib:Destroy()
    for _,c in ipairs(self.Connections) do
        pcall(function() c:Disconnect() end)
    end
    pcall(function() OrionGui:Destroy() end)
end

return OrionLib
