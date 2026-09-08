# atrion-instagram-assets

Mídia e calendário de publicação do Instagram **@atrion.ia**. Consumido pelo workflow n8n
`[ATRION] Op - Publicar Instagram Agendado`.

## calendar.json

Array de posts. O n8n lê o raw deste arquivo **a cada 15 min** e publica o que estiver
**`status: "agendado"`** e com **`publicar_em`** já no passado (ignora atraso > 6h).

Pra agendar um post: adicionar um objeto no array. Pra desagendar: mudar `status` pra
`"rascunho"`. **Não precisa mexer no n8n** — o workflow é fixo, só o calendário muda.

| campo | o quê |
|---|---|
| `id` | identificador único, formato `AAAA-MM-DD-tema`. Nunca repetir |
| `publicar_em` | data/hora ISO 8601 com fuso `-03:00`. Ex: `2026-09-20T09:00:00-03:00` |
| `tipo` | `imagem` (1 foto) · `carrossel` (2–10 fotos) · `story` (1 foto ou vídeo) · `reel` (só manual, n8n não faz) |
| `midia` | lista de URLs públicas. Carrossel: na ordem dos slides. Story/imagem: 1 item |
| `legenda` | texto + hashtags (story ignora legenda) |
| `status` | `rascunho` (não publica) · `agendado` (publica na hora marcada) · `publicado` (histórico) |

Depois de publicado, o n8n **não** reescreve este arquivo (guarda os `id` já publicados na
tabela `atrion_ig_publicados`). O Claude atualiza o `status` nas sessões.

## media/

Imagens e vídeos renderizados, uma pasta por post: `media/<id>/slide-1.png` ...
URL raw: `https://raw.githubusercontent.com/thelionrush/atrion-instagram-assets/main/media/<id>/<arquivo>`
