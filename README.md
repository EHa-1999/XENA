# Records-grade storage for the employee

**English** · [Nederlands](README.nl.md) · [Deutsch](README.de.md)

**▶ [Open the demo](https://eha-1999.github.io/XENA/#en)** · also in [Nederlands](https://eha-1999.github.io/XENA/#nl) · [Deutsch](https://eha-1999.github.io/XENA/#de) · [Français](https://eha-1999.github.io/XENA/#fr) · [Español](https://eha-1999.github.io/XENA/#es) · [Italiano](https://eha-1999.github.io/XENA/#it) · [Polski](https://eha-1999.github.io/XENA/#pl)

An interactive demo of what sovereign, records-grade file storage on **Nextcloud** and **S3 object storage** looks like for an ordinary municipal employee. Retention, legal hold, metadata and access rules are enforced underneath, while people keep working in the windows they already know.

![File Explorer view with the properties panel](docs/screenshot-explorer.png)

> **A demo, not a product.** All sample data is fictitious: people, dossiers and case numbers do not exist. The demo shows the long-term destination; the *Time frame* switch and the *Roadmap* view show what is available when.

---

## Try it

Open `index.html` in a browser. It is a single self-contained file: no installation, no build step, no server.

Or open it online: **[https://eha-1999.github.io/XENA/](https://eha-1999.github.io/XENA/)**. Add a language code to open it in that language, for example `https://eha-1999.github.io/XENA/#de`.

## What the demo shows

| View | What you see |
|---|---|
| **File Explorer** | The desktop file explorer with drives M:, P:, I: and W:. Every drive is a bucket in one Nextcloud instance. |
| **Document library** | The file list on a collaboration site, for example SharePoint, with columns for classification and retention. |
| **Team channel** | The Files tab of a team channel, for example Teams. Choose the channel files or any connected drive. |
| **Search** | The search page in the web interface: search by name, attributes and content, with filters. In Woo mode (Dutch Open Government Act requests) you create a Woo dossier and add documents from the results. |
| **Office Assistant** | An add-in for office suites, shown here in Word: attributes, suggestions, accessibility and workflow next to the document. The same set-up works in LibreOffice and other suites: one thin layer, with a small add-in per suite. |
| **Architecture** | How the windows, Nextcloud, the register and the object storage fit together, with sample WebDAV and S3 messages. |
| **Engineering** | Per feature, what it asks of Nextcloud: standard, extension point, core change, or something outside Nextcloud. |
| **Roadmap** | Six steps from network drives to the long-term destination, with milestones and decision points. |
| **Help** | Features, why the combination matters, FAQ, glossary and instructions for administrators. |

The bar at the bottom (*Under the hood*) shows for every action which message goes to the storage.

## Main features

- **Working with files:** create files, folders and dossiers; open, rename, copy, cut and paste; filter on attributes.
- **Search:** by name, reference, identifier and content through the register's search index, with filters such as classification, confidentiality and personal data. The employee's permissions determine the search scope; encrypted content is not in the index.
- **Woo requests:** a separate search mode in which you create a Woo dossier, add documents as references and record the search. The included version is pinned in the object storage for as long as the request is open; work on the document can continue.
- **Records management:** business or personal, MDTO metadata, dossiers that pass on classification and retention, retention enforced by S3 Object Lock, legal hold.
- **Correcting mistakes:** a revocation window after registration; for locked items, rendering content unreadable by destroying its key (crypto-shredding).
- **Versions:** view and restore earlier versions; restoring creates a new version.
- **Sharing and access:** durable links through a register and resolver; three roles (read, edit, manage) per person or group; visibility (discoverable or hidden) set by the object's manager; access requests.
- **Collaboration:** "in use by" locking for desktop apps; co-editing in the browser editor; a per-object workflow panel.
- **Time frame:** switch between *Today*, *End of 2027* and *Horizon* to see which features exist when.
- **Real WebDAV server:** connect a real server in the standalone file (see below).

## Why this combination

Each of the three exists already. Together, in one storage, they are rare, and only together do they solve the problem public bodies have:

1. **Records-grade storage.** The storage enforces retention and legal hold itself, per version. Without that, compliance is a promise made by an application.
2. **Records management functions.** Metadata, dossiers, versions, access rules and workflow give every file the context needed to find it for a freedom-of-information request, publish it, or destroy it responsibly.
3. **Integration with familiar windows.** Without it, files stay on old drives and in mailboxes.

On self-managed, open-source storage, and with an identifier that is independent of the platform, the organisation stays in control of its information through the next migration. The approach complements Common Ground: the case management system stays leading for cases; this storage takes care of all other documents.

![Roadmap view](docs/screenshot-roadmap.png)

## Languages

The demo is available in Dutch, German, English, French, Spanish, Italian and Polish. All translations are inside `index.html`.

- The language follows the browser; choose another one top right.
- Link straight to a language with a hash, for example `index.html#de` or `index.html#fr`.
- The choice is remembered in the browser (`localStorage`).

The translations were made with care for professional terminology, but have not been reviewed by native speakers. Corrections are welcome.

## Connecting a real WebDAV server

In the standalone file, *Map network drive* also accepts the address of a real WebDAV server, with user name and password. Browsing and opening work, and creating, renaming, making folders and deleting **really happen on that server**; deleting is permanent. Records functions (metadata, retention, dossiers) and copy/cut/paste are disabled there. Use a test server with test data.

The browser only allows this when the server permits it (CORS) and its certificate is trusted. The Help view (*For administrators*) describes two clean options:

1. Serve the HTML from the same server as the WebDAV drive (same scheme, host and port). CORS then plays no role.
2. Have the server send CORS headers, answer the preflight `OPTIONS` request without authentication, and read header names case-insensitively.

Inside claude.ai the connection does not work, because pages there may not make outside connections.

## Architecture and roadmap in brief

- **Presentation layer:** File Explorer, office suites (Word, LibreOffice and others) with the Office Assistant, document library, team channel, Nextcloud Files in the browser, Nextcloud client.
- **Nextcloud:** WebDAV endpoint, Files, a governance and archive app, the storage interface.
- **Records-grade layer:** an object register, a resolver and key management beside S3 object storage with versioning, Object Lock and legal hold; one bucket per drive.
- **Six requests to Nextcloud:** change notification, delegated version history, read-only metadata from the register, governed deletion, durable identity, and from file to information object. Only requests 3 and 4 fall within the current assignment.
- **Access control:** roles now (RBAC); central policy rules translated into Nextcloud access rules in step 4; a central policy decision point per request on the horizon (PBAC).

![Architecture view](docs/screenshot-architecture.png)

## Technical notes

- One HTML file with vanilla JavaScript and CSS. No framework, no dependencies, no build.
- The only external request is the IBM Plex font from Google Fonts. Without it, the browser falls back to a system font.
- Light and dark mode follow the operating system.
- The demo keeps its state in memory: what you create lasts until you reload the page.

## Repository structure

```
index.html                  the demo
README.md                   this file (English)
README.nl.md                Dutch version
README.de.md                German version
docs/                       screenshots used in the README
```

## Credits

Made by **Erik Hoekstra**, programme architect and senior consultant, i-Ontwikkeling department, Municipality of Haarlem, with assistance from Claude Opus 5.5 (Anthropic).

Prepared for the discussion with Nextcloud about records-grade storage, the Common Ground team and the OWC partnership, and staff, records managers and architects of the municipalities of Haarlem and Zandvoort.

Contact: [ehoekstra@haarlem.nl](mailto:ehoekstra@haarlem.nl) · [erik@erikhoekstra.com](mailto:erik@erikhoekstra.com)

## Licence

© 2026 Municipality of Haarlem. Free to use, modify and distribute under the [European Union Public Licence (EUPL) 1.2](https://interoperable-europe.ec.europa.eu/collection/eupl/eupl-text-eupl-12). See `LICENSE`.
