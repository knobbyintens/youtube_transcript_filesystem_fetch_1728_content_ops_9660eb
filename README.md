# Northwind Creator Ops

Internal repository for the creator operations team. It holds the weekly
processing queue, the archived episode transcripts, and the templates used by
the digest pipeline.

## Layout

- `pipeline/queue.json` - the active processing batch and its episode queue
- `transcripts/` - transcript archive exported from the video platform
- `docs/publishing-rules.md` - digest, classification, and issue rules
- `templates/digest-template.md` - the digest template
- `digests/` - digest files produced by the pipeline (created as episodes are processed)

## Published keyword taxonomy

The canonical keyword taxonomy for classification is published here:

https://gist.githubusercontent.com/knobbyintens/685e0866d10ba79f8b2f98323e9a923c/raw/content-ops-taxonomy-9660eb.json

Always use that published taxonomy; do not invent category ids.
