# PALTALK MIC TIMER 2.0

**A Windows mic timer, mic queue and auto-dot tool for Paltalk room admins. Written in C++.**

![Platform: Windows 10 and 11](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078D6)
![Language: C++17](https://img.shields.io/badge/language-C%2B%2B17-00599C)
![Made for Paltalk room admins](https://img.shields.io/badge/made%20for-Paltalk%20admins-C81E2D)

![Screenshot of PALTALK MIC TIMER 2.0](https://github.com/SodaDaPimp/PALTALK-MIC-TIMER/blob/main/My%20Snapshot_3.jpg?raw=true)

## Table of contents

* [What it does](#what-it-does)
* [Changelog](#changelog)
* [What you need](#what-you-need)
* [Quick start](#quick-start)
* [What happens during a turn](#what-happens-during-a-turn)
* [The main window](#the-main-window)
* [Settings, one by one](#settings-one-by-one)
* [Admin commands](#admin-commands)
* [Sounds](#sounds)
* [Tools tab](#tools-tab)
* [Troubleshooting](#troubleshooting)
* [Build from source](#build-from-source)
* [Credits and disclaimer](#credits-and-disclaimer)

## What it does

PALTALK MIC TIMER 2.0 keeps a Paltalk voice room fair. It watches who is on the mic, times each turn, warns people as time runs out, and **dots** (restricts) anyone who goes over the limit. It tells the room why, then takes the dot off a few seconds later. It also shows the mic queue, plays sound effects (a bell when time is up, and more), and lets your admins dot and undot from the chat by typing `!dot-nickname` and `!undot-nickname`.

**Dotting** is Paltalk's **Restrict** option on a member's right-click menu; **Remove Restrictions** undoes it. The timer uses both for you.

* Times whoever is on the mic and shows the mic queue.
* Posts a time check, a final warning and a time's-up message in the room.
* Dots people who go over the limit, explains why in the room, then removes the dot.
* Keeps the mic queue in order and dots anyone who takes the mic ahead of people still waiting, so the next person in line can talk.
* A **Free mic** switch turns the timer off for everyone: no time limit, no warnings, no dots. With it off, three rules for **who may take the mic**: no jumping the line, only people in the queue, or strict (everyone who takes the mic without being in the queue is dotted, even on a free mic). Each rule includes the one before it, and whoever is dotted is told why in the room.
* Lets admins dot and undot from the chat with `!dot-nickname` and `!undot-nickname`.
* Posts a mic check if the person on the mic goes silent.
* Shows an animated poster card in the banner. Use the built-in waving-flag poster, **your own picture (a GIF, PNG or JPG)**, or switch it off.
* Plays sounds on your speakers and, if you set it up, into the room. It can even click Paltalk's mic button for you to do that.
* One small program. Nothing to install.

## Changelog

This is everything that changed from the original Python program (version 1.x) to **2.0**: what was added, what was changed and what was fixed. 2.0 is a complete rewrite in C++, so it is one small program with nothing else to install. Your old `config.json` is converted automatically and keeps working the way it did.

Jump to: [Added](#added-in-20) | [Changed](#changed-in-20) | [Fixed](#fixed-in-20) | [Upgrading from 1.x](#upgrading-from-1x)

### Added in 2.0

**The program**

* **Rewritten in C++.** A native Windows program in one small `.exe`. No Python and nothing to install.
* **A practice room.** Choose *Practice room (no Paltalk needed)* in the Room box and press **Take mic** for a pretend person, to watch a whole turn in seconds (set the limit to 30 seconds to make it quicker).
* **Automated tests.** 334 tests run the timer against a pretend Windows and a pretend Paltalk, so the rules (turns, dots, the queue, sounds, settings, pictures) can be checked without a real room. Run them with `sh run_tests.sh` on Linux, macOS or WSL.
* **A redesigned window:** a photo background with frosted-glass panels, a control strip with a live **TEST MODE / LIVE** badge, a guide line that always says what to do next, big round speaker cards, rounded buttons and tabs, and the same careful spacing everywhere. It shrinks itself to fit small screens and high Windows scaling.
* **A Start tab for new users:** five steps that tick themselves off, each with a button that does it for you, plus a short *How it works* and *Where do I find things?* guide.
* **A Soundboard tab:** a button for every built-in sound and every `.wav` file in your `sounds` folder.
* **A Jumped column on the Speakers tab:** how often each person took the mic ahead of people who were waiting, next to turns taken, talk time, longest turn, warnings and dots.
* **A tidier Tools tab:** five numbered cards that check the timer works with your copy of Paltalk.
* **Settings on six pages:** General, Time \& queue, Time's up, Admins, Messages and Sounds, each in cards with a plain explanation. Changes save as you make them; only the text boxes use the **Save** button at the bottom.

**The banner poster**

* **An animated poster card in the banner:** a waving American flag that plays at the GIF's own speed. Click it to skip ahead, or switch it off in **Settings > General**.
* **Your own picture:** use a GIF (animated or not), PNG or JPG. Press **Choose your own picture...** or drag a picture file onto the window. The card resizes to fit it, and **Use the built-in poster** puts the original back. Phone photos that are stored sideways are turned the right way up, see-through PNGs work, and files up to 25 MB are accepted. A file that cannot be used is refused with a plain-English reason and you keep the picture you had.

**The mic queue and who may take the mic**

* **Queue jumpers are dotted.** The timer keeps the mic queue in order. Anyone who takes the mic ahead of people still waiting is dotted, and the room is told who is next. Admins are exempt.
* **Three rules for who may take the mic**, one choice on **Settings > Time \& queue**: *No jumping the line*, *Only people in the queue*, or *Strict*. Each rule includes everything in the one before it. *Only people in the queue* also dots anyone who takes the mic without being in the queue while somebody is talking or people are waiting. *Strict* dots them even when the mic is empty and nobody is waiting. Whoever is dotted is told why in the room, and a person who was already on the mic when you connected is never dotted for it.
* **The front of the line has 2 minutes** (you can change it; 0 means never) to take a free mic before they lose their turn.

**Sounds and the room's microphone**

* **Eleven built-in sounds:** Bell, Double ding, Chime, Heads-up beeps, Fanfare, Air horn, Buzzer, Pop, Tick-tock (10 and 5 seconds) and Horse race caller.
* **Tick-tock and Horse race caller** for the final warning. The tick-tock is a ticking clock that speeds up. The race caller is hoofbeats, a bugle and a crowd with a spoken race call made with Windows' own voice (or your own recording).
* **Your own sounds:** put `.wav` files in the `sounds` folder. A file that is broken falls back to the built-in sound.
* **A sound for every moment:** each timer event can play its own sound on your speakers, into the room, or both, with a master switch and a volume control.
* **Sounds go out on your real mic.** With **Take the mic** ticked, every warning, bell and soundboard button takes the mic when it happens, plays into the room and lets go. Choose click, hold or automatic.
* **Mic helper tools** on the Tools tab: **Test the mic**, **Find the mic button**, **Teach it the mic button** and **Forget the taught spot**, for when the timer cannot find Paltalk's mic button by itself.
* **A command that cannot be done is reported.** If `!dot` or `!undot` fails, the room hears a line like *Boss, Ghost could not be dotted.* (the admin who typed it, then the person).

**Built to keep running**

* **A crash log.** A problem inside the program is written to `logs\crash.log` and the timer carries on.
* **One copy at a time,** and closing the window never leaves an invisible copy running.
* **Limits that stop a mess:** the timer never holds your mic for more than 90 seconds at a time, and a dot that is waiting for the speaker to finish comes off after 30 minutes at the latest.

### Changed in 2.0

* **One name everywhere:** the program, the window, the file properties and the exe are all called **PALTALK MIC TIMER 2.0 Created by SodaDaPimp**. The old exe was called *Paltalk Mic Timer Created by SodaDaPimp.exe*.
* **Commands only is now Free mic.** It is the same idea (the timer is off for everyone: no time limit, no warnings, no dots), now one switch at the top of **Settings > Time \& queue**. Your old setting is carried over.
* **The queue ticks became one choice.** The separate queue ticks are now the single choice of three rules above. An old config that had them is converted to the matching rule.
* **Nothing is listed twice any more.** The *explain why*, *say so*, *grace period* and *read nickname colours* ticks are gone. Leave a message empty to say nothing, set the grace to 0 for no grace, and leave the colour list empty to skip colours. Old files are converted so everything behaves the way it did.
* **The room is read more often:** every 0.4 seconds by default, instead of every second.
* **Messages are plain text.** The built-in messages have no emoji, and emoji in an older config are removed (your own edits are kept).
* **The reply to someone who is not an admin** now reads *Name, only room admins can use the dot commands.* It no longer contains the command words.

### Fixed in 2.0

**Chat commands and replies**

* **The timer answered itself in a loop.** Its own *only room admins can use !dot and !undot* reply was read as if somebody had typed a command, so the timer kept replying to its own reply and flooded the room. Now the timer never reacts to its own posts, a command only counts when it is the whole message, the reply no longer contains the command words, and it is limited to one reply per person per minute and one every 10 seconds overall. Old config files that still had the looping wording are cleaned automatically.
* **Commands failed on some nicknames.** Paltalk can put an invisible symbol on the end of a nickname in chat (it showed up as a small box in the logs), so `!dot-Name` did not match the person. Names are now compared with hidden characters and extra spaces removed and capital letters ignored.
* **Commands could be missed or run twice when the chat was busy.** The timer now follows only the new chat lines and keeps its place even when Paltalk trims old lines.
* **Emoji in room messages** came out wrong because Paltalk cannot show them from a bot. They are no longer sent, and when text has to be simplified the emoji are dropped cleanly.

**Dotting and undotting (the right-click menu)**

* **Dots that failed with *the right-click menu didn't show up*, <i>none of its entries could be read</i>, <i>the member search box didn't open</i> or <i>no Restrict option in the menu</i>.** The timer now finds the person by name, falls back to Paltalk's member search when the name has scrolled out of view, and reads the menu entries even when there is no *Bounce* entry. If it cannot be sure, it clicks nothing and saves what Paltalk showed (text and pictures) in the `logs` folder so the problem can be fixed.
* **Failed dots are retried, then reported.** A dot is tried up to 3 times, and a queue jumper is retried every second up to 6 times because Paltalk's own list can lag a moment. If it still fails, you get an alert to dot the person by hand.
* **The error `CoInitialize has not been called`** when dotting from a chat command (seen in the Python version). Windows' UI Automation is now started properly on the thread that drives Paltalk.
* **The right person, every time.** Two people with the same name are never guessed between, a name that has scrolled out of sight is never clicked, a blank or highlighted first menu row is read correctly and never clicked, and a sub-menu row is never taken for *Restrict*. *Remove Restrictions* means the person is dotted.
* **No double toggling.** Dotting someone who is already dotted, or undotting someone who is not, clicks nothing.
* **False *dot didn't work* warnings.** The timer only warns when a person is still on the mic list several seconds after being dotted. If the dot worked and they left the list, you hear nothing, and a dot that is taken off again at once is not judged at all.

**The mic queue and who may take the mic**

* **A stuck hand no longer gets every speaker dotted.** A person who has walked away, or whose hand never comes down, is passed over and stops holding everybody else up.
* **The next person in line is not dotted** when Paltalk shows them on the mic a moment after their hand goes down, and a person who gave up their place is no longer counted as waiting.
* **The timer's own mic clicks are never a jump,** and it remembers its own name, so somebody else grabbing the mic at the same moment is not mistaken for you.
* **Fair judgement of people who arrive together.** Two people who raise their hands at the same moment are not judged against each other, and an outsider who arrives with a person from the queue is the one who is dotted.
* **One dot, not two,** when a rule includes the one before it.
* **A jumper who grabs the mic again** after the dot comes off is dotted again.

**Turns, timers and announcements**

* **Quick taps on the mic are no longer announced,** and a quick re-grab does not repeat the *has taken the mic* message.
* **A speaker who drops off the mic list while a sound plays keeps their timer,** and the room is not told twice that they took the mic. A short blip off the mic never ends a turn.
* **Switching Free mic off gives everyone on the mic a fresh turn.**

**Sounds and the mic button**

* **A pile of long sounds could keep your mic for minutes.** The timer now never holds it for more than 90 seconds at a time.
* **A sound that is not switched on for the room never takes the mic,** and nothing plays or clicks in TEST MODE or when sounds are off.
* **A push-to-talk button is always let go.** It is never held forever, it is released if the room goes away or the mic never opens, a dot waits while it is held, and a locked mic that ignores the second click is let go with Ctrl.
* **Only the real mic button is ever clicked.** *Join queue to talk*, the little arrow next to the lock button and other buttons are never clicked.
* **A broken sound card, a broken `.wav` file or a voice that cannot be made never stops the timer.** The sound is skipped (a broken file falls back to the built-in one) and everything else carries on.

**The window**

* **Scroll bars did not match the dark window.** Every scroll bar and list header is now dark, whatever Windows' light or dark setting is.
* **The window could be too big for a small screen or lose its layout** when dragged to a screen with different Windows scaling. It now scales itself down to fit and keeps its layout at every scale.
* **Empty tables** (Speakers and the queue) stay clean and say what they are waiting for, and the red bar clears itself after about 25 seconds.
* **Every setting appears exactly once,** every control points at its own field, and the texts have no double spaces or leftover section numbers.
* **A confusing label on the Messages page.** The *Time is up - grace period* message used to talk about a tick that no longer exists. It now says when it is posted: at the limit, when the grace period is more than 0 seconds.

**Staying up**

* **A problem inside the program no longer takes it down.** It is written to `logs\crash.log` and the timer carries on. A second copy will not open, and closing the window never leaves an invisible copy running, even when the background work is stuck waiting for Paltalk.
* **Damaged or unusual pictures** (GIF, PNG or JPG) can never crash the timer or make it hang. They are refused with a plain reason.
* **Bad values in `config.json` are clamped** to sensible ones instead of breaking the timer.
* **Paltalk oddities are handled.** An empty or unreadable room is reported instead of failing silently, a room that was closed is reported instead of crashing, names that cannot be read are counted, and a bogus *hand up* flag in Paltalk's member list is ignored.

### Upgrading from 1.x

* Put the new `.exe` in its own folder, as before. If you copy your old `config.json` next to it, it is converted the first time the new program reads it. Your admins, colours and settings carry over, and so do your own message edits.
* The timer still saves its settings in `config.json`, its logs in a `logs` folder and your own sounds in a `sounds` folder, all next to the `.exe`.

<details>
<summary>How old settings files are converted (technical)</summary>

Each settings file carries a version number. When an older file is read, these steps are applied in order:

|Version|What the conversion does|
|-|-|
|2|Settings from the very first version take the new messages and timings.|
|3|Emoji are removed from messages (Paltalk cannot show emoji sent by a bot). The old send-encoding and sound-threshold settings are dropped.|
|4|An old *not an admin* reply that contained the command words is removed, because it set off the timer itself.|
|5|A room check interval of exactly 1 second goes back to the new faster default (0.4 seconds).|
|6|Options that said the same thing twice are merged: an *off* tick becomes a grace of 0, an empty message or an empty colour list.|
|7|*Commands only* becomes *Free mic*, and the separate queue ticks become the single queue rule.|

A config file written by the Python version is read as it is.

</details>

## What you need

* A Windows 10 or 11 PC.
* The Paltalk desktop app, signed in and with your room open.
* **Admin or owner rights in the room.** The timer dots people the same way you do (it right-clicks their name in Paltalk), so it needs your permissions.

## Quick start

The timer starts in **TEST MODE**. Nothing is dotted, posted or clicked while it is on; the Activity tab only shows what the timer would do. That makes it safe to look around first.

The program opens on the **Start** tab. It lists five steps, top to bottom. Each step ticks itself off when it is done, the red one is what to do next, and every step has a button that does it for you or takes you to the right page. The line under the banner always says what to do next, too.

1. Open Paltalk and join your room as an admin.
2. Download **PALTALK MIC TIMER 2.0 Created by SodaDaPimp.exe** from the [Releases page](https://github.com/SodaDaPimp/PALTALK-MIC-TIMER/releases), put it in its own folder and double-click it. If Windows says *Windows protected your PC*, click **More info**, then **Run anyway**. Windows shows this for every new program.
3. In the timer, pick your room in the **Room** box at the top (click **Refresh** if it is missing), then click **Connect**. The timer posts one line in the room to say it is connected. The dot beside the room box turns green when it can read the room.
4. Optional: change the time limit on **Settings > Time \& queue** (the default is 2 minutes).
5. Open **Settings > Admins**. Type your own nickname and your admins' nicknames, one per line, spelled exactly as Paltalk shows them. Press **Save** at the bottom of the window.
6. Let someone take the mic and watch the **Activity** tab. With TEST MODE on it says things like *Would post: ...* and *Would dot ...*.
7. When you are happy, press **Go live** on the Start tab, or untick **TEST MODE** on **Settings > General**. The timer is now live.
8. To stop, click **Disconnect** or close the window. It removes any dot it is still holding and posts that it has disconnected.

**Want to practise without a real room?** Choose *Practice room (no Paltalk needed)* in the Room box and click Connect. A Practice window opens: pick a pretend person and press *Take mic*. Set the time limit to 30 seconds to watch the whole cycle quickly.

The timer saves your settings in **config.json**, its logs in a **logs** folder and your own sounds in a **sounds** folder. All three are created next to the .exe, which is why it should live in its own folder.

## What happens during a turn

This is the default behaviour with a 2-minute limit. Every time and message below can be changed in Settings.

|When|What happens|
|-|-|
|0:00|Someone takes the mic. Their timer starts.|
|0:03|The room reads: *Sam has taken the mic. Allocated time: 2 minutes.* (You hear a soft pop.) The 3-second wait stops quick taps from filling the chat.|
|0:30, 1:00, 1:30|A time check: *1 minute 30 seconds remaining for Sam.*|
|1:50|The final warning: *10 seconds left! Please wrap up and pass the mic.* (Three quick beeps.)|
|2:00|Time is up. The bell rings. The room reads: *Sam, time is up! Release the mic now or you will be dotted in 5 seconds.*|
|2:05|Still talking? The timer dots Sam, plays a double ding, and explains in the room why Sam was dotted.|
|2:10|The dot comes off by itself and the room reads: *Sam, your dot has been removed. Thanks for understanding!* (A chime.) Sam can raise a hand to get back in the queue.|

* **Grace period set to 0?** The bell and the dot both happen at 2:00, with no warning message in between.
* **Admins and untimed colours** are never timed or dotted. Their card turns grey and says *timer paused*.
* **Queue jumpers** are dotted at once (see *The mic queue* below). With the **Only people in the queue** rule (or **Strict**), so is anyone who takes the mic without being in the queue (see *Who may take the mic* below).
* **A short blip** off the mic does not end a turn. If someone drops off and is back within a few seconds, their timer simply continues.
* **A dot given with !dot-name** stays on until an admin types `!undot-name`.
* **Silent mic?** If exactly one person is on the mic and nothing has been heard for 15 seconds, the timer posts *Mic check Sam - no audio detected.* and plays a buzzer.
* When it connects and when it disconnects, the timer posts a one-line credit message. That is built in and cannot be switched off.

## The main window

The window has the same layout all the time: a banner at the top, a control strip with a guide line under it, the speakers on the left and six tabs on the right. The **photo behind everything** is only decoration.

### Top and left

|Part|What it shows|
|-|-|
|Banner and poster|The title, and in the top right a little animated poster card. The built-in poster is a waving American flag that plays at its own speed; an animated GIF of your own does too. Click it to jump to the next picture. You can switch it off or use your own picture (see *Using your own picture* below).|
|Room box, Refresh, Connect|Pick your Paltalk room and connect. The button becomes Disconnect while connected.|
|Status dot and words|Green = connected and reading the room. Amber or red = connected but it cannot read the room (see Troubleshooting). Grey = not connected.|
|TEST MODE / LIVE badge|The round badge at the right of the control strip. Amber **TEST MODE** = practice, nothing is really dotted or posted. Green **LIVE** = the timer is really acting. Click it to go to the switch on Settings > General.|
|Guide line|The one line under the control strip that tells you the single next thing to do, for example *Pick your room above and press Connect*. It turns amber or green when something needs attention or all is well.|
|Red bar|A problem that needs your attention. Click it to dismiss it, or leave it - it clears by itself after about 25 seconds. Everything is also kept in the activity log.|
|ON THE MIC|One card per person on the mic: their name, how long they have talked, and a progress bar. Green = within the limit. Amber = almost out of time. Red = over the limit or dotted. Grey = timer paused (an admin or an untimed colour). When nobody is on the mic it says so.|
|Pink line|Appears under the cards while a dot is on and counts down to when it comes off.|
|MIC QUEUE|Everyone with a hand up, in order, with how long they have waited.|
|Bottom line|A summary of the current setup: how many people are in the room, the limit, grace period and the dead air check.|

### The six tabs

|Tab|What it is for|
|-|-|
|Start|The five-step checklist for new users, plus a short *How it works* and a *Where do I find things?* guide. Come back to it any time.|
|Activity|A colour-coded log of everything the timer sees and does. Blue = mic events, purple = queue, amber = warnings, pink = actions such as dots and mic clicks, green = messages it posted, red = problems. The same log is saved in the logs folder, one file per day.|
|Speakers|Statistics since the timer started: turns taken, total talk time, longest turn, and how often each person was warned, dotted or jumped the mic queue. Clear stats resets them.|
|Soundboard|Buttons for every built-in sound and every .wav file in your sounds folder. See Sounds below.|
|Settings|Every option, on six pages: General, Time \& queue, Time's up, Admins, Messages and Sounds. Explained one by one below.|
|Tools|Five numbered cards that check the timer works with your copy of Paltalk, and the buttons to send us a report if something does not. See Tools tab below.|

### Using your own picture

The banner poster can be **a picture of your own**: a **GIF** (animated or not), a **PNG** or a **JPG** (also called JPEG, the kind a phone camera makes). An animated GIF plays at **its own speed**: each frame stays up for exactly the time the GIF gives it, the same as in a web browser, so a quick cartoon-style GIF animates smoothly and a slow slideshow-style GIF (a picture every second or more) slides gently from one picture to the next. A PNG or JPG is one still picture. Tall, square and wide pictures all fit. Only an extremely tall or wide one is trimmed a little at the edges. The card makes itself bigger or smaller to fit your picture.

1. Open **Settings > General**, find the *This window* card and make sure **Show the poster in the banner** is ticked.
2. Press **Choose your own picture...** and pick a .gif, .png, .jpg or .jpeg file. (Quicker: drag a picture file from a folder and drop it onto the timer window.)
3. That is it. The banner starts showing it right away, and the line under the button says *Using your own picture: <file name>*.
4. To go back, press **Use the built-in poster**.
* The timer keeps its own copy of your picture as **my\_poster.gif**, **my\_poster.png** or **my\_poster.jpg** next to the .exe (only one at a time), so you can move or delete the original. It remembers your choice the next time you start.
* The timer looks at what is *inside* the file, not at its name, so a PNG that somebody named .jpg still works. Files can be up to 25 MB.
* If the file cannot be used the timer tells you why in plain words and keeps the picture you had.
* **JPG:** normal, progressive and grayscale JPGs work, and a phone photo that is stored sideways is turned the right way up automatically. Print-style CMYK JPGs and very rare kinds (arithmetic or 12-bit) are refused: re-save the picture as an ordinary JPG.
* **PNG:** every kind works, including see-through ones (the see-through part shows the banner colour behind the card).
* **Big pictures** (more than 30 megapixels) are refused; anything over 1600 pixels on its longest side is shrunk when it is loaded, because the card is small.
* If your picture file goes missing or breaks, the timer falls back to the built-in poster and writes a warning in Activity.
* **Speed:** the timer follows the timing stored inside the GIF. A GIF that says 0 or 0.01 seconds per picture is shown at 0.1 seconds, which is what web browsers do. If a GIF looks too fast or slow, it was made that way - re-save it at the speed you want in a GIF editor.
* It only moves while the window is showing, and holds still if Windows is set not to show animations (Settings > Accessibility > Visual effects).

**Changing the built-in poster (for people who build the program).** The built-in poster is the animated GIF **res/poster.gif** (a waving flag). To swap it, put your GIF in the **res** folder as `poster.gif`, run `python tools/make_assets.py --poster res/poster.gif` (this rewrites `src/assets_poster.cpp`) and run **Build EXE.bat** again. Everyone else should just use *Choose your own picture* above.

## Settings, one by one

The Settings tab has a row of six small tabs across the top of it: **General**, **Time \& queue**, **Time's up**, **Admins**, **Messages** and **Sounds**. Everything saves the moment you change it, **except** the text boxes: the Admins list, the Name colours and the Room messages. After typing in those, press the **Save** button in the bar at the bottom of the Settings page (it says *You have changes that are not saved yet* until you do). The +/- buttons next to a number change it by a fixed step; you can also type a number.

### General

|Setting|Default|What it does|
|-|-|-|
|TEST MODE (practice) - nothing is really dotted, posted or clicked|On|While ticked, nothing is really dotted, posted in the room or clicked. The Activity tab shows what the timer would have done. Untick it to go live. The Tools tab buttons ignore this switch on purpose and act for real.|
|Keep this window on top of other windows|Off|Keeps the timer window above other windows.|
|Show the poster in the banner|On|Shows the poster in the top-right corner of the banner. Untick it to hide the poster. It only moves while the window is showing, and holds still if Windows is set not to show animations (Settings > Accessibility > Visual effects).|
|Choose your own picture...|-|Opens a file box. Pick a .gif, .png or .jpg picture and it becomes the banner poster at once (an animated GIF plays at its own speed). You can also drag a picture file onto the window. See *Using your own picture* above.|
|Use the built-in poster|-|Goes back to the waving flag that comes with the program. The line under the two buttons says which poster is in use.|
|Open config.json|-|Opens the settings file (in the *Advanced* card). Close the program before you edit it by hand.|

### Time \& queue

**Free mic** card (the master switch):

|Setting|Default|What it does|
|-|-|-|
|Turn the timer off for everyone (free mic)|Off|Everybody may talk on the mic for as long as they like: no time limit, no warnings, no auto-dot, no silent-mic check and no queue rules. The MIC QUEUE list still shows who is waiting, and admins can still type !dot-name and !undot-name (if that is ticked on the Admins page). The badge at the top shows **FREE MIC** while it is on. Untick it to turn the timer and the queue rule back on.|

**Time limit** card (only used while Free mic is off):

|Setting|Default|What it does|
|-|-|-|
|Mic time limit (seconds)|120|How long one turn may last. 120 = 2 minutes, 180 = 3 minutes. The figure beside the box shows it as minutes:seconds.|
|Final warning - seconds before the limit|10|Posts the final-warning message and plays the final-warning sound this many seconds before time is up. 0 = no final warning.|
|Time check - post the time left every (seconds)|30|How often the room is told how much time is left, for example *1 minute remaining for Sam*. 0 = no time checks. A check is skipped if it would land on top of the final warning.|
|Announce a new speaker after (seconds)|3|Posts *Sam has taken the mic. Allocated time: 2 minutes.* once someone has held the mic this long. The wait stops quick taps from filling the chat. 0 = announce at once.|

**Who may take the mic?** card. Pick **one** of three rules. **Each rule includes everything the rule above it does** (the details are under *Who may take the mic* below):

|Setting|Default|What it does|
|-|-|-|
|No jumping the line (recommended)|On|Nobody may take the mic ahead of people who are still waiting in the queue. If someone does, they are dotted and the room is told who is next.|
|Only people in the queue|-|Everything in *No jumping the line*, plus: anyone who is **not** in the queue and takes the mic while somebody is talking or people are waiting is dotted. The dot stays on until the person they interrupted is done speaking.|
|Strict: only people in the queue, always|-|Everything in the two rules above, plus: anyone who takes the mic without being in the queue is dotted, even when nobody is talking and nobody is waiting. People must raise their hand first.|
|Next in line has to take an empty mic within (seconds)|120|If the person at the front of the queue leaves an empty mic alone for this long (120 = 2 minutes), the mic is open to everyone else. This stops someone who walked away from getting everybody dotted. 0 = the front of the line never loses their turn.|

### Time's up

**The dot** card:

|Setting|Default|What it does|
|-|-|-|
|Dot people who go over the limit (auto-dot)|On|A dot (restriction) takes the person off the mic. Untick it and people who go over the time limit only get the warning and the bell; they are not dotted. The mic queue rules (Settings > Time \& queue) still dot people who break them.|
|Grace period after the bell (seconds)|5|The bell rings at the limit and the person has this long to let go before the dot. **0 = no grace:** the bell and the dot happen the instant time is up.|
|Remove the dot - seconds after the explanation|5|How long the dot stays on after the explanation is posted. A dot an admin gave with !dot-name is not removed automatically.|

What the room is told when someone is dotted, and when the dot comes off, is written on the **Messages** page. **Leave a message empty and nothing is said.**

**Silent mic (dead air)** card:

|Setting|Default|What it does|
|-|-|-|
|Post a mic check when the person on the mic is silent|On|Catches someone who holds the mic but says nothing. The timer measures how loud the sound playing on this PC is; it records nothing. It only checks while exactly one person is on the mic, and music or a video playing on your PC counts as sound.|
|Silence before the mic check (seconds)|15|How long it must be quiet before the mic check is posted.|

### Admins

|Setting|Default|What it does|
|-|-|-|
|Let admins type !dot-name and !undot-name in the room|On|See Admin commands below. Only people on the Admins list can use them.|
|Admins (one nickname per line)|Empty|Your own nickname and every admin's, spelled exactly as Paltalk shows it. The timer never times or dots an admin, and only admins can use the commands. Click Save after changing the list.|
|Name colours with no time limit|Empty|Colours separated by commas, for example *orange, purple*. Anyone whose nickname is one of those colours is never timed. Empty = nobody is skipped by colour. It can tell apart: black, blue, green, orange, purple, red, pink, yellow.|

### Messages

**Master switch** card:

|Setting|Default|What it does|
|-|-|-|
|Post the timer's messages in the room|On|The master switch for everything the timer says in the chat. Unticked, the timer stays silent in the room but still times people, rings sounds and dots. The Activity tab shows what it would have said. The words of each message are on the Messages page.|

**The messages** card:

The exact words the timer posts. Edit them freely. **Leave a box empty and that message is never posted.** Put these placeholders in a message and the timer fills them in:

|Placeholder|Becomes|
|-|-|
|{name}|the person's nickname|
|{left}|seconds left, as a number|
|{left\_text}|time left in words, e.g. 1 minute 30 seconds|
|{limit}|the limit as minutes:seconds, e.g. 2:00|
|{limit\_text}|the limit as an adjective, e.g. 2-minute|
|{limit\_words}|the limit in words, e.g. 2 minutes|
|{talked}|how long the person talked|
|{grace}|the grace seconds|
|{undot\_in}|seconds until the dot comes off|
|{admin}|the admin who typed a command|
|{action}|dotted or undotted|
|{next}|the person next in line (used in the queue jump and queue-only messages)|
|{speaker}|who was interrupted, e.g. Sam or Sam and Ana (used in the queue-only message)|
|{dot\_off}|when the dot comes off, e.g. *when Sam is done speaking* or *in 5 seconds* (used in the queue-only message)|

And when each message is posted:

|Message|When it is posted|
|-|-|
|Someone took the mic|After they have held the mic for the announce time (Settings > Time \& queue).|
|Time check|Every few seconds while they talk (Settings > Time \& queue).|
|Final warning|Shortly before the limit (Settings > Time \& queue).|
|Time is up - grace period|At the limit, when the grace period is more than 0 seconds.|
|Time is up - no dot|At the limit, only when auto-dot is off or the dot could not be done.|
|After a dot - why|After someone is dotted for going over the limit. Empty = say nothing.|
|After the dot is removed|When the dot comes off. Empty = say nothing.|
|Someone jumped the queue|Right after a queue jumper is dotted (rule *No jumping the line* or stricter). {next} is the person who was next in line.|
|Took the mic without being in the queue|Right after someone who was not in the queue is dotted (rule *Only people in the queue* or *Strict*). {speaker} is who they interrupted and {dot\_off} says when the dot comes off.|
|Silent mic|When the dead air check finds a silent mic.|
|An admin dotted someone|After a successful !dot-name.|
|An admin removed a dot|After a successful !undot-name.|
|A command could not be done|When a !dot-name or !undot-name failed.|
|A non-admin typed a command|As a reply to someone who is not on the Admins list.|

**Reset messages** puts every message back to its default words. **Open config.json** opens the settings file.

### Sounds

**Sounds** card:

|Setting|Default|What it does|
|-|-|-|
|Sounds ON|On|Untick to silence everything: the timer's sounds and the soundboard.|
|Volume (0 - 100)|80|How loud the sounds are.|
|Send the room's sound through|Same as my speakers|Which audio output carries the sounds meant for the room. Leave it alone unless you use a virtual audio cable. See Sounds below.|

**Take the mic to play sounds** card:

These settings let the timer click Paltalk's mic button so the room really hears your sounds. How it works and how to set it up is explained in full under *Playing sounds on your mic* below.

|Setting|Default|What it does|
|-|-|-|
|Take the mic automatically to play sounds into the room|Off|The timer clicks Paltalk's mic button, plays the sound into the room, then lets go. Only sounds whose Room (mic) box is ticked in Settings > Sounds use it. It never clicks anything in TEST MODE.|
|Play each sound the moment it happens|On|Ticked: each sound takes the mic as it happens, even while someone is talking. Unticked: the timer only takes the mic when nobody is on it, so the room hears the sounds at the end of a turn.|
|How should the timer press Paltalk's mic button?|Automatic|**Click once to talk, click again to let go** (Lock Mic), **Hold the button down while the sound plays** (Push To Talk), or **Automatic** (hold a Push To Talk button, click a Lock Mic button).|
|Delay before the sound starts (milliseconds)|1200|How long to wait after clicking the mic before the sound starts. Raise it if the very start of a sound is cut off.|
|Give up on a sound if the mic stays busy (seconds)|12|How long a sound may wait for its turn on the mic before it is skipped.|

**Which sound plays for which event** card:

One row per event. **Speakers** = you hear it on this PC. **Room (mic)** = the room hears it. Pick which sound plays with the Sound button and press **Test** to hear it.

|Event|Default sound|Speakers|Room (mic)|
|-|-|-|-|
|Someone takes the mic|Pop|Yes|No|
|Final warning (time almost up)|Heads-up beeps|Yes|Yes|
|Time's up (limit reached)|Bell|Yes|Yes|
|Someone gets red-dotted|Double ding|Yes|Yes|
|Dot removed|Chime|Yes|No|
|Dead air (mic open, no sound)|Buzzer|Yes|No|

The built-in sounds are Bell, Double ding, Chime, Heads-up beeps, Fanfare, Air horn, Buzzer, Pop, **Tick-tock 10 sec**, **Tick-tock 5 sec** and **Horse race caller**. The program makes them itself; there is nothing to download. You can also pick any .wav file from your sounds folder.

### Tick-tock and the horse race caller

Both are made for the **Final warning** (the last seconds before the limit), but you can give them to any event. Open Settings > Sounds, press the Sound button on the *Final warning* row and choose one. Press **Test** to hear it. They are also on the Soundboard tab.

* **Tick-tock 10 sec / 5 sec:** a wall clock ticking and tocking, speeding up toward the end. It lasts 10 (or 5) seconds, so match it to *Final warning - seconds before the limit* in Settings > Time \& queue: with the default of 10 seconds, the clock finishes just as time is up. It is an original ticking sound, not a recording of any TV show.
* **Horse race caller:** a bugle, galloping hooves that speed up, a crowd that builds, a bell at the wire, and an announcer shouting "They're turning for home! Down the stretch they come!" over the top. It lasts about 10 seconds.
* **Where the announcer's voice comes from:** Windows reads the race call aloud with its own built-in text-to-speech voice. The timer asks for it **once**, in the background (a few seconds), the first time you use the Horse race caller, and saves it in your sounds folder as *Race caller voice only.wav*. After that it is instant. It is a computer voice, not a real person.
* **Want a real announcer?** Record or download your own race call (a plain .wav, up to 30 seconds) and save it in the sounds folder with exactly that name, *Race caller voice only.wav*, replacing the one Windows made. The Horse race caller then uses your recording. Press **Reload sounds** on the Soundboard tab.
* If Windows cannot make the voice, Activity says why once, and the Horse race caller plays without the voice (the hoofbeats, crowd and bell are still there). **Reload sounds** tries again.
* In the room: tick **Room (mic)** for the event, as for any sound (see Settings > Sounds). The race lasts about 10 seconds, so the timer holds your mic that long when *Take the mic* is on.

## The mic queue and queue jumpers

The **MIC QUEUE** list in the timer is numbered 1, 2, 3... in the order hands went up, the same order as Paltalk's Mic Queue. When someone takes the mic while people ahead of them are **still waiting**, they have jumped the line. The timer dots them straight away, so the person who was next in line can talk, and posts a message naming who is next.

|Situation|What the timer does|
|-|-|
|The person at #1 takes the mic|Nothing. That is their turn.|
|#2 or #3 takes the mic while #1 is still waiting|Dots them. #1 is named as next in line.|
|Someone who was not in the queue at all takes the mic while others are waiting|Dots them.|
|Nobody is waiting|Nothing, except under the **Strict** rule (see *Who may take the mic* below).|
|The person who jumped is an admin or an untimed colour|Never dotted. The Activity tab notes the jump.|
|Two mics are free and #1 and #2 both take one|Nothing. Nobody was skipped.|
|#1 leaves an empty mic alone for 2 minutes|#1 loses their turn at the front, so someone who walked away cannot get everyone else dotted. #2 then gets the same time, and so on. You can change the time or set it to 0 to switch this off.|
|Two people raised their hands at the very same moment|Nothing. Nobody can tell who was first.|

* The dot comes off after the *Remove the dot* delay (Settings > Time's up). The person raises their hand again to go to the back of the line.
* The **Jumped** column on the Speakers tab counts how often each person did it.
* No jumping the line is part of all three rules in Settings > Time \& queue, so it is always on while the timer is on. Nothing is dotted in TEST MODE or while **Free mic** is on.
* **Try it safely:** open the Practice room. Raise hands for Alice and then BigMike (a few seconds apart), then press *Take mic* for Carmen\_77. Untick TEST MODE first to see her really dotted; the transcript then shows the message naming who is next. With TEST MODE on, the Activity tab says *Would dot Carmen\_77*.

### Who may take the mic

On **Settings > Time \& queue** the **Who may take the mic?** card has three rules. Pick one; **each rule includes everything the one before it does**. (If you want nobody dotted at all, use the **Free mic** switch at the top of the page instead: it turns the whole timer off.)

|Rule|What the timer does|
|-|-|
|No jumping the line (recommended)|Dots anyone who takes the mic while people ahead of them in the queue are still waiting, and names who is next.|
|Only people in the queue|Everything above, plus: dots anyone who is **not** in the queue and takes the mic while somebody is talking or people are waiting. **The dot stays on until the person they interrupted is done speaking.** Then the timer removes it after the usual delay (Settings > Time's up). A free mic with nobody waiting is left alone.|
|Strict: only people in the queue, always|Everything above, plus: dots anyone who is not in the queue and takes a **free** mic when nobody is waiting. Nobody may speak without raising a hand first.|

Whoever is dotted is told **why** in the room: the *Someone jumped the queue* message when someone in the queue skips ahead of the people before them, the *Took the mic without being in the queue* message when someone who is not in the queue takes the mic. You can change those words on the Messages page.

|Situation|What the timer does|
|-|-|
|Somebody who is #3 in the queue takes the mic while #1 and #2 are still waiting|(All three rules) Dots them: they jumped the line. #1 is named as next.|
|Sam is talking and somebody who is not in the queue takes a second mic|(Only people in the queue, Strict) Dots them at once and keeps the dot on until Sam is done. The room is told who was interrupted and when the dot comes off.|
|Sam is talking and somebody from the queue takes a second mic|Nothing. They were waiting, so they may.|
|Nobody is talking, people are waiting, and somebody who is not in the queue takes the mic|(Only people in the queue, Strict) Dots them. The dot comes off after the usual delay, since nobody was interrupted.|
|Nobody is talking, nobody is waiting, and somebody takes the mic|(Strict) Dots them and says why. With the other rules: nothing.|
|Somebody was already on the mic when you clicked Connect|Never dotted for that.|
|Two people take the mic in the same second and neither was in the queue|Nothing. Nobody can tell who was first.|
|Somebody who was in the queue takes the mic at the same moment as somebody who was not|Only the one who was not in the queue is dotted.|
|Several people were talking|The dot stays on until all of them are done.|
|The person who took the mic is an admin|Never dotted. The Activity tab notes it.|
|The speaker never stops|The dot comes off by itself after 30 minutes.|

* A person is *in the queue* while their hand is up, and for a few seconds after they lower it, because Paltalk can drop the hand a moment before it shows them on the mic.
* Someone who was dotted by this rule is not counted as a speaker when the next person takes the mic, so the dots never wait on each other.
* A **name colour** can only be read when exactly one person is on the mic, so the untimed-colour exemption cannot protect someone who takes the mic while another person is talking. Add trusted people to the **Admins** list (Settings > Admins).
* Closing the timer, or choosing a different room, removes every dot it was holding.
* Nothing is dotted in TEST MODE or while **Free mic** is on. With TEST MODE on, the Activity tab says *Would dot ...*.
* **Try it first** with TEST MODE ticked and watch the Activity tab, especially with **Strict**. In a room where Paltalk puts someone on the mic in the same second they raise a hand, the timer may never have seen the hand and will dot them. If that happens, choose **Only people in the queue** instead.

## Admin commands

People on the Admins list can type these in the room:

|Command|What it does|
|-|-|
|!dot-nickname|Dots that person.|
|!undot-nickname|Removes the dot.|

Example: `!dot-BigMike`

* The command must be the whole message. A sentence that only mentions !dot is ignored.
* A dot given by command stays until an admin removes it.
* Admins cannot be dotted by command.
* Anyone who is not on the Admins list gets a short reply saying only admins can use the commands.
* The commands work in TEST MODE too, but only pretend: Activity shows what would have happened.

## Sounds

### What you hear and what the room hears

You always hear the sounds on your own speakers. **The room only hears a sound if it reaches Paltalk's microphone.** There are three ways to do that, from easiest to best:

|Way|What you do|The catch|
|-|-|-|
|A. Speakers|Leave *Send the room's sound through* on *Same as my speakers* and tick Room (mic) for the events you want.|The room only hears it if your microphone picks it up, so use speakers, not headphones. The sound quality is poor.|
|B. Virtual audio cable|Install a free cable such as VB-CABLE (vb-audio.com). Settings > Sounds: choose *CABLE Input*. In Paltalk's audio settings set the microphone to *CABLE Output*. So the room still hears you, open Windows Sound settings > Recording > your real microphone > Properties > Listen > tick *Listen to this device* and play it through *CABLE Input*.|A one-time setup and a PC restart after installing the cable. The sound is clean.|
|C. Take the mic|Add the *Take the mic to play sounds* card (Settings > Sounds) to A or B so the timer also holds Paltalk's mic while the sound plays.|It handles *pressing the mic* only. The sound still has to reach Paltalk's microphone through A or B.|

Nothing is ever sent into the room while TEST MODE is on. You still hear the sound on your speakers.

### Playing sounds on your mic

Paltalk only sends sound while you hold the mic. With **Take the mic** ticked (Settings > Sounds), every sound whose **Room (mic)** box is ticked in Settings > Sounds, plus soundboard buttons with Room (mic) ticked, goes into the room like this:

1. The timer presses Paltalk's mic button (your mouse moves, as when it dots someone).
2. After a short delay (Settings: *Delay before the sound starts*) it plays the sound into the room.
3. It lets go of the mic and checks that you are really off it.

A sound whose Room (mic) box is **unticked** never touches the mic. It plays on your speakers if Speakers is ticked, and nothing plays at all if both boxes are unticked or *Sounds ON* is unticked.

### When it takes the mic

The setting **Play each sound the moment it happens** (Settings > Sounds) decides this.

|Setting|Result|
|-|-|
|If ticked (default)|Each sound takes the mic as it happens: the final warning at 10 seconds left, the bell at time's up, the double ding when someone is dotted. This happens even while the speaker is still talking. Whether Paltalk lets the room hear you over them is Paltalk's rule, not the timer's. If the mic list never shows you, the timer plays the sound anyway and says so in Activity.|
|If unticked|The timer only takes the mic when nobody is on it. The final warning is skipped (the speaker is still talking) and the bell and double ding wait until the speaker has been dotted, so the room hears them just after the dot. Your own speakers always ring at once.|

### Click, hold or automatic?

Paltalk's mic button comes in two kinds. This is how the timer presses each one:

|Paltalk shows|How the timer presses it|
|-|-|
|Push To Talk|You talk only while the button is held. The timer holds the left mouse button on it while the sound plays, then lets go. **Keep your hand off the mouse for those few seconds.** If the pointer leaves the button, Paltalk stops sending. The timer never holds it longer than 30 seconds and lets go if you disconnect or close it.|
|Lock Mic|One click opens the mic and keeps it open. The timer clicks it to start. To let go it clicks again; if the mic is still open it taps the Ctrl key (Paltalk's way to release a locked mic) and tries once more. If it is still open it tells you in Activity so you can click it yourself.|

The little arrow beside Paltalk's mic button switches Paltalk between Push To Talk and Lock Mic. Choose **Automatic** if you are not sure: the timer works out which one your room shows. Push To Talk is the more dependable, because letting go is just releasing the mouse button.

### Good to know

* It does nothing until you tick it, and nothing in TEST MODE. In test mode Activity says *Would take the mic to play the ... sound*.
* If clicking the mic does not put you on the mic list, the timer clicks only once, writes a warning in Activity and stops trying for 30 seconds.
* A dot needs the mouse, so it waits until a held Push To Talk button has been let go (a second or two). An admin's !dot command in the chat lets go early instead.
* With auto-dot off the speaker keeps the mic, so with *Play each sound the moment it happens* unticked the room's bell waits and is dropped after the *give up* seconds.
* Paltalk is not built to be clicked by other programs. The mic button is found by its class, its name, or its place beside the chat box. If a Paltalk update moves things around, use Tools > Teach it the mic button.

### The Soundboard tab and your own sounds

* Every built-in sound and every .wav file in the sounds folder is a button. Click one to play it.
* Tick **My speakers** and/or **Room (mic)** to choose where a click plays. **STOP** cuts off every sound that is playing.
* To add your own: click **Open sounds folder**, copy in plain .wav files (up to 30 seconds each), then click **Reload sounds**. Each file becomes a button.
* To use one for a timer event, pick it in Settings > Sounds.
* If a file cannot be used, Activity says why and the built-in sound plays instead.

## Tools tab

Connect to your room first. These buttons check that the timer works with your copy of Paltalk.

|Button|What it does|
|-|-|
|Read the room now|Reads Paltalk's member list once. Activity then shows who is on the mic and who has a hand up. Nothing is changed in the room.|
|Send|Posts the line in the box next to it in the room right now. It posts for real, even in TEST MODE.|
|Dot / Undot|Really dots or undots the nickname you typed, even in TEST MODE. Try it on a friend. Keep the Paltalk room window visible; your mouse moves for a second or two.|
|Test the mic|Grabs Paltalk's mic button, plays the time-up sound into the room and lets go. Do it while nobody is talking.|
|Find the mic button|Lists the buttons it can see beside the chat box and which one it would click.|
|Teach it the mic button|If it cannot find the button: press this, then hold the mouse still over Paltalk's mic button for 2 seconds. It remembers the spot, measured from the window's bottom-right corner, so resizing Paltalk is fine.|
|Forget the taught spot|Goes back to finding the mic button by itself.|
|Run diagnostics|Saves a report of what this copy of Paltalk shows the timer.|
|Inspect Paltalk|Right-clicks a name, opens the member search and saves what Paltalk showed (text and pictures).|
|Capture right-click menu|Right-click a nickname in Paltalk within 10 seconds and it records the menu.|
|Show chat it can read|Prints the last few chat lines the timer can see in Activity.|
|Open logs folder|Opens the folder where the daily logs and the reports above are saved.|

## Troubleshooting

### No Paltalk rooms found

Join the room in Paltalk first, then click Refresh. If Paltalk was started as administrator, right-click the timer and choose *Run as administrator* too.

### Nothing shows under ON THE MIC, or the status dot is not green

Open Tools and click **Read the room now**. If it reports a problem, click **Run diagnostics**.

### Someone jumped the queue and was not dotted

* Is **TEST MODE** ticked (Settings > General)? The Activity tab then says *Would dot ...* and nobody is really dotted.
* Is **Free mic** ticked on Settings > Time \& queue (the badge at the top says FREE MIC)? Then the timer is off and nobody is dotted. The first line in the Activity tab when the timer starts says which rule is on.
* Is the person on your **Admins** list, or an untimed name colour? Admins are never dotted. The Activity tab says *Not dotted: they are an admin or untimed*.
* Look in the Activity tab right after the jump. A line starting **QUEUE JUMP** means the timer saw it and tried to dot. A line saying *can't tell who was first* means two people raised their hands at the same moment, or were already in the queue when you clicked Connect. A line saying *had already let a free mic go by* means the front of the line left a free mic alone longer than the time in Settings > Time \& queue.
* If you see no line at all, the timer did not see the queue: check that the **MIC QUEUE** list in the timer window shows the people waiting. If it is empty while Paltalk's Mic Queue is not, run Tools > **Run diagnostics** while two people are in the queue, and include the file in your bug report.
* If it says *Couldn't dot ... for jumping the queue*, the dot itself failed (see *It does not dot anyone* below). You must be an admin or the owner of the room.
* Make sure you rebuilt the program: the first Activity line should say *Build: queue-jump rule v2*.

### Someone took the mic without being in the queue and was not dotted

* Is **TEST MODE** ticked (Settings > General)? The Activity tab then says *Would dot ...*.
* Is the rule **Only people in the queue** (or **Strict**) chosen on Settings > Time \& queue? The first line in the Activity tab when the timer starts says which rule is on.
* Was the mic free with nobody waiting? Only the **Strict** rule dots in that case. With **Only people in the queue** the Activity tab says *the mic was free and nobody was waiting* and nothing is done. Was the person already on the mic when you clicked Connect? They are never dotted for that.
* Is the person on your **Admins** list? Admins are never dotted. A name colour only counts when the person is alone on the mic.
* A line starting **QUEUE ONLY** (or **QUEUE ONLY (strict)**) in the Activity tab means the timer saw it and tried to dot. If it says *Couldn't dot ...* the dot itself failed (see *It does not dot anyone* below). You must be an admin or the owner of the room.

### Someone was dotted for taking the mic without being in the queue and should not have been

* Check the Activity tab. The line starting *QUEUE ONLY* says who was talking and who was waiting. The person's hand must have been up before they took the mic: if Paltalk gave them the mic within a second of the hand going up, the timer never saw the hand.
* Add trusted people to the Admins list (Settings > Admins), or choose a gentler rule in Settings > Time \& queue. With **Strict**, someone Paltalk puts on the mic in the same second they raise a hand can be dotted: **Only people in the queue** does not do that.
* To take a dot off early, type `!undot-nickname` as an admin, or remove it by hand in Paltalk.

### Someone was dotted for jumping the queue and should not have been

* The timer learns the queue by watching hands go up. People who were already in the queue when you clicked Connect count as equal: they are never judged against each other. It cannot know their real order.
* Check the Activity tab. The line starting *QUEUE JUMP* names who was waiting ahead of them and for how long. If that person had really lowered their hand, the timer allows a few seconds before it notices.
* Admins are never dotted. Add trusted people to the Admins list (Settings > Admins).
* To switch the timer and the rule off for a while, tick **Free mic** at the top of Settings > Time \& queue. To be more patient with someone at the front who is slow to take the mic, raise *Next in line has to take an empty mic within (seconds)*.

### It does not dot anyone

* Untick TEST MODE (Settings > General).
* Make sure you are an admin or the owner of the room.
* Keep the Paltalk room window visible on screen, not minimised.
* Is the person on your Admins list? Admins are never dotted.
* Open Tools > **Inspect Paltalk** and send the files it saves in the logs folder.

### !dot or !undot is ignored

The person typing it must be on the Admins list, spelled exactly as in Paltalk, and you must have clicked Save after changing the list. The command must also be the whole message.

### I hear no sounds

* Settings > Sounds: *Sounds ON* is ticked and the volume is above 0.
* Settings > Sounds: Speakers is ticked for that event. Click **Test**.
* Check your Windows volume and that the right speakers are the Windows default.

### The room does not hear the sounds

* Settings > Sounds: tick **Room (mic)** for that event.
* Untick TEST MODE. Nothing goes into the room in test mode.
* Set up the audio path (way A or B under Sounds), and either be sending your microphone in Paltalk or tick **Take the mic**.

### Take the mic does not click the mic

* Untick TEST MODE. While it is on, Activity only says *Would take the mic ...*.
* Settings > Sounds: Room (mic) must be ticked for that event, and Sounds ON must be ticked.
* If sounds only play at the end of a turn, tick *Play each sound the moment it happens*. Activity says *Skipped the ... sound on the mic - the mic was busy* when a sound had to be dropped.
* Pick the mic style that matches your Paltalk (click, hold or automatic).
* Keep the Paltalk room window visible, not minimised.
* Tools > **Find the mic button**. If it says none found, click **Teach it the mic button** and hold the mouse still over Paltalk's mic button for 2 seconds.
* Tools > **Test the mic** (when the mic is free) shows in Activity exactly which step failed.

### The horse race caller has no voice

* The voice is made the first time the sound is used, in the background. Wait a few seconds and play it again. Activity says *The horse race caller's voice is ready* when it is.
* If Activity says *Couldn't make the horse race caller's voice*, it gives the reason (for example Windows has no speech voice installed, or PowerShell is blocked on your PC). Fix that and press **Reload sounds** on the Soundboard tab to try again.
* You can always put your own recording in the sounds folder as *Race caller voice only.wav*.

### My .wav file is not in the list

Put it in the sounds folder and click **Reload sounds** on the Soundboard tab. Use plain .wav files up to 30 seconds.

### Things to know while it runs

* Keep the Paltalk room window open and not covered by other windows. The timer right-clicks names in it to dot people.
* When it dots or undots someone, your mouse moves by itself for a second or two. Let it finish.

### The program closed by itself, or a window looks wrong

The timer catches unexpected problems and keeps running. It writes each one, with the time, to **crash.log** in the logs folder (Tools > **Open logs folder**). If it ever does close on its own, it writes a line there first. If someone was dotted at that moment, take their dot off by hand - the timer is not running to do it. Please send crash.log to SodaDaPimp.

### A second copy does not open

Only one copy of the timer can run from the same folder, because two copies would fight over the same room and dot people twice. Starting it again just brings the running window to the front. If you cannot see it, look for it in the taskbar.

### Still stuck

Open Tools, click **Run diagnostics**, and send the report plus the newest file from the logs folder to SodaDaPimp.

## Build from source

Everyone can just download the `.ZIP` from the [Releases page](https://github.com/SodaDaPimp/PALTALK-MIC-TIMER/releases).

## Credits and disclaimer

**PALTALK MIC TIMER 2.0** - created and coded in C++ by **SodaDaPimp**. This is an independent tool. It is not made by, endorsed by or affiliated with Paltalk.

