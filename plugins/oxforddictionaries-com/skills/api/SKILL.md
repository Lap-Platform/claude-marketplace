---
name: api
description: " API skill. Use when working with  for inflections, entries, search. Covers 26 endpoints."
version: 1.0.0
generator: lapsh
---

# 
API version: 1.11.0

## Auth
ApiKey app_id in header

## Base URL
https://od-api-demo.oxforddictionaries.com:443/api/v1

## Setup
1. Set your API key in the appropriate header
2. GET /languages -- verify access

## Endpoints

26 endpoints across 12 groups. See references/api-spec.lap for full details.

### inflections
| Method | Path | Description |
|--------|------|-------------|
| GET | /inflections/{source_lang}/{word_id}/{filters} | Check a word exists in the dictionary and retrieve its root form |

### entries
| Method | Path | Description |
|--------|------|-------------|
| GET | /entries/{source_lang}/{word_id} | Retrieve dictionary information for a given word |
| GET | /entries/{source_lang}/{word_id}/regions={region} | Specify GB or US dictionary for English entry search |
| GET | /entries/{source_lang}/{word_id}/{filters} | Apply filters to response |
| GET | /entries/{source_lang}/{word_id}/synonyms | Retrieve words that are similar |
| GET | /entries/{source_lang}/{word_id}/antonyms | Retrieve words that mean the opposite |
| GET | /entries/{source_lang}/{word_id}/synonyms;antonyms | Retrieve synonyms and antonyms for a given word |
| GET | /entries/{source_translation_language}/{word_id}/translations={target_translation_language} | Retrieve translation for a given word |
| GET | /entries/{source_language}/{word_id}/sentences | Retrieve corpus sentences for a given word |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/{source_lang} | Retrieve possible matches to input |
| GET | /search/{source_search_language}/translations={target_search_language} | Retrieve possible translation matches to input |

### wordlist
| Method | Path | Description |
|--------|------|-------------|
| GET | /wordlist/{source_lang}/{filters_basic} | Retrieve a list of words in a category |
| GET | /wordlist/{source_lang}/{filters_advanced} | Retrieve list of words for category with advanced options |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats/frequency/word/{source_lang}/ | Retrieve the frequency of a word derived from a corpus. |
| GET | /stats/frequency/words/{source_lang}/ | Retrieve a list of frequencies of a word/words derived from a corpus. |
| GET | /stats/frequency/ngrams/{source_lang}/{corpus}/{ngram-size}/ | Retrieve the frequency of ngrams (1-4) derived from a corpus |

### languages
| Method | Path | Description |
|--------|------|-------------|
| GET | /languages | Lists available dictionaries |

### filters
| Method | Path | Description |
|--------|------|-------------|
| GET | /filters | Lists available filters |
| GET | /filters/{endpoint} | Lists available filters for specific endpoint |

### lexicalcategories
| Method | Path | Description |
|--------|------|-------------|
| GET | /lexicalcategories/{language} | Lists available lexical categories in a dataset |

### registers
| Method | Path | Description |
|--------|------|-------------|
| GET | /registers/{source_language} | Lists available registers in a  monolingual dataset |
| GET | /registers/{source_register_language}/{target_register_language} | Lists available registers in a bilingual dataset |

### domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /domains/{source_language} | Lists available domains in a monolingual dataset |
| GET | /domains/{source_domains_language}/{target_domains_language} | Lists available domains in a bilingual dataset |

### regions
| Method | Path | Description |
|--------|------|-------------|
| GET | /regions/{source_language} | Lists available regions in a monolingual dataset |

### grammaticalFeatures
| Method | Path | Description |
|--------|------|-------------|
| GET | /grammaticalFeatures/{source_language} | Lists available grammatical features in a dataset |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get inflection details?" -> GET /inflections/{source_lang}/{word_id}/{filters}
- "Get entry details?" -> GET /entries/{source_lang}/{word_id}
- "Get regions={region} details?" -> GET /entries/{source_lang}/{word_id}/regions={region}
- "Get entry details?" -> GET /entries/{source_lang}/{word_id}/{filters}
- "List all synonyms?" -> GET /entries/{source_lang}/{word_id}/synonyms
- "List all antonyms?" -> GET /entries/{source_lang}/{word_id}/antonyms
- "List all synonyms;antonyms?" -> GET /entries/{source_lang}/{word_id}/synonyms;antonyms
- "Search search?" -> GET /search/{source_lang}
- "Search translations={target_search_language}?" -> GET /search/{source_search_language}/translations={target_search_language}
- "Get translations={target_translation_language} details?" -> GET /entries/{source_translation_language}/{word_id}/translations={target_translation_language}
- "Get wordlist details?" -> GET /wordlist/{source_lang}/{filters_basic}
- "Get wordlist details?" -> GET /wordlist/{source_lang}/{filters_advanced}
- "List all sentences?" -> GET /entries/{source_language}/{word_id}/sentences
- "Get word details?" -> GET /stats/frequency/word/{source_lang}/
- "Get word details?" -> GET /stats/frequency/words/{source_lang}/
- "Get ngram details?" -> GET /stats/frequency/ngrams/{source_lang}/{corpus}/{ngram-size}/
- "List all languages?" -> GET /languages
- "List all filters?" -> GET /filters
- "Get filter details?" -> GET /filters/{endpoint}
- "Get lexicalcategory details?" -> GET /lexicalcategories/{language}
- "Get register details?" -> GET /registers/{source_language}
- "Get register details?" -> GET /registers/{source_register_language}/{target_register_language}
- "Get domain details?" -> GET /domains/{source_language}
- "Get domain details?" -> GET /domains/{source_domains_language}/{target_domains_language}
- "Get region details?" -> GET /regions/{source_language}
- "Get grammaticalFeature details?" -> GET /grammaticalFeatures/{source_language}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
