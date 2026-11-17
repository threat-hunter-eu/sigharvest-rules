# Licences of the rules in this repository

This repository has **no single licence**. It republishes Sigma rules written by many people and organisations, and
every rule keeps the licence of the repository it was taken from. Nothing here re-licenses a rule.

## The repository itself

The files on the `main` branch (this note, the README, `.github/`) are written by the sigharvest contributors and are
available under the MIT licence, like [sigharvest](https://github.com/threat-hunter-eu/sigharvest/blob/main/LICENSE).
That licence does **not** extend to the release files.

## The release files

| Where | Licence |
|---|---|
| Rule YAML in `sigharvest-rules-permissive.zip` | The licence of each rule's source: Detection Rule License 1.1 (SigmaHQ), MIT, Apache-2.0, BSD, CC0 and similar permissive licences |
| Rule YAML in `sigharvest-rules-copyleft.zip` | The licence of each rule's source: GPL, AGPL, LGPL, MPL, EUPL, CC-BY-SA and similar. Kept in a separate archive so it is never mixed into the permissive pack by accident |
| Metadata files (`rules.jsonl.gz`, `index.json.gz`, `provenance.json.gz`, `attack-navigator-layer.json`, `manifest.json`, `changes.json`, `stats.json`) | Short factual fields (ids, title, logsource, level, tags, licence, link). For rules that are not redistributed, the description and author are left out |
| ATT&CK technique names | © 2026 The MITRE Corporation. This work is reproduced and distributed with the permission of The MITRE Corporation ([terms of use](https://attack.mitre.org/resources/legal-and-branding/terms-of-use/)). MITRE ATT&CK® and ATT&CK® are registered trademarks of The MITRE Corporation |

Rules are shipped **byte-identical** to the source file (the `author:` field stays). The only exception is a rule
taken from a legacy multi-document collection: it is shipped as the flattened effective document and marked
`modified` in `ATTRIBUTION.md` and in the archive's `manifest.jsonl`.

## Where to find the licence of one rule

- `manifest.jsonl` inside each zip and `provenance.json.gz` in the release: source repository, commit, path, author
  and licence of every rule.
- `NOTICE.md`: every source with its licence, its copyright lines and any `NOTICE` file it ships, verbatim.
- `LICENSES/` in each zip and `LICENSES.zip` in the release: the full text of every licence named, and each source's
  own `LICENSE` / `COPYING` / `NOTICE` files.

## What is never published

- Rules from a repository that states no licence.
- Rules under non-commercial, no-derivatives, source-available or custom terms.
- Rules from sources not marked as redistributable in sigharvest's source lists.

These appear only as metadata with a link to the original file.

## Redistributing a pack

Keep `NOTICE.md`, `ATTRIBUTION.md` and `LICENSES/` with the rules, keep each rule's author and source link (the
Detection Rule License asks for it), and do not merge the copyleft pack into a work under an incompatible licence.

This note is not legal advice. The licence classes are decided by code
([licensing.py](https://github.com/threat-hunter-eu/sigharvest/blob/main/src/sigharvest/licensing.py)) from each source's
declared licence. If you are an author and a rule is listed with the wrong licence, or you want it removed, open an
issue in [threat-hunter-eu/sigharvest](https://github.com/threat-hunter-eu/sigharvest/issues) or write to security@threat-hunting.eu.

Not affiliated with or endorsed by SigmaHQ, OISF, Proofpoint/Emerging Threats or MITRE.
