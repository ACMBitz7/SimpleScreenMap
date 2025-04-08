# SimpleScreenMap
A python module that makes working with multiple displays or compatibility with other displays easier.


Only works for Windows.


This module is just to save time writing multiple functions or code. Here's what you can do with it:

getDisplays()
  
  -Lists all displays in order and their properties.
  
  -Example output:
  
    [Display(name='\\.\DISPLAY1', width=2560, height=1440, originX=0, originY=0, primary=True), Display(name='\\.\DISPLAY2', width=2560, height=1440, originX=2560, originY=0, primary=False)]
 
  -can assign a variable to it using a for loop or PrimaryMonitor = getDisplays()[0]
  
  -Properties:
    
    Monitor.name, Monitor.width, Monitor.height, Monitor.originX, Monitor.originY, Monitor.primary


screenPosition(x, y, display, bordered, relative)
  
  Example: Display size is 1920, 1080. screenPosition(0.5, 1, 0) returns 960, 1080.
  
  -x, y: any value between 0, 0 and 1, 1 that determines the output. 1, 1 would be 100 percent of the display, which is the bottom right corner.
  
  -display: an integer that determines which monitor to use, starting with 0 (primary) monitor.
  
  -bordered: a boolean that determines if the values may extend to another display, including displays that don't exist (off screen positions). (True by default)
  
  -relative: a boolean the determines if the position is relative to the origin of the selected display, as if it was the primary display.


screenpositionCentered(x, y, display, bordered, relative)

  Example: Display size is 1920, 1080. screenPositionCentered(1, 0, 0) returns 1920, 540.

  -x, y: any value between -1, -1, and 1, 1 originating from the center. 0, 0 is the center, -1, -1 is the top left, and 1, 1 is the bottom right.

  -display: an integer that determines which monitor to use, starting with 0 (primary) monitor.

  -bordered: a boolean that determines if the values may extend to another display, including displays that don't exist (off screen positions). (True by default)

  -relative: a boolean the determines if the position is relative to the origin of the selected display, as if it was the primary display.


positionPercent(x, y, display, bordered)

  Example: Display size is 1920, 1080. positionPercent(1920, 1080, 0) returns 1, 1

  -x, y: Any pixel on the display.

  -display: integer that determines which monitor to use, starting with 0 (primary) monitor.

  bordered: a boolean that determines if the percentage for each coordinate can extend past 0 or 1.


Uses for this module:

You can use screenPosition or screenPositionCentered to get a position on screen that accurately scales between multiple displays/screens. Useful for GUI.

Example: GUIElement.position = screenPositionCentered(0.5, 0.5, 1) #This will always place the GUIElement in the top right quadrant of the second display.
 
  GUIElement.position += screenPosition(0.25, 0) #Move GUIElement a fourth of the screen to the right

You can use positionPercent to return the percentage of the screen a position is at for both coordinates.

Example: SliderPosX, SliderPosY = positionPercent(Slider.position)
  
  SliderPosition = screenPosition(SliderPosX, SliderPosY * 2) #Moves Slider twice as far down than it's original position
