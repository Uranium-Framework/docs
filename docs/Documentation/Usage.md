## Expansion usage
In Sunrise Expansion are scripts which the Sunrise loader loads.

Making expansions are very easy to add, it will also save your ServerScriptService from getting packed with scripts. Now how do you make expansions?

There are 2 methods:

The 1st method is doing the expansion manually, first you should know that only module scripts are accpeted by the loader anything else will be removed.


First open your Sunrise framework 

<img src="https://i.imgur.com/dtwnVwT.png" width="35%">

It should look something like this, this is out-of-the-box look of Sunrise.

As you can see there are a few things in the directory but we will only consentrate on ``Expansions``. Anything in the expansion folder that is a ``Module Script`` with the native Sunrise format. 

Secondly create a module script script in the ``Expansions`` folder like and name it anything for simplicity I will name it test, you should have something like this:

<img src="https://i.imgur.com/m9RA2H0.png" width="35%">

Great! Now then remember how I mentioned the Sunrise expansion format? Well now lets dive into that, open your expansion and copy and paste the following code into your expansion:

```lua
local self = {
	Name = "test", -- The name of the expansion
	LoaderVersion = "1.0.0", -- Version of the Framework Loader
	Path = "Server", -- "Server", "Client", or "Both"
    Extends = {} -- Extensions
};

function self:Execute() -- Runs Automatically
	print("Hello World");
end;

return self;
```

Looks a bit complicated right? Well let me go through what everything does and get you up to speed, lets begin

Lets go through the expansion datatable first as it is a very important part of the format

``Name`` - This is the name you want your expansion to be known as within the Sunrise runtime, each expansion will be regonised by the name you set in future updates. It is a good practice to set the name to the name you set the module script to, but hey its up to your preference!

``LoaderVersion`` - This as important as the ``Name``, but why? When Sunrise framework is first initialized the loader reads all the expansions, if the ``LoaderVersion`` is not set to the same exact version as the loader then the expansion will simply be put into containment and ignored by the framework. Bare in mind that you do not have to use the exact version of the framework all you need is simply the 3 digits in my instance of it is ``1.0.0`` but in reality the version this tutorial is taken place is ``1.0.0-alpha.1``

``Path`` - This is used to determine where your script will be ran. Sunrise loader does not load the script immediately, instead it first reads the ``Name``, ``LoaderVersion`` and ``Path`` it is then correctly placed to its desgined location and then executes the ``Execute()`` method.

I will not be covering ``Extends`` as we have a separate [tutorial](/docs/Documentation/Settings/Extends.md) for it, now then lets move onto the execution of the script and how that works.

``function self:Execute()`` - this is out executer, the framework will first check all of the data from the expansions datatable, it is after the script is on the correct path, only then ``Execute()`` will be ran.

Anything can be placed in the ``Execute()`` method, you can even do a ``PlayerAdded`` event which will then continue the script when a player joins!

``Client Trick`` - When a script is sent to run on a client, it will be placed in the playerGUI meaning you can do ``local player = script.Parent`` this will automatically get the player the script belongs to!

<span style="color:red"> Method 2 is currently in works and will not be ready till full release of 1.0.0! </span>

## API Usage
Just like any framework, Sunrise has its own [API](/docs/API/Introduction.md), this API uses other libraries to make Sunrise 10x better! In this section of the doc I will be teaching you how to use the API within your expansion in the correct way! Lets get started.

First of all open the expansion you want to use the API in, if you haven't coded anything into this expansion and you got it using a template it should look similar to mine
```lua
local self = {
	Name = "test", -- The name of the expansion
	LoaderVersion = "1.0.0", -- Version of the Framework Loader
	Path = "Server", -- "Server", "Client", or "Both"
    Extends = {} -- Extensions
};

function self:Execute() -- Runs Automatically
	print("Hello World");
end;

return self;
```
This is the same exact example like in the previous [Expansion](#expansion-usage) tutorial, remember even if you coded anything this will work the same!

Lets get started with Example 1. First we need to decide what <span style="color:orange">*table*</span> to use. What is a table? A table is a section of the API, this section holds each function for that part of the API. You can see these at the start of each API section. It will look something like the following code, let me break it down for you. 

```lua
local API = self.API;
local DataStore = API.DataStore;
```
Ok lets start with <span style="color:red">self</span>. This keyword is used to import things like the API from the loader, sounds confusing? Don't worry about this too much just know that it is used to get the API into your expansion.

Now then in the first line what you are doing is casting the API into the API variable.

In the second line we can see we use the variable *API* followed by *DataStore* now then what does this do? This will get all the functions from the *DataStore* table and cast it into the *DataStore* variable.

Ok, for example 1 I will be using the *Replica* API table. 

```lua
local self = {
	Name = "test", 
	LoaderVersion = "1.0.0", 
	Path = "Server", 
    Extends = {} 
};

function self:Execute() 
	local API = self.API; --We get the API into the API variable
    local Replica = API.Replica; --We now cast the Replica table into the Replica variable

    Replica.new({data}) --We now call the API function for Replica, all of these can be found within the API reference!
end;

return self;
```
Ok that is it for example 1, you can use any API function for *Replica* from just the *Replica* variable without having to worry about importing functions individually!

This is not all however as there is also the client API, in the example above Replica is a <span style="color:red">SERVER ONLY</span> table meaning you cannot use it on the client, however the method of getting the API has not changed!

For example 2 we will be using a client table

```lua
local self = {
	Name = "test", 
	LoaderVersion = "1.0.0", 
	Path = "Client", 
    Extends = {} 
};

function self:Execute() 
	local API = self.API; --This is exactly the same as the example above
    local icon = API.TopBar; --This gets the client Icon table

    icon.new({data}); --Use any function you want!
end;

return self;
```
Bare in mind it is not recommended to use client tables in a server expansion!

There is also the shared section which works exactly the same but can be safely used on both the client and server but I will not be getting into this!

This is it for the API section!

## Framework usage example