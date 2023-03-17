# Specimen - Instance Standard

## Specimen Information

Collected from `/specimen`. i.e. `gmesh.org/specimen`

| field name | type     |
| ---------- | -------- |
| name       | string   |
| version    | string   |
| nightly    | bool     |
| extrinsic  | bool     |

* `version`: Must be a valid standard version, either nightly or stable.
* `nightly`: If enabled, this specimen should be expected to be carrying the latest nightly standard.
* `extrinsic`: Depicts whether this specimen is connected to the global Fediverse.

If, within a span of time, a server tries to give 1mb+ of data within this chamber,
the server will be called abusive and stunned.

Specimen information can be cached, at maximum, for 30 minutes.
