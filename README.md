SPELUNKY CLASSIC FOR MIYOO MINI+ (ONION OS)
Unofficial port - version 1.0
============================================================

Spelunky Classic running natively on the Miyoo Mini+ under Onion OS,
launched from the PORTS menu. You do not need any game files: the art and
sound are inside the game.

This is a free, non-commercial fan port. It is not affiliated with or
endorsed by Derek Yu or Mossmouth. It is based on the open-source
"spelunky-psp" project by dbeef, a C++ rewrite of Spelunky Classic. Port by
@AUTHOR@.


TESTED ON
---------
Miyoo Mini+ with Onion OS. Other Miyoo Mini models and other
devices have not been tested.

You need a PORTS section in Onion's menu. If your card does not have one,
add it first (from Onion's package manager).


INSTALL
-------
1. Extract the zip.
2. Copy the "Roms" folder onto the root of your SD card, merging it with the
   Roms folder that is already there.
3. Put the card back in the Mini+ and open PORTS. If Spelunky is not listed,
   run "Import ports" (it may be shown as ~Import ports) once, then look
   again.
4. Launch Spelunky.

To update: copy the new files over the old ones. Your stats (stats.txt) and
button layout (controls.txt) in the game folder are kept.


WHERE THINGS LIVE ON THE SD CARD
--------------------------------
Roms/PORTS/Games/Spelunky/
    spelunky          the game itself
    launch.sh         starts the game and writes log.txt
    config.json       descriptive info (label, description)
    lib/              libraries the game brings with it
    README.txt        this file
    LICENSES.txt      credits and licenses
    log.txt           created on every run (safe to delete)
    stats.txt         your saved statistics (created by the game)
    stats_backup.txt  copy of your stats made just before a reset
    controls.txt      which button does what (created by the game, editable)

Roms/PORTS/Shortcuts/Spelunky.port
    The menu entry. It is a small shell script that runs launch.sh.


CONTROLS
--------
D-pad left/right ... move
D-pad up ........... climb up / look up
D-pad down ......... climb down AND duck
A .................. jump
B .................. whip / attack
X .................. bomb
Y .................. rope
R1 and R2 .......... run
L1 ................. buy / accept in shops
L2 ................. duck
START .............. pause
SELECT ............. request death (KILLS your character - avoid mid-run)
MENU ............... quit request (from the pause / title screen)


REMAPPING THE BUTTONS
---------------------
The first time the game starts it writes controls.txt into the game folder
with the layout above. Open it in Notepad to change which button does what:
one line per action, for example "run = R1, R2". Actions: jump, whip, bomb,
rope, run, duck, buy, pause, death, quit. Buttons: A, B, X, Y, L1, L2, R1, R2,
START, SELECT, MENU. The D-pad cannot be changed. Delete controls.txt to get
the defaults back.

To swap the L and R buttons (L1 <-> R1 and L2 <-> R2) without editing
anything, create an empty file named swaptriggers in the game folder. With
it, L1 and L2 run, R1 buys and R2 ducks. The button names shown in on-screen
prompts follow the swap. Delete the file to undo it.


LADDERS, ROPES AND LEDGES
-------------------------
- The platform at the top of a ladder is solid when you land on it from
  above. You can still climb up through it from below.
- Standing on that platform and pressing D-pad down (lined up with the
  ladder) steps you onto the ladder and climbs down. This also works while
  running: press down as you cross the ladder. Holding down before you get
  there makes you crawl instead.
- On a ladder or rope, hold LEFT or RIGHT and press B to whip to that side
  while staying on the ladder. You stay still until the swing ends, then you
  can carry on climbing. Holding only up or down does nothing for B. If you
  are carrying an item, B throws the item first.
- While hanging from a ledge: A jumps off, D-pad down + A lets you drop, and
  B (whip) also drops you.


STATISTICS
----------
The score screen (the Scores door on the title screen) shows six numbers:

    Top Defilers: Money, Kills, Saves    best single run
    Statistics:   Plays, Deaths, Wins    totals

They are saved in stats.txt and kept between play sessions.
- Plays goes up each time you walk through the Start door.
- Deaths goes up when you die. Quitting in the middle of a run is not a death.
- Money, Kills and Saves keep your best single run, compared when you die.
- Saves counts each damsel you carry out through the exit.
- Wins stays at 0 (this version has no ending).

Resetting: on the score screen, stand next to the RESET sign and whip it
once. The sign starts to blink for about 15 seconds. Whip it again while it
is blinking and the death sound plays, your stats are cleared and the numbers
on the screen drop to zero. If the 15 seconds run out, the sign goes back to
normal and it takes two whips again. Leaving the room also starts it over.
The old numbers are copied to stats_backup.txt first (only the most recent
copy is kept, and nothing is copied if the stats were already all zero).
To reset by hand, delete stats.txt.


OPTION FILES
------------
Create an empty file with one of these names (no extension) in
Roms/PORTS/Games/Spelunky/ to change how the game runs. Delete the file to
undo it.

    widescreen   16:9 picture with black bars instead of full 4:3
    swaptriggers swap L1 <-> R1 and L2 <-> R2 (see REMAPPING THE BUTTONS)
    noaudio      start with sound turned off (use if audio start-up crashes)
    nofast       use slower, exact drawing for everything (troubleshooting
                 odd-looking sprites; the game runs noticeably slower)
    oldtiming    use the original frame timing (SDL_Delay) instead of the
                 precise wait loop (troubleshooting only)


WHAT WAS CHANGED FROM THE ORIGINAL PROJECT
------------------------------------------
- A new "Miyoo" platform (SDL 1.2, software drawing, Mini+ buttons).
- Title screen, stage-complete screen and score screen: four extra rows of
  dirt (with some gold-flecked blocks) so the 4:3 picture is filled.
- Score screen and stage-complete screen: text is placed for the 16:9 design
  height so it stays inside the black boxes.
- The title screen no longer lets you spend bombs and ropes: they are locked
  at zero there and set to the normal 4 each when a run starts.
- Statistics saved between sessions, with a working Reset sign.
- Sprites that are not 16x16 (taller climbing frames, wider crouch frames)
  are drawn at their real size instead of being squashed into a square.
- Icons on the stage-complete screen no longer flicker (the sprite draw
  order is now stable).
- Frame timing: the game waits with a short loop, because SDL_Delay on this
  device oversleeps and made movement feel loose.
- Ladder platforms are one-way floors; step down onto the ladder with
  D-pad down; whip sideways while on a ladder or rope.
- Ledges: D-pad down + A lets you drop from a hang.
- Buttons can be remapped with controls.txt, with a simple L/R swap option.
- Pressing down while running across a ladder platform steps onto the ladder.
- On a ladder or rope, items (guns, etc.) now work facing right: the held
  LEFT/RIGHT button sets which way you face.
- Items from crates appear at your feet instead of above you (no more items
  stuck in walls). The pop-up animation is unchanged.
- Chests, idols and other items dropped in a tight space (blocks above and
  below) are put at your feet instead of inside the wall.
- The music now repeats instead of stopping after one play, and the title
  music stops when a run starts.


KNOWN LIMITATIONS
-----------------
These come from the base project, which is unfinished:
- Only the first area (the Caves) exists. After level 4 the game keeps
  making cave levels; there is no second area.
- The intro and the tutorial are not playable.
- Grabbing the golden idol does not set off the traps.


TROUBLESHOOTING
---------------
- The game closes straight away: open Roms/PORTS/Games/Spelunky/log.txt.
  The last lines show how far it got.
- No sound, or a crash while audio starts: use the "noaudio" file.
- Odd-looking sprites: try the "nofast" file to see whether the fast
  rectangle drawing is involved.
- Stats look wrong: close the game, look at stats.txt (plain text, one
  "name number" pair per line), or delete it to start fresh.


SOURCE CODE
-----------
The complete source code of this port, with the changes listed above, is
published together with this download in the file
Spelunky-Miyoo-Mini-v@VERSION@-source.zip. It includes build notes
(BUILDING.txt).


CREDITS AND LICENSE
-------------------
- Spelunky Classic was created by Derek Yu (Mossmouth).
- spelunky-psp, the rewrite this port is based on, is by dbeef.
- Miyoo Mini build environment: union-miyoomini-toolchain (Shaun Inman).
- Onion OS: the OnionUI project.
- Port to the Miyoo Mini+: Chawinyaw

See LICENSES.txt for the licenses. In short: the code is under the GNU GPL,
and the Spelunky Classic art and sound are used under the Spelunky User
License, which allows free use but not for profit.
