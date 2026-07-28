# app-updates

Sparkle update feeds and release assets for Shawn Bowers' Mac apps.

This repo exists only to be *served*. Sparkle fetches an appcast with no
credentials, so the feed can't live in a private source repo — but nothing here
is source. It's the published output of each app's release script.

## Layout

One directory per app, each with its own `appcast.xml`:

```
lookit/
  appcast.xml          # the feed Lookit checks
  Lookit-<version>.zip # the archives Sparkle downloads
```

**Apps must not share an appcast.** Sparkle picks the newest `CFBundleVersion`
in whatever feed it was pointed at, with no filtering by bundle identifier — so
two apps in one feed means each would try to "update" itself into the other.

The repo name is deliberately product-neutral. Feed URLs are compiled into every
build and checked for the life of that install, so they have to outlive any
product rename.

## Feeds

| App | Feed URL |
| --- | --- |
| Lookit | https://shawnbowers.github.io/app-updates/lookit/appcast.xml |

## Publishing

Don't hand-edit `appcast.xml`. Each app's `scripts/release.sh` regenerates it
with Sparkle's `generate_appcast`, which rebuilds the whole feed from the
archives in that app's directory — so **past release archives have to stay
here**. Removing one drops it from the feed.
