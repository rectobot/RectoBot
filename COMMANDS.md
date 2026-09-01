# ⚡ Recto — Complete Command Documentation & Guide

Welcome to the official command manual for **Recto**, the high-performance, next-generation Discord role engine, statistics counter, and graphics suite.

All interactions in Recto are powered by official Discord Slash Commands (`/`), interactive button components, and select menus with sub-18ms execution times.

---

## 📑 Table of Contents
1. [🎭 Role Management Suite](#-role-management-suite)
   - [🔘 Button Roles Studio (`/roles button`)](#-button-roles-studio-roles-button)
   - [🔽 Dropdown Select Roles (`/roles dropdown`)](#-dropdown-select-roles-roles-dropdown)
   - [⚡ Temporary & Timed Roles (`/temprole`)](#-temporary--timed-roles-temprole)
   - [🤖 Auto Roles on Join (`/autorole`)](#-auto-roles-on-join-autorole)
2. [⭐ Reaction Roles System (`/reaction`)](#-reaction-roles-system-reaction)
3. [📊 Live Server Counters (`/counter`)](#-live-server-counters-counter)
4. [🖼️ Canvas Welcome & Graphic Studio (`/welcome`)](#️-canvas-welcome--graphic-studio-welcome)
5. [🎨 Interactive Embed Studio (`/embed`)](#-interactive-embed-studio-embed)
6. [🛡️ Audit Logging & Security (`/logs`)](#️-audit-logging--security-logs)
7. [⚙️ System & Utilities (`/ping`, `/stats`, `/help`)](#️-system--utilities-ping-stats-help)

---

## 🎭 Role Management Suite

### 🔘 Button Roles Studio (`/roles button`)
Create customizable button panels in any channel where members click buttons to claim or remove roles.

```bash
/roles button channel:#roles-channel
```

* **Interactive Features:**
  - **Live Preview:** Renders an in-chat simulation of the embed and attached buttons before publishing.
  - **Customizable Buttons:** Choose between 4 button styles (`Primary Blurple`, `Secondary Gray`, `Success Green`, `Danger Red`), custom labels, and emojis.
  - **Modes:** Support for `Toggle` (add/remove), `Give Once` (verification gate), and `Remove` (strip role).
  - **Zero Rate-Limit Lag:** Handled via Discord Component interactions.

---

### 🔽 Dropdown Select Roles (`/roles dropdown`)
Deploy sleek dropdown select menus where users choose one or multiple roles in a single interactive menu.

```bash
/roles dropdown channel:#roles-channel title:"Select Your Gaming Squad" placeholder:"Choose your favorite games..."
```

* **Parameters:**
  - `channel` *(Required)*: Target text channel.
  - `title` *(Optional)*: Title for the embed panel.
  - `placeholder` *(Optional)*: The placeholder text displayed inside the select menu.
  - `min_values` / `max_values`: Control how many roles a member can select simultaneously.

---

### ⚡ Temporary & Timed Roles (`/temprole`)
Assign roles that automatically expire after a set duration. Perfect for VIP subscriptions, tournament badges, or timed access passes.

```bash
/temprole give user:@Alex role:@VIP duration:30d reason:"VIP Monthly Pass"
```

* **Available Subcommands:**
  - `/temprole give user role duration [reason]` — Grants a temporary role.
    - Supported duration formats: `10m`, `2h`, `7d`, `30d`, `1y` (up to 1 full year).
  - `/temprole list [user]` — Lists all active temporary roles with countdown expiration timestamps.
  - `/temprole revoke user role` — Instantly cancels a temporary role assignment.

---

### 🤖 Auto Roles on Join (`/autorole`)
Automatically grant specific roles to new members or invited bots the moment they join your server.

```bash
/autorole add role:@Member target:humans
/autorole add role:@VerifiedBots target:bots
```

* **Available Subcommands:**
  - `/autorole add role target` — Adds a role to the automatic join dispatcher (`humans`, `bots`, or `all`).
  - `/autorole list` — Displays all configured auto-roles.
  - `/autorole remove role` — Deletes an auto-role rule.

---

## ⭐ Reaction Roles System (`/reaction`)

Attach reaction roles to **any** message in your server (existing announcement messages, rules, embeds, or bot messages).

```bash
/reaction add message:https://discord.com/channels/... emoji::tada: role:@GiveawayPings mode:toggle
```

### Subcommands & Options:

#### `/reaction add`
| Option | Type | Description |
| :--- | :--- | :--- |
| `message` | `String` *(Required)* | Message Link or Message ID. |
| `emoji` | `String` *(Required)* | Unicode emoji (`⭐`), Shortcode (`:tada:`), Custom Tag (`<:name:id>`), or Emoji ID. |
| `role` | `Role` *(Required)* | The Discord role to assign or remove. |
| `mode` | `Choice` | `toggle` (default), `give_once`, `remove`, `exclusive` (radio group), or `temp`. |
| `duration` | `String` | Expiration time if mode is `temp` (e.g. `24h`, `7d`, `30d`). |
| `required_role`| `Role` | Prerequisite role required before claiming this role. |
| `max_uses` | `Integer` | Usage cap (e.g. only first 50 users can claim). |
| `group` | `String` | Group name for radio/exclusive selection (e.g. `colors`). |
| `dm_message` | `String` | Custom DM notification sent to the member on reaction. |

#### Other Reaction Subcommands:
* `/reaction remove message:URL emoji::tada:` — Unbinds a single reaction role from a message.
* `/reaction list` — Lists all reaction roles across the entire server.
* `/reaction clear message:URL` — Removes all reaction role bindings from a specific message.

---

## 📊 Live Server Counters (`/counter`)

Create locked voice channels that track real-time server statistics with automatic live synchronization.

```bash
/counter create type:all_members style:spark
```

### Metrics & Styles:
* **Counter Types:**
  - `all_members` — Total server members (Humans + Bots).
  - `human_members` — Real human members only.
  - `bot_members` — Bot count.
  - `boost_count` — Active server Nitro boosts.
  - `online_members` — Online members count.

* **Style Presets:**
  - `✦ Spark`: `✦ Members: 1,420`
  - `・Dot`: `・Members: 1,420`
  - `◈ Diamond`: `◈ Members: 1,420`
  - `[ Boxed ]`: `[ Members: 1,420 ]`
  - `| Bar`: `| Members: 1,420`
  - `Clean`: `Members: 1,420`

### Counter Subcommands:
* `/counter create type [style] [custom_name]` — Creates a new tracked voice channel.
* `/counter list` — Lists active server counters and current cached metrics.
* `/counter sync` — Forces an instant update of all counter channel names.
* `/counter remove channel:#channel` — Deletes and unregisters a counter channel.

---

## 🖼️ Canvas Welcome & Graphic Studio (`/welcome`)

Recto features a native high-resolution **Canvas 2D Engine (1024×460)** that renders custom graphical welcome cards with glowing avatar borders, server icons, custom gradient themes, and customizable text.

```bash
/welcome studio
```

### Features:
* **5 Built-in Themes:** `Cyberpunk Neon`, `Neon Glow`, `Galaxy Cosmic`, `Sunset Horizon`, `Minimal Luxury`.
* **Direct Image Support:** Use external image URLs or upload local banner files via the Web Dashboard.
* **Smart Variable Interpolation:**
  - `{user}` — User mention (e.g. `@Alex`)
  - `{username}` — Username (e.g. `Alex`)
  - `{server}` — Server Name
  - `{count}` — Formatted Member Count (e.g. `#1,250`)
* **Commands:**
  - `/welcome studio` — Opens the in-chat welcome configuration studio.
  - `/welcome test` — Dispatches a live simulated welcome message to the configured channel.
  - `/welcome preview` — Renders a temporary preview of your current Canvas welcome card.

---

## 🎨 Interactive Embed Studio (`/embed`)

Design embeds directly inside Discord without needing external json editors.

```bash
/embed create channel:#announcements
```

* **Interactive Controls:**
  - **Edit Title & Description** via popup Discord Modals.
  - **Set Color Palette** with hex codes or quick-select colors.
  - **Add Fields** (inline or full-width).
  - **Add Images & Thumbnails**.
  - **Set Author & Footer** details.
  - **Attach Action Buttons** directly below the embed.

---

## 🛡️ Audit Logging & Security (`/logs`)

Track and record all role modifications, permission checks, and server configurations in a dedicated logging channel.

```bash
/logs set channel:#audit-log
/logs toggle dm_notifications:true
```

* **Recorded Events:**
  - Role claimed / removed via reactions or buttons.
  - Temp role assignment and automated expiry sweeps.
  - Permission hierarchy protection warnings.
  - Counter creations, auto-setups, and deletions.

---

## ⚙️ System & Utilities

* `/ping` — Measures bot WebSocket heartbeat, REST API round-trip, and SQLite query latency.
* `/stats` — Displays real-time memory usage (RAM), total servers, active counters, and role engine uptime.
* `/help` — Categorized help menu with direct links to the Web Dashboard and Support.

---

<div align="center">
  <sub>Built for speed, reliability, and modern communities • <strong>Recto Role Engine</strong></sub>
</div>
