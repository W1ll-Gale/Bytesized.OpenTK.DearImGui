# Bytesized.OpenTK.DearImGui

A production-ready ImGui controller for OpenTK, designed for ease of use and modern features.

Installation

Install via NuGet:

``` ps
dotnet add package Bytesized.OpenTK.DearImGui
```

Usage

1. Initialize

In your GameWindow class:

```c#
using Bytesized.OpenTK.DearImGui;

ImGuiController _controller;

protected override void OnLoad()
{
    base.OnLoad();
    
    // The controller automatically hooks into Resize and CharInput events.
    _controller = new ImGuiController(this);
}
```

2. Update & Render

In your loop:

```c#
protected override void OnRenderFrame(FrameEventArgs args)
{
    base.OnRenderFrame(args);
    GL.Clear(ClearBufferMask.ColorBufferBit);

    // Update ImGui (handles Input, Gamepad, and HighDPI scaling)
    _controller.Update((float)args.Time);

    // --- Draw your UI here ---
    ImGuiNET.ImGui.ShowDemoWindow();

    // Render ImGui geometry
    _controller.Render();

    SwapBuffers();
}
```


Font Configuration
 
By default, the controller is packaged with a higher res roboto font, if this fails  loads the standard ImGui bitmap font. You can load a custom .ttf file easily:

```c#
// If you embed "Roboto.ttf" in your assembly as a resource:
_controller.LoadEmbeddedFont("Roboto.ttf", 16.0f);

// Or load from disk:
_controller.LoadCustomFont("Assets/Fonts/Roboto.ttf", 16.0f);
```
