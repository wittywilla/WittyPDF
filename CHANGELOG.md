# Changelog

What changed in WittyPDF, newest first. What changed before it had a repository of its own is in the
[WittyMediaServer changelog](https://github.com/wittywilla/WittyMediaServer/blob/master/CHANGELOG.md).

## Unreleased

- **Module API 4**, for WittyMediaServer 0.8.0-alpha and later: the module carries its own server-driven UI in `sdui.json`, which `wittymodule pack` puts in every archive.
- Carries `sdui.json` with its theme scope, so an administrator can give the PDF reader colours of its own. Its pages come with WittyInk, which every reader shares.
- **WittyPDF 0.3.0:** Fits WittyMediaServer 0.8.x.

- A PDF with a password says so in plain words, instead of showing the error from inside the PDF reader. It doesn't ask for the password: nothing here opens protected files.
- Module API 3 and WittyMediaServer 0.6.0-alpha: this is how a server gets it now, with no copy compiled in.
- Uses pdf.js 6.4.299. It has no eval option to turn off any more, and fetches its image decoders from the folder the host names (`pdf.wasmUrl`, `pdf.iccUrl`).
- WittyPDF is now a project of its own, developed and released from this repository.
