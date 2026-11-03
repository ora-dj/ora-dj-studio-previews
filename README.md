# Ora DJ installer previews

This repository holds isolated installer-testing builds. It is separate from
[normal Ora DJ releases](https://github.com/ora-dj/ora-dj-studio-releases).
The production website and stable/beta updaters do not use this repository.

## Availability

No Mac preview is available yet. An empty Releases page is expected until a
signed candidate has passed preparation and is published by the maintained
preview workflow. Repository setup alone does not produce an installer.

## Distribution rules

- Publish immutable, uniquely tagged prereleases; never mark them Latest.
- Include the signed/notarized Mac mini, its exact version-bound app payload,
  the full DMG fallback, and a manifest recording source and artifact hashes.
- The downloader must verify payload size, cryptographic hash and publisher/app
  identity before installing. A preview download URL must be bound at build time.
- Do not upload production updater feeds or change any existing release assets.
- Publish through the maintained GitHub Actions preview workflow, with access
  restricted to this repository. Do not store product source or credentials here.
- Synthetic telemetry must stay out of the production acquisition funnel.

## Testing a Mac preview

Use the direct link for one published preview; do not mix artifacts from different
preview tags. Record the version, macOS version, chip and result for each test.

1. Download the mini in a browser and open it normally, preserving macOS quarantine.
2. Confirm it immediately downloads the app from GitHub and displays progress.
3. Confirm installation completes and the real Ora window opens automatically.
4. Quit and reopen Ora. Confirm that library/settings remain intact.
5. On a disposable installation, retry with Ora running, cancel a download, and
   interrupt the network. Confirm the previous app remains usable and Ora is not
   force-quit. Restore the network and retry.
6. Test the matching full DMG as the manual/offline fallback.

To protect a working installation and library, use a disposable macOS VM or a
separate boot volume, or a spare Mac with disposable data. A second user account
alone does not isolate the shared /Applications directory. Never treat mounting
the DMG or an installer launch callback as proof that Ora reached a usable UI.

Preview results qualify only the cases and machines actually tested. They do not
authorize a production release or establish that an unexplained missing event is
normal abandonment.
