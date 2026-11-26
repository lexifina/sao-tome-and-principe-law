# Estrutura / Structure

Um ficheiro por artigo; um commit por versão de cada ato. / One file per article; one commit per version of each act.

| Pasta | Conteúdo | Atos |
| --- | --- | ---: |
| `constituicao/` | Constituição (seis versões, 1975–2003) | 1 |
| `codigos/` | `codigos/<codigo>/`: o código (subpasta `codigo/`) e a lei que o aprova (na raiz) | 8 |
| `decretos/` | `decretos/<ano>/<número>-<assunto>/` | 25 |
| `decretos-legislativos/` | `decretos-legislativos/<ano>/…` | 1 |
| `decretos-lei/` | `decretos-lei/<ano>/<número>-<assunto>/` | 28 |
| `decretos-presidenciais/` | `decretos-presidenciais/<ano>/…` | 4 |
| `leis/` | `leis/<ano>/<número>-<assunto>/` | 35 |
| `resolucoes/` | `resolucoes/<ano>/<número>-<legislatura>-<assunto>/` | 19 |
| `diario-da-republica/<ano>/<número>/` | índice de cada edição do Diário da República: os atos dela neste repositório | 94 |

Em cada pasta de ato / In each act folder:

- `README.md`: título, edição do Diário da República, fonte (PDF) e lista de ficheiros.
- `preambulo.md`: o texto antes do artigo 1.º (preâmbulo, nota justificativa, fórmula de aprovação).
- `art-001.md`, `art-012-a.md`, …: um artigo por ficheiro (`# Artigo N.º (epígrafe)`).
- `codigo/` ou `anexo/`: quando o diploma aprova um código ou um anexo com numeração própria.
- `assinaturas.md`: aprovação, promulgação e assinaturas.
- `texto.md`: diplomas sem artigos.

Datas: cada commit tem a data do meio-dia (Africa/Sao_Tome, UTC+0) do dia de publicação no Diário da República, indicada no trailer `Published:` com `Date-basis: published`, ou do dia da entrada em vigor quando o diploma a fixa (trailers `In-force:` e `In-force-basis:`, com `Date-basis: in-force`). Nenhuma data é a do dia de recolha.

Dates: each commit is dated noon (Africa/Sao_Tome, UTC+0) on the Diário da República publication day, given in the `Published:` trailer with `Date-basis: published`, or on the entry-into-force day where the act states it (`In-force:` and `In-force-basis:` trailers, `Date-basis: in-force`). No date is a retrieval date.
