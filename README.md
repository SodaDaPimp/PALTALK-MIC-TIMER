# Paltalk Mic Timer
https://www.youtube.com/watch?v=EVKKVns7Xj4

**A Windows mic timer, mic queue and auto-dot tool for Paltalk room admins. Written in C++.**

![Platform: Windows 10 and 11](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078D6)
![Language: C++17](https://img.shields.io/badge/language-C%2B%2B17-00599C)
![Made for Paltalk room admins](https://img.shields.io/badge/made%20for-Paltalk%20admins-C81E2D)

Paltalk Mic Timer keeps your Paltalk room fair. It times whoever is on the mic, posts warnings in the room, **dots (restricts) anyone who goes over the limit**, explains why, and removes the dot a few seconds later. Your admins can also dot and undot from chat with `!dot-nickname` and `!undot-nickname`. One small program, no installer.

![Paltalk Mic Timer showing the speaker on the mic, the mic queue and the activity log]([[https://raw.githubusercontent.com/SodaDaPimp/PALTALK-MIC-TIMER/refs/heads/main/Screenshot%202026-11-10%20100218.png]

## Table of contents

- [What is Paltalk Mic Timer?](#what-is-paltalk-mic-timer)
- [Features](#features)
- [Requirements](#requirements)
- [Download and quick start](#download-and-quick-start)
- [First-time setup](#first-time-setup)
- [What it posts in the room](#what-it-posts-in-the-room)
- [Admin commands: !dot and !undot](#admin-commands-dot-and-undot)
- [Settings](#settings)
- [Practice room (no Paltalk needed)](#practice-room-no-paltalk-needed)
- [While it is running](#while-it-is-running)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)
- [Build from source](#build-from-source)
- [Credits and disclaimer](#credits-and-disclaimer)

## What is Paltalk Mic Timer?

Paltalk Mic Timer is a desktop helper for people who run **Paltalk chat rooms** as an admin or owner. Voice rooms with a busy mic queue need someone to keep time, give warnings and restrict people who hold the mic too long. This program does that automatically, the same way you would: it reads who is on the mic, counts their time, posts in the room, and uses Paltalk's own right-click **Restrict** and **Remove Restrictions** options to dot and undot.

It is built for room owners and admins who want a **mic time limit**, a visible **mic queue**, and **admin chat commands** without watching the clock themselves.

## Features

- **Mic time limit.** Set any limit you like. 120 seconds is 2 minutes, 180 is 3 minutes.
- **Live speaker cards and mic queue.** See who is on the mic, how long they have talked, and who has a hand up, in order.
- **Automatic warnings.** Time-remaining reminders every 30 seconds, a final warning in the last seconds, and a grace period at the limit.
- **Auto-dot and auto-undot.** Dots a speaker who stays on after the grace period, explains why in the room, then removes the dot.
- **Admin chat commands.** `!dot-nickname` and `!undot-nickname`, usable only by the admins you list. No cooldown.
- **Admin list.** Admins you list are never timed or dotted by the timer, and cannot be dotted by command.
- **Dead air check.** If the person on the mic is silent for 15 seconds, it posts a mic check.
- **Nickname colour rules.** Optionally skip the time limit for names in colours you choose, such as orange or purple.
- **Custom room messages.** Rewrite every message the timer posts. Leave one empty to stop it posting.
- **Test mode.** Shows what the timer would do without dotting or posting. It starts this way.
- **Commands-only mode.** Turns off the timer and alerts but keeps `!dot` and `!undot` working.
- **Practice room.** A pretend Paltalk room so you can try everything first.
- **Speaker stats.** Turns, total talk time, longest turn, warnings and dots for each speaker.
- **Logs and diagnostics.** Daily log files plus built-in tools that save what the timer sees if something goes wrong.
- **Single program.** One `.exe`. Settings are saved in a `config.json` file next to it.

## Requirements

- Windows 10 or 11.
- The Paltalk desktop app, signed in.
- **Admin or owner rights in the room.** The timer dots people the same way you do, so it needs your permissions.

Nothing else to install.

## Download and quick start

1. Download **Paltalk Mic Timer Created by SodaDaPimp.exe** from the [Releases page](https://github.com/SodaDaPimp/PALTALK-MIC-TIMER/releases) and put it in its own folder.
2. Open Paltalk and join your room.
3. Double-click the `.exe`.
   If Windows shows **Windows protected your PC**, click **More info**, then **Run anyway**. Windows shows this for any program it has not seen before.
4. Pick your room in the **Room** box. If you do not see it, click **Refresh**.
5. Click **Connect**. The timer posts a line in the room to say it is connected.
6. To stop, click **Disconnect** or close the window. It removes any dot it is still holding and posts that it has disconnected.

The timer creates these next to the `.exe`:

```text
Paltalk Mic Timer Created by SodaDaPimp.exe
config.json        your settings
logs/              one log file per day
```

## First-time setup

The timer starts in **test mode**. Nobody is dotted and no timer messages are posted until you turn it off.

1. Open the **Settings** tab.
2. In the **Admins** box, type your own nickname and each admin's nickname, one per line. Spell them exactly as they appear in Paltalk.
3. Click **Save admins, colours & messages**.
4. Set the mic time limit if you want something other than 2 minutes.
5. Untick **Test mode**. The timer is now live.

## What it posts in the room

With the default messages, a turn on the mic looks like this:

```text
[Name] has taken the mic. Allocated time: 2 minutes.
1 minute remaining for [Name].
10 seconds left! Please wrap up and pass the mic.
```

At the limit there is a 5 second grace period. If the speaker is still on the mic after that, the timer dots them, explains why in the room, and removes the dot a few seconds later.

If the person on the mic is silent for 15 seconds, it posts a mic check (dead air). When it connects and when it disconnects, it posts a credit line. The credit line is built in and cannot be switched off.

You can reword any of these messages on the Settings tab.

## Admin commands: !dot and !undot

Admins on your list can type these in the room:

```text
!dot-nickname       dots that person
!undot-nickname     removes the dot
```

Example:

```text
!dot-BigMike
!undot-BigMike
```

- The command must be the whole message. A sentence that only mentions `!dot` is ignored.
- A dot given by command stays until an admin removes it.
- Admins cannot be dotted by command.
- Anyone who is not on the admins list gets a short reply saying only admins can use the commands.
- There is no cooldown.

## Settings

All settings are on the **Settings** tab. Most save automatically. Click **Save admins, colours & messages** after editing the admins, colours or messages.

| Setting | What it does |
|---|---|
| Mic time limit | How long someone may hold the mic, in seconds. |
| Final warning | How many seconds before the limit the last warning is posted. |
| Grace period | Seconds after the limit before the dot. |
| Time remaining reminders | How often the time left is posted. `0` turns them off. |
| Auto-dot | Dot people who go over the limit, then remove the dot. |
| Dead air check | Post a mic check when the person on the mic is silent. |
| Admin commands | Let listed admins use `!dot-name` and `!undot-name`. |
| Name colour rules | Skip the time limit for the colours you list. |
| Test mode | Show what would happen without doing it. |
| Commands only | Turn off the timer and alerts, keep the commands. |
| Keep on top | Keep the timer window above other windows. |
| Room messages | Change the wording of every message the timer posts. |

Message text can use placeholders such as `{name}`, `{limit_text}` and `{talked}`.

## Practice room (no Paltalk needed)

Want to see how it works first?

1. In the **Room** box choose **Practice room (no Paltalk needed)**.
2. Click **Connect**. A Practice window opens.
3. Pick a pretend person and click **Take mic**.
4. Watch the timer count, warn, dot, explain and undot.

Tip: set the time limit to 30 seconds on the Settings tab to see the whole cycle quickly. You can also type `!dot-name` as a pretend person.

## While it is running

- Keep the Paltalk room window open and not covered by other windows. The timer right-clicks names in it to dot people.
- When it dots or undots someone, your mouse moves by itself for a second or two. Let it finish.
- The dead air check listens to the level of the sound playing on your PC. It does not record anything. Music or a video playing on your PC counts as sound.

## Troubleshooting

**"No Paltalk rooms found"**
Join the room in Paltalk first, then click **Refresh**. If Paltalk was started as administrator, right-click the timer `.exe` and choose **Run as administrator** too.

**It does not dot anyone**
- Make sure **Test mode** is unticked.
- Make sure you are an admin in the room.
- Make sure the Paltalk room window is visible on screen.
- Open the **Tools** tab, click **Inspect Paltalk**, and send the files it saves in the `logs` folder to SodaDaPimp.

**`!dot` or `!undot` is ignored**
The person typing it must be on the admins list, spelled exactly as in Paltalk. Click **Save** after changing the list.

**Nothing shows under "On the mic"**
Open the **Tools** tab and click **Read the room now**. If it reports a problem, click **Run diagnostics**.

**Still stuck**
Open the **Tools** tab, click **Run diagnostics**, and send the report file plus the newest file from the `logs` folder to SodaDaPimp.

## FAQ

### What does "dotting" mean in Paltalk?
Dotting is Paltalk's **Restrict** option on a member's right-click menu. **Remove Restrictions** undoes it. The timer uses both for you.

### Do I need to be an admin?
Yes. You must be an admin or the owner of the room, because the timer uses your own permissions to dot and undot.

### Does it record my audio?
No. The dead air check only looks at how loud the sound on your PC is. Nothing is recorded or saved.

### Can I try it without a live Paltalk room?
Yes. Choose **Practice room (no Paltalk needed)** in the Room box.

### Who can use `!dot` and `!undot`?
Only the admins you list in Settings. Anyone else gets a short reply saying the commands are for admins.

### Why does my mouse move on its own?
Paltalk's right-click menu is driven with the mouse, so the timer moves your pointer for a second or two when it dots or undots someone.

### Which version of Windows do I need?
Windows 10 or 11.
```## Credits and disclaimer

**Paltalk Mic Timer** — coded in C++ by **SodaDaPimp**.

This is an independent tool. It is not made by, endorsed by or affiliated with Paltalk.
