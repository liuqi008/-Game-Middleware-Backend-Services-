# Game Middleware & Backend Services Proxy Rules

Mihomo / Clash Meta compatible proxy rules for game middleware and backend services.

Designed to route game SDK traffic through a low-latency proxy node (e.g. `🎮 Game-Proxy`) to reduce connection failures caused by ISP interference or geographic restrictions.

---

## Coverage

### Multiplayer Networking

| Service | Domain | Notes |
|---|---|---|
| Photon Engine | `photonengine.io` / `photonengine.com` / `exitgames.com` | World's most widely used multiplayer networking SDK |
| Edgegap | `edgegap.com` / `edgegap.net` | Game server orchestration & distributed relay |
| SmartFoxServer | `smartfoxserver.com` | Java-based multiplayer game server framework |
| Colyseus | `colyseus.io` / `colyseus.dev` | Node.js multiplayer game framework |

### Game Backend as a Service (BaaS)

| Service | Domain | Notes |
|---|---|---|
| Microsoft Azure PlayFab | `playfab.com` / `playfabapi.com` | Microsoft's game backend platform |
| Heroic Labs (Nakama) | `heroiclabs.com` / `heroic.cloud` | Open-source backend + Satori LiveOps |
| AccelByte | `accelbyte.io` / `accelbyte.net` | Cross-platform game backend |
| Beamable | `beamable.com` / `beamable.net` | Unity/Unreal integrated backend |
| LootLocker | `lootlocker.com` / `lootlocker.io` | Player accounts & in-game economy |
| brainCloud | `braincloudservers.com` / `getbraincloud.com` | Independent BaaS platform |
| Pragma Engine | `pragma.gg` | Enterprise-grade multiplayer backend |
| Amazon GameSparks | `gamesparks.net` | Sunset in 2023; retained for legacy live games |

### Game Server Hosting / Orchestration

| Service | Domain | Notes |
|---|---|---|
| Gameye | `gameye.com` | Game server orchestration platform |
| i3D.net | `i3d.net` | Global dedicated game server infrastructure |
| Unity Multiplay | `multiplay.co.uk` / `multiplay.com` | Unity-owned game server hosting |

### Game Engine Services

| Service | Domain | Notes |
|---|---|---|
| Unity Gaming Services | `unity3d.com` / `unity.com` | Relay, Matchmaking, Vivox voice |
| Unity Vivox | `vivox.com` | Voice SDK used in many multiplayer games |
| Epic Online Services | `epicgames.dev` / `on.epicgames.com` | EOS SDK runtime endpoints |

### Platform SDKs

| Service | Domain | Notes |
|---|---|---|
| Valve Steam | `steamgames.com` / `steampowered.com` / `steamcontent.com` | Steam platform & CDN |
| GOG | `gog.com` | GOG platform (no China-specific domain) |

### Analytics & LiveOps

| Service | Domain | Notes |
|---|---|---|
| GameAnalytics | `gameanalytics.com` | Game telemetry & analytics |

### Anti-Cheat

| Service | Domain | Notes |
|---|---|---|
| Easy Anti-Cheat | `easyanticheat.net` | Epic-owned; used in many AAA titles |
| BattlEye | `battleye.com` | Used in Arma, PUBG, Rainbow Six, etc. |

### Matchmaking / Tournament

| Service | Domain | Notes |
|---|---|---|
| GGPO | `ggpo.net` | Rollback networking for fighting games |

---

## Usage

Add the rules to your Mihomo / Clash Meta `rules` section. Make sure the `🎮 Game-Proxy` proxy group is defined and points to a node with good UDP support and FullCone NAT capability.

```yaml
proxy-groups:
  - name: "🎮 Game-Proxy"
    type: select
    proxies:
      - YOUR_FULLCONE_NODE
      - DIRECT
```

For best results, the proxy node assigned to `🎮 Game-Proxy` should:
- Support UDP forwarding
- Have `endpoint-independent-nat: true` configured on the Mihomo TUN interface
- Be geographically close to the game's server region

---

## Scope

These rules cover **global** game middleware and backend services only. No China-operated or China-specific domains are included. Platform CDN domains (e.g. Akamai, Cloudflare) are intentionally excluded as they serve general web traffic and should be handled by your existing ruleset.

---

## Notes

- **Amazon GameSparks** was shut down in 2023 but is retained for legacy games still in production that have not migrated.
- **Hathora** shut down on May 5, 2026 and is not included.
- **deltaDNA** (Unity) shut down in 2023 and is not included.
- Steam's China-operated domains (`steamchina.com` etc.) are intentionally excluded as they are handled by China direct rules.

---

## Related

- [IPv6 Test Sites Rule](./ipv6-test.yaml)
