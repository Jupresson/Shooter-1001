# Shooter 1001 – High Concept Document

**Author:** Jupresson
**Created:** 12.11.2026

---

## High Concept

A fast-paced multiplayer arena shooter that combines the light and fun atmosphere of Banana Shooter with the precise gunplay of CS:GO and the smooth movement of CS:Source.

**Project goal:** Learn to build multiplayer games from the ground up. We use a **Godot 4 + ENet + GodotSteam** stack because we want to keep our tools as low-level as possible. This way we avoid the "black box" problem and understand how online multiplayer actually works.

---

## Features

- **Precise shooting:** Weapons have learnable recoil patterns, like in CS:GO, and accuracy drops while moving. Hitting shots is skill, not luck.
- **Smooth movement:** CS:Source-style air movement, where strafe jumps carry the player smoothly around the arena.
- **Bunnyhop and wallhop:** Movement techniques from CS:Source and other Source games are added to the game on purpose, not as bugs. They are reasonably hard to learn but possible: a skilled player gains extra speed with them and can reach surprising places.
- **Light and fun style:** Colorful, simple graphics and humor, like Banana Shooter. No serious war theme.
- **Fast arena matches:** Short deathmatch games of about 5–10 minutes on small maps. After dying, the player returns to the game immediately.
- **Easy to play with friends:** Invite a friend through Steam and join a lobby in a couple of clicks.
- **Direct connect and LAN:** The game can also be played over a direct IP connection or on a local network (ENet) without Steam.

---

## Player Motivation

The player competes against other players and tries to get the most kills during a match. They are driven by the desire to compete and by improving their own skill: better aim, better movement and better game sense.

---

## Genre

Multiplayer FPS, arena shooter.

---

## Target Customer

PC gamers aged roughly 13–25 who play games like Counter-Strike 2, Banana Shooter or Krunker, and want fast, skill-based matches with friends without long rounds.

---

## Competition

Banana Shooter, Krunker and Counter-Strike 2.

- **Counter-Strike 2** is serious and slow-paced, and a single round can take a long time.
- **Banana Shooter** is light and fun, but its shooting and movement are not as deep.

This game combines the best parts of both: Counter-Strike's skill ceiling in a light and fast package.

---

## Unique Selling Points

- **CS-level weapon feel:** Learnable recoil patterns and precise hit mechanics in a light, fun game.
- **Intentional bhop and wallhop:** In other games these are often bugs that get patched out. Here they are part of the design and the maps, and mastering them separates a skilled player from a beginner.
- **Quick to get into a match:** No waiting between rounds: instant respawn and short matches.

---

## Target Hardware

PC (Windows, possibly Linux too). Played with mouse and keyboard. Online play requires Steam; direct IP connection or LAN works without it. The goal is for the game to also run on lower-end machines.

---

## Design Goals

- **Skill-based:** The winner is decided by aim and movement. Accuracy depends on what the player is doing: while running or in the air, weapons such as the pistol can shoot well off target, so the player has to pick the right moment to fire. Recoil is always the same, so it can be learned.
- **Fast:** The player gets into a match within seconds and returns to the action immediately after dying. No boring waiting time.
- **Learnable movement:** Bunnyhop and wallhop are reasonably difficult but possible to learn. The game doesn't require them, but they reward practice, so the player always has something new to hone.
- **Fair-feeling netcode:** Hits must feel fair even with latency. Synchronization and lag compensation are built from scratch, which is also the project's most important learning goal.

---

## Characters

Characters are cosmetic: everyone has the same stats, as in Counter-Strike, to keep the game fair. At the start there will be 2–3 different character models, each with its own look and personality (e.g. funny celebrations or voice lines).

---

## Moodboard / Art Exploration / References

_TODO: add images and references._
