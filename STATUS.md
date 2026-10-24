# Status

On hold (feature freeze, 24 Oct 2026). Nothing is published, and the sybenx/cosign-umbrel
repo doesn't exist yet.

## Tested

The YAML parses, nothing more. It hasn't been installed on an Umbrel.

## Needs 0.11.2

`COSIGN_PERSONAL=weighted` (your own key, made with your phone, and "Add your phone" on
the page) exists only from 0.11.2. The compose is pinned to 0.11.1, which doesn't know it.

## To publish

1. Re-pin `cosign-server/docker-compose.yml` to `ghcr.io/sybenx/cosign-server:0.11.2@sha256:<index digest>`
   (multi-arch index, check that both amd64 and arm64 are in it) and set `version: "0.11.2"` in umbrel-app.yml.
2. Install it on a test Umbrel: settings show COSIGN_OPERATOR, COSIGN_ENROLL (invite),
   COSIGN_INVITES; the page opens behind the Umbrel login and shows "Add your phone"; a
   phone pairs and signs; a restart keeps it; `data/groups/*` is left out of backups.
3. Rescan for home-network details, create the public repo sybenx/cosign-umbrel, push.
