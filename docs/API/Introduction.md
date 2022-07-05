
## Replica Service


## Profile Service


## Top Bar
API Section for the Top Bar library.
!!! info "To use this use the following API table"
    ```lua	
    local API = self.API;
    local TopBar = API.TopBar
    ```

!!! warning 
    Through out the reference for TopBar, I use terms like ```chained``` and ```unchained```. What this means is that if something is chained it is connected to a constructor like this:
	```lua
	local new = TopBar.newIcon() --Chained constuctor
	new:chainFunction(nil,function(icon)) --This is the constuructor chained to another function
	```
	If it is unchained it does not have a constructor attached to it instead it uses a parameter **All of our TopBar API section is made to accept a ```TopBar.rawIcon``` as a parameter**! 

	```lua
	local new = TopBar.rawIcon() --Unchained constructor meaning this cannot be chanined with other function instead it has to be passed as a parameter!
	TopBar:chainFunction(new, function(icon)) --This is a function that is not chained instead it uses the first parameter as the icon
	```
### Constructors
!!! success inline end "Can be chained"
#### newIcon
```lua
local new = TopBar.newIcon(name,{})
```
*name* - ```string``` sets the name of the icon.

*{}* - ```table``` pass in any setting to be used to style or add functions to your icon.

Used to create a new Icon. This constructor takes any ```TopBar``` setting and name within the table, to search through these settings check [this](https://github.com/1ForeverHD/TopbarPlus/blob/main/src/Icon/Themes/Default.lua) page out! 

Example:
```lua
local API = self.API;
local TopBar = API.TopBar;	
local new = TopBar.newIcon("Name",
	{
		iconText = "Hello",
		iconBackgroundColor = Color3.fromRGB(96, 255, 122)
	});
```
___
!!! fail inline end "Cannot be chained"
#### rawIcon

```lua
local new = TopBar.rawIcon(name,{})
```
*name* - ```string``` sets the name of the icon.

*{}* - ```table``` pass in any setting to be used to style or add functions to your icon.

Used to create a new Icon. This constructor takes any ```TopBar``` setting and name within the table, to search through these settings check [this](https://github.com/1ForeverHD/TopbarPlus/blob/main/src/Icon/Themes/Default.lua) page out! The only difference between this and ```TopBar.newIcon``` is that this is used to construct menus and dropdowns!


Example:
```lua
local API = self.API;
local TopBar = API.TopBar;	
TopBar.rawIcon("Name", {
	iconText = "Hello",
	iconBackgroundColor = Color3.fromRGB(96, 255, 122)
});
```
### Functions



#### chainFunction 

```lua
Any:ChainFunction(Icon,function(icon))
```
*Icon* - ```icon instance``` pass ```TopBar.rawIcon``` when making menus and dropdowns, when not making a dropdown or a menu pass as ```nil```

*function(icon)* - ```function``` make your own code here, use ```icon``` to change anything with your current icon

Adds a function to the constructed icon. The argument ```icon``` acts as the icon constructed previously, to manipulate anything make sure you use that argument.
Check [this](https://1foreverhd.github.io/TopbarPlus/api/icon/) for any methods, that are not included in this API! All methods from the library are compatible with the ```icon``` argument! This can also change any setting nessessary all you need to do is ```icon:AnyMethodFromTopBarHere!()```

Example: 
```lua
local API = self.API;
local TopBar = API.TopBar;
local new = TopBar.newIcon("Name",{iconText = "hi"});
new:chainFunction(function(icon)
	icon.toggled:Connect(function()
		print("hello");
	end);
end);
```
Example 2:
```lua
local API = self.API;
local TopBar = API.TopBar;
local new = TopBar.newIcon("Name",{iconText = "hi"});
new:chainFunction(function(icon)
	icon:setMid();
end);
```
Example 3(Unchained):
```lua
local API = self.API;
local TopBar = API.TopBar;
local new = TopBar.rawIcon("name1", {iconText = "hi"});
TopBar:chainFunction(new, function(icon)
	icon.toggled:Connect(function()
		print("hi");
	end);
end);
```

### Methods


#### notifyUser

```lua
Any:notifyUser(Icon)
```
*Icon* - ```icon instance``` pass in an icon if you are trying to send an notification to an icon made from ```TopBar.rawIcon``` otherwise set it to nil.=

Creates a small bubble on the parented icon. If used on a certain icon of a dropdown or a menu it will also show the bubble on that specific icon.

Example(Non-Menu):
```lua
local API = self.API;
local TopBar = API.TopBar;
local new = TopBar.newIcon("Name",{iconText = "hi"});
part.Touched:Connect(function(victim)
	new:notifyUser();
end)
```
Example(Menu):
```lua
local API = self.API;
local TopBar = API.TopBar;
	local new = TopBar.newIcon("Name",{iconText = "hi"});
--//Dropdown
new:createDropdown({TopBar.rawIcon("name1",{iconText = "hi"}),
	TopBar.rawIcon("name2", {iconText = "no"})});
--//Notification to icon text no 	
local current = TopBar:retrieveIcon("name2")
part.Touched:Connect(function()
	TopBar:notifyUser(current);
end);
```
___
#### retrieveIcon
```lua
local icon = TopBar:retrieveIcon(name)
```
*name* - ```string``` pass in a name of any icon made

Returns an icon with the name that was passed in 

Example:
```lua
local current = TopBar:retrieveIcon("name2")
part.Touched:Connect(function()
	TopBar:notifyUser(current);
end);
```
___
#### createDropdown
```lua
Any:createDropdown(Icon, {})
```
*Icon* - ```icon instance``` pass in a custom icon to be the parent, if you want to use an icon made from ```TopBar.newIcon``` simply chain it by doing ```new:createDropDown(nil, {})```

*{}* - ```table``` pass in multiple of new icons using ```TopBar.rawIcon```, bare in mind ```TopBar.newIcon``` will not work with this

Creates a dropdown menu using all the ```TopBar.rawIcon``` from the ```children``` table(*{}*)

Example 1(Chained):
```lua
local API = self.API;
local TopBar = API.TopBar;	
	
local new = TopBar.newIcon("Name",{iconText = "hi"});
new:createDropdown({TopBar.rawIcon("name1",{iconText = "hi"}),
TopBar.rawIcon("name2", {iconText = "no"})});
```
Example 2(Unchained):
```lua
local new = TopBar.rawIcon("hello", {iconText = "hi"});
	
TopBar:createDropdown(
	new,{TopBar.rawIcon("name1",{iconText = "yes"}),
	TopBar.rawIcon("name2",{iconText = "no"})}
);
```
___
#### createMenu
```lua
Any:createMenu(Icon, {})
```
*Icon* - ```icon instance``` pass in a custom icon to be the parent, if you want to use an icon made from ```TopBar.newIcon``` simply chain it by doing ```new:createDropDown(nil, {})```

*{}* - ```table``` pass in multiple of new icons using ```TopBar.rawIcon```, bare in mind ```TopBar.newIcon``` will not work with this

Creates a menu using all the ```TopBar.rawIcon``` from the ```children``` table(*{}*)

Example 1(Chained):
```lua
local API = self.API;
local TopBar = API.TopBar;	
	
local new = TopBar.newIcon("name", {iconText = "hi"})
	
new:createMenu(nil, {
	TopBar.rawIcon("name2", {iconText = "no"})
});
```

Example 2(Unchained):
```lua
local API = self.API;
local TopBar = API.TopBar;	
	
local new = TopBar.rawIcon("name", {iconText = "hi"})
	
TopBar:createMenu(new, {
	TopBar.rawIcon("name2", {iconText = "no"})
});

```



## Bezier 


## Tween
API Section for Tween.
!!! info "To use this use the following API table"
    ```lua	
    local API = self.API;
    local Tween = API.Tween
    ```

### Constructors

#### new
```lua
local new = Tween.new({})
```
*{}* - ```table``` pass in the data for the tween to use. [BoatTween](https://devforum.roblox.com/t/boattween-module/540277) has many new styles to pick and choose from, they can he found [here](/site/TweenStyles)

Creates and returns a new tween from all the setting passed into ```{}```

Example -
```lua
local API = self.API;
local Tween = API.Tween;	
local part = workspace.Part;
	
local new = Tween.new({
	obj = part, --This is the instance you want the tween to be aplied to, this can be anything from parts to ui.
	numTime = 20, --This is how long the tween will take place(in seconds).
	easingStyle = "Quint", --This is a style your tween will take.
	easingDirection = "Out", --This is a direction your tween will take.
	reverse = false, --This is an option to make the tween go back to it previous state(before the tween took place).
	delayTime = 10, --This is a time before the tween will play from being called using void:play().
	repeatCount = 0, --This is how much times your tween will be repeated.
	stepType = "Heartbeat", --This is when your tween will be played. Check TweenStyles for more info on these!
	goal = {Transparency = 1;} --This is what you want the tween to do, there can be multiple things the tween does at once.
});
```

### Methods

#### play
```lua
new:play()
```
Plays a created tween.

Example-
```lua
local API = self.API;
local Tween = API.Tween;	
local part = workspace.Part;
	
local new = Tween.new({
	obj = part, --This is the instance you want the tween to be aplied to, this can be anything from parts to ui.
	numTime = 20, --This is how long the tween will take place(in seconds).
	easingStyle = "Quint", --This is a style your tween will take.
	easingDirection = "Out", --This is a direction your tween will take.
	reverse = false, --This is an option to make the tween go back to it previous state(before the tween took place).
	delayTime = 10, --This is a time before the tween will play from being called using void:play().
	repeatCount = 0, --This is how much times your tween will be repeated.
	stepType = "Heartbeat", --This is when your tween will be played. Check TweenStyles for more info on these!
	goal = {Transparency = 1;} --This is what you want the tween to do, there can be multiple things the tween does at once.
});
new:play(); -- :play() needs to be connected to a Tween.new() constructor via the new variable(This variable can be changed just make sure to connect :play() to it!)
```


## Roact


## Promise
