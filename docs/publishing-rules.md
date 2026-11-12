# Publishing Rules

These rules apply to every batch listed in `pipeline/queue.json`.

## 1. Batch selection

For the active batch, process an episode only when:

- `status` is `pending`, AND
- `priority` is `high`.

Every other episode must be left untouched: no digest, no queue change, no
follow-up issue.

## 2. Category classification

Fetch the published keyword taxonomy (link in `README.md`) and classify the
transcript. Count the case-insensitive, whole-word occurrences of every
keyword listed for each category, sum the counts per category, and assign the
category with the highest total. If two categories tie, use the one that
appears first in the taxonomy.

## 3. Digest file

For each processed episode, create `digests/<episode_id>.md` from
`templates/digest-template.md` with these sections:

- `## Overview` - title, series, category id, duration
- `## Key Points` - 3 to 6 bullet points summarising the conversation
- `## Notable Quotes` - at least one short quote from the transcript
- `## Action Items` - the action items found in the transcript (write `- None` if there are none)
- `## Sponsor Disclosure` - include this section ONLY when a sponsor marker appears in the
  transcript; name the sponsor there. Omit the whole section when no sponsor is mentioned.

## 4. Follow-up issues

For each processed episode that has at least one action item, open a repository
issue:

- Title: `Follow-up: <episode_id>`
- Body must contain these lines exactly:
  - `Episode: <episode_id>`
  - `Category: <category id>`
  - `Compliance review required: yes` or `Compliance review required: no`
  - `Action items:` followed by a `- <item>` bullet for every action item.
- Mark compliance as `yes` when the transcript contains any compliance marker
  listed in the taxonomy.

Do not open an issue for an episode without action items.

## 5. Queue update

For every processed episode, set `status` to `processed`, add
`processed_at` (the processing date), and add `digest_path` pointing at the
new digest. Do not change any other field. Skipped episodes must stay exactly
as they are.
