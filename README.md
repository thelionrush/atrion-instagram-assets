# atrion-instagram-assets

Mídia e calendário de publicação do Instagram **@atrion.ia**. Consumido pelo workflow n8n
`[ATRION] Op - Publicar Instagram Agendado`.

## calendar.json

Array de posts. O n8n lê o raw deste arquivo a cada 15 min e publica o que estiver
**`status: "agendado"`** e com **`publicar_em`** já no passado.

| campo | o quê |
|---|---|
| `id` | identificador único (não repetir). Ex: `2026-09-20-integracao` |
| `publicar_em` | data/hora ISO 8601 com fuso `-03:00`. Ex: `2026-09-20T09:00:00-03:00` |
| `tipo` | `imagem` (1 foto) · `carrossel` (2–10) · `reel` |
| `midia` | lista de URLs públicas. Pra `carrossel`, na ordem dos slides. Pra `reel`, 1 vídeo |
| `legenda` | texto + hashtags |
| `status` | `rascunho` (não publica) · `agendado` (publica na hora) · `publicado` (histórico) |

Depois de publicado, o n8n **não** reescreve este arquivo (ele guarda os `id` já
publicados internamente). O Claude limpa/atualiza o `status` nas sessões.

## media/

Imagens e vídeos renderizados, uma pasta por post: `media/<id>/slide-1.png` ...
Referenciar pela URL raw: `https://raw.githubusercontent.com/thelionrush/atrion-instagram-assets/main/media/<id>/<arquivo>`
