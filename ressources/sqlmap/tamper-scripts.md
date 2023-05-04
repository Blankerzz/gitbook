# Tamper-Scripts

Tamper scripts can be chained, one after another, within the `--tamper` option (e.g. `--tamper=between,randomcase`), where they are run based on their predefined priority. A priority is predefined to prevent any unwanted behavior, as some scripts modify payloads by modifying their SQL syntax (e.g. [ifnull2ifisnull](https://github.com/sqlmapproject/sqlmap/blob/master/tamper/ifnull2ifisnull.py)). In contrast, some tamper scripts do not care about the inner content (e.g. [appendnullbyte](https://github.com/sqlmapproject/sqlmap/blob/master/tamper/appendnullbyte.py)).

Tamper scripts can modify any part of the request, although the majority change the payload content. The most notable tamper scripts are the following:

| **Tamper-Script**           | **Description**                                                                                                              |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `0eunion`                   | Replaces instances of UNION with e0UNION                                                                                     |
| `base64encode`              | Base64-encodes all characters in a given payload                                                                             |
| `between`                   | Replaces greater than operator (`>`) with `NOT BETWEEN 0 AND #` and equals operator (`=`) with `BETWEEN # AND #`             |
| `commalesslimit`            | Replaces (MySQL) instances like `LIMIT M, N` with `LIMIT N OFFSET M` counterpart                                             |
| `equaltolike`               | Replaces all occurrences of operator equal (`=`) with `LIKE` counterpart                                                     |
| `halfversionedmorekeywords` | Adds (MySQL) versioned comment before each keyword                                                                           |
| `modsecurityversioned`      | Embraces complete query with (MySQL) versioned comment                                                                       |
| `modsecurityzeroversioned`  | Embraces complete query with (MySQL) zero-versioned comment                                                                  |
| `percentage`                | Adds a percentage sign (`%`) in front of each character (e.g. SELECT -> %S%E%L%E%C%T)                                        |
| `plus2concat`               | Replaces plus operator (`+`) with (MsSQL) function CONCAT() counterpart                                                      |
| `randomcase`                | Replaces each keyword character with random case value (e.g. SELECT -> SEleCt)                                               |
| `space2comment`             | Replaces space character ( ) with comments \`/                                                                               |
| `space2dash`                | Replaces space character ( ) with a dash comment (`--`) followed by a random string and a new line ()                        |
| `space2hash`                | Replaces (MySQL) instances of space character ( ) with a pound character (`#`) followed by a random string and a new line () |
| `space2mssqlblank`          | Replaces (MsSQL) instances of space character ( ) with a random blank character from a valid set of alternate characters     |
| `space2plus`                | Replaces space character ( ) with plus (`+`)                                                                                 |
| `space2randomblank`         | Replaces space character ( ) with a random blank character from a valid set of alternate characters                          |
| `symboliclogical`           | Replaces AND and OR logical operators with their symbolic counterparts (`&&` and `\|\|`)                                     |
| `versionedkeywords`         | Encloses each non-function keyword with (MySQL) versioned comment                                                            |
| `versionedmorekeywords`     | Encloses each keyword with (MySQL) versioned comment                                                                         |

To get a whole list of implemented tamper scripts, along with the description as above, switch `--list-tampers` can be used
