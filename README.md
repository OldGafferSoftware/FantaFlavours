# FantaFlavours

The flavour catalog for the Fanta Tracker app, published so the app can download updates.

App help: [Support](SUPPORT.md) · [Privacy policy](PRIVACY.md) · [Report a problem or flavour correction](https://github.com/OldGafferSoftware/FantaFlavours/issues/new) · info@oldgaffersoftware.com

- `catalog.json`: the full catalog (released flavours only)
- `version.json`: a small file the app checks first, so it only downloads the catalog when it changed
- `scripts/validate.py`: run before every commit; checks the rules below and writes `version.json`

The app reads these through raw GitHub links:

```
https://raw.githubusercontent.com/OldGafferSoftware/FantaFlavours/main/version.json
https://raw.githubusercontent.com/OldGafferSoftware/FantaFlavours/main/catalog.json
```

Each update is one commit, so the history is a record of every change. (A daily refresh task, like the one for Dew Tracker, is not set up yet.)

## Format

```json
{
  "schemaVersion": 1,
  "version": 1,
  "generated": "2026-10-14",
  "count": 33,
  "license": "CC BY-SA 4.0",
  "attribution": "https://github.com/OldGafferSoftware/FantaFlavours#attribution",
  "flavours": [
    {
      "id": "fanta-grape",
      "name": "Fanta Grape",
      "notes": "Description shown at the top of the flavour screen",
      "status": "current",
      "markets": ["US", "UK"],
      "availability": "Where to find it, if not ordinary stores",
      "zeroSugar": true,
      "since": "2004",
      "update": "Short note on the latest status",
      "sourceURL": "https://…",
      "changed": "2026-11-13",
      "discontinued": false
    }
  ]
}
```

`status` is `current`, `limited` (on sale for a limited time), `retired`, or `null` when the current status isn't known. `discontinued` repeats `status == "retired"` for app version 0.1, which only reads that field. Every field except `id` and `name` may be `null`.

`changed` is the date (YYYY-MM-DD) this entry was last added or changed in the catalog. The app's "Recent changes" view lists flavours by this date. It is `null` for entries that haven't changed since the catalog started (2026-11-12).

## Rules

1. Released flavours only. No upcoming, rumoured or cancelled flavours, and no alcoholic products.
2. An `id` is permanent. Never remove or rename one: people's tastings are stored against it. A flavour that ends is marked `retired`.
3. Any change to `flavours` raises `version` by exactly 1, and every new or changed entry gets `changed` set to the catalog's `generated` date.
4. Run `python3 scripts/validate.py` before committing. It refuses a catalog that breaks these rules.

## Attribution

Some entries, and some `notes` text, are adapted from the Wikipedia article [Fanta](https://en.wikipedia.org/wiki/Fanta) by its contributors ([history](https://en.wikipedia.org/w/index.php?title=Fanta&action=history)), as read on 2026-11-12. Wikipedia has no full table of Fanta flavours, so most entries, and status, market and availability details, are researched with AI assistance from news reports and company announcements, linked in each entry's `sourceURL` and written in our own words.

Changes from the article: took the flavours named in its text and infobox and wrote each one's notes in short form; added `id`, `status`, `markets`, `availability`, `zeroSugar`, `since`, `update` and `sourceURL`; added entries for flavours not named in the article. Where the article doesn't say whether a flavour is still sold, `status` is `null`.

Some older and regional entries come from fan lists (for example a 2018 list of Fanta flavours by country, and Japanese snack-shop guides). Their `update` says so, and their `status` stays `null` (unknown) until a newer source confirms it.

The catalog is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). This license covers the catalog data only, not the names, which may be trademarks of their owners. This is an unofficial fan project, not affiliated with or endorsed by any brand owner or by Wikipedia.
