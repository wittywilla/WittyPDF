# Changelog

What changed in WittyPDF, newest first. What changed before it had a repository of its own is in the
[WittyMediaServer changelog](https://github.com/wittywilla/WittyMediaServer/blob/master/CHANGELOG.md).

## Unreleased

- PDFs open with pdf.js told not to compile code for their fonts.

## 0.4.2

- The README's pictures are retaken from WittyMediaServer 0.8.0-alpha.

## 0.4.1

- The first release on module API 5. The tag v0.4.0 was made before these build changes and was never published.


- Built on WittyModule 0.5.4 and module API 5: its workflows and SDUI kit are WittyModule 0.5.4's.
- **WittyPDF 0.4.0: module API 5.** `integration.json` claims the `pdf` format with the readers hook (`web.readers`), and the bundle exports `register(host)`, which hands the app the reader for it (`{ readers: { pdf: … } }`). The app finds a reader by what the modules in use claim, loading WittyInk first; it no longer keeps a map of formats to readers of its own. The default export stays, for apps that embed the reader (WittyReader).
- Built with WittyModule's one builder (`kit/web/build-bundle.mjs`, Vite 8); this repository's own copy of the builder is gone. `npm test` checks that `register` hands over exactly the formats `integration.json` claims.
- **Settings in every app's Settings, under Modules** (`sdui.json`, each profile's own): fit width or page, two pages across, and page colour. A PDF opens with them on every device, and changes made while reading are saved to them. The reading surface itself stays in the reader.
- A PDF that can't be opened, or is password-protected, is now reported to the host's log (`host.report`), with no addresses' query strings in it.
- **Module API 4**, for WittyMediaServer 0.8.0-alpha and later: the module carries its own server-driven UI in `sdui.json`, which `wittymodule pack` puts in every archive.
- Carries `sdui.json` with its theme scope, so an administrator can give the PDF reader colours of its own. Its pages come with WittyInk, which every reader shares.
- **WittyPDF 0.3.0:** Fits WittyMediaServer 0.8.x.

- A PDF with a password says so in plain words, instead of showing the error from inside the PDF reader. It doesn't ask for the password: nothing here opens protected files.
- Module API 3 and WittyMediaServer 0.6.0-alpha: this is how a server gets it now, with no copy compiled in.
- Uses pdf.js 6.4.299. It has no eval option to turn off any more, and fetches its image decoders from the folder the host names (`pdf.wasmUrl`, `pdf.iccUrl`).
- WittyPDF is now a project of its own, developed and released from this repository.
