---
description: Tracks offenses against specific origins.
---

# 👩⚖ Offences

## Configuration Trait

`Event`

`IdentificationTuple` - Full ID of the validator

`OnOffenceHandler` - A handler called for every offense report.

## Storage

`Reports` - a StorageMap which stores the report ID can the offense detail for all offense reports.

`ConcurrentReportsIndex` - A vector of reports of the same kind that happened at the same time slot.

`ReportsByKindIndex` - Enumerates all reports of a kind along with the time they happened.

