# hong.web

Public website of Hóng, an iPhone and iPad app: a reader-mode browser for the news sites and
forums you choose, with on-device AI. Here: the landing page, privacy policy, terms, plus the
signed reading templates the app reads. Published from a private repository by a script; edits here are overwritten.

- `index.html`, `assets/` — the landing page (static HTML, no JavaScript).
- `privacy.html`, `terms.html` — privacy policy and terms of use.
- `bot.html` — what the `Hong-User` and `Hong-Refresh` user agents are and how to block them.
- `NOTICE.txt` — rights notice and how to ask for a removal.
- `v2/status.txt` — kill switch (the whole app, or one forum template) and request pacing.
- `v2/hints.txt` — how news pages are read (XPath rules).
- `v2/forums.txt` — forum templates: routes, selectors, sign-in parameters, and which of the
  app's built-in actions a forum supports.
- `v2/forum.txt` — legacy forum selector overrides, kept for older app versions.
- `v2/catalog.txt` — the optional directory of news sites and forums.
- `v2/packs.txt` — the monthly Hóng Pro data pack (filter phrases, topic keywords, digest formats).

The `v2/` files are readable plain text, signed with Ed25519:

```
hong-envelope-v2
<base64 header: key, source, kind, version, notAfter, minAppVersion>
<base64 signature over "hong.web/envelope/v2\0" ‖ u32be(len(header)) ‖ header ‖ SHA-256(payload)>
<payload JSON, exactly as signed>
```

The app verifies the signature against keys built into it before it reads anything, and ignores a
file that fails, so editing these files here does nothing. They are declarative data: they describe
pages, and a forum template can only bind actions from a closed set compiled into the app (reply,
edit, delete, react, bookmark, watch, mark read, report, ignore, private conversations, upload,
import ignored list); it can never add an action, a script or an expression. Hosts of forums with
sign-in are pinned in the app and cannot be added by these files. To check a file yourself, decode
the second line and verify the third with the public keys in the app.

The templates and the directory are a selection and arrangement by the app's author; see
`NOTICE.txt`. Any site owner, paper or forum, can ask to remove or limit its template there.
Hóng is an unofficial, independently developed app, not affiliated with, sponsored or endorsed
by any forum or newspaper you read through it.
