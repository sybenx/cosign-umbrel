# Status

## Tested

- The official Umbrel linter (`npm run lint:apps -- marble-server --check-images` in
  getumbrel/umbrel-apps): 0 errors, 1 warning (security_opt: `no-new-privileges`, a
  hardening option, to explain in the PR).
- The compose run as umbrelOS would run it (minus Umbrel's own app_proxy), on the
  published 0.12.2 image, read-only, against a local test relay: fresh start makes your
  own key (weighted, phone + this server), `enroll: invite`, and the account's page
  (`/g/<id>/`) shows "Add your phone" with its pairing code.

- Installed on an Umbrel (umbrelOS 2.0, amd64) from this community store, 25 Oct 2026:
  ready, the page asks for the Umbrel login, its settings show COSIGN_OPERATOR,
  COSIGN_ENROLL (invite) and COSIGN_INVITES, the logs show the key waiting for the phone
  and `enroll: invite (0 invited)`, and after a restart it's the same account and host key.

## Not tested yet

- A phone pairing with it and signing (the owner's real phone test).
- Backups leaving out `data/a` and `data/groups`.
- wss://nos.lol never came up from the Umbrel (syb.lol and relay.primal.net did).

## Before the official submission

- Re-pin to 0.12.3 (new pair card wording, "Your server", the root page's Add your phone
  card, a new account after a restore), then take the screenshots.
- The official package drops `icon:` and sets `submission:` to the PR's URL.

## 0.12.3: Add this server to your account (25 Oct 2026)

Pinned to the 0.12.3 multi-arch index (amd64 + arm64). The page shows "Add this server to
your account", a one-time code that Marble 0.12.3's Add a server scans: it works once, on
this server only, for an hour. Checked locally on the pinned image (read-only, no
network): no account of its own, the card and code on the page, the same unused code on
reload. Not yet: the phone test on the Umbrel with the new flow, and screenshots.

## Later: join modes

Only me (the default) / people I follow / people I invite / anyone: the page says it's
coming. When the server takes it, map the app's settings to it and add "or share it with
people you follow" to the description.
