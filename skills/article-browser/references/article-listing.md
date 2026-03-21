# Article listing reference

## Purpose

This reference supports the `article-browser` skill.

Use it when building read-only article discovery flows:

- get available site variations
- list articles for a selected variation

## Site variations endpoint

Use the site variations library endpoint to discover valid variation values before listing articles when needed.

Returned variation objects may include:

- `variation`
- `lang`
- `country`
- `currency`
- `href-lang`

### Operational rule

Never invent variation values.  
If the user requests a variation that is not confirmed, first retrieve the site variations library.

## Article list endpoint

The article list endpoint requires variation in the path.

Typical usage:

- list articles for `default`
- list active articles for a selected variation
- sort by `publish_date`
- paginate through results

The endpoint returns a paginated article list for the selected variation.

Article records may include fields such as:

- `id`
- `name`
- `slug`
- `publish_date`
- `is_active`
- `rubric_ids`
- `tags`
- `preview_text`

## Default behavior

If the user asks for article list without specifying variation:

- use `default`

If the user asks which variations exist:

- retrieve the site variations library first

## Scope limits

This skill does not support:

- article creation
- article update
- article activation or deactivation
- article deletion

Those actions belong in a separate write-enabled article management skill.

## Good request examples

- Show available article site variations
- List articles for default
- Show active articles for default
- Show inactive articles for en
- List first page of articles sorted by publish date

## Bad assumptions to avoid

- Do not assume a locale exists because it is common
- Do not invent filters that the endpoint may not support
- Do not switch variation automatically without telling the user
