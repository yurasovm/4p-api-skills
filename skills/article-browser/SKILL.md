---
name: article-browser
description: browse available article site variations and retrieve article lists for a selected variation. use when the user wants to see available article locales, inspect configured article variations, or get a paginated list of articles for a specific variation such as default or another configured site variation. also use when the user asks for active or inactive article lists, sorting, paging, or simple article discovery without creating or modifying content.
---

Use this skill for read-only article discovery workflows in the ecommerce CMS API.

## References

Before making requests, read:

- [../references/authentication.md](../references/authentication.md) — how to obtain and use the `X-Auth-Token` header
- [../references/base-urls.md](../references/base-urls.md) — API base URL and rate limits
- [references/article-listing.md](references/article-listing.md) — endpoint details for this skill

## Supported tasks

- get available article site variations
- get article list for a selected variation
- apply simple list controls such as:
  - active status filtering
  - sorting
  - paging
  - optional inclusion flags when explicitly requested and supported

## Core behavior

Interpret requests like these as article browsing tasks:

- show available article variations
- what article locales are available
- list article site variations
- show articles for default
- show published articles for en
- list inactive articles for ru
- show first page of articles sorted by publish date

## Endpoint selection rules

Use the site variations endpoint when the user asks:

- which variations exist
- which locales are available
- which article site versions are configured
- what variation values are valid

Use the article list endpoint when the user asks:

- to list articles
- to see published or unpublished articles
- to browse articles for a variation
- to view a page of article results

## Variation rules

- variation is a required context for article listing
- if the user requests article list and does not specify variation, use `default`
- if the user specifies variation explicitly, use it exactly as given
- never invent a variation value
- if a requested variation seems invalid, first retrieve the site variations library and use only returned values

## Request construction rules

For article list requests:

- keep the request body minimal
- include only controls the user explicitly requested
- do not add speculative filters
- do not assume undocumented search fields
- do not request markdown or extra content fields unless the user asks and the endpoint supports it

When the user asks for simple article browsing without extra constraints:

- use the selected variation
- omit unnecessary request body fields

## Output formatting rules

### When returning site variations

Present each variation with:

- variation
- language
- country
- currency
- hreflang

Explain briefly which variation will be used by default for later list requests.

### When returning article lists

Prefer concise tabular or bullet-style summaries with:

- id
- name
- slug
- publish_date when available
- is_active
- variation context

Include extra fields only when useful to the request, such as:

- rubric_ids
- tags
- preview_text

If the result set is large:

- summarize the page
- show the most useful fields only
- mention pagination context if available

## Safety and scope boundaries

This skill is strictly read-only.

Do not:

- create articles
- update articles
- activate or deactivate articles
- delete articles
- delete variations
- infer missing write payloads
- fabricate ids, variation values, or filters

If the user asks for article creation, editing, activation, or deletion:

- explain that this skill only supports browsing and listing
- continue only if the user narrows the request back to read-only browsing

## Handling ambiguity

If the user says:

- show articles
- list blog posts
- what articles do we have

Then:

1. use `default` variation
2. return the article list
3. mention that other site variations can also be listed if needed

If the user asks for a variation that is not known:

1. retrieve available site variations
2. show valid options
3. continue using only a valid returned variation

## Correctness rules

- trust the API response as the source of truth
- do not assume that `en`, `ru`, or other locale codes exist unless returned by the site variations library
- preserve exact variation values from the API
- keep read operations deterministic and narrow
