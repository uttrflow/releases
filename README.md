# Uttrflow releases

Downloads for [Uttrflow](https://uttrflow.com) — dictation and a clipboard that
remembers, entirely on your Mac.

**This repository holds no source code.** It exists because a download link has to be
public and the source does not. Everything here is published by the release workflow in
`uttrflow-mac`; nothing is committed by hand.

## Getting Uttrflow

**[uttrflow.com/download](https://uttrflow.com/download)** — works out which Mac you are
on and starts the download.

Or take it straight from here:

**https://github.com/uttrflow/releases/releases/latest/download/Uttrflow.dmg**

That URL is permanent. GitHub resolves `/releases/latest/download/<asset>` to the newest
release carrying an asset of that name, so it always gives you the current version — which
is also why the file is called `Uttrflow.dmg` and not `Uttrflow-1.2.3.dmg`. A version in
the name would make this link a 404 the day after it was written.

## latest.json

`latest.json` is the same information for machines, and it is what the download page reads
to name the version and its size:

```json
{
  "version": "0.1.0",
  "published": "2026-08-26T09:00:00Z",
  "notes": "https://github.com/uttrflow/releases/releases/tag/v0.1.0",
  "builds": [
    {
      "os": "macos",
      "architecture": "appleSilicon",
      "version": "0.1.0",
      "url": "https://github.com/uttrflow/releases/releases/latest/download/Uttrflow.dmg",
      "size": 7160000,
      "requires": "macOS 26",
      "gatekeeper": "notarised"
    }
  ]
}
```

`gatekeeper` is the field to read before installing. `notarised` means Apple has checked
the build and it opens with a double-click. `unsigned` means it is a test build: macOS
will refuse it, saying the app is damaged, and it is not — see below.

The download page treats this file as decoration, never as the source of the link. If it
is stale, missing or unreachable, the button still works and simply stops naming a
version.

## Test builds

Prereleases marked `unsigned` have not been through Apple. macOS stamps anything a browser
downloads with a quarantine attribute and refuses to open an un-notarised app carrying it,
with a message claiming the app is damaged. It is not damaged. After dragging Uttrflow to
Applications, run this once:

```
xattr -dr com.apple.quarantine /Applications/Uttrflow.app
```

Transferring the file with `scp`, `rsync` or a USB stick sets no quarantine attribute at
all, in which case nothing is needed.

## Requirements

Apple Silicon, macOS 26 or later.
