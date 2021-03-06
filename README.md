Compatibilty issue with the About Face module and Melee attack animations. Melee attack animations utilize the drawTowards function from FX Master, and About Face mars up the token size. I'll log an issue with FX Master to see if this can be fixed. In the meantime, if you want to fix this on your game you can make the following change in the FXMasterLayer.js file:

**Implement at your own risk**

change line 133 from:  
effectData.distance = Math.sqrt(deltaX * deltaX + deltaY * deltaY) - (1 - effectData.anchor.x) * tok2width;  
to  
effectData.distance = Math.sqrt(deltaX * deltaX + deltaY * deltaY) - (1 - effectData.anchor.x) * tok2.data.width * canvas.grid.size;  

Thanks Kandashi for finding the problem and solution.

Additionally, you have the option for the macros in the "On-Use Only Macro" compendium to always have the animations play, or to only play on hits. Currently they are all set to play on every attack. If you would like to change them to ONLY play on Hits, find this line about 2/3 down in the macros:  

var myStringArray = lastArg.targets;

and change it to:

var myStringArray = lastArg.hitTargets;

## UPDATE NOTES
0.1.3
**NOTE** Moved the Token Magic effects around on some of the code so if you're using it to apply to Hit Targets, or not play on misses, it won't apply the Token Magic FX if the animation doesn't play

2. Added a check and switch to all macros that are also available in the Free JB2A module, so free users don't have to modify anything to get them to run. This includes all macros in the "On-Use Only Macro" compendium

2. AllMeleeAttacks Macro:

- Changed code so your token doesn't need to be selected when attacking
- Removed Dagger, Handaxe and Spear (moved to Melee-Range-Switch macro)
- Add check on actor for the Improved Divine Smite feature, and activates a small blue explosion on hit if found

3. AllRangedWeapons Macro:

- Removed Dagger, Handaxe and Spear (moved to Melee-Range-Switch macro)

4. Melee-Range-Switch Macro:

- Fully updated for use with the Dagger (all 3 thrown variants), Handaxe and Spear with TMFX.

5. AllAttackSpells:

- Added a save check, so spells in this macro that require a save will not play Token Magic FX on a successful save

Updated the PDF tutorial for using the following macros:
1. AllMeleeAttacks: All Melee Weapon attacks by JB2A
2. AllRangedWeapons: All Ranged Weapon attacks by JB2A
3. Melee-Range-Switch: All Melee/Range Weapons by JB2A (Dagger01, Dagger02, Kunai, Handaxe, Spear). Switches between melee and range based on distance to target
4. AllAttackSpells: All Attack Spells by JB2A minus Magic Missiles
5. AllCreatureAttacks: Bite and Claw attacks by JB2A

Moving forward, I'll still be updating macros as needed and adding new ones for future releases of JB2A content. However, I'm working on a separate module now that will run all this silly stuff from the background without needing to go and add macros to all of the items. If anyone wants to help alpha test it let me know and I'll get you the info, it should be ready for testing mid next week.


0.1.1

2. I've fixed all of the macros for the new naming convention adopted by JB2A.

2. I fixed the typo in the Thunderwave Macro
 
3. New macros to cover all the great new colors in the latest JB2A release for melee weapons

4. Added a new Compendium: On-Use Only Macros
   
   The macros in this new compendium will NOT work from the macro bar. They are only for use with the On-Use macro field from Midi-QOL.
   Requires: Token Magic FX, FX Master, Midi-QOL, The Furnace
   
   These new macros read the Item Name and Source Field for each item using it.
   
   ![Alt text](pictures/NameAndSource.PNG)
   
   Example:
   
   AllMeleeAttacks is the macro we will use. Use this as the On-Use Macro. When activated it will parse the Name and Source information for that item to pull the correct animation. Let's use a Greataxe as an example:
   
    ![Alt text](pictures/NameAndSourceExample.PNG)
   
   Here you see the name Greataxe is in the Name field, and I've put Purple into the source field. When I attack with the weapon it will activate the Purple Greataxe animation.
   Had I left the source field blank, it would use the standard Greataxe animation.
   
   
   The SAME goes for all macros in this compendium.
   
   1. AllAttackSpells
      Works for: Fire Bolt, Ray of Frost, Witch Bolt, Scorching Ray, Disintegrate
      For these, just put the color you want in the source field since it will recognize the spell name
   2. AllMeleeAttacks
      Works for all released JB2A melee animations. Use either the Name or Source field to use what animation you want.
      Such as: Sword Blue, Mace Red, Handaxe green, etc etc
   3. AllRangedWeaponsMacro
      Works for all the ranged weapon attacks just like the Melee

I've created a quick PDF tutorial for how to use the 3 big macros in the new compendium. Check it out here:
https://github.com/otigon/otigons-animation-macros/blob/main/PDF/On-Use%20Only%20Macro%20Compendium%20Tutorial.pdf

# otigons-animation-macros
This is a collection of Macros I've made for use with the JB2A Animations Patreon Module. These are based on the D&D 5e system, but can be used for other systems as well.

Credit goes to the following for helping with many of these:
- JB2A (check them out on Patreon: https://www.patreon.com/JB2A )
- Kandashi (Check out Kandashi's highly effective modules such as Next Up, DAE SRD, Active Auras, and more!. (https://www.patreon.com/Kandashi)
- Lazytron
- Crymic (Check out some incredible macros https://www.patreon.com/crymic)
- Freeze
- Enso
- FXMaster
- Token Magic FX
- and many others

# Installation
Currently this will only be availble thru manual installation. I have no current plans to issue this through Foundry

To install this module manually: 

1. Inside the Foundry "Configuration and Setup" screen, click "Add-on Modules"
2. Click "Install Module"
3. In the "Manifest URL" field (bottom) paste the following url: https://github.com/otigon/otigons-animation-macros/releases/latest/download/module.json
4. Click "Install" and wait for installation to complete
5. Don't forget to enable the module in game using the "Manage Module" button

## About the Macros
99% of these macros will function with just **Midi-Qol**, **JB2A Patreon module** and **FXMaster**. The Furnace is suggested, and I will be uploading a new compendium in the following week that utilizes Midi-Qol automation to help run the animations.

The Compendiums in this module are separated as such:
1. Spell Animations
2. Ranged Weapon Attacks
3. Melee Weapon Attacks
4. Explosions
5. Miscellaneous

These are all written for the Patreon version of JB2A. To use with the Free module version, you'll need to edit the macro to point to the correct folders. Usually this is written like:

let file = "modules/jb2a_patreon/......

Just change the jb2a_patreon to the file name for the free version and you're good to go

## Fun Add-Ons

For further fun I have added the following to all of the macros:
**NOTE**: THESE ARE INACTIVE (commented out) and will need to be activated to use

1. Audio: Each has a section to add an audio path and file to play a sound effect along with the animation. Some even have a randomizing audio call to switch up the sounds.

2. Token Magic FX: I have added in some fun Token Magic FX (requires module) that can be activated to give more 'oomph' to the effects. I left these inactive for now, but may activate them on a later release depending on feedback. They really are fun!

## How to Use these Macros

Most every macro can be used without attaching it to an item/spell. They can sit in the macro bar and be used at-will.
For use in conjuction with an item/spell, instructions are as follows:

Bare Minimum Instructions for use:
**NOTE** 1st check out the Tutorial video by JB2A that gives a good run down of how to use these types of macros: https://www.youtube.com/watch?v=264xZJjPHD8 

1. In the Midi-Qol workflow settings, at the very bottom, is a check box for "Add macro to call on use". Ensure this is checked

2. This activates a new fillable field "One Use Macro" in the item/spell details page, also at the bottom.

3. Import whichever macro you would like to use into your world.

4. Add the name of the macro you would like to use in the "On Use Macro" field. This MUST match exactly the name of the macro (case sensitive). I suggest copy/pasting from the macro to ensure no errors are made.

Now you're ready to go!

Whenver you use the item/spell, it will call the macro once the damage is rolled. **For 99% of these, you will need to have a target(s) Targeted, and the casting/hitting token Selected**. Some have options to play the animation on the "selected" token instead of the targeted token, such as the Explosions in the Explosions Compendium.

## How to Activate Sounds or TMFX codes

In progress

In almost every macro there is a section for adding Token Magic FX. This is noted at the start of the inactive code by something like: Delete comments to activate Token Magic FX code. This does requires the TMFX module to be installed and activated.

**NOTE** You will need to enable "Permissive Mode" from the Token Magic FX module settings to allow players to apply the TMFX filters

To activate the code, delete the /\*  at the start of the code, and then the \*/ at the end.
For example you would delete the start of the comment out:

![Alt text](pictures/ActivateTMFX01.PNG)

Next you need to look for the end comment after the TMFX Code and delete that as well

![Alt text](pictures/ActivateTMFX02.PNG)

A few macros also have additional inactive code at the end that will need to be activated for TMFX. This will remove the effects after a duration

![Alt text](pictures/ActivateTMFX03.PNG)


#### SOUNDS

To activate sounds, find the sound section in the code. This is usually before the Token Magic FX code. Activate by removing the comment marks as described above.

![Alt text](pictures/ActivateSound01.PNG)

Also, some have an option to use multiple sounds to randomize what is played each time the item is rolled:

![Alt text](pictures/ActivateSound02.PNG)
