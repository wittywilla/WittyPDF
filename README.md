# WittyPDF

A PDF reader for papers, textbooks and scans. You need it to read PDFs in WittyMediaServer.

It's a module of [WittyMediaServer](https://github.com/wittywilla/WittyMediaServer) ([wittymediaserver.com](https://wittymediaserver.com)), on module API 5, built on [WittyInk](https://github.com/wittywilla/WittyInk). The same reader also runs in the [WittyReader](https://github.com/wittywilla/WittyReader) app.

<!-- pictures -->

![A PDF open in the reader](docs/images/reader-pdf.webp)

<sub>Earth as Art, NASA, public domain.</sub>

<!-- /pictures -->

## What it does

- **Continuous pages:** one or two across, fit width, fit page, or 50 to 400 percent.
- **Night reading:** dark or sepia pages.
- **Getting around:** the document's own contents, page thumbnails, and search across the whole document, with results arriving while a long file is searched.
- **Exact resume:** the page and how far down it.
- **Study tools from WittyInk:** highlights and notes, citations with page numbers, a pen with pressure, and reading aloud.
- **Light on small machines:** pdf.js loads only when a PDF is opened, only nearby pages are drawn, and large files stream in parts.
- **Safe with any PDF:** PDF scripts never run, and XFA forms are off.

pdf.js and its worker, which do the actual reading, stay with the app so they aren't carried twice. No documents come with it.

How to use it is in **Help** inside WittyMediaServer: see Books, PDFs and comics.

## How to get it

An admin adds it from the module store inside WittyMediaServer: **Settings → Modules**, then **Browse the store**, then **Add** beside WittyPDF. The range this version fits is in `module.json`: WittyMediaServer 0.8.0-alpha through 0.8.x, module API 5. The server takes API 5 modules only, so older servers can't use this version. How modules work on the server is in its [docs/MODULES.md](https://github.com/wittywilla/WittyMediaServer/blob/master/docs/MODULES.md).

Adding it brings WittyInk, which it's built on.

## What it needs

- [WittyInk](https://github.com/wittywilla/WittyInk), and React 18 or newer, which the app provides.
- [pdf.js](https://mozilla.github.io/pdf.js/), from `pdfjs-dist`, which draws the pages. It uses the build for older browsers, so TV web views can open it.

## Platforms

It's one browser bundle for every system the server runs on, and it runs on whichever device opens the server. It has been seen working in a desktop browser, against a test server on Linux. It also runs in the WittyReader app. Safari, real phones and real TVs have not been tried.

## Building and testing

You need Node.js 22, as CI uses, and Go for the manifest check. In a worktree, first run WittyMediaServer's `scripts/dev-modules.mjs` (or the copy its `--root` option keeps in the folder above the repositories). It writes only links that git ignores, so the checkout builds against the repositories beside it.

```bash
npm install
```

```bash
npm run build:bundle
```

That makes one script and one stylesheet, as a server installs them, with WittyModule's builder (`kit/web/build-bundle.mjs` in a WittyModule checkout beside this one, or wherever `WITTYMODULE` names). To check the manifest:

```bash
go run github.com/wittywilla/wittymodule/cmd/wittymodule check .
```

`npm test` checks `sdui.json`, and that `register` hands over a reader for exactly the formats `integration.json` claims. CI checks the manifest and builds the bundle.

To use it in another app, give it a `ReaderHost` whose `pdf` field is what to open, and load it lazily so pdf.js only downloads when a PDF is opened: see [Embedding](wiki/Embedding.md). The other guides in [wiki/](wiki/Home.md) cover [viewing and zoom](wiki/Viewing-and-zoom.md), [getting around](wiki/Getting-around.md), [study tools](wiki/Study-tools-and-handwriting.md), and [performance and security](wiki/Performance-and-security.md).

## How the app finds it

Module API 5: `integration.json` claims the `pdf` format with the readers hook (`web.readers`), and the bundle's `register(host)` hands over the reader for it. The web app opens a book with whichever module in use claims its format, after loading WittyInk, which every reader is built on. The app has no list of readers of its own.

## In every app: its server-driven UI

It carries its own `sdui.json`: its theme scope, and **Settings, PDFs** (each profile's own): fit width or page, two pages across, and page colour. Its library and book pages come with WittyInk, which every reader shares.

**Stays in the reader's own code:** the reading surface, zoom steps, outline and thumbnails, going to a page, search, and notes.

The file is checked with `wittymodule check` and described in WittyMediaServer's [docs/SDUI-MODULES.md](https://github.com/wittywilla/WittyMediaServer/blob/master/docs/SDUI-MODULES.md).

## Licence

GNU Affero General Public License v3.0 (or later): see [LICENSE](LICENSE) and [NOTICE](NOTICE). If you redistribute it or build on it, please keep the NOTICE attribution.

It uses pdf.js (`pdfjs-dist`), Copyright Mozilla Foundation, under Apache-2.0. The text-layer styles in `pdf.css` are adapted from pdf.js.

WittyPDF is part of the WittyMediaServer project: [server repository](https://github.com/wittywilla/WittyMediaServer), [wittymediaserver.com](https://wittymediaserver.com).

<!-- module-kit -->
## Releasing

A version tag builds the bundle for the browser, signs the checksum list, and publishes a release that servers can install.

Versions move in small steps as work lands. `go run github.com/wittywilla/wittymodule/cmd/wittymodule@v0.5.4 bump .` raises it
everywhere it is written (add `-part minor` for a bigger step). A bump isn't a release: nothing is
tagged or published until you tag it. CI fails when code changed since the last tag and the version
didn't, because tags never move.

To release:

1. Check that `version` in `module.json` is the one to publish, with the bump committed.
2. Tag that commit and push the tag: `git tag vX.Y.Z`, then `git push origin vX.Y.Z`. A tag with a
   suffix, such as `v1.2.0-beta`, is published as a prerelease.
3. Watch the *Actions* tab. The signing step uses the `WMS_SIGNING_KEY` secret of the `release` environment, and nothing is published without it.

To take a version back, run the *withdraw* workflow from the *Actions* tab. It adds the version to a signed list on the release tagged `withdrawals`, which servers read.

Licensed under AGPL-3.0-or-later: see [LICENSE](LICENSE) and [NOTICE](NOTICE).
<!-- /module-kit -->

## Legal

WittyPDF is an independent open-source project. It isn't associated with, sponsored by or endorsed
by any publisher, rights holder, service or other media software project. No documents come with it,
and it doesn't check the ones you open: you're responsible for having the rights to them. Any
third-party names here only describe what it works with, and belong to their owners. It's provided
“as is”, with no warranty; see [LICENSE](LICENSE). Local law applies to how you use it. This isn't
legal advice.
