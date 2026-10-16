# ECLIPSE: REALMS OF RUIN — Online RPG prototype

This project is a mobile-friendly 2D side-scrolling dark-fantasy RPG prototype with:
- Canvas-rendered pixel-style world and player/monster/NPC sprites drawn in code
- Touch controls and keyboard controls
- Four-direction top-down movement, monster combat, respawning monsters
- Multiple zones, NPCs, quest, XP/leveling, races, classes, attributes
- Inventory, equipment, potions, gold and local save
- WebSocket multiplayer presence and world chat (requires separate server deployment)
- Capacitor Android build workflow

## Build APK with GitHub Actions
1. Upload the project files to a new GitHub repository, preserving `.github/workflows/build-apk.yml`.
2. Open Actions and run **Build Eclipse RPG APK** (or push a commit).
3. Download the `eclipse-realms-rpg-apk` artifact from the successful run.
4. Extract the downloaded ZIP and install `app-debug.apk` on Android.

## Enable multiplayer
The APK/game is playable offline without a server. To enable real online presence and chat, deploy the WebSocket server separately:
1. Create a new service on a Node.js hosting platform such as Render and connect this repository.
2. The service should use `npm install` for build and `npm start` for start. `render.yaml` is included as a blueprint.
3. Once deployed, use the service's secure WebSocket URL in game → **Online**, for example `wss://YOUR-SERVICE.onrender.com`.
4. The server root `/` and `/health` return a small JSON health status.

Important limitations of this prototype:
- Multiplayer currently synchronizes player presence/position and world chat only. Combat, inventory, quest progress, and monster state are still local to each device; this is not yet a fully authoritative MMORPG.
- Free server hosting may sleep when idle and can have cold-start delays.
- Sprite graphics are pixel-style shapes drawn on Canvas, not a full external sprite pack. Add original sprite sheets, sound, music, and more maps to expand quality/size.
- Do not expose credentials or private keys in client code.

## Local server test
```sh
npm install
npm start
```
Then connect from the game using a WebSocket URL reachable by your device. For a local PC server, use `ws://PC-LAN-IP:10000` on the same Wi-Fi. For deployed hosting, use `wss://...`.


## Top-down controls
- Move with the four-way touch pad or WASD/arrow keys.
- Tap Attack or Skill to fight nearby monsters.
- Tap Interaksi or press Space near NPCs.
