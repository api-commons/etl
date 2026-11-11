# Data Integration and ETL

The common data-integration vocabulary -- sources and destinations, the connections or pipelines between them, and the sync jobs that move data -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged ETL, ELT, Data Integration, Data Pipelines, Reverse ETL, Data Engineering, Change Data Capture in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| source | 15 | 14 | name 64%, id 57% | sources 13, source 4 |
| destination | 12 | 10 | name 90%, id 70%, destination_type 60%, configuration 50%, created_at 50% | destinations 8, targets 2, destination 2, sinks 2 |
| data_pipeline | 37 | 35 | id 86%, name 83%, type 51% | connections 18, pipelines 11, connectors 9, connection 6 |
| sync_job | 28 | 26 | status 77%, id 69% | run 13, jobs 11, runs 8, sync 7 |

Cohort: 101 providers with harvested OpenAPI, 47 crosswalks. Of the providers exposing a source: 73% create, 93% list, 73% fetch, 67% update, 60% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Destinations agree on name, id, destination_type, configuration and created_at: a typed connector with an opaque configuration object. Sources agree only on name and id; source_type reaches 36%.
- Pipelines -- called connections, connectors, flows or pipelines -- agree on id, name and type. Sync jobs agree on status and id; started_at and finished_at reach 42%.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The pipeline is data_pipeline and its run is sync_job, because connection, job and run are used in ci-cd, workflow-automation and identity.
- configuration stays opaque: each connector type defines its own settings.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
