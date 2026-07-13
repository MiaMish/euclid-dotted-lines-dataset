# Datasets

The repository is organized as follows:

| File                       | Description                                                                                                                                                             |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `data/classifications.csv` | Main dataset containing bibliographical metadata for each edition or related work, together with the manual classification of dotted lines and dots used in this study. |
| `data/facsimiles.csv`      | Links between editions and publicly available digitized facsimiles. An edition may be associated with multiple facsimiles.                                              |
| `data/crop_detections.csv` | Metadata describing automatically detected visual elements within the digitized facsimiles. Each row corresponds to a single detection on a page.                       |

The three datasets are linked through the `edition_key` field, which serves as the primary identifier for each edition.

## Classifications

File: [data/classifications.csv](data/classifications.csv)

Each row represents a single edition or work in the study corpus. The table contains metadata and dotted-line classifications.

| Column                                         | Type           | Description                                                                                                                                                                                                                                                                                       |
|------------------------------------------------|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `edition_key`                                  | String         | Unique identifier for the edition within the dataset.                                                                                                                                                                                                                                             |
| `corpus`                                       | Enum           | Corpus to which the edition belongs. Either `Main Elements`, indicating that the edition is considered part of the *Euclid's Elements* corpus in the context of this research, or `Additional Work`, indicating that the work is classified as another mathematical related work from the period. |
| `year`                                         | String         | Year of publication. May contain approximate or compound dates (for example, `1491/1492`).                                                                                                                                                                                                        |
| `city`                                         | String         | City where the edition was printed or published as indicated on its title page or colophon.                                                                                                                                                                                                       |
| `language`                                     | String         | Language of the edition. May contain multiple languages for bilingual or multilingual editions.                                                                                                                                                                                                   |
| `format`                                       | Integer        | Bibliographical format of the printed book (for example, `2` = folio, `4` = quarto, `8` = octavo).                                                                                                                                                                                                |
| `dots_represent_continuous_lines`              | Enum           | Whether the edition contains dotted lines used to represent continuous geometrical lines. Possible values are `TRUE`, `FALSE` and `CONTEXT_DEPENDENT`. `CONTEXT_DEPENDENT` indicates that the interpretation is highly dependent on the research context.                                         |
| `dots_represent_numbers_units`                 | Enum           | Whether the edition contains dots representing discrete numerical units arranged in rows. Possible values are `TRUE`, `FALSE` and `CONTEXT_DEPENDENT`.                                                                                                                                            |
| `doted_lines_notes`                            | String         | Free-text notes describing the use of dotted lines or dots in the edition, including examples and relevant observations.                                                                                                                                                                          |
| `has_diagrams`                                 | Enum           | Indicates whether the edition contains diagrams. Possible values are `TRUE`, `FALSE` and `CONTEXT_DEPENDENT`.                                                                                                                                                                                     |
| `reprint_of`                                   | String         | Identifier of an earlier edition if this edition is a reprint. Empty if not applicable.                                                                                                                                                                                                           |
| `short_title`                                  | String         | Short title of the edition.                                                                                                                                                                                                                                                                       |
| `author_or_editor`                             | String         | The early modern author, translator, editor, adapter or compiler associated with the edition.                                                                                                                                                                                                     |
| `publisher_or_printer`                         | String         | Printer and/or publisher of the edition.                                                                                                                                                                                                                                                          |
| `ustc_id`                                      | Integer/String | Identifier of the edition in the [Universal Short Title Catalogue (USTC)](https://www.ustc.ac.uk/), when available.                                                                                                                                                                               |
| `elements_books`                               | String         | Comma-separated list of the books of *Euclid's Elements* included in the edition. This field is relevant only for editions classified as `Main Elements`.                                                                                                                                         |
| `includes_elements_plane_geometry_books_1_6`   | Boolean        | Indicates whether the edition includes Books I–VI of the *Elements* (plane geometry). This field is relevant only for editions classified as `Main Elements`.                                                                                                                                     |
| `includes_elements_arithmetical_books_7_9`     | Boolean        | Indicates whether the edition includes Books VII–IX of the *Elements* (arithmetical books). This field is relevant only for editions classified as `Main Elements`.                                                                                                                               |
| `includes_elements_book_10`                    | Boolean        | Indicates whether the edition includes Book X of the *Elements*. This field is relevant only for editions classified as `Main Elements`.                                                                                                                                                          |
| `includes_elements_solid_geometry_books_11_13` | Boolean        | Indicates whether the edition includes Books XI–XIII of the *Elements* (solid geometry). This field is relevant only for editions classified as `Main Elements`.                                                                                                                                  |
| `additional_content`                           | String         | Notes on additional material included in the edition beyond the *Elements*. This field is relevant only for editions classified as `Main Elements`.                                                                                                                                               |


## Facsimiles

File: [data/facsimiles.csv](data/facsimiles.csv)

Each row represents a link between an edition and a digitized facsimile. Some editions include multiple facsimiles.

| Column          | Type   | Description                                       |
|-----------------|--------|---------------------------------------------------|
| `edition_key`   | string | Foreign key to `classifications.csv`.             |
| `facsimile_url` | URI    | URL of the digitized facsimile or catalogue view. |

## Crop Detections

File: [data/crop_detections.csv](data/crop_detections.csv)

Each row represents an automated detection record associated with a page in a digitized facsimile.

| Column                          | Type              | Description                                                            |
|---------------------------------|-------------------|------------------------------------------------------------------------|
| `edition_key`                   | string            | Foreign key to `classifications.csv`.                                  |
| `page_in_facsimile`             | integer           | One-based page position in the digital facsimile.                      |
| `sequence_on_page`              | integer           | Sequence number assigned to a detection on the page.                   |
| `automatically_identified_type` | controlled string | Raw label assigned by the automated visual-element detection workflow. |
