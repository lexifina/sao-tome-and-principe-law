# São Tomé and Príncipe: law history in git

The Constitution of São Tomé and Príncipe as a git history: one file per article, one commit per constitutional law on the day it took effect, and the law that made each change as the commit's author. `git blame` names the law behind every article; `git log` lists every change to an article; picking a date gives the text in force that day.

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law), which places it at `st/`. The official language is **Portuguese**; the texts here are in Portuguese and nothing is translated.

**What is in it now**

| Folder | Act | Versions | History |
| --- | --- | ---: | --- |
| `constituicao/` | Constituição da República Democrática de São Tomé e Príncipe | 6 | 1975 (original), 1980, 1982, 1987 (Lei 1/87, arts 47-51 only), 1990, and the revision of 2003 (in force 28 Feb 2003) |

Every version is the full official text of that law, taken from the PDFs the Assembleia Nacional published on its old site (parlamento.st, "Legislação Constitucional"), read through pinned Internet Archive captures from February 2007 (`scripts` list them in `sources.json`).

## Dates

- Each commit is dated on the day the law took effect. Laws 1/80, 2/82, 1/87 and 7/90 take effect on publication; the 2003 revision takes effect on the thirtieth day after its publication (art. 160), 28 February 2003, using the Diário da República date the Assembleia gives (n.º 2 of 29 January 2003). The government's copy says "n.º 1, de 26 de Janeiro de 2003"; the Assembleia date is used.
- Article numbers were reused with different content across revisions, so a changed article is shown as changed, not moved.

## How it is checked

- Every version is read back from git on its in-force day and the day before, and must match `corpus.json` (0 mismatches, 0 trailer errors).
- The 2003 text was compared word by word with the government's own copy (gov.st `constistp.pdf`). **They are not identical**: about 90 places differ (orthography such as *juizes*/*juízes*, *decretos lei*/*leis*, and a few word-level differences where one copy has an evident typing slip). The Assembleia Nacional text is kept as published and not corrected. The differences are in `verification-2003-vs-govst.txt` in the build scripts.

## What it does not show

- **Currentness.** No later amendment of the 2003 text was found in any official source that could be read (parliament, government, ministry and DGRN sites and their archives). This record ends at 2003 and does not claim the 2003 text is the law in force today.
- **Lei 1/87.** Its first block (alíneas b, i, r, t, u of an unnumbered article) is not applied; only arts 47-51 are.
- **Articles 80 to 82 of 2003** applied only from the next presidential term (art. 160.2-3); the source gives no date, so the full text is shown from 28 Feb 2003.
- **Other legislation.** Codes and ordinary laws are not here.
- **Copyright.** Official legislative texts are generally outside copyright in Portuguese-model law; we could not confirm São Tomé's Decree-Law 02/2017 on the point. See `LICENSE`.

This repository is not legal advice. For anything that matters, read the original.
