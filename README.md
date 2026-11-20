# 25 Years of Digital Government Research: dg.o Data and Collaboration Atlas (2000 to 2024)

Data, co-authorship networks and an interactive atlas for the editorial
"25 Years of Digital Government Research: Transforming Public Governance" (Government Information Quarterly, in preparation).

- Live atlas: https://cred1747.github.io/dgo_research25/ (mirror: https://chrisreddish.com/dgo-atlas/)
- Repository: https://github.com/Cred1747/dgo_research25
- DOI: [added when the archive is published]
- Version: 1.0 (data frozen November 20, 2026)

## What this covers
812 papers from the International Conference on Digital Government Research (dg.o), 2000 to 2024, from the
DGRL v2.1 dg.o corpus. Every paper has author affiliations and every author has a country.
The co-authorship network includes all 812 papers: 1,491 unique authors, 2,464 authorships and 3,247 co-author links.
Topics come from a BERTopic model with 10 topics.

## Folders
| Folder | Contents |
|---|---|
| `data/` | `papers.csv` (one row per paper), `authorships.csv` (one row per author per paper), summary tables |
| `networks/` | Co-authorship and country networks as GEXF (open in Gephi) and as node/edge CSV files |
| `index.html` | The interactive atlas (served as the live site; also opens from a download in any browser, loads D3 from a CDN) |
| `figures/` | Figure 1 (two versions) |
| `provenance/` | Every manually collected affiliation with its source URL, source type, date and collector; run manifest |
| `code/` | `DGRL_Enrichment_Replication.ipynb`, the Colab notebook that rebuilds everything with Run all |

## Codebook

### data/papers.csv
| Column | Meaning |
|---|---|
| paper_id | Row id in the DGRL corpus; links all files |
| year | Conference year |
| title | Paper title (conference suffix removed) |
| authors_dgrl | Author string as given in the DGRL corpus |
| doi | DOI, when one exists |
| topic_k10, topic_name_k10 | BERTopic topic number and label (10-topic model) |
| countries, n_countries, regions, institutions | Countries, regions and institutions of all authors (ISO 3166-1 alpha-2 codes, separated by ";") |
| affiliation_source | Where the paper's affiliations came from: OpenAlex, Crossref + ROR, or a manual lookup (ACM Digital Library or the paper itself) |

### data/authorships.csv
| Column | Meaning |
|---|---|
| author, institution, country, country_code | Author name and affiliation at the time of the paper |
| year, paper_title, doi, topic, paper_id | The paper |
| author_position | Order on the paper (1 = first author) |
| co_authors | Other authors on the same paper |
| location_source | Where this author's affiliation came from |

### networks/
- `coauthorship_network_2000_2024.gexf`: full network. Nodes are authors (country, institution, papers, main_topic, first_year, last_year); edges are co-authorship (weight = papers co-written, first_year, last_year).
- `coauthorship_network_2000_2005.gexf`, `coauthorship_network_2000_2012.gexf`: cumulative networks for those periods, with paper counts and weights recounted for the period.
- `country_network.gexf`, `country_nodes.csv`, `country_edges.csv`: countries linked when their authors co-wrote a paper. `Weight` = papers; `papers_2000-2005` etc. give counts by period; `same_place` marks same-country collaboration.

## Methods in brief
Affiliations were matched in this order: OpenAlex (by DOI or title), Crossref with ROR matching, then manual
lookup in the ACM Digital Library or the paper's title page. Manual entries are logged in `provenance/` with their sources.
An author with two affiliations is coded by the first one listed. One author listed only as an "Independent scholar" was
coded US because all co-authors were at a US university (noted in the provenance file).
Authors were matched across sources by first initial and full surname, and merged only with supporting evidence
(a shared institution, a shared co-author or a hyphenated surname). Counts use full counting: each author and each
country on a paper counts once, regardless of the number of co-authors.

## Sources
- DGRL v2.1 dg.o corpus (Digital Government Reference Library)
- OpenAlex (Priem, Piwowar and Orr, 2022)
- Crossref REST API
- Research Organization Registry (ROR) API v2
- DBLP (Ley, 2009)
- ACM Digital Library paper pages (manual lookups)

## How to cite
[Authors, in the order the team agrees]. (2026). 25 Years of Digital Government Research: dg.o Data and
Collaboration Atlas (2000 to 2024) (Version 1.0) [Data set]. https://github.com/Cred1747/dgo_research25

## License
[To be decided by the authors. Suggested: CC BY 4.0 for data and atlas, MIT for code. Check the DGRL corpus terms first.]
