---
name: crossbar-data-api
description: "CROssBAR Data API skill. Use when working with CROssBAR Data for activities, assays, drugs. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# CROssBAR Data API
API version: 1.0

## Auth
No authentication required.

## Base URL
https://www.ebi.ac.uk/Tools/crossbar

## Setup
1. No auth setup needed
2. GET /activities -- verify access

## Endpoints

13 endpoints across 10 groups. See references/api-spec.lap for full details.

### activities
| Method | Path | Description |
|--------|------|-------------|
| GET | /activities | Get ChEMBL activities |

### assays
| Method | Path | Description |
|--------|------|-------------|
| GET | /assays | Get ChEMBL assays |

### drugs
| Method | Path | Description |
|--------|------|-------------|
| GET | /drugs | drugs collected from Drugbank |

### efo
| Method | Path | Description |
|--------|------|-------------|
| GET | /efo | Get EFO diseases data |

### hpo
| Method | Path | Description |
|--------|------|-------------|
| GET | /hpo | Get HPO phenotypes data |

### intact
| Method | Path | Description |
|--------|------|-------------|
| GET | /intact | Molecular Interactions collected from IntAct |

### molecules
| Method | Path | Description |
|--------|------|-------------|
| GET | /molecules | Get ChEMBL molecules |

### proteins
| Method | Path | Description |
|--------|------|-------------|
| GET | /proteins | Proteins collected from Uniprot for selective tax ids  HUMAN(9606), MOUSE(10090), RAT(10116), BOVINE(9913), ESCHERICHIA_COLI(83333), SUS_SCROFA(9823), MYCOBACTERIUM_TUBERCULOSIS(83332), ORYCTOLAGUS_CUNICULUS(9986), SACCHAROMYCES_CEREVISIAE(559292), CVHSA(694009) & SARS2(2697049) |

### pubchem
| Method | Path | Description |
|--------|------|-------------|
| GET | /pubchem/bioassays | Get pubchem bioassays |
| GET | /pubchem/bioassays/sids | Get pubchem bioassays associated to particular substance ids (sid) & outcome |
| GET | /pubchem/compounds | Get pubchem compounds |
| GET | /pubchem/substances | Get pubchem substances |

### targets
| Method | Path | Description |
|--------|------|-------------|
| GET | /targets | Get ChEMBL targets |

## Enhanced Skill Content
## Question Mapping

- "What bioactivities exist for a given molecule?" -> GET /activities
- "Which assays target a specific ChEMBL target?" -> GET /assays
- "Find drug information by name or PubChem CID" -> GET /drugs
- "What diseases are associated with a MeSH or OMIM identifier?" -> GET /efo
- "Which genes are linked to a phenotype term in HPO?" -> GET /hpo
- "What protein-protein interactions exist for a gene?" -> GET /intact
- "Look up a molecule by InChIKey or SMILES string" -> GET /molecules
- "Get protein details by UniProt accession or gene name" -> GET /proteins
- "Find PubChem bioassays associated with a protein accession" -> GET /pubchem/bioassays
- "What substance outcomes exist for a given SID list?" -> GET /pubchem/bioassays/sids
- "Look up a PubChem compound by CID or canonical SMILES" -> GET /pubchem/compounds
- "Map a PubChem substance SID to its parent compound CID" -> GET /pubchem/substances
- "Which targets correspond to a UniProt accession?" -> GET /targets
- "What assays and activities exist for a drug's ChEMBL ID?" -> GET /assays + GET /activities (multi-step: query assays by chemblId, then activities by assayChemblId)
- "Find all interaction partners and their bioactivities for a gene?" -> GET /intact + GET /activities (multi-step: get interactors by gene, then activities by target)

## Response Tips

- **Activities/Assays/Targets**: Results are ChEMBL-sourced; filter by `pchemblValue` for potency-ranked activity data. Use `limit` and `page` for pagination on all endpoints.
- **Drugs/Molecules**: Identifiers may cross-reference between ChEMBL and PubChem; check both `chemblId` and `pubchemCid` fields when linking datasets.
- **EFO/HPO**: Ontology endpoints return terms with synonyms and cross-references (DOID, MeSH, OMIM); absent matches return 404, not empty arrays.
- **IntAct**: Interaction confidence scores are normalized; filter by `confidence` to control stringency.
- **PubChem group**: Four sub-endpoints cover bioassays, substance-assay outcomes (sids), compounds, and substances; 401/403 errors indicate upstream EBI access issues, not credential problems.
- **Pagination**: All endpoints accept `limit` and `page` as common fields; omitting them returns server defaults. Always check if more pages exist before assuming complete results.

## Anomaly Flags

- **401/403 on public endpoints**: CROssBAR is unauthenticated; these errors signal upstream EBI service issues or IP-based throttling -- surface immediately with a retry suggestion.
- **404 vs empty results**: A 404 means the identifier is unrecognized, not merely unmatched; flag when a user-provided accession or ChEMBL ID returns 404 as it likely indicates a typo or wrong ID type.
- **Cross-database ID mismatches**: When a ChEMBL molecule ID returns data in `/molecules` but not in `/drugs`, flag that the compound may not be an approved drug.
- **Pagination exhaustion**: If sequential page requests return identical or empty data, flag potential pagination boundary reached.
- **Stale ontology terms**: If an EFO or HPO query by `oboId` returns 404 but a synonym search succeeds, flag that the term may have been deprecated or merged in a newer ontology release.
- **High-confidence interaction filtering**: If `/intact` returns results but none meet a reasonable confidence threshold (e.g., > 0.4), proactively note that available interactions are low-confidence.

## Playbook

### 1. Drug-Target-Activity Pipeline

1. Query `/drugs` with the drug `name` or `chemblId` to retrieve the drug record and its ChEMBL molecule ID.
2. Query `/activities` with `moleculeChemblId` from step 1 to get all bioactivity measurements.
3. Extract unique `targetChemblId` values from the activity results.
4. Query `/targets` with each `targetIds` to retrieve target protein details.
5. Optionally query `/proteins` with the target `accession` for full UniProt annotation.

### 2. Phenotype-to-Protein Investigation

1. Query `/hpo` with `hpotermname` or `synonym` to find the matching HPO term and associated gene symbols.
2. For each `genesymbol`, query `/proteins` with the `gene` parameter to get UniProt accessions.
3. Query `/intact` with each `accession` to discover protein-protein interaction partners.
4. Optionally query `/efo` with related disease identifiers (OMIM, MeSH) to cross-reference disease ontology terms.

### 3. Compound Cross-Database Lookup

1. Query `/molecules` with `canonicalSmiles` or `inchiKey` to find the ChEMBL record.
2. Query `/pubchem/compounds` with the same `canonicalSmiles` or `inchiKey` to find the PubChem CID.
3. Query `/drugs` with the `chemblId` from step 1 to check if the compound is an approved drug.
4. If a PubChem CID was found, query `/pubchem/bioassays` with `assayPubchemId` context to find associated bioassay data.

### 4. Protein Interaction and Assay Enrichment

1. Query `/proteins` with a UniProt `accession` to confirm the protein exists and retrieve metadata.
2. Query `/intact` with the same `accession` to get interaction partners and confidence scores.
3. Query `/targets` with the `accession` to find the corresponding ChEMBL target ID.
4. Query `/assays` with `targetChemblId` from step 3 to discover all assays run against this target.
5. Page through results using `limit` and `page` if assay counts are high.

### 5. PubChem Substance-to-Activity Mapping

1. Query `/pubchem/substances` with a known `sid` to resolve the parent compound `cid`.
2. Query `/pubchem/compounds` with the `cid` to get structural details (SMILES, InChIKey).
3. Query `/pubchem/bioassays` to find bioassays associated with the compound's protein targets.
4. Query `/pubchem/bioassays/sids` with the original `sids` and filter by `outcome` to check activity classification (active, inactive, inconclusive).


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
