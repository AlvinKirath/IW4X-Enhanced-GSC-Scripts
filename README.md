# IW4X-Enhanced-GSC-Scripts
Enhanced and custom GSC scripts for IW4X: Gun Game improvements, a new Next Match menu, bot/server utilities, and experimental multiplayer enhancements.
IW4X Enhanced GSC Scripts

A collection of enhanced and custom GSC scripts for IW4X, focused on improving multiplayer servers, Gun Game, bot behavior, and match management.

These scripts are intended for experimentation, custom servers, and personal IW4X setups. Some scripts are based on or modified from IW4X's original rawfiles, while nextmatch.gsc is a new script created specifically for this collection.

What's included

maps/mp/gametypes/gun.gsc

An enhanced version of the IW4X/MW2 Gun Game gametype.

Changes and additions include:

Expanded/custom Gun Game weapon progression.

A curated 42-tier weapon list.

Riot Shield removed from the progression and replaced with an RPG.

Deaths no longer intentionally reduce the player's Gun Game weapon rank.

Random weapon-attachment support using actual weapon asset names.

Attachment selection checks the available IW4X weapon list before choosing a combination.

Supports legitimate one- and two-attachment weapon variants when those assets exist.

90-second interval for the custom Gun Game lead/status voice logic.

Bot knife/melee disabled for Gun Game.

Existing Gun Game score and progression behavior is otherwise kept close to the original implementation.

The attachment system is designed around IW4X's existing buildWeaponName() mechanism. The script first selects candidate attachments and then builds the final weapon name used by _giveWeapon().

scripts/nextmatch.gsc

A new custom Next Match menu written for this project.

The script adds an in-game host menu for changing the next match without manually editing the server configuration.

Current functionality includes:

Host-only menu handling.

Game-type selection.

Map-category navigation.

Original-map selection.

DLC/map-pack categories.

Custom-map category support.

Start-next-match controls.

Match/map DVAR handling.

Automatic host-spawn recovery logic.

On-screen loading feedback.

Debug messages for troubleshooting.

This file is not a stock IW4X rawfile replacement; it was created as a standalone script for this project.

maps/mp/gametypes/_teams.gsc

An enhanced/modified version of the IW4X team-management script.

The modified version is used together with the custom gametypes and server setup in this repository. Changes are intended to preserve normal IW4X team/player behavior while allowing the custom gametypes and bot/server features in this collection to coexist.

Use this file only when the corresponding custom setup requires it.

maps/mp/gametypes/_gamelogic.gsc

A modified copy of IW4X's core gametype logic.

This file exists to support the custom gametype environment and the additional server behavior used by the included scripts.

Because _gamelogic.gsc is a shared core script, replacing it can affect multiple gametypes. Back up the original before installing.

maps/mp/bots/_bot_utility.gsc

Bot Warfare utility code used by the bot system.

This is derived from the Bot Warfare project by INeedGames and should be treated as third-party code rather than original code from this repository.

Bot Warfare provides shared helpers for:

Bot engine built-ins.

Movement and stance.

ADS, firing, fragging and smoke actions.

Bot state checks.

Objectives and scripted goals.

Weapon/loadout handling.

Weapon attachment handling.

Console/file helper functions.

See the Credits section before redistributing modified copies of this file.

Installation

Simple userraw installation

For scripts that do not require replacing a stock gametype/core file:

Create the required directory under your IW4X installation, for example:

IW4X/
└── userraw/
    ├── maps/
    │   └── mp/
    │       └── gametypes/
    └── scripts/

Copy each GSC to the same path expected by IW4X.

Start IW4X and test the relevant gametype.

Important: core file replacements

Files such as:

maps/mp/gametypes/_teams.gsc
maps/mp/gametypes/_gamelogic.gsc

are shared game scripts.

Do not blindly overwrite your working files without making a backup.

Recommended:

Backup/
├── _teams.gsc.original
├── _gamelogic.gsc.original
└── gun.gsc.original

Compatibility

These scripts are written for IW4X and may depend on IW4X-specific GSC functions or behavior.

They are not guaranteed to work unchanged on:

stock MW2,

AlterWare clients,

other Call of Duty engines,

other GSC-based clients.

Bot Warfare itself is designed for IW4x and uses engine integrations that are specific to that environment.

Relationship to the original IW4X scripts

The repository contains both new scripts and modified versions of existing IW4X gametype infrastructure.

The main philosophy is:

Preserve the original MW2/IW4X behavior wherever possible, then add the requested customization on top.

Examples:

gun.gsc keeps the original Gun Game structure while changing the weapon progression and adding custom behavior.

_teams.gsc and _gamelogic.gsc remain based on IW4X's original shared systems.

nextmatch.gsc is new rather than a modification of an existing stock script.

The official IW4X rawfiles repository contains the original game rawfiles used by the client. [https://github.com/iw4x/iw4x-rawfiles](https://github.com/iw4x/iw4x-rawfiles?utm_source=chatgpt.com)

Gun Game attachment system

The custom Gun Game attachment system is deliberately weapon-specific.

Instead of assuming that every assault rifle, SMG, or sniper supports the same attachments, it checks whether the corresponding weapon asset exists in the available weapon list.

For example, an attachment is only accepted when the resulting weapon asset actually exists.

This is important because MW2 contains many weapon-specific combinations rather than one universal attachment set.

The script then uses:

buildWeaponName( weaponName, attach1, attach2 );

before giving the weapon.

This is similar in principle to Bot Warfare's loadout handling, which retrieves weapon attachments and passes the resulting values through IW4X's normal buildweaponname() path before _giveweapon(). https://github.com/ineedbots/iw4_bot_warfare

Known limitations

This collection is experimental.

Some behavior may depend on the exact IW4X build, Bot Warfare version, loaded rawfiles, mods, and server configuration.

In particular:

Custom battle chatter behavior may not be identical to normal TDM/War.

Core-script replacements can interact with other server mods.

Attachment availability depends on the weapon assets actually present in the current IW4X installation.

Some experimental configurations may generate runtime warnings/errors even when the match continues to run.

nextmatch.gsc contains debug console messages that can be removed once your installation is stable.

If a script fails to compile, enable IW4X developer script diagnostics so the console reports the exact file and line.

Development notes

These scripts were developed incrementally through live IW4X testing.

The preferred workflow is:

Back up the original script.

Change one subsystem at a time.

Start IW4X with developer script diagnostics enabled.

Test the relevant gametype.

Check the console for compile/runtime errors.

Keep working behavior unchanged unless a change is intentional.

For shared scripts such as _gamelogic.gsc and _teams.gsc, test multiple gametypes after making changes.

Credits

IW4X

Original IW4X rawfiles and gametype infrastructure:

https://github.com/iw4x/iw4x-rawfiles

IW4X is a community-driven project extending Call of Duty: Modern Warfare 2 (2009).

Bot Warfare

Bot-related code is derived from:

IW4 Bot Warfare — INeedGames

https://github.com/ineedbots/iw4_bot_warfare

Bot Warfare's project explicitly allows code to be used, hosted, modified and merged provided credit is retained. This repository therefore retains attribution for the Bot Warfare-derived code.

License / attribution

Check the original license and attribution requirements for each upstream file before redistributing it.

This repository does not claim ownership of upstream IW4X or Bot Warfare code.

New code created specifically for this collection may be used according to the terms specified by the repository owner, subject to any upstream code contained in the same file.

Contributing

Bug reports, improvements, compatibility fixes and new IW4X GSC experiments are welcome.

When submitting a change, please include:

the IW4X build/version,

the affected gametype,

the relevant console error if one exists,

what changed,

and whether the original stock script was modified or a new script was added.

Disclaimer

Use these scripts at your own risk.

Always keep backups of your working IW4X installation and original GSC files before replacing shared gametype scripts.
