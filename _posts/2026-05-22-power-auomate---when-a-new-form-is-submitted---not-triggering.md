---
layout: single
date: 2026-05-27
categories: PowerAutomate
---
Scenario: User set up a Power Automate flow 100% correctly, standard:

- When a new form is submitted
- Get Form Details
- Do Stuff

However, when it came to testing the MS Forms submission was not triggering and all form submissions weren't being triggered. Very annoying.

Did the standard:

- Log in and log out
- Turn flow off and on
- Re-point the form Ids to a different form, save, switch back, save

Nothing.

Solution:

1. Open the MS Form directly
2. Copy the form ID (All the text after 'id=')
3. Open Power Automate and edit the trigger and first action:
	1. Where you specify the form name, click "enter custom value"
	2. Paste the form id into the custom value
4. Test and save.

Magic. Power Automate is weird sometimes.