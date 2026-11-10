PALTALK MIC TIMER
Created in C++ by SodaDaPimp
==============================================================

A mic timer and admin helper for Paltalk chat rooms.

   - Times whoever is on the mic and shows the mic queue.
   - Posts warnings in the room as time runs low.
   - Dots people who go over the limit, explains why in the
     room, then removes the dot a few seconds later.
   - Lets your admins dot and undot from the chat with simple
     commands: !dot-nickname and !undot-nickname.
   - Posts a "mic check" if the person on the mic goes silent.


WHAT YOU NEED
--------------------------------------------------------------
- A Windows PC (Windows 10 or 11).
- The Paltalk desktop app, signed in.
- You must be an ADMIN or the OWNER of the room. The timer dots
  people the same way you do, so it needs your admin rights.

There is nothing to install. Just run the .exe.


HOW TO RUN IT
--------------------------------------------------------------
1. Open Paltalk and join your room.

2. Put "Paltalk Mic Timer Created by SodaDaPimp.exe" in its own
   folder, then double-click it.
   - If Windows says "Windows protected your PC", click
     "More info", then "Run anyway". Windows shows this for any
     new program it hasn't seen before.

3. In the timer, pick your room in the ROOM box.
   (Don't see it? Click Refresh.)

4. Click Connect.
   The timer posts a line in the room to say it is connected.

5. To stop, click Disconnect or just close the window. It
   removes any dot it is still holding and posts that it has
   disconnected.

The timer saves your settings in a file called config.json and
its logs in a folder called "logs". Both are created next to
the .exe, which is why it should live in its own folder.


FIRST-TIME SETUP  (2 minutes)
--------------------------------------------------------------
The timer starts in TEST MODE. In test mode it only shows what
it WOULD do (on the Activity tab). Nobody is dotted and no
timer messages are posted. That makes it safe to look around.

1. Click the SETTINGS tab.

2. In the ADMINS box, type your own nickname and the nickname
   of each of your admins, one per line. Spell them exactly as
   they appear in Paltalk.

3. Click "Save admins, colours & messages".

4. Set the mic time limit if you want something other than
   2 minutes (120 = 2 minutes, 180 = 3 minutes).

5. Untick TEST MODE. The timer is now live.


TRY IT FIRST (PRACTICE ROOM)
--------------------------------------------------------------
Want to see how it works without a real room?

1. In the ROOM box choose "Practice room (no Paltalk needed)".
2. Click Connect. A Practice window opens.
3. Pick a pretend person and click "Take mic".
4. Watch the timer count, warn, dot, explain and undot.

Tip: set the time limit to 30 seconds on the Settings tab to
watch the whole cycle quickly.


WHAT IT DOES IN THE ROOM
--------------------------------------------------------------
When someone takes the mic:
   "[Name] has taken the mic. Allocated time: 2 minutes."

Every 30 seconds:
   "1 minute remaining for [Name]."

Near the end:
   "10 seconds left! Please wrap up and pass the mic."

At the limit there is a 5 second grace period. If they are
still on the mic after that, the timer dots them, explains why
in the room, and removes the dot a few seconds later.

Admins on your list are never timed or dotted.

If the person on the mic is silent for 15 seconds, it posts a
mic check ("dead air").

When it connects and when it disconnects, the timer posts a
credit line. This is built in and cannot be switched off.


ADMIN COMMANDS
--------------------------------------------------------------
Admins on your list can type these in the room:

   !dot-nickname       dots that person
   !undot-nickname     removes the dot

Example:   !dot-BigMike

- A dot given by command stays until an admin removes it.
- Admins cannot be dotted by command.
- Anyone who is not on the admins list gets a short reply
  saying only admins can use the commands.
- The command must be the whole message. A sentence that only
  mentions !dot is ignored.
- There is no cooldown on these commands.


USEFUL SETTINGS  (Settings tab)
--------------------------------------------------------------
COMMANDS ONLY    Turns off the timer and all alerts. Only !dot
                 and !undot keep working.
TEST MODE        Shows what would happen without doing it.
Dead air check   Turn the silent-mic warning on or off.
Explain / undot messages
                 Turn the "why you were dotted" and "dot
                 removed" posts on or off.
Timing           Change the limit, warning time, grace period
                 and how often the time remaining is posted.
Room messages    Change the wording of any message. Leave a box
                 empty to stop that message from posting.
Keep on top      Keeps the timer window above other windows.

Settings save automatically. Admins, colours and messages save
when you click "Save admins, colours & messages".


IMPORTANT WHILE IT IS RUNNING
--------------------------------------------------------------
- Keep the Paltalk room window open and not covered by other
  windows. The timer right-clicks names in it to dot people.
- When it dots or undots someone, your mouse moves by itself
  for a second or two. Let it finish.
- The dead air check listens to the level of the sound playing
  on your PC. It does not record anything. Music or a video
  playing on your PC counts as sound.


IF SOMETHING GOES WRONG
--------------------------------------------------------------
"No Paltalk rooms found"
   Join the room in Paltalk first, then click Refresh.
   If Paltalk was started as administrator, right-click the
   timer .exe and choose "Run as administrator" too.

It doesn't dot anyone
   - Make sure TEST MODE is unticked.
   - Make sure you are an admin in the room.
   - Make sure the Paltalk room window is visible on screen.

!dot or !undot is ignored
   The person typing it must be on the ADMINS list, spelled
   exactly as in Paltalk. Click Save after changing the list.

Nothing shows under "On the mic"
   Click the TOOLS tab and click "Read the room now". If it
   reports a problem, click "Run diagnostics".

Still stuck
   Click the TOOLS tab, click "Run diagnostics", and send the
   report file plus the newest file from the "logs" folder to
   SodaDaPimp.


--------------------------------------------------------------
Paltalk Mic Timer - Created by SodaDaPimp
This is an independent tool and is not made by or affiliated
with Paltalk.
