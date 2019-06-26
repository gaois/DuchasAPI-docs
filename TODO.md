# Issues to be addressed

## Essential

- A number of the filter parameters in the Main Manuscript Collection API, e.g. `CollectorID`, `InformantID`, `PlaceID`, etc., do not retrieve the complete result sets that they should. This is not due to any technical issue with the API, rather is the result of changes that are currently underway to the data structure of this collection. The editors have requested that certain data be associated with manuscript items rather than manuscript parts. This issue is currently being addressed.
- Transcripts in the Schools' Collection API are served from a copy of the production database. These services need to be integrated so that transcripts are retrived from the 'live' data.

## Planned

- First name/surname

## Desirable

- Fulltext search across collections, e.g. `/api/v1.0/cbes/?Query=St.+John's+Eve`
