# Hellcat

Multiplayer arena game for Souls-like fans, built in public with Devin bots.

## The game

- 8-player arena, third-person melee combat
- Dodge-roll with i-frames, stamina that gates every action and regens
- One training dummy with HP to warm up on
- Death screen + respawn, keep fighting

## Stack

- Server: Node + `ws`, authoritative, fixed 20Hz tick
- Client: Three.js + Vite
- Language: TypeScript, strict everywhere
- Repo: npm workspaces monorepo — `apps/server`, `apps/client`, `packages/shared`
- Hosting: own VPS for dev/testing, cheap VPS for the live server once real players show up, frontend stays static

## How it works

The server is the authority. Clients send inputs, never positions.
`packages/shared` is the single source of truth for the versioned JSON protocol.

### Events

Client → server:

- `join` { name }
- `input` { seq, x, z, sprint, roll }
- `attack` — on click, server checks range, arc, stamina

Server → client:

- `snapshot` { tick, players: [...] } — 20Hz, the whole game state
- `damage` { target, amount, from }
- `death` { player }
- `respawn` { player, pos }

## Day 1 — the skeleton

- Working monorepo: server + client + shared protocol
- One arena room, up to 8 players, two browsers seeing each other live
- Melee by range + arc, dummy with HP
- 20Hz tick stable for 10 minutes with 2 clients

Out of scope for day 1: matchmaking, accounts, DB, chat, inventory, classes, levels/XP, boss phases, sound, real art, mobile, anti-cheat, deployment/CI.

## How it's built

Devin builds it via PRs. I review every PR and playtest as a Souls fan.
Working rules: no `any` without a comment, no silent TODOs in the critical path,
every PR states what changed and how to test it.

## Status

In testing — AI helps with the testing.
