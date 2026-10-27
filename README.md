# Nuclear Directory: US nuclear supply chain dataset

In short: every published fact in [Nuclear Directory](https://nuclear-directory.org), the companies and facilities of the US nuclear industry and the links between them, with the public documents each fact comes from.

**Download:** companies [CSV](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/companies.csv) | [JSON](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/companies.json) · facilities [CSV](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/facilities.csv) | [JSON](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/facilities.json) · relationships [CSV](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/relationships.csv) | [JSON](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/relationships.json) · sources [CSV](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/sources.csv) | [JSON](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/sources.json) · evidence [CSV](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/evidence.csv) | [JSON](https://raw.githubusercontent.com/tosinoladokun/nuclear-directory-data/v2026.11/evidence.json)

Version 2026.11, released 2026-10-27. Each release is archived on Zenodo, which gives it a DOI.

## Files

Each table is in CSV and JSON. In CSV, lists (aliases, buckets, roles, technologies) are joined with "; "; in JSON they're arrays. Every column is described in [DATA-DICTIONARY.md](DATA-DICTIONARY.md).

| Table | Rows | Holds |
|---|---|---|
| `companies` | 157 | One row per company, by brand |
| `facilities` | 211 | Sites (power plants, fuel plants, test reactors, mines, fusion plants) and the reactor units under them |
| `relationships` | 411 | Links between two companies, and companies' roles at facilities |
| `sources` | 420 | The public documents the facts come from |
| `evidence` | 1582 | Which source states each fact |

Other files: `DATA-DICTIONARY.md`, `CITATION.cff`, `LICENSE`, `CHANGELOG.md` and `manifest.json`.

## Fields

| Table | Columns |
|---|---|
| `companies` | `slug`, `name`, `legal_name`, `aliases`, `website`, `description`, `hq_city`, `hq_state`, `country_code`, `founded_year`, `status`, `buckets`, `roles`, `technologies`, `checked_on`, `url` |
| `facilities` | `slug`, `name`, `level`, `site_slug`, `facility_type`, `status`, `technology`, `reactor_type`, `capacity_mw`, `nrc_docket`, `eia_plant_id`, `city`, `state`, `country_code`, `latitude`, `longitude`, `checked_on`, `url` |
| `relationships` | `id`, `type`, `from_slug`, `to_table`, `to_slug`, `ownership_pct`, `description`, `started_on`, `ended_on`, `checked_on` |
| `sources` | `id`, `url`, `title`, `publisher`, `document_type`, `published_on`, `accessed_on` |
| `evidence` | `fact_table`, `fact_key`, `fact_part`, `source_id` |

### How the tables join

- `facilities.site_slug` is the `slug` of a unit's site.
- `relationships.from_slug` is a company `slug`. `relationships.to_slug` is a `slug` in `companies` or `facilities`, as `to_table` says.
- `evidence.fact_table` and `evidence.fact_key` point at a row in `companies`, `facilities` or `relationships`, and `evidence.source_id` is a `sources.id`. For a company's category or technology, `fact_part` says which one (`role:<key>` or `technology:<key>`).

## How it's collected

1. Crawlers read public records: NRC's list of power reactors, NRC's daily power reactor status reports, NRC's list of reactors being decommissioned, EIA's monthly generator inventory (EIA-860M), DOE awards on USAspending.gov, NRC's pages for each operating reactor (its vendor), NRC's fuel cycle facility pages, NRC's uranium recovery sites, DOE program pages, and DOE Isotope Program sites.
2. People research the rest from companies' own pages, press releases, SEC filings and agency pages.
3. AI models help: they read pages and propose facts, and a separate model checks each proposal against its quote. Neither publishes anything. Tosin Oladokun is the editor of record.

## How it's checked

- Every published fact has a public source and a quote that states it. A fact we can't source isn't published.
- A person approves every fact before it's published, and a person's decision is not overwritten by a crawler.
- Sources are official records first (NRC, EIA, DOE, SEC), then the company itself, then named reporting. Aggregators and directories are used as leads, not cited as sources. Power deals, investments and awards need an official record or the parties' own statement.
- Crawled sources are read again on a schedule; a fact whose source changes or drops it goes back to a person.
- The full rules are in the project's [data standard](https://github.com/tosinoladokun/nuclear-directory/blob/main/docs/DATA.md).

## Limits

- US only, and not every company or facility in the industry yet.
- A blank value means no source states it. Nothing is guessed.
- Capacity is net summer capacity in MW, from EIA, for reactor units. A site's capacity is the sum of its operating units.
- Buckets are computed from each company's sourced categories and links, so a company can be in several. Count companies, not the sum of buckets.
- Quotes aren't in this dataset, because they're other publishers' text. Each fact's page on nuclear-directory.org shows its quote, and the `sources` table links to every document.
- Slugs are stable keys, but a merged or renamed company can change slug. The website redirects the old one; this dataset doesn't list old slugs, so check the changelog when joining two releases.
- The data is as of the release date. The website changes daily.

## How to cite

Cite the DOI that covers all versions, and say which version you used and when you downloaded it.

**Reference list (APA style):**

> Oladokun, T. (2026). *Nuclear Directory: US nuclear supply chain dataset* (Version 2026.11) [Data set]. Nuclear Directory. DOI from Zenodo. Add the date you downloaded it.

**BibTeX:**

```
@misc{oladokun_nuclear_directory,
  author    = {Oladokun, Tosin},
  title     = {Nuclear Directory: US nuclear supply chain dataset},
  year      = {2026},
  version   = {2026.11},
  publisher = {Nuclear Directory},
  note      = {Data set},
  url       = {https://nuclear-directory.org}
}
```

**In running text:** "Nuclear Directory (Oladokun, 2026)", linking the DOI.

**One fact from the website:** name the company or plant page and the date you read it. Each page shows the source document behind every fact; citing that document directly is better than citing us for the fact.

## Licence

Creative Commons Attribution 4.0 International ([CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)). You may share and adapt the data, including commercially, as long as you credit it (see How to cite), link the licence and say whether you made changes. This licence covers the data in this repository. The website's code is not covered.

## Corrections

Report a wrong or missing fact from its page on nuclear-directory.org, with a link to a public source.
