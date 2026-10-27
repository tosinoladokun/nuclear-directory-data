# Data dictionary

Every column in every table of Nuclear Directory: US nuclear supply chain dataset, version 2026.11. Dates are ISO 8601 (`2026-10-09`). Values follow the project's [data standard](https://github.com/tosinoladokun/nuclear-directory/blob/main/docs/DATA.md).

## companies

| Column | Holds |
|---|---|
| `slug` | The company's key, also the end of its page URL. Never reused; a renamed or merged company's old slug redirects |
| `name` | Display name: the brand the company uses on its own site |
| `legal_name` | Registered legal name, when a source states it |
| `aliases` | Other names sources use for it: legal entities, abbreviations, other spellings |
| `website` | The company's own website |
| `description` | One or two sentences on what the company does, written by Nuclear Directory from its sources |
| `hq_city` | Headquarters city, when a source states it |
| `hq_state` | Headquarters state, as a two-letter USPS code |
| `country_code` | Country it's based in, ISO 3166 alpha-2, only when a source states it |
| `founded_year` | Year founded, when a source states it |
| `status` | active, acquired or defunct |
| `buckets` | Every industry group its sourced categories and links put it in (see Buckets) |
| `roles` | Its categories, each from a quote that states it (see Roles) |
| `technologies` | Technologies it works on: fission, fusion, smr |
| `checked_on` | Date a person or the verifier last checked it |
| `url` | Its page on nuclear-directory.org |

## facilities

| Column | Holds |
|---|---|
| `slug` | The facility's key, also the end of its page URL |
| `name` | Display name: the operator's name for the plant; units follow NRC's list (Vogtle 3) |
| `level` | site (a place) or unit (one reactor under its site) |
| `site_slug` | For a unit, the slug of its site |
| `facility_type` | Kind of facility: power_reactor, research_reactor, fuel_facility, enrichment, fusion_facility, uranium_mine, mill or other; blank when not stated |
| `status` | operating, not_operating, under_construction, planned, shut_down or decommissioning; blank when not stated |
| `technology` | fission or fusion, when stated |
| `reactor_type` | Reactor design type as the source states it, e.g. PWR, BWR |
| `capacity_mw` | Net summer capacity in MW, from EIA-860M. For a unit, its own. For a site, the total of its operating units when each is known (blank otherwise); a one-record plant gives its own figure while it operates |
| `nrc_docket` | NRC docket number, for a licensed reactor |
| `eia_plant_id` | EIA plant ID, on a site |
| `city` | City, when a source names it |
| `state` | State, as a two-letter USPS code |
| `country_code` | Country, ISO 3166 alpha-2 |
| `latitude` | Latitude, from EIA or an official record, to 6 decimal places |
| `longitude` | Longitude, from EIA or an official record, to 6 decimal places |
| `checked_on` | Date a person or the verifier last checked it |
| `url` | Its page on nuclear-directory.org |

## relationships

| Column | Holds |
|---|---|
| `id` | The link's key: company-<n> for a link between companies, facility-<n> for a company's role at a facility |
| `type` | What the link means (see Relationship types) |
| `from_slug` | Slug of the company the link starts from (in companies) |
| `to_table` | companies or facilities: where to_slug is |
| `to_slug` | Slug of the company or facility the link points to |
| `ownership_pct` | Ownership share in percent, on owns links, only as stated |
| `description` | Detail the source gives, e.g. the deal stage (MOU, signed PPA) or the units covered |
| `started_on` | Date the link began, when stated |
| `ended_on` | Date the link ended, when stated |
| `checked_on` | Date a person or the verifier last checked it |

## sources

| Column | Holds |
|---|---|
| `id` | The source's key |
| `url` | Address of the public document |
| `title` | The document's title |
| `publisher` | Who publishes it. When it isn't known, its web domain |
| `document_type` | What kind of document it is (see Document types) |
| `published_on` | Date the document was published, when known |
| `accessed_on` | Date Nuclear Directory last read it |

## evidence

| Column | Holds |
|---|---|
| `fact_table` | Table of the fact: companies, facilities or relationships |
| `fact_key` | The fact's slug or id in that table |
| `fact_part` | For a company's category or technology, which one (role:<key> or technology:<key>); blank for the record or link itself |
| `source_id` | The source that states it (in sources) |

## Relationship types

| Type | Means |
|---|---|
| `operates` | Company to facility. Runs it day to day; for a power reactor, holds the NRC operating license |
| `owns` | Company to facility. Holds an ownership share; ownership_pct only when the source states it |
| `vendor_for` | Company to facility. Designed or supplies the reactor |
| `offtakes_from` | Company to facility. Has agreed to buy the plant's power |
| `supplies` | Company to company. Provides fuel, equipment or services under a stated agreement |
| `invests_in` | Company to company. Takes equity |
| `funds` | Company to company. Grants, awards or cost-shared programs |
| `offtake_with` | Company to company. Has agreed to buy power from the company's fleet, not one plant |
| `subsidiary_of` | Company to company. Points from the child to its parent |

## Buckets

| Bucket | Name |
|---|---|
| `reactor-developers` | Developers |
| `fuel` | Fuel and materials |
| `components` | Components and manufacturing |
| `waste-decommissioning` | Waste and decommissioning |
| `utilities` | Power plant owners and operators |
| `power-buyers` | Power buyers |
| `services` | Services and engineering |
| `investors` | Investors |
| `government-research` | Government and research |

## Roles

| Role | Name |
|---|---|
| `components` | Components |
| `conversion` | Conversion |
| `coolant` | Coolant |
| `data_center_offtaker` | Data center offtaker |
| `enrichment` | Enrichment |
| `fabrication` | Fuel fabrication |
| `fuel` | Fuel |
| `government_agency` | Government agency |
| `heavy_water` | Heavy water |
| `helium` | Helium |
| `isotopes` | Isotopes |
| `lead` | Lead |
| `mining` | Mining and milling |
| `molten_salt` | Molten salt |
| `national_lab` | National lab |
| `operator` | Operator |
| `project_developer` | Project developer |
| `reactor_services` | Reactor services |
| `reactor_vendor` | Reactor vendor |
| `regulatory_consultant` | Regulatory consultant |
| `research_organization` | Research organization |
| `sodium` | Sodium |
| `university` | University |
| `utility` | Utility |
| `venture_capital` | Venture capital |
| `waste_decommissioning` | Waste and decommissioning |
| `water` | Water |

## Document types

| Type | Means |
|---|---|
| `government_dataset` | A data file an agency publishes, e.g. EIA-860M |
| `regulator_list` | A list or report a regulator publishes, e.g. NRC's reactor list |
| `award_record` | A federal award record on USAspending.gov |
| `sec_filing` | A filing with the U.S. Securities and Exchange Commission |
| `federal_register` | A Federal Register notice or other U.S. government publication |
| `government_page` | Another page an agency publishes |
| `company_page` | A company's own page, press release or report |
| `news_article` | Named reporting: trade press or news |
| `web_page` | Any other public page |
