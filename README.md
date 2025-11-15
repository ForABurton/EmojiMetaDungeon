# 🕹️ EmojiMetaDungeon

A tiny, experimental, emoji-powered RPG "engine" for the browser. One HTML file. One tiny universe. Internet-enabled infinite chaos.

**EmojiMetaDungeon** is a small, hackable, and "artless" RPG engine with metaverse, hypermedia, and moddability elements designed to be easy to read and modify. It’s ideal for anyone who wants a simple, self-contained example of how to build tile-based worlds, basic gameplay loops, and scripted interactions in the browser without relying on frameworks or really any assets other than code and encoding at all! It also serves as a lightweight playground for procedural generation, RL experiments, small gameplay prototypes, and LLM-driven content ideas. 

Built-in netcode hooks will make it possible to explore minimal multiplayer or “micro-metaverse” protocols with almost no infrastructure, and AI procgen and RL integration hooks are also planned. Overall, this project is a compact environment for exploration, teaching, learning, and low-stakes experimentation.
## ✨ Features & Roadmap

EmojiMetaDungeon "ships" with a wide range of systems in various stages of completeness. This README separates them clearly so contributors and curious hackers know what’s done and what’s still evolving.

### 🎮 Already wired
These systems are complete, integrated, and ready to build upon:
- 🧱 **Emoji Tilemap Renderer** (16×12 interactive grid, with plans for jagged, dynamic, larger, and palisaded rooms)
- 🚶 **Movement + Collision Engine**
- 🧙 **NPC System**  dialog trees, triggers, callbacks
- 🎒 **Inventory + Items**
- ⚔️ **Weapon & Item Scripts**
- 🚪 **Portals & Multi-Room Travel**
- 💾 **Local & Remote Room Loading** (CORS-enabled)
- 🎬 **Animations, effects, message log**
- 🌍 **Room Parsing + Runtime World Model**

These components form the stable backbone of the engine.

### ⚠️ Unintegrated
These systems work individually but still need UI glue, triggers, or deeper gameplay connections. They are powerful in isolation and awaiting their turn in the main loop:
- 📜 **Quest Engine**: Logic + HUD are implemented; NPC trigger wiring still pending.
- ✏️ **Inline Editor Backend**: Tile/entity editing works; needs polished UI + complete export pipeline.
- 🔮 **Procedural Generation Tools**: Perlin noise + Wave Function Collapse generate valid structures but are not yet injected into the runtime room flow.
- 🧪 **DynamicRoom Runtime Generator**: Builds and transforms rooms on the fly; not tied to gameplay events yet.
- 🧠 **LLM-Based Generators**: Promptable generators exist; need integration with the editor flow.
- 🧍‍♂️ **Multiplayer Client Hooks**: Remote player rendering works; handshake/protocol formalization TBD.
- 🌐 **Multiplayer Server Generator Script**: WebSocket server scaffold is included; protocol polish still needed.
- 🤖 **Reinforcement Learning Playground**: Step/reset/observation pipeline functions; no dedicated UI or mode switch yet.

These are the “mid-layer” features, functional foundations awaiting connection to the core loop.

### 🧩 Uncemented
These modules exist as conceptual scaffolding for future features. They work in isolation and provide a structural outline of where the engine can grow next:
- 🔧 **Interactors**  proximity-based action triggers
- 🧩 **PuzzleAssemblage**  multi-step puzzle composer
- 🛠️ **Gadget System**  modular devices (locks, switches, toggles)
- ✨ **MagicEffect Pipeline**  animations and FX sequencing
- 🧪 **Sandboxed Script Execution Architecture**  secure way to run item scripts (probably iframe, WebWorker, or free-monad based, possibly a WASM mini VM)


## 🚀 Getting Started

1️⃣ **Download the Engine**  
Grab the file: `EmojiMetaDungeon.html`  
That’s the whole engine.

2️⃣ **Run it Locally**  
Because the engine loads rooms via fetch(), it must run from HTTP.  
- Node: `npx http-server -p 8080`  
- Python: `python3 -m http.server 8080`  
Any webserver should be fine for local use.

3️⃣ **Visit the Dungeon**  
Open in your browser: `http://localhost:8080/EmojiMetaDungeon.html`  
You’re in.

### 🌐 Remote Rooms & CORS
EmojiMetaDungeon can load room JSON from any URL.
- **Same origin** → no CORS required
- **Different origin** → add: `Access-Control-Allow-Origin: *`, so find a web server that allows configuring this.

Room files can be `.json`, `.txt`, or any extension as long as the content is valid JSON.

Code for integration with pastebins and the like, including "Web3"/distributed-decentralized-object-stores is available.

#### 🗺️ Room Format
Example minimal room:

```json
{
  "name": "start",
  "tilemap": [
    "🌲🌲🌲🌲🌲",
    "🌲🙂 🌲",
    "🌲 🪨🌲",
    "🌲🌲🌲🌲🌲"
  ],
  "portals": [
    { "x": 2, "y": 0, "target": "mountain" }
  ],
  "entities": [],
  "items": []

}
```

Add NPCs, enemies, puzzles, triggers, scripts, or chaos.

### ✏️ Inline Editor (Future)
Press **E** to open the editor. You can:
- Paint tiles
- Add/drag NPCs and enemies
- Drop items
- Create portals
- Edit room JSON
- Script item and NPC behaviors
- Change tilesets
- Export worlds


### ⚔️ Item & Weapon Scripting
Define logic with Javascript:

**Items:**
```json
onUse: ({ player, showMessage }) => {  
  player.hp += 10;  
  showMessage("✨ You feel renewed!");  
}
```
**Weapons:**
```json
onAttack: ({ attacker, defender }) => {  
  defender.hp -= 4;  
  return "⚡ Zapped!";  
}
```
### 📜 Quests
Quest logic and HUD are fully implemented:
```json
{
  "id": "find-orb",  
  "name": "Find the Orb",  
  "stages": [  
    "Speak with the wizard",  
    "Retrieve the Orb",  
    "Return it to him"  
  ]  
}
```
They simply need to be triggered from NPCs or events.

### 🌐 Multiplayer Hooks (Future)
Client supports:
- Remote players
- Room/position syncing
- Actions
- Name tags

A generator script is included to bootstrap a WebSocket server.

### 🤖 Reinforcement Learning Playground (Future)
EmojiMetaDungeon includes a Gym-style API:
- `reset()`
- `step(action)`
- Reward signals
- Observations as tensors
- Deterministic debugging mode

Use it for navigation, puzzle-solving, or agent behavior experiments.

### 🔮 Procedural Generation Tools (Future)
Includes:
- Perlin noise
- Wave Function Collapse
- Biome templates
- Room patching/synthesis tools
- Dynamic geometry generation

Use these to build infinite emoji worlds.

## 🛠️ Development Philosophy
Everything lives inside: `EmojiMetaDungeon.html`  
Renderer, AI, editor, RL, netcode... all in one decently readable file.  
The engine is built to be hacked, mangled, remixed, and extended.

## 📜 License
MIT License.

## 💬 Final Notes
EmojiMetaDungeon is intentionally:
- Tiny
- Playful
- Hacker-friendly
- Anarchic
- Amorphous
- Moddable
- Metaversal
- Decentralized
- Hypermedia-based
- 90s open Internet retro
- Experimental
- Fun to break

If you make cursed emoji weapons or endless procedural nightmare realms, the engine approves.

