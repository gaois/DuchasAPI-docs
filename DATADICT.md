# Dúchas Application Programming Interface (Version 0.5): Data dictionary

**Note:** This documentation describes a prerelease version of the Dúchas API. Features are being added on an ongoing basis. URLs in this document refer to the test.duchas.ie test domain. These links and other aspects of the documentation will be revised in advance of the v1.0 release.

This document describes the data structure of the collections made available via the Dúchas Application Programming Interface (API). Dúchas is a project is to initiate the digitization of the [National Folklore Collection](https://www.ucd.ie/irishfolklore/en) (NFC). For general information regarding the API and for developer guidelines please consult the [developer documentation](https://github.com/gaois/DuchasAPI-docs/blob/master/README.md).

## Contents

- [The Main Manuscript Collection](#the-main-manuscript-collection-cbé)
  - [`volume`](#volume)
  - [`page`](#page)
  - [`part`](#part)
  - [`item`](#item)
- [The Photographic Collection](#the-photographic-collection-cbég)
  - [`photograph`](#photograph)
  - [`handbookTopic`](#handbookTopic)
  - [`format`](#format)
  - [`archivedInfo`](#archivedInfo)
  - [`digitization`](#digitization)
  - [Values](#values)
- [The Persons Database](#the-persons-database-cbéd)
  - [`person`](#person)
  - [`name`](#name)
  - [`occupation`](#occupation)
- [Common entities](#common-entities)
  - [`county`](#county)
  - [`country`](#country)
  - [`date`](#date)
  - [`locationAbroad`](#locationAbroad)
  - [`locationIreland`](#locationIreland)
- [Common values](#common-values)
  - [`status`](#status)
  
## The Main Manuscript Collection (CBÉ)

Queries to the Main Manuscript Collection may return one or more `volume` objects. The information below describes the properties of this object type.

### `volume`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| ID              | integer             | one                 | The volume identifier (unique within collection) |
| DateCreated     | ISO 8601 datetime   | none or one         | The date and time of entry creation  |
| DateModified    | ISO 8601 datetime   | none or one         | The date and time of most recent modification to entry  |
| VolumeNumber    | string              | none or one         | The volume number         |
| Status          | integer             | one                 | Specifies the entry's editorial [status](#status)  |
| Pages           | [`page`](#page)     | one                 |  |
| Parts           | [`part`](#part)     | none or one         |  |

### `page`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| ID              | integer             | one                 | The page identifier (unique within collection) |
| PageNumber      | string              | one                 | The page number     |
| ListingOrder    | string              | one                 |  |
| ImageFileName   | string              | one                 |  |
| Sensitive       | boolean             | one                 | If true the page contains sensitive content and should not be made publicly available |

### `part`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| ID              | integer             | one                 | The part identifier (unique within collection) |
| DateCreated     | ISO 8601 datetime   | none or one         | The date and time of entry creation  |
| DateModified    | ISO 8601 datetime   | none or one         | The date and time of most recent modification to entry  |
| TitlePages      | integer             | none or one or more |  |
| Date            | [`date`](#date)     | none or one         |  |
| Counties        | [`county`](#county) | none or one or many | Denotes the Irish administrative county or counties in which the photograph was captured |
| LocationsIreland | [`locationIreland`](#locationIreland)  | none or one or many | Denotes a location or locations in Ireland associated with the photograph |
| Countries       | [`country`](#country) | none or one or many | Denotes a country or countries, apart from Ireland, associated with the photograph |
| LocationsAbroad | [`locationAbroad`](#locationAbroad) | none or one or many | Denotes a location or locations outside of Ireland associated with the photograph |
| Collectors      | [`person`](#person) | none or one or many |  |
| Informants      | [`person`](#person) | none or one or many |  |
| RelevantPersons | [`person`](#person) | none or one or many |  |
| Items           | [`item`](#item)     | none or one or many |  |

### `item`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| ID              | integer             | one                 | The item identifier (unique within collection) |
| DateCreated     | ISO 8601 datetime   | none or one         | The date and time of entry creation  |
| DateModified    | ISO 8601 datetime   | none or one         | The date and time of most recent modification to entry  |

### Values

This section describes values particular to properties of the `volume` object and its child objects.

#### `status`

Specifies the volume's editorial status. Only entries with a status value of **4** are deemed ready for publication.

| Value           | Description               |
| :-------------- | :------------------------ |
| 0               | The photograph is newly ingested |
| 1               | First editorial pass complete |
| 2               | First editorial check complete |
| 3               | Second editorial pass complete |
| 4               | Second editorial check complete |

## The Photographic Collection (CBÉG)

Queries to the Photographic Collection may return one or more `photograph` objects. The information below describes the properties of this object type.

### `photograph`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| ID              | integer             | one                 | The photograph identifier (unique within collection) |
| DateCreated     | ISO 8601 datetime   | one                 | The date and time of entry creation  |
| DateModified    | ISO 8601 datetime   | none or one         | The date and time of most recent modification to entry  |
| ReferenceNumber | string              | none or one         | The NFC archival reference for the photograph      |
| Status          | integer             | one                 | Specifies the entry's editorial [status](#status)  |
| Sensitive       | boolean             | one                 | If true the entry contains sensitive content and should not be made publicly available |
| Digitized       | boolean             | one                 | If true the entry is associated with a digitized image  |
| Copyright       | string              | none or one         | Denotes the [copyright](#copyright) holder for the entry  |
| Condition       | integer             | none or one         | Denotes the overall [condition](#condition) or clarity of the digitized image associated with this entry  |
| ConditionDescription | string              | none or one         | Additional commentary on the image condition, where appropriate  |
| HandbookTopic   | [`handbookTopic`](#handbookTopic)     | none or one         | Denotes the associated subject heading (topic) in Seán Ó Súilleabháin's [*A Handbook of Irish Folklore*](https://www.duchas.ie/en/tpc/cbeg) |
| Date            | [`date`](#date)     | none or one         | Metadata associated with the photograph's capture date |
| Photographer    | [`person`](#person) | none or one         | Denotes the person who captured the photograph |
| RelevantPersons | [`person`](#person) | none or one or many | Denotes persons visible in, or otherwise associated with, the photograph |
| Counties        | [`county`](#county) | none or one or many | Denotes the Irish administrative county or counties in which the photograph was captured |
| LocationsIreland | [`locationIreland`](#locationIreland)  | none or one or many | Denotes a location or locations in Ireland associated with the photograph |
| Countries       | [`country`](#country) | none or one or many | Denotes a country or countries, apart from Ireland, associated with the photograph |
| LocationsAbroad | [`locationAbroad`](#locationAbroad) | none or one or many | Denotes a location or locations outside of Ireland associated with the photograph |
| ArchivedDescriptionStatus | string        | none or one         | Specifies the publication [status](#archivedDescriptionStatus) of the `ArchivedDescription` field   |
| ArchivedDescription | string             | none or one         | A free-text archival description of the photograph. Imported from NFC's previous data management system at the outset of the digitization process. |
| ExtraInfoStatus | string              | none or one         | Specifies the publication [status](#extraInfoStatus) of the `ExtraInfoEN` and `ExtraInfoGA` fields |
| ExtraInfoEN     | string              | none or one         | A free-text commentary on the photograph (in English). Authored as part of the Dúchas project. |
| ExtraInfoGA     | string              | none or one         | A free-text commentary on the photograph (in Irish). Authored as part of the Dúchas project. |
| Formats         | [`format`](#format)             | none or one or many  | Describes the physical image formats held by the NFC that are associated with the entry |
| ArchivedInfo    | [`archivedInfo`](#archivedInfo)      | none or one         | Comprises the archival information imported from NFC's previous data management system at the outset of the digitization process |
| Digitization    | [`digitization`](#digitization)      | none or one         | Metadata associated with the digitization of the archive image or images associated with this entry |

### `handbookTopic`

Denotes a subject heading (topic) in Seán Ó Súilleabháin's [*A Handbook of Irish Folklore*](https://www.duchas.ie/en/tpc/cbeg). It has been archival practice in NFC to associate photographs in CBÉG with a *Handbook* topic and a *Handbook* topic ID constitutes the first segment of the photograph `ReferenceNumber`.

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| ID              | string              | one                 | The topic's unique identifier |
| TopicEN         | string              | one                 | The general topic category (in English) |
| TopicGA         | string              | one                 | The general topic category (in Irish) |
| SubTopicEN      | string              | one                 | The specific topic category (in English) |
| SubTopicGA      | string              | one                 | The specific topic category (in Irish) |

### `format`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| Quantity        | integer             | none or one         | The quantity of images in this format held by NFC |
| Color           | string              | none or one         | Denotes the image color type |
| ColorComment    | string              | none or one         | Additional commentary regarding the image color type |
| Dimensions      | string              | none or one         | The dimensions of the physical image |
| DimensionsComment | string              | none or one         | Additional commentary regarding the image dimensions |
| Medium          | string              | none or one         | The image medium |
| MediumComment   | string              | none or one         | Additional commentary regarding the image medium |
| Physical        | string              | none or one         | Denotes the physical character of the image |
| PhysicalComment | string              | none or one         | Additional commentary regarding the physical character of the image |

### `archivedInfo`

As part of the Dúchas project photograph metadata from the NFC's previous data management system was ingested for archival purposes. The `ArchivedInfo` object holds this metadata.

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| Copyright       | string              | none or one         | Denotes the photograph copyright holder(s) |
| Condition       | string              | none or one         | Describes the photograph's physical condition |
| Topic           | string              | none or one         | Denotes the associated subject heading (topic) in Seán Ó Súilleabháin's [*A Handbook of Irish Folklore*](https://www.duchas.ie/en/tpc/cbeg) |
| Date            | string              | none or one         | The date of photograph capture |
| Photographer    | string              | none or one         | The photographer name |
| Location        | string              | none or one         | The location where the photograph was captured |
| Format          | string              | none or one         | Information regarding the physical image formats held by NFC |

### `digitization`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| DateCaptured    | string              | one                 | Denotes the date of image digitization |
| Operator        | string              | one                 | The name of the operator responsible |
| CaptureDevice   | string              | one                 | The capture device used |
| CaptureSoftware | string              | one                 | The capture software used |
| SourceCondition | string              | one                 | The condition of the physical source image |
| CopyNote        | string              | one                 | ? |
| MimeType        | string              | one                 | The [MIME](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) type of the digitized image |
| ImageBitDepth   | string              | one                 | The bit depth of the digitized image |
| ImageEditor     | string              | one                 | The image editing software used |
| ImageResolution | string              | one                 | The resolution of the digitized image |
| ImageSize       | string              | one                 | The pixel size of the digitized image |
| FileSize        | string              | one                 | The file size of the digitized image |
| ComputerOS      | string              | one                 | The operating system used |
| Storage         | string              | one                 | Image storage details |

### Values

This section describes values particular to properties of the `photograph` object.

#### `copyright`

| Value           | Description               |
| :-------------- | :------------------------ |
| CBE             | NFC is the copyright holder |
| OTH             | Copyright is held by an entity other than NFC |
| NOT             | Copyright does not apply  |
| UNK             | Copyright status is unknown |

#### `condition`

| Value           | Description               |
| :-------------- | :------------------------ |
| 0               | Poor condition            |
| 1               | Medium condition          |
| 2               | Good condition            |

#### `archivedDescriptionStatus`

Specifies the publication status of the `ArchivedDescription` field.

| Value           | Description               |
| :-------------- | :------------------------ |
| EDIT            | The `ArchivedDescription` field is not suitable for publication |
| PUB             | The `ArchivedDescription` field is suitable for publication |

#### `extraInfoStatus`

Specifies the publication status of the `extraInfo` field.

| Value           | Description               |
| :-------------- | :------------------------ |
| EDIT            | The `extraInfo` field is not suitable for publication |
| PUB             | The `extraInfo` field is suitable for publication |

## The Persons Database (CBÉD)

Queries to the Persons Database may return one or more `person` objects. The information below describes the properties of this object type.

### `person`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| ID              | integer             | one                 | The person identifier (unique within collection) |
| DateCreated     | ISO 8601 datetime   | one                 | The date and time of entry creation  |
| DateModified    | ISO 8601 datetime   | none or one         | The date and time of most recent modification to entry  |
| Names           | [`name`](#name)     | one or many         | Names associated with the person  |
| Gender          | string              | none or one         | The person's gender (`f` or `m`) |
| AinmID          | integer             | none or one         | The person's unique identifier in the [ainm.ie](https://www.ainm.ie) database |
| ViafID          | integer             | none or one         | The person's unique identifier in the [VIAF](https://viaf.org/) database |
| BirthDate       | [`date`](#date)     | none or one         | The person's date of birth |
| DeathDate       | [`date`](#date)     | none or one         | The person's date of death |
| BirthCounty     | [`county`](#county) | none or one         | The person's county of birth if born in Ireland |
| BirthPlaceIreland | [`locationIreland`](#locationIreland) | none or one         | The person's birth location if born in Ireland  |
| BirthCountry    | [`country`](#country) | none or one         | The person's country of birth if born outside of Ireland  |
| BirthPlaceAbroad | [`locationAbroad`](#locationAbroad) | none or one         | The person's birth location if born outside of Ireland |
| Counties        | [`county`](#county) | none or one or many | Denotes an Irish administrative county or counties associated with the person |
| AddressesIreland | [`locationIreland`](#locationIreland) | none or one or many | Denotes a location or locations in Ireland associated with the person |
| Countries       | [`country`](#country) | none or one or many | Denotes a country or countries, apart from Ireland, associated with the person |
| AddressesAbroad | [`locationAbroad`](#locationAbroad) | none or one or many | Denotes a location or locations outside of Ireland associated with the person |
| Occupations     | [`occupation`](#occupation) | none or one or many | Occupations associated with the person |

### `name`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| FirstNames      | string              | none or one         | A person's first name(s) and, optionally, middle names or nickname |
| Surname         | string              | none or one         | A person's surname        |
| FullName        | string              | one                 | A person's full name, including first names and surname |

### `occupation`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| ID              | string              | one                 | The occupation's unique identifier |
| NameEN          | string              | one                 | The occupation name (in English) |
| NameGA          | string              | one                 | The occupation name (in Irish) |

## Common entities

A number of entities are common to multiple collections. These are described below.

### `coordinates`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| Latitude        | double              | one                 | The latitudinal coordinate |
| Longitude       | double              | one                 | The longitudinal coordinate |

### `county`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| LogainmID       | integer             | one                 | The county's unique identifier in the [logainm.ie](https://www.logainm.ie) database |
| NameEN          | string              | one                 | The county name (in English) |
| NameGA          | string              | one                 | The county name (in Irish) |
| QualifiedNameEN | string              | one                 | The county name including county (Co.) qualifier (in English) |
| QualifiedNameGA | string              | one                 | The county name including county (Co.) qualifier (in Irish) |
| Coordinates     | [`coordinates`](#coordinates) | one                 | The location's geographical coordinates |

### `country`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| IsoCode         | string              | one                 | The country's unique ISO 3166 country code (see note below) |
| GeoNameID       | integer             | one                 | The country's unique identifier in the [geonames.org](http://www.geonames.org) database |
| NameEN          | string              | one                 | The country name (in English) |
| NameGA          | string              | one                 | The country name (in Irish) |
| Coordinates     | [`coordinates`](#coordinates) | one                 | The location's geographical coordinates |

**Note:** Country codes in the `IsoCode` property adhere to the ISO 3166-1 standard except for England (`GB-ENG`), Northern Ireland (`GB-NIR`), Scotland (`GB-SCT`) and Wales (`GB-WLS`) where ISO 3166-2 codes are used. For these countries it was necessary to have greater resolution than the ISO 3166-1 standard provides.

### `date`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| IsoDate         | ISO 8601 datetime   | none or one         | Aggregates the values of the `Year`, `Month` and `Day` properties below in the form of an ISO 8601 datetime string |
| IsoStartDate    | ISO 8601 datetime   | none or one         | Aggreates the values of the `PeriodStartYear`, `PeriodStartMonth` and `PeriodStartDay` properties below to represent the start date in a time interval |
| IsoEndDate      | ISO 8601 datetime   | none or one         | Aggreates the values of the `PeriodEndYear`, `PeriodEndMonth` and `PeriodEndDay` properties below to represent the end date in a time interval |
| IsoDuration     | ISO 8601 datetime   | none or one         | Represents the span of time between the `IsoStartDate` and `IsoEndDate` properties, where appropriate |
| Accuracy        | string              | none or one         | Indicates the accuracy of the date information using standard [MODS](http://www.loc.gov/standards/mods/) date qualifier vocabulary |
| Year            | integer             | none or one         | Denotes year in `YYYY` format |
| Month           | integer             | none or one         | Denotes calendar month (values 1-12) |
| Day             | integer             | none or one         | Denotes day of month (values 1-31) |
| PeriodStartYear | integer             | none or one         | Denotes the start year in a time interval in `YYYY` format |
| PeriodStartMonth | integer             | none or one         | Denotes the start calendar month (values 1-12) in a time interval |
| PeriodStartDay  | integer             | none or one         | Denotes the start day of month (values 1-31) in a time interval |
| PeriodEndYear   | integer             | none or one         | Denotes the end year in a time interval in `YYYY` format |
| PeriodEndMonth  | integer             | none or one         | Denotes the end calendar month (values 1-12) in a time interval |
| PeriodEndDay    | integer             | none or one         | Denotes the end day of month (values 1-31) in a time interval |

#### `Accuracy`

This property indicates the accuracy of the date information using standard [MODS](http://www.loc.gov/standards/mods/) date qualifier vocabulary.

| Value           | Description               |
| :-------------- | :------------------------ |
| APPROX          | The date is approximate   |
| INFER           | The date is inferred      |
| QUESTION        | The date is questionable  |

### `locationAbroad`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| GeoNameID       | integer             | one                 | The location's unique identifier in the [geonames.org](http://www.geonames.org) database |
| NameEN          | string              | one                 | The location name (in English) |
| NameGA          | string              | one                 | The location name (in Irish) |
| Coordinates     | [`coordinates`](#coordinates) | one                 | The location's geographical coordinates |
| Country         | [`country`](#country) | one                 | The country in which the location is situated |

### `locationIreland`

| Property name   | Type                | Cardinality         | Description               |
| :-------------- | :------------------ | :------------------ | :------------------------ |
| LogainmID       | integer             | one                 | The location's unique identifier in the [logainm.ie](https://www.logainm.ie) database |
| NameEN          | string              | one                 | The location name (in English) |
| NameGA          | string              | one                 | The location name (in Irish) |
| Coordinates     | [`coordinates`](#coordinates) | one                 | The location's geographical coordinates |
| Counties        | [`county`](#county) | one or many         | The county or counties in which the location is situated |

## Common values

A number of properties with standardized values are common to multiple collections. These are described below.

### `status`

Specifies the entry's editorial status. Only entries with a status value of **4** are deemed ready for publication.

| Value           | Description               |
| :-------------- | :------------------------ |
| 0               | The entry is newly ingested |
| 1               | First editorial pass complete |
| 2               | First editorial check complete |
| 3               | Second editorial pass complete |
| 4               | Second editorial check complete |
