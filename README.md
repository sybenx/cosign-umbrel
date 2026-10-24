# Cosign for Umbrel

An Umbrel community app store with one app: **Cosign Server**, your own always-on
co-signer for your Nostr key ([Cosign](https://github.com/sybenx/cosign)).

Cosign splits your key so no single device or server holds it: your phone holds a big
piece, servers hold small ones, and a device plus any one server signs. A server you run
yourself is the one the Cosign app asks first, so public servers see less of what you
sign. It connects out to public relays, so it needs no open port.

## Install

1. In umbrelOS: App Store, ⋯ (top right), **Community App Stores**, add
   `https://github.com/sybenx/cosign-umbrel`.
2. Install **Cosign Server**, open it, and scan **Add your phone** with the Cosign app.
3. In the app's settings, set `COSIGN_OPERATOR` to your npub, so the server announces
   itself naming you. Then name it back from your key: a kind 10243 event with a `p` tag
   for its host key (`"host"` on its `/status` page). See
   [Make it count as yours](https://github.com/sybenx/cosign/tree/main/deploy#make-it-count-as-yours).

## Settings

| Setting | Default | What it is |
| --- | --- | --- |
| `COSIGN_OPERATOR` | none | your npub |
| `COSIGN_ENROLL` | `invite` | `invite` keeps it yours. `open` lets strangers store pieces of their keys on your home network, and it connects out from your home IP: a public server belongs on a VPS, with its outbound connections limited ([relay sidecars](https://github.com/sybenx/cosign/tree/main/deploy)). |
| `COSIGN_INVITES` | none | with `invite`, other devices' pubkeys (hex, comma separated) that may enroll |

## Good to know

- Its page lists the accounts it serves. It's behind your Umbrel login: keep that on.
- Its shares (`data/groups/`) are left out of Umbrel backups on purpose. After a refresh,
  old shares must be gone for good. If this server loses its data, your device and
  another server still sign.
- It doesn't use Umbrel's Nostr Relay app: that relay is only reachable at home (or over
  Tor or Tailscale), so your phone couldn't reach it from elsewhere.

**Not tested on an Umbrel yet.**

MIT
