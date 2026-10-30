# How this repository was made (São Tomé and Príncipe)

This file is written by the build on 2026-10-30, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
| Assembleia Nacional de São Tomé e Príncipe: Legislação Constitucional (parlamento.st) | <http://www.parlamento.st/Legisl/leg%20Constit/leg_const.htm> | 2026-10-28 | Official legislative texts of the Assembleia Nacional; the site states no licence. |
| Governo de São Tomé e Príncipe: constistp.pdf (gov.st) | <http://www.gov.st/data/filestorage/docs/constistp.pdf> | 2026-10-28 | Official text; the site states no licence. |
| Internet Archive Wayback Machine | <https://web.archive.org/> | 2026-10-28 | Internet Archive terms of use; the archived texts keep their publishers' status. |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

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
- 0 commits on the branch `futuro`: laws not yet in force on 2026-10-30.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 6 laws in the record.
- 12 tags.

## Dates

Each commit is dated at noon (Africa/Sao_Tome) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Each constitutional text sets its own entry into force, which is used: 1975 art. 49 (on approval), Lei 1/80 art. 70, Lei 2/82 art. 72, Lei 1/87 art. 3.º and Lei 7/90 art. 128 (on publication), Lei 1/2003 art. 160.1 (thirtieth day after publication). http://www.parlamento.st/Legisl/leg%20Constit/leg_const.htm

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `d85c95e2274583cedf69353933e2504e5cb86a358b5af2adb31e153f96138a13` (315033 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3e59cb6f05eccb94a9ec14431a7f6781221e83ef`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.12.10; git version 2.46.0.windows.1.

## Checks

Not yet run for this build.

No second build of this corpus has been compared yet.

## Decisions made by hand

- No official legislation portal of São Tomé and Príncipe is online today (dre.gov.st, the electronic Diário da República, no longer resolves).
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
- The 2003 text was compared with the government's own copy (gov.st constistp.pdf, the same file the Assembleia Nacional published as parlamento.st/Lei/constistp.zip); the two copies are not identical: about 90 places differ (orthography such as juizes/juízes, decretos lei/leis, and a few word-level differences where one copy has an evident typing slip), listed in verification-2003-vs-govst.txt. The Assembleia Nacional PDF is kept as published and is not corrected from the government copy.
- No later amendment of the 2003 Constitution was found in any official source that could be read (parliament, government, ministry and DGRN sites and their archives). The record ends at the 2003 text and does not claim it is current today.

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code with Claude Opus 5.5 (claude-opus-5-5) found the sources and wrote Lexifina's code; no model wrote, read or corrected any legal text, and no model runs at build time.
