# Getting started with the Earth books API

The Earth books API lets users retrieve and filter book metadata. The API is a
REST API. Primary use cases for the Book Finder API include the following:

* Social sites that let users find books, catalog books, create book lists,
  write book reviews, discover new books according to preferences, and recommend
  books to others in the community.

* Libraries that let users search authors, book titles, ISBNs, book themes, book
  genres, publish dates, and publishers. Users can also place holds on materials
  and manage those borrowed materials.

## API documentation

View general API documentation for the Book Finder API
at: https://docs.earthbooks.org/api. Each endpoint’s documentation includes
the URL of the endpoint and details about its parameters, JSON results, and HTTP
result codes for success or failure. See [Endpoints](#endpoints) for examples of
API usage.

## Key concepts

<table>
  <thead>
    <tr>
      <th style="width: 25%;">Concept</th>
      <th style="width: 75%;">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Author</strong></td>
      <td>Metadata about a person who wrote one the book.</td>
    </tr>
    <tr>
      <td><strong>Book title</strong></td>
      <td>The primary resource. Each book has metadata related to author, title, ISBNs, publish date, and publisher.</td>
    </tr>
    <tr>
      <td><strong>ISBN</strong></td>
      <td>A unique numeric identifier of a book edition.</td>
    </tr>
    <tr>
      <td><strong>Genre</strong></td>
      <td>A category to which a book belongs (e.g., fiction, romance).</td>
    </tr>
    <tr>
      <td><strong>Sub-genre</strong></td>
      <td>A sub-category to which a book belongs (e.g., dystopian, coming-of-age).<td>
    </tr>
    <tr>
      <td><strong>Subject</strong></td>
      <td>The main topic of the book (e.g., astronomy, gardening).<td>
    </tr>
    <tr>
      <td><strong>Review</strong></td>
      <td>A user-generated rating and optional comment attached to a book.<td>
    </tr>
    <tr>
      <td><strong>Lists</strong></td>
      <td>A set of books filtered by specific criteria (e.g., books adapted to film).<td>
    </tr>
    <tr>
      <td><strong>Sub-genre</strong></td>
      <td>A sub-category to which a book belongs (e.g., dystopian, coming-of-age).<td>
    </tr>
    <tr>
      <td><strong>Publish date</strong></td>
      <td>The original date the book edition was published.<td>
    </tr>
    <tr>
      <td><strong>Publisher</strong></td>
      <td>The name of the publisher of the title.<td>
    </tr>
    <tr>
      <td><strong>Subject</strong></td>
      <td>The subject of the book (e.g, cooking, meditation).<td>
    </tr>
  </tbody>
</table>

### Book search endpoints

Parameters include:
q (general query), or specific fields, for example: `title=...`, `author=...`, `ISBN=...`.

#### Search titles

Endpoint: `GET /search.json?title={title}`

```text
/search.json?title=the+road
```
Example response body:

```json
{
    "numFound": 18510,
    "start": 0,
    "numFoundExact": true,
    "num_found": 18510,
    "documentation_url": "https://docs/api/bookish.org/search",
    "q": "\"the road\"",
    "offset": null,
    "docs": [
        {
            "author_key": [
                "..."
            ],
            "author_name": [
                "Cormac McCarthy"
            ],
            "cover_edition_key": "...",
            "cover_i": 34655,
            "ebook_access": "borrowable",
            "edition_count": 122,
            "publish_year": 2006,
            "language": [
                "spa",
                "jpn",
                "fre",
                "chi",
                "eng",
                "ita",
                "ger",
                "tur"
            ],
            "title": "The Road"
        },
        {
            ...: "Tructated to maintain clarity"
        }
    ]
}
```

Example cURL command for titles search:

```bash
curl "https://bookish.org/search.json?title=the+road"
```

#### Search authors

Endpoint: `GET /search.json?author={author}`

```text
/search.json?author=cormac+mccarthy
```

Example response body:

```json
{
    "numFound": 124,
    "start": 0,
    "numFoundExact": true,
    "num_found": 124,
    "documentation_url": "https://docs/api/bookish.org/search",
    "q": "",
    "offset": null,
    "docs": [
        {
            "author_key": [
                "",
                ""
            ],
            "author_name": [
                "Cormac McCarthy",
                "Rob Wood"
            ],
            "title": "Blood Meridian - Lettered Edition"
        },
        {
            "author_key": [
                "",
                ""
            ],
            "author_name": [
                "Cormac McCarthy",
                "Pedro Fontana"
            ],
            "title": "Suttree"
        },
        {
            "author_key": [
                "",
                ""
            ],
            "author_name": [
                "Cormac McCarthy",
                "Hans Wolf"
            ],
            "title": "Grenzgänger"
        }
        {
        ...: "Tructated to maintain clarity"
        }
    ]
}
```

Example cURL command for authors search:

```bash
curl "https://bookish.org/search.json?author=cormac+mccarthy"
```

#### Search ISBNs

Endpoint: `GET /search.json?isbn={ISBN}`

```text
/search.json?isbn=9780307387899
```
Example response body:

```json
{
    "numFound": 1,
    "start": 0,
    "numFoundExact": true,
    "num_found": 1,
    "documentation_url": "https://docs/api/bookish.org/search",
    "q": "",
    "offset": null,
    "docs": [
        {
            "author_key": [...
            ],
            "author_name": [
                "Cormac McCarthy"
            ],
            "cover_edition_key": "",
            "cover_i": 198120,
            "ebook_access": "borrowable",
            "edition_count": 66,
            "first_publish_year": 2006,
            "has_fulltext": true,
            "ia": [...
            ],
            "language": [
                "eng",
                "pol",
                "fre",
                "ita",
                "por",
                "chi",
                "spa",
                "cat",
                "heb"
            ],
            "title": "The Road"
        }
    ]
}
```

Example cURL command for ISBN search:

```bash
curl "https://bookish.org/search.json?isbn=cormac+mccarthy"
```

## API Response Codes
The API returns the following response codes:
<!-- create table -->
Code	Description	Example Body
200	The request was successful
401	Expired or invalid token	{ error: "Unable to verify token" }
403	User does not have access to the requested resource or query	{ error: "Message describing the error" }
404	Not Found
429	Too Many Requests, try again later	{ error: "Throttled" }
500	Internal Server Error	{ error: "An unknown error occurred" }
