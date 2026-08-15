# Sistema

Interface de uma página para planejar conteúdo: um guia editorial fixo à esquerda e a semana sendo
montada ao lado, com banco de ideias e histórico.

Este repositório contém **apenas a interface**. Nenhum conteúdo, dado ou métrica mora aqui.
Tudo é carregado em tempo de execução de um `sistema.json` guardado num repositório privado do usuário,
acessado com um token pessoal que fica apenas no navegador de quem usa.

Sem essa conexão, a página abre vazia.

## Estrutura do `sistema.json`

```jsonc
{
  "v": 1,
  "atualizadoEm": "ISO-8601",
  "guia": {
    "titulo": "...", "subtitulo": "...",
    "arquetipo": { "titulo": "...", "texto": "..." },
    "niveis":  { "topo": { "nome": "Topo", "foco": "...", "cor": "#2E6BE6" } },
    "quadros": [{ "id", "nivel", "nome", "desc", "formato", "canais": [], "precisa" }],
    "intencoes": [{ "nome", "desc" }],
    "formatos": ["..."],
    "metricas": [{ "nome", "forte": true }],
    "blocos":   [{ "eyebrow", "titulo", "itens": [] }]
  },
  "semanas":    { "2026-W33": { "dias": { "seg": [{ "nivel", "quadro", "tema", "hook", "canal", "status", "alcance" }] } } },
  "ideias":     [{ "id", "tema", "hook", "intencao", "formato", "quadro", "criadoEm" }],
  "publicados": [{ "data", "tema", "hook", "canal", "quadro", "metrica" }]
}
```

Os níveis do funil, os quadros e os blocos do guia são livres: a interface se monta a partir do que
estiver no arquivo.

## Conectar

Clique na pílula de status no topo e informe:

- **Repositório**: `usuario/repo-privado`
- **Token**: fine-grained token do GitHub com permissão de *Contents* (leitura e escrita) restrita a
  esse único repositório

O token é gravado no `localStorage` e usado só para chamar a API do GitHub. Alterações salvam sozinhas,
com um atraso de 1,4s para agrupar edições seguidas.

## Rodar local

```
python3 -m http.server 8765
```

Arquivo único, sem build e sem dependências. As fontes vêm do Google Fonts.
