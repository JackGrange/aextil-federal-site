# aextilfederal.com

The public website for **Aextil Federal**, a software platform operated by Federal IQ LLC.

Every file here is **generated, including this one.** The source is `packages/marketing/` in the
private application repository and the build is `scripts/build-marketing.mjs`. Editing a page in this
repository by hand is a change the next publish silently discards.

## Publishing

    node scripts/publish-marketing.mjs                  # dry run: exactly what would change
    node scripts/publish-marketing.mjs --publish --yes  # publish, then verify the live bytes

The dry run is the default. It builds, runs the guards, clones this repository and compares it file by
file, and pushes nothing. After a real publish it fetches every file from the live domain and hashes it
against the digest recorded in `release.json`, because a release stamp says which build was published
and does not say the bytes arrived.

## What is checked before anything is published

- `packages/marketing/marketing.test.mjs` — the marketing build imports no tenant context at all, so
  "the public site cannot leak customer data" is a property of the code rather than a promise.
- `scripts/check-public-assets.mjs` — loads the operator's own identifier list at run time and refuses
  to publish a directory that names a customer, or that holds a binary whose origin nobody recorded.
- `scripts/scan-walkthrough-frames.mjs` — reads the published video back frame by frame and OCRs it,
  because a name rendered into pixels cannot be found by searching text.

## Provenance

`release.json` records the source commit and a SHA-256 of every published file.
`asset-provenance.json` records which screen each binary was captured from. Screenshots and the
walkthrough come from a synthetic demonstration company — an invented firm against real public SAM.gov
notices — never from a customer.

`node scripts/marketing-release-audit.mjs` compares this live site to what the repository would
produce, and is the thing that notices when they differ.
