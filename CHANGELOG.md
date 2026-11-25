# Changelog

What changed in WittyPDF, newest first. What changed before it had a repository of its own is in the
[WittyMediaServer changelog](https://github.com/wittywilla/WittyMediaServer/blob/master/CHANGELOG.md).

## 0.4.5

- **Fixed:** apps that check WittyPDF's types (WittyReader) build again with pdf.js 6.5.438. The reader no longer passes pdf.js an option it dropped; fonts still never run as code.

## 0.4.4

- **Updated dependencies:** actions/setup-go from 7.0.0 to 7.1.0; vite from 8.3.5 to 8.3.8; pdfjs-dist from 6.4.299 to 6.5.438.

## 0.4.3

- **Back on any TV remote closes the document** (or the open panel first). Some remotes' Back button did nothing in the reader. Back no longer also leaves the page before it, as it could with some remotes.
- **Long documents use less memory.** Pages you've scrolled past give back what the reader kept to draw them.
- **On a television,** the display settings explain the remote's arrows and Back instead of Ctrl, + and − and Page Up.
- **Fixed:** closing the page list while its small pictures were still on their way could leave errors behind in the browser.
- **Safer documents:** PDFs open without the reader compiling code for their fonts.

## Developer notes for 0.4.3

- Back keys (`preventDefault`, so the browser does not go back as well): `Escape`, `GoBack`, `BrowserBack`, `Back` and `XF86Back`.
- A page that was drawn and goes off screen calls `PDFPageProxy.cleanup()` (only those: asking for undrawn pages would fetch them).
- `Thumb` ignores a page that arrives after it unmounted and catches a `getPage` rejected by a destroyed document.

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
