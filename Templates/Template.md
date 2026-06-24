---
layout: single
date:
categories:
classes: wide
keywords:
  - 
  - 
  - 
title:
---
<%*
// Pops up an interactive box so you can type the title on creation 
let cleanTitle = await tp.system.prompt("Enter Post Title:");
if (!cleanTitle) cleanTitle = "untitled"; 
let slug = cleanTitle .toLowerCase() .replace(/[^a-z0-9\s-]/g, '') .replace(/\s+/g, '-'); 
let datePrefix = tp.file.creation_date("YYYY-MM-DD"); // Renames the file immediately to the web-safe slug 
await tp.file.rename(datePrefix + "-" + slug);
-%>