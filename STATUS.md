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

## Next: the new join modes (waiting on the Cosign server)

The agreed design. Marble Server serves **only me** (the default), **people I follow**
(optionally follows-of-follows), **people I invite**, or **anyone**. Its main flow is
"Add this server to your Marble account": Marble's Add a server scans the page's code.
It no longer creates a new account. When the Cosign server ships it:

- re-pin the image;
- map the app's settings to the join mode (default "only me"), and drop the raw
  COSIGN_ENROLL / COSIGN_INVITES settings for whatever the server takes;
- add "or share it with people you follow" to the description;
- retest on the Umbrel, then the phone test with the new flow, then screenshots;
- then the official PR, still unopened.

Until then the app makes no account of its own (`COSIGN_PERSONAL=0`): it runs and waits,
holding nothing, and the listing says "Coming soon: add this server to your Marble
account". The page shows the server's own status and an empty list. The test Umbrel
installed before this change still has its own 1-server account from "Add your phone":
use it only with a throwaway account.
