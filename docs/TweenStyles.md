# Tween

## Tween styles

```lua 
{
    "Linear",			
    "Quad",				
    "Cubic",
	"Quart",			
    "Quint",				
    "Sine",
	"Expo",			
    "Circ",				
    "Elastic",
	"Back",			
    "Bounce",					
    "Smooth",
	"Smoother",			
    "RidiculousWiggle",		
    "RevBack",
	"Spring",			
    "SoftSpring",				
    "Standard",
	"Sharp",				
    "Acceleration",			
    "Deceleration",
	"StandardProductive",	
    "EntranceProductive",	
    "ExitProductive",
	"StandardExpressive",	
    "EntranceExpressive",		
    "ExitExpressive",
	"FabricStandard",		
    "FabricAccelerate",		
    "FabricDecelerate",
	"UWPAccelerate",		
    "MozillaCurve"
}
```

## Tween directions

```lua
{
    "In",
    "Out",
    "InOut"
}
```

## Tween StepTypes
StepTypes are a [RunService](https://developer.roblox.com/en-us/api-reference/class/RunService) event desgined to fire at different times

```lua
{
    "Heartbeat", --Fires every frame after the physics simulation has completed(Dont worry about this too much! It pretty much just runs everytime you move your character!)
    "RenderStepped", --Fires every frame prior to the frame being rendered(This means that it will constantly run, this will run before Heartbeat!)
    "Stepped" --Fires every frame prior to the physics simulation(This is also fatser than Heartbeat and it does the opposite of Heartbeat)
}
```