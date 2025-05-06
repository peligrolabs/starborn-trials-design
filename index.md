---
layout: default
title: Home
nav_order: 1
---

### Overview
{: .no_toc .fs-9 }

This document makes up the <i>Starborn Trials Game Design Document</i> which is the game prototype design used to inform implementation strategies for the architecture of Peligro Labs' [AetherCore](https://github.com/peligrolabs/AetherCore) game framework. This design document is open source and can its GitHub repository can be accessed here: [Starborn Trials Design](https://github.com/peligrolabs/starborn-trials-design).
{: .fs-6 .fw-300 }

<p align="left">
    <img
        alt="Starborn Trials Logo"
        src="./assets/logos/starborn-trials-logo.png"
        width="300"
    />
</p>

> <b>Figure 1</b>: Starborn Trials logo.

<!-- [Purpose](./purpose.html){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [Architecture](./architecture.html){: .btn .fs-5 .mb-4 .mb-md-0 } -->

### Table of Contents
{: .no_toc .text-delta }

* TOC
{:toc }

---

### 1. Purpose of the Prototype

To begin construction of the AetherCore Game Framework, designed to power Quest for the Morningstar, Trinity Fighters, Cyber Surfers, and future titles by:
- Establishing core modular systems
- Testing plug-in integration (BeeHave, Dialogue)
- Proving architectural scalability for MMO-lite infrastructure
- Serving as an “Initiation Game” that captures mythos and mechanics

---

### 2. Genre & Core Loop

<b>Genre</b>: 2D top-down action RPG<br>
<b>Loop</b>: Explore → Fight → Speak → Grow → Traverse
- Unlock secrets of a single World-Server Seed Map
- Combat mythic beasts, uncover relics, dialogue with spirit-NPCs
- Receive temporary “Blessings of the Aether” that alter combat/play
- Reach the Ember Chamber, survive the Trial

---

### 3. Core Systems for Prototype

| System  | Details |
| ------------- | ------------- |
| Day / Night System  | Influences ambient creatures, combat difficulty, available quests  |
| World Zoning (Octograph)  | World split into 8 navigable regions—each zone with unique traits  |
| Enterable Buildings  | Scene transitions with persistence  |
| Open World Map  | 2D tile-based with procedural map seeded per World-Server  |
| World-Server Seed Logic  | Each server runs a persistent, procedurally-generated map until a scheduled “apocalypse”  |
| Combat System  | Combo- and dodge-heavy; spiritual affinities; inspiration from Dragalia Lost & Genshin Impact  |
| RPG Mechanics  | Ability loadouts, gear upgrades, stat growth (Xenoblade/Maple Story influence)  |
| Dialogue System  | Branching, emotion-tagged NPC interactions using a chosen plugin  |
| AI (BeeHave Plugin)  | For both enemies and NPC behavior trees  |
| UI & Inventory Framework  | Modular UI skin; items, blessings, and relic management  |

---

### 4. Network Infrastructure

| Layer  | Tech Stack |
| ------------- | ------------- |
| Lobby Server  | .NET Core / Rust / Go  |
| Lobby Client  | Godot (preferred) or React Native  |
| Game Server  | Godot (preferred) or .NET Core / Rust / Go  |
| Game Client  | Godot  |

---

### 5. Narrative Frame

> <i>In the wake of a cosmic apocalypse, the Aether’s sparks scatter into World-Seeds. One fragment—you—awakens in a fractured world of fire and shadow. You must survive the Fire Gauntlet to rekindle the Flame of the Morningstar.</i>

<b>Note</b>: For Starborn Trials game prototype only.

---

### 6. Milestone-Based Development Timeline

| Phase  | Goals  | Duration  |
| ------------- | ------------- | ------------- |
| 1. Blueprint & Scaffolding  | ECS base, Octograph map logic, server architecture sketch  | 1 week  |
| 2. Player Control & Combat  | Core movement/combat loop, targeting, damage types  | 2-3 weeks  |
| 3. AI & Day/Night Cycle  | BeeHave behavior trees, time cycle affecting AI & lighting changes  | 2 weeks  |
| 4. Dialogue & Inventory  | Dialogue system & dynamic inventory loadouts  | 2 weeks  |
| 5. World-Server Seed System  | Procedural map logic, enter/exit buildings  | 2–3 weeks  |
| 6. Lobby Infrastructure  | MVP client/server architecture, server switching  | 1–2 weeks  |
| 7. Final Integration & Playtesting  | Polish, bugfixes, stress tests  | 1 week  |

<b>Note</b>: These are suggested timelines for developers working on AetherCore.

---

### 7. Architecture Diagrams

#### AetherCore - Network Architecture: An Orchestration of Realms

<p align="left">
    <img
        alt="AetherCore Full Network Design Diagram"
        src="./assets/diagrams/AetherCore-full-network-design.png"
        width="1000"
    />
</p>

> <b>Figure 2</b>: This diagram illustrates the distributed network topology of the AetherCore Game Framework—a modular, scalable backend architecture designed for real-time multiplayer gameplay. It delineates the interactions between the Main Server (handling account systems and monetization), Region Servers powered by Agones (spawning dynamic Lobby and World server pods), and the Player Machine. The Game Client communicates via HTTP, WebSockets, and UDP protocols to synchronize world state, leveraging Godot-based instances across zones for seamless gameplay. Persistent storage, backups, and RESTful APIs ensure resilience, modularity, and expansibility for a living virtual cosmos.

#### AetherCore - Network Architecture: Prototype Design

<p align="left">
    <img
        alt="AetherCore Network Infrastructure Diagram"
        src="./assets/diagrams/AetherCore-network-infra-diagram-cropped.jpg"
        width="600"
    />
</p>

> <b>Figure 3</b>: Lobby Server manages world-server routing, player profiles, and matchmaking. Game Server handles in-game logic per persistent world-server seed.

#### AetherCore - Core Systems Layer

<p align="left">
    <img
        alt="AetherCore Core Systems Diagram"
        src="./assets/diagrams/AetherCore-core-systems-diagram-cropped.jpg"
        width="600"
    />
</p>

> <b>Figure 4</b>: These persistent systems form the foundation of the AetherCore game framework, enabling procedurally generated worlds, interactive NPCs, combat, and dynamic behavior.

#### AetherCore - Player Interaction & Game World Layer

<p align="left">
    <img
        alt="AetherCore Player Interaction & Game World Layer Diagram"
        src="./assets/diagrams/AetherCore-player-interaction-and-game-world-layer-diagram-cropped.jpg"
        width="600"
    />
</p>

> <b>Figure 5</b>: This layer defines the visible, touchable, and explorable world of Aether. All player-facing systems—characters, enemies, professions, interactions, and UI—reside here.

#### AetherCore - Storage & Save Architecture

<p align="left">
    <img
        alt="AetherCore Persistent Storage & Save/Load Architecture Diagram"
        src="./assets/diagrams/AetherCore-storage-and-save-state-diagram-cropped.jpg"
        width="600"
    />
</p>

> <b>Figure 6</b>: This layer stores all persistent information across sessions including player states, world evolution, relationship trees, timeline-linked events as well as players' skill, level, & professions progression.

---

Copyright &copy; 2025 [Peligro Labs, LLC](https://peligrolabs.com/).