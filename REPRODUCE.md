# How this repository was made (São Tomé and Príncipe)

This file is written by the build on 2026-10-28, the day the source data was retrieved. Everything below is enough to rebuild this repository hash for hash.

## Sources

| Source | Address | Retrieved | Requests | Licence |
| --- | --- | --- | ---: | --- |
| Assembleia Nacional de São Tomé e Príncipe: Legislação Constitucional (parlamento.st) | <http://www.parlamento.st/Legisl/leg%20Constit/leg_const.htm> | 2026-10-28 | 7 | Official legislative texts of the Assembleia Nacional; the site states no licence. |
| Governo de São Tomé e Príncipe: constistp.pdf (gov.st) | <http://www.gov.st/data/filestorage/docs/constistp.pdf> | 2026-10-28 | 1 | Official text; the site states no licence. |
| Internet Archive Wayback Machine | <https://web.archive.org/> | 2026-10-28 | 14 | Internet Archive terms of use; the archived texts keep their publishers' status. |

Every response is cached by the sha256 of its URL, and the table above lists every source with its retrieval date. Lexifina keeps its fetch scripts privately; `tools/parse.py` reads only the cache and writes `corpus.json`, so the same cache always gives the same corpus.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constituicao` | Constituição da República Democrática de São Tomé e Príncipe | 6 | 1975-11-05 to 2003-02-28 |

The build made 6 commits:

| Commits | Kind |
| ---: | --- |
| 1 | first version of an act |
| 5 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `futuro`: laws not yet in force on 2026-10-28.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 6 laws in the record.
- 12 tags.

## Dates

Each commit is dated at noon (Africa/Sao_Tome) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Each constitutional text sets its own entry into force, which is used: 1975 art. 49 (on approval), Lei 1/80 art. 70, Lei 2/82 art. 72, Lei 1/87 art. 3.º and Lei 7/90 art. 128 (on publication), Lei 1/2003 art. 160.1 (thirtieth day after publication). http://www.parlamento.st/Legisl/leg%20Constit/leg_const.htm

## Commands, in order

```sh
# fill the cache from the sources listed above (network; Lexifina's fetch scripts are kept privately)
python -X utf8 tools/parse.py                  # cache -> corpus.json (no network)
python -X utf8 tools/build.py <folder> --repo <empty folder> --docs-date 2026-10-28
python -X utf8 tools/check_repo.py <repo> --corpus <folder>/corpus.json --write
python -X utf8 tools/build.py <folder> --repo <another empty folder> --docs-date 2026-10-28 --compare <repo>
```

In the main Lexifina repository these files live as follows:
- `fetch.py`, `parse.py` and `repo/`: in `scripts/sao-tome-and-principe-law/`.
- `build.py`, `check_repo.py` (`check.py` there) and `on.py`: in `scripts/gitlaw_common/`, with the corpus format in `SCHEMA.md`.

## Exact inputs

- `corpus.json` sha256 `f6b5ec5bc3918d11bc0be2621ef79fdb4a58f1e108676baa5c73febdcb23bb98` (314693 bytes)
- Script blob hashes (`git hash-object`):

| Script | Blob |
| --- | --- |
| build.py | `2bfc4ac9df193a7be844556d7f69cdb9d93ec3f2` |
| check.py | `cd346c7ff9996d450240e3bab52bcae03b2bc865` |
| on.py | `644a6c0857fbcc72562032b58d57aa113fee0641` |
| fetch.py | `58b9eae986fdfa8b8b39791978ef5e114b69b8c6` |
| parse.py | `b5a4698658d5f2448240eff7545040367d5feeef` |

- Tools:
  - Python 3.14.0
  - git version 2.52.0.windows.1
  - curl 8.21.0 (Windows) libcurl/8.21.0 Schannel zlib/1.3.2 WinIDN WinLDAP

## Checks

6 versions of 1 acts read back from git on the day each took effect and on the day before: 0 mismatches. Trailers: 0 commits whose trailers git cannot parse. Health: 0 merge commits on main, 0 commit dates that go backwards, 0 commits dated after the build.

Not yet run for this build.

These results are from the check run on the build before this one, from the same corpus.

## Decisions made by hand

- No official legislation portal of São Tomé and Príncipe is online today (dre.gov.st, the electronic Diário da República, no longer resolves). Every text is read from the Assembleia Nacional's own former site, parlamento.st, through pinned Internet Archive id_ captures of February 2007.
- The Assembleia Nacional's page "Legislação Constitucional" (parlamento.st/Legisl/leg Constit/leg_const.htm, captured 2007-02-03) lists every constitutional law with its Diário da República issue and links one zipped PDF per law; those PDFs have a text layer and are the only texts used.
- Text is read with xpdf pdftotext 4.00 -layout -enc UTF-8. Page numbers and the title block are dropped; wrapped lines are joined into one paragraph per line, a paragraph ending at . ; : ! ? » or a quote, and numbered items and alíneas starting new lines.
- Typesetting is normalised once: non-breaking spaces, curly quotes to straight, em dash to en dash, runs of spaces collapsed. Spelling and typing slips in the official copies (for example "Princípios de lgualdade") are kept as published.
- One file per article (art-NNN). The article number and, from 1990 on, its epígrafe form the first line. Part, title, chapter and section headings are listed in constituicao/estrutura.md with the first article under each.
- Every revision from 1980 to 2003 republished the whole Constitution, so each version is the full official text of that law and every changed article is credited to it. Article numbers were reused with different content across revisions; the history shows such an article as changed, not moved.
- 1975: the Assembleia Nacional's file holds the Lei Fundamental of 12 Jul 1975, the Constituição Política and, after it, an annex "Lei da Nacionalidade". Only the Constituição Política is used; the Lei Fundamental (a separate provisional act, superseded by the Constitution) and the nationality law are left out.
- 1975: in force on its approval on 5 Nov 1975 under its own art. 49 ("entra imediatamente em vigor após a sua aprovação"), although the Diário da República issue (n.º 39) is dated 15 Dec 1975. In the official copy Article 4 is set inline as "Art.4º - 1. ..." and is read as Article 4.
- Lei n.º 1/80, 2/82, 1/87 and 7/90 each say they enter into force on publication; the in-force day used is the Diário da República date that the Assembleia Nacional's index and the 2003 text (art. 159) give for each.
- Lei n.º 1/87 replaces Articles 47 to 51 of the 1982 text in full, and those are applied. Its first block ("Art.º - b) ... u)") amends alíneas of an article whose number the official copy omits; that change is not applied rather than guessed, so the 1987 version shows that article in its 1982 wording. The 1990 revision replaced the whole text.
- Lei n.º 1/2003: the Assembleia Nacional's index and the 2003 text's own art. 159 give Diário da República n.º 2 of 29 Jan 2003. The government's copy (gov.st/data/filestorage/docs/constistp.pdf, captured 2007-08-13) says "n.º 1, de 26 de Janeiro de 2003" in the same place. The parliament's date is used; with art. 160.1 (in force on the thirtieth day after publication) the in-force day is 28 Feb 2003.
- Lei n.º 1/2003, art. 160.2-3: Articles 80 to 82 applied only from the start of the next presidential term, with a single transitional Article 80 meanwhile. The source gives no date for that term, so the record shows the full 2003 text from 28 Feb 2003 and says so in the version note; no typed applicability is set.
- The 2003 text was compared with the government's own copy (gov.st constistp.pdf, the same file the Assembleia Nacional published as parlamento.st/Lei/constistp.zip); see verify.py.
- No later amendment of the 2003 Constitution was found in any official source that could be read (parliament, government, ministry and DGRN sites and their archives). The record ends at the 2003 text and does not claim it is current today.

## What AI did and did not do

The fetch, parse and check scripts were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above, through code that anyone can rerun.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code with Claude Opus 5.5 (claude-opus-5-5) found the sources and wrote fetch.py and parse.py; no model wrote, read or corrected any legal text, and no model runs at build time.
