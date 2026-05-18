---
layout: single
date:   2013-06-28 13:21:00 +0100
categories: Dynamics CRM
tags: [DynamicsCRM]
---

THe benefit of having a development environment which only I touch means I can break code whenever I want. It allows me to see what happens when I try and convert client side code (JS) to server side (C#) or to see if I can optimise anything I’ve done.. I’ve hit the “**Error registering plugins and/or workflows. Plug-in assembly does not contain the required types or assembly content cannot be updated.**” error more than once though. Usually after I create a new plugin to an existing solution, deploy it, realise it’s not needed, remove it then redeploy..

The way I tend to stop this from happening is as followed..

Delete plugin assemblies from CRM.  
Remove class from solution.  
Remove the corresponding plugin section from “RegisterFile.crmregister” file (and save)  
Build solution.  
Redeploy solution.

This probably isn’t the best way of doing it (NOT A DEVELOPER) but that’s how I’ve figured it out so far..

EDIT: If I find the proper way of doing this (I imagine it’s going to be something silly, I’ll update)