# Changelog

What changed in WittyPDF, newest first. What changed before it had a repository of its own is in the
[WittyMediaServer changelog](https://github.com/wittywilla/WittyMediaServer/blob/master/CHANGELOG.md).

## Unreleased

- Module API 3 and WittyMediaServer 0.6.0-alpha: this is how a server gets it now, with no copy compiled in.
- Uses pdf.js 6.4.299. It has no eval option to turn off any more, and fetches its image decoders from the folder the host names (`pdf.wasmUrl`, `pdf.iccUrl`).
- WittyPDF is now a project of its own, developed and released from this repository.
