# São Tomé and Príncipe: law history in git


The law of São Tomé and Príncipe as a git history: one file per article, one commit per version on the day it took effect, and the act that made each change as the commit's author. `git blame` names the act behind every paragraph; `git log` lists every change to an article; picking a date gives the text in force that day.

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is São Tomé and Príncipe's national law, which global-law reads at `sao-tome-and-principe/national/acts/`.

**What is in it now:** the Constitution (Constituição da República Democrática de São Tomé e Príncipe) in six versions: as approved in 1975, and as revised by Lei n.º 1/80, Lei n.º 2/82, Lei n.º 1/87, Lei n.º 7/90 and Lei n.º 1/2003, whose text has a preamble and 160 articles. No other act yet. [`constituicao/README.md`](constituicao/README.md) lists every provision, and [`data/laws.csv`](data/laws.csv) the six laws with their dates.

Each article is one file in `constituicao/` (`art-001.md` is Article 1, República Democrática de São Tomé e Príncipe), with the preamble in `preambulo.md`; the headings (partes, títulos, capítulos, secções) are gathered in [`constituicao/estrutura.md`](constituicao/estrutura.md), each naming the first article under it. The revisions reused article numbers for other subjects, so a file holds whatever article bore its number in each version.

The text is in Portuguese, as the Assembleia Nacional published it. An English translation is not part of this record.

## Questions as git commands

| Question | Command |
| --- | --- |
| Every change to Article 1 of the Constitution | `git log -p --word-diff -- constituicao/art-001.md` |
| Which act wrote each paragraph of Article 1? | `git blame constituicao/art-001.md` |
| Every version of Article 1, with the day each took effect | `git log --format="%h %(trailers:key=In-force,valueonly,separator=) %an" -- constituicao/art-001.md` |
| Article 1 as in force on 1 January 1985 | `python tools/on.py 1985-01-01 constituicao 1` |

**Outside git**, we also host this record publicly, for free:

- **[Ask Claude about the law of São Tomé and Príncipe](https://global-law.lexifina.com/v1/try_claude?country=sao-tome-and-principe)**: opens Claude with a first question ready.
- **[Ask ChatGPT](https://global-law.lexifina.com/v1/try_chatgpt?country=sao-tome-and-principe)**: the same question in ChatGPT.
- **[Call the API in your browser](https://global-law.lexifina.com/v1/search_law?query=f%C3%A9rias&jurisdictions=sao-tome-and-principe)**: a search of the law of São Tomé and Príncipe for "férias" (paid holidays), returned as JSON. See the [documentation here](https://lexifina.com/api/global-law).

Both assistants read the record through the free Global law connector (MCP, `https://global-law.lexifina.com/mcp`); the first time, the chat gives you the link that adds it. Ask in Portuguese or in English.

**Host it yourself easily.** All it takes is git and Python, and the tools run on your machine:

```sh
git clone --depth 1 https://github.com/lexifina/global-law && cd global-law
python3 tools/countries.py add sao-tome-and-principe/national/acts
python3 tools/law.py show 2026-01-01 sao-tome-and-principe/national/acts/constituicao/art-001.md
```

Opened in Claude Code, Cursor, VS Code or Codex, the clone also starts a local MCP server with the same tools ([MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md)).

## Dates

Each commit is dated at noon, Africa/Sao_Tome, on the day the version took effect, and carries it in its `In-force:` trailer:

- the 1975 Constitution took effect on its approval, 5 November 1975 (its art. 49), though the Diário da República that printed it (n.º 39) is dated 15 December 1975;
- Leis n.º 1/80, 2/82, 1/87 and 7/90 took effect on publication: 7 February 1980, 31 December 1982, 31 December 1987 and 20 September 1990, the Diário da República dates the Assembleia Nacional's index and art. 159 of the 2003 text give;
- Lei n.º 1/2003 took effect on the thirtieth day after its publication (art. 160.1) in Diário da República n.º 2 of 29 January 2003: 28 February 2003. The government's copy gives "n.º 1, de 26 de Janeiro de 2003"; the Assembleia Nacional's date is used;
- `tools/on.py` picks the version by that trailer, not by the commit date.

The first version is credited to the Constituição Política de 1975 itself, and each later one to the law that made it. The revisions of 1980, 1982, 1990 and 2003 republished the whole Constitution, so each is credited with every article that differs; Lei n.º 1/87 with the five articles it replaced. The committer is always Lexifina.

## How it is checked

- `tools/check_repo.py` reads every version back from git on the day it took effect and on the day before, and both must match the corpus: 6 versions, 0 mismatches, and every commit's trailers parse.
- The texts are read from the text layer of the Assembleia Nacional's PDFs, not from scans; spelling and typing slips are kept as printed.
- The 2003 text was compared word by word with the government's own copy. About 90 places differ (spellings such as *juizes*/*juízes*, and a few evident typing slips in one copy or the other); the Assembleia Nacional's text is kept as published, not corrected. [`REPRODUCE.md`](REPRODUCE.md) lists every decision made by hand.
- History is append-only: no merge commits, no commit dated in the future.

## What it does not show

- **Today's law.** No amendment of the 2003 text was found in any official source that could be read (the parliament, government, ministry and DGRN sites and their archives). The record ends at 2003 and does not claim the 2003 text is in force today.
- **Part of Lei n.º 1/87.** Its new Articles 47 to 51 are applied; its first block, which amends alíneas of an article whose number the official copy leaves out, is not, so that article keeps its 1982 wording until 1990.
- **Articles 80 to 82 of 2003 applied only from the next presidential term** (art. 160.2-3), with a transitional Article 80 until then. The source gives no date for it, so the full 2003 text is shown from 28 February 2003.
- **The 1975 Lei Fundamental and Lei da Nacionalidade**, printed in the same file as the Constituição Política, are left out.
- **Any other act.** Codes, ordinary laws and case law are not here. The DGRN's editions of nine acts (among them the Labour Code, the Family Code and the Road Code) were examined but are left out: their latest amendments and the basis for reusing them are not confirmed.

## Sources

| Source | Kind | Past versions | Notes |
| --- | --- | --- | --- |
| Assembleia Nacional: [Legislação Constitucional](https://web.archive.org/web/20070203155103/http://www.parlamento.st/Legisl/leg%20Constit/leg_const.htm) (parlamento.st, read through Internet Archive captures of February 2007) | Official texts: one PDF per constitutional law, with its Diário da República issue | yes, every constitutional law as published | The only texts used; parlamento.st is offline and no official legislation portal is online today |
| Governo de São Tomé e Príncipe: [constistp.pdf](https://web.archive.org/web/20070813190023/http://www.gov.st/data/filestorage/docs/constistp.pdf) (gov.st, Internet Archive capture of August 2007) | Official text of 2003 | no | A word-for-word cross-check only |

## Licence

See [`LICENSE`](LICENSE). Laws and other official legislative texts are outside copyright under the usual rule of Portuguese-model copyright codes; no explicit statement of the position was found in São Tomé's own Decree-Law 02/2017, so this is an assumption, not a licence. The source site states no licence terms.

No AI model wrote, translated or corrected legal text, and none runs when the history is built; the scripts were written by an AI model (see [`REPRODUCE.md`](REPRODUCE.md)).

## More

From [lexifina/global-law](https://github.com/lexifina/global-law):

- [FEATURES.md](https://github.com/lexifina/global-law/blob/main/FEATURES.md): every feature, and what every corpus must support (`git blame`, `law.py`, the MCP tools)
- [FAQ.md](https://github.com/lexifina/global-law/blob/main/FAQ.md): questions and answers · [CONTRIBUTING.md](https://github.com/lexifina/global-law/blob/main/CONTRIBUTING.md): proposing changes · [MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md): the MCP server · [REPRODUCE.md](https://github.com/lexifina/global-law/blob/main/REPRODUCE.md): how it was built · [CHANGELOG.md](https://github.com/lexifina/global-law/blob/main/CHANGELOG.md)
- [FRESHNESS.md](https://github.com/lexifina/global-law/blob/main/FRESHNESS.md): how current each corpus is · [Monitoring](https://github.com/lexifina/global-law/tree/main/monitoring): whether updates are running · [WATCHING.md](https://github.com/lexifina/global-law/blob/main/WATCHING.md): how each official source is watched for changes
- [performance/](https://github.com/lexifina/global-law/tree/main/performance): how fast the tools are, measured
- [visualisations/](https://github.com/lexifina/global-law/tree/main/visualisations): charts and bridges across the world's law
- [Vulnerabilities](https://github.com/lexifina/global-law/tree/main/vulnerabilities): mistakes in legislation as published
