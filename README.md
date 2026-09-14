# aextilfederal.com

The public website for **Aextil Federal**, a software platform operated by Federal IQ LLC.

Every file here is **generated**. The source is `packages/marketing/` in the private application
repository and the build is `scripts/build-marketing.mjs`; edit those, rebuild, and copy the output
here. Editing a page in this repository by hand is a change the next build silently discards.

Two guards run before anything is published:

- `packages/marketing/marketing.test.mjs` — the marketing build imports no tenant context at all, so
  "the public site cannot leak customer data" is a property of the code rather than a promise.
- `scripts/check-public-assets.mjs` — loads the operator's own identifier list at run time and refuses
  to publish a directory that names a customer, or that holds a binary whose origin nobody recorded.

Screenshots come from a synthetic demonstration company with invented notices, not from a customer.
