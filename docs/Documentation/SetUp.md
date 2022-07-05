## Setup

### **Roblox Marketplace Install**
One of the main installation methods is the [marketplace](https://www.roblox.com/library/9028757712/Project-Sunrise) however you need to place everything in the correct place! No worries the image below will show you just where everything is!

## Settings

Settings are used to customize your experience with Project Sunrise.

### **Knit Usage**

This framework can also be used with [Knit](https://sleitnick.github.io/Knit/docs/intro). In order to use Knit, you will need to turn the <span style="color:grey">**isUsingKnit**</span> option to true.
Example:
```lua
local settings = {
	isUsingKnit = true;
    --... Other Settings
}

return settings
```

### **Extension**

Extensions are an organized way of requiring our libraries. They help avoid the hassel of having to require modules for every script. In order to Initialize an Extension you must use the Exends table inside of Settings.

```lua
local settings = {
	--... Other Settings
	Extends = {
		ExampleExtension = true; -- "true" means Client Exposed, "false" means only Server
	};
}

return settings
```

## API Usage

This section explains how to use and modify Project Sunrise to help developers customize the framework to their wants and needs.

### **Expansions**

Expansions are used as scripts, they help to organize the workspace evnironment. You can make an expansion by using our plugin or use this template:

```lua
local self = {
	Name = "test2", -- The name of the expansion
	LoaderVersion = "1.0.0", -- Version of the Framework Loader
	Path = "Server", -- "Server", "Client", or "Both"
    Extends = {
        Print = true; -- ["NameOfLibrary"] = true
    } -- Extensions
};

function self:Execute() -- Runs Automatically
	print("Hello World");
end;

return self;
```

As in the Extensions Catagory, we have had to initialize the etxensions. Now we need to tell our handler that we want to use an extension in our expansion. Therefore, we need to make another Extends table in our Expansion, as seen above.

### **Using the API**

Like any other framework Project Sunrise has a nicely constructed API, but to actually use it we need to first get it into our expansion, the example below will show you a couple of methods how you can get the API into your expansion.

```lua
local self = {
	Name = "test2", -- The name of the expansion
	LoaderVersion = "1.0.0", -- Version of the Framework Loader
	Path = "Server", -- "Server", "Client", or "Both"
    Extends = {
        Print = true; -- ["NameOfLibrary"] = true
    } -- Extensions
}

function self:Execute()
	local API = self.API.*YourTableHere* --Our API is separate into multiple tables, each table and its function will be provided in
	--API References! 
	API:APIFUNCTIONHERE() --This will run a certain function within the table of the API
	self.API.*YourTableHere*:APIFUNCTIONHERE() --This is another way you can run an API function, this does not use a variable!
end

return self
```
!!! Info "The self keyword"
    As you can see we use the <span style="color:red">**self**</span> keyword. What this does is it allows to pull any external sources like the API or Extensions
