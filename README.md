# Marble Server for Umbrel

An Umbrel community app store with one app: **Marble Server**, your own always-on helper
for the [Marble app](https://cosign.aaro.cc) on your phone. (Marble is the phone app; the
server and its protocol are [Cosign](https://github.com/sybenx/cosign).)

Marble keeps your key out of any one place: your phone holds 3 shares, each server 1,
and it takes 4 to sign. A server you run yourself is the one the Marble app asks first,
so public servers see less of what you sign. It connects out to public relays, so it
needs no open port.

## Install

1. In umbrelOS: App Store, ⋯ (top right), **Community App Stores**, add
   `https://github.com/sybenx/cosign-umbrel`.
2. Install **Marble Server** and open it. On first start it has no key yet: scan **Add
   your phone** with the Marble app, and your phone and the server make one together.
3. Optional: in the app's settings, set `COSIGN_OPERATOR` to your npub, so the server
   announces itself naming you. Then name it back from your key: a kind 10243 event with
   a `p` tag for its host key (`"host"` on its `/status` page). See
   [Make it count as yours](https://github.com/sybenx/cosign/tree/main/deploy#make-it-count-as-yours).

## Settings

| Setting | Default | What it is |
| --- | --- | --- |
| `COSIGN_OPERATOR` | none | your npub |
| `COSIGN_ENROLL` | `invite` | `invite` keeps it yours. `open` lets strangers store pieces of their keys on your home network, and it connects out from your home IP: a public server belongs on a VPS, with its outbound connections limited ([relay sidecars](https://github.com/sybenx/cosign/tree/main/deploy)). |
| `COSIGN_INVITES` | none | with `invite`, other devices' pubkeys (hex, comma separated) that may enroll a new account here |

## Good to know

- Its page shows your key's members, your sites and recent changes. It's behind your
  Umbrel login: keep that on.
- **Its shares are left out of Umbrel backups** (`data/a/`, `data/groups/`) on purpose.
  After a device is lost, every share is renewed, and an old one must not come back from
  a backup. If this server loses its share, replace it from the Marble app.
- It doesn't use Umbrel's Nostr Relay app: that relay is only reachable at home (or over
  Tor or Tailscale), so your phone couldn't reach it from elsewhere.
- It runs read-only, with no Linux capabilities.

MIT
