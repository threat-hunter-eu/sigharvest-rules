# sigharvest-rules

Nightly packs of public Sigma rules, collected, deduplicated and checked by
[sigharvest](https://github.com/threat-hunter-eu/sigharvest). This repository holds only the published packs (as GitHub
Releases) and the search site. The code, the source lists and the issue tracker are in
[threat-hunter-eu/sigharvest](https://github.com/threat-hunter-eu/sigharvest).

- **Search the rules:** <https://threat-hunter-eu.github.io/sigharvest-rules/>
- **Latest pack:** [Releases -> Latest](https://github.com/threat-hunter-eu/sigharvest-rules/releases/latest)

## What is in a release

A release `rules-YYYY-MM-DD` is published when the corpus changed since the previous one (`.2`, `.3` on a same-day
rerun).

| File | What's inside |
|---|---|
| `sigharvest-rules-permissive.zip` | Rule YAML under DRL-1.1, MIT, Apache-2.0, BSD, CC0 and similar, with `NOTICE.md` and `LICENSES/` |
| `sigharvest-rules-copyleft.zip` | Rule YAML under GPL, LGPL, MPL and similar, kept in a separate archive |
| `rules.jsonl.gz`, `index.json.gz` | Metadata for **every** rule (title, logsource, level, ATT&CK, licence, link to the original file) |
| `provenance.json.gz` | Source repository, commit, path, licence and author of each published rule |
| `attack-navigator-layer.json` | Rule count per ATT&CK technique, for [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/) |
| `changes.json`, `RELEASE_NOTES.md` | What was added, changed or removed since the previous release |
| `manifest.json`, `stats.json` | Counts, versions, sources and the content id of the pack |
| `NOTICE.md`, `ATTRIBUTION.md`, `LICENSES.zip` | Licence and copyright lines per source, the licence texts, each source's own LICENSE / NOTICE files |
| `SHA256SUMS`, `SHA256SUMS.sigstore.json` | Checksums of every file, and a keyless Sigstore signature of them (when signing is enabled) |
| `build-info.json` | Which sigharvest commit and workflow run built the release (informational, not in `SHA256SUMS`) |

Rules whose licence does not allow redistribution, or that state no licence, are **never** in the zips: the
metadata files list them with a link to the original file.

## Download

These links always point at the newest release:

```bash
curl -LO https://github.com/threat-hunter-eu/sigharvest-rules/releases/latest/download/sigharvest-rules-permissive.zip
curl -LO https://github.com/threat-hunter-eu/sigharvest-rules/releases/latest/download/SHA256SUMS
sha256sum --check --ignore-missing SHA256SUMS
```

To pin one day, replace `latest/download` with `download/rules-YYYY-MM-DD`.

Start a local sigharvest workspace from the newest pack (search, exports, web UI, SIEM queries) in about ten minutes:

```bash
sigharvest init ~/sigma --from-release latest
```

Lint your own rules against the corpus in CI with the
[sigharvest lint action](https://github.com/threat-hunter-eu/sigharvest/blob/main/docs/automation.md#the-lint-action).

## Verify

```bash
sha256sum --check --ignore-missing SHA256SUMS

cosign verify-blob SHA256SUMS \
  --bundle SHA256SUMS.sigstore.json \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com \
  --certificate-identity https://github.com/threat-hunter-eu/sigharvest/.github/workflows/nightly.yml@refs/heads/main
```

The signature names the **sigharvest** repository: the packs are built and signed there and only published here.

## Licences

Each rule keeps the licence of the repository it comes from. Read [LICENSE-NOTE.md](LICENSE-NOTE.md) before
redistributing a pack, and `NOTICE.md` in the release for the full list of sources, licences and copyright lines.

## How it is built

Every night the workflow `nightly.yml` of [sigharvest](https://github.com/threat-hunter-eu/sigharvest) fetches the public
rule repositories in its curated and extended lists, validates and deduplicates the rules, builds these files
reproducibly, checks their checksums and publishes a release here only when the content changed. The search site is
rebuilt from each new release by this repository's `pages.yml`.

Retention: the newest 30 releases, plus the first release of each month for the last 12 months.

## Questions, removals, new sources

Open an issue in [threat-hunter-eu/sigharvest](https://github.com/threat-hunter-eu/sigharvest/issues) or write to
security@threat-hunting.eu. Authors who want a rule
removed or attributed differently: please say so there; it is handled in the next nightly build.

Not affiliated with or endorsed by SigmaHQ, OISF, Proofpoint/Emerging Threats or MITRE.
