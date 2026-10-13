# soundcraft-snap

Snap packaging for [SoundCraft](https://getartcraft.com/apps/soundcraft), a digital audio workstation for audio and MIDI,
from the open-source [ArtCraft](https://getartcraft.com/) Crafting Apps.
Upstream: <https://github.com/storytold/soundcraft>.

The snap repackages the official upstream Linux release tarball
(checksum-verified against the release's `SHA256SUMS.txt`) for amd64 and arm64.

```sh
sudo snap install soundcraft
soundcraft          # desktop app
soundcraft.cli      # headless CLI / MCP server
```

## Workflows

- **Build and publish** (`build.yml`): builds the snap on amd64 and arm64 for
  every push and pull request. Pushes to `main` release to `edge`; a manual run
  can pick any channel (leave it empty to only build).
- **Check upstream release** (`check-upstream.yml`): runs every 6 hours, and when
  a newer upstream release exists it bumps `version` in `snap/snapcraft.yaml`,
  commits to `main` and releases a new build to `candidate`.

## Setup

1. Register the name: `snapcraft register soundcraft`.
2. Export store credentials and save them as the `SNAPCRAFT_STORE_CREDENTIALS`
   repository secret:
   `snapcraft export-login --snaps soundcraft --channels edge,candidate,beta,stable --acls package_access,package_push,package_release -`
