# Status

## Tested

- The official Umbrel linter (`npm run lint:apps -- marble-server --check-images` in
  getumbrel/umbrel-apps): 0 errors, 1 warning (security_opt: `no-new-privileges`, a
  hardening option, to explain in the PR).
- The compose run as umbrelOS would run it (minus Umbrel's own app_proxy), on the
  published 0.12.2 image, read-only, against a local test relay: fresh start makes your
  own key (weighted, phone + this server), `enroll: invite`, and the account's page
  (`/g/<id>/`) shows "Add your phone" with its pairing code.

## Not tested yet

- Installing it on a real Umbrel through this community store (planned on a test Umbrel).
- A phone pairing with it, signing, a restart, and backups leaving out `data/a` and
  `data/groups`.

## Before the official submission

- Screenshots, once the page says Marble (it still says "Open Cosign on your phone").
- The official package drops `icon:` and sets `submission:` to the PR's URL.
