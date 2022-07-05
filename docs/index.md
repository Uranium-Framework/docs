## Introduction
Welcome to the official website for Sunrise Framework, if you are looking for a documentation on how to use the framework you are in the correct place! Anyways lets get this doc started! You can find what you are looking for in the [Getting Started](#getting-started) section!

!!! note
    To find these extensions, you can either visit our discord or find some <span style="color:red">**creator**</span> verified ones [here](/site/Releases/#community-extensions)

### **Getting started**
[Installation](#installation)

[Documentation](/site/Documentation)

[API References](/site/API/)

[Releases](/site/Releases/#latest)


### **What is Sunrise Framework?**

### **Why Sunrise Framework?**


## Installation
There are multiple ways to install Project Sunrise! Read on to find out all of the current methods:

!!! warning "Make sure to get the libraries and The Project Sunrise it self from the marketplace!"
    While not all methods require roblox asset insertion it is still recommended to get the [libraries](https://www.roblox.com/library/9118715085/SunriseLibs) as well as the [framework](https://www.roblox.com/library/9028757712/Project-Sunrise) it self just incase you wish to use the commands that come with the framework!
____
### **Roblox Marketplace**
You can pick up the module from the [Roblox Marketplace](https://www.roblox.com/library/9028757712/Project-Sunrise). While this is a good method of installation, you have to place everything in the correct places on your own. Please refer to the [docs](/site/Documentation#) in order to place everything correctly!

### **Bootstrapper**
____
A good and easy way to install Project Sunrise is to use the following code into the roblox command bar, this however may have some complications as stated below!.
```
local httpservice = game:GetService("HttpService") local enabled = httpservice.HttpEnabled httpservice.HttpEnabled = true loadstring(httpservice:GetAsync("https://raw.githubusercontent.com/SyntalDev/Project-Sunrise/main/install.lua"))(enabled)
```  
!!! danger "Some manual action required"
    This method requires you to simply purchase(<span style="color:red">**THIS DOES NOT COST ANYTHING!**</span>) our [libraries](https://www.roblox.com/library/9118715085/SunriseLibs) model. Otherwise the framework will not have any libraries!
  


