# Trilha Tech PM

Página estática com a trilha de estudos Tech PM: painel, semanas, entregas,
recursos, checklist e anotações. Todo o progresso é salvo **no navegador do
usuário** (`localStorage`), sem backend e sem enviar nada para servidor algum.

🔗 https://eraldooneto.github.io/tech-pm/

## Estrutura

| Caminho | O que é |
| --- | --- |
| `index.html` | A página. Marcação, estilos e a lógica do app. |
| `assets/runtime.js` | Runtime de templating (`sc-if`, `sc-for`, `{{ }}`) que monta a página. |
| `assets/react.min.js`, `assets/react-dom.min.js` | React 18.3.1 (UMD), servidos localmente — sem CDN. |
| `assets/font-*.woff2` | Plus Jakarta Sans, subsets locais. |
| `favicon.svg` | Ícone da aba. |
| `.nojekyll` | Desliga o Jekyll no GitHub Pages. |
| `source/` | O arquivo original exportado (bundle único), guardado como referência. |
| `.github/workflows/deploy.yml` | Publica o repositório no GitHub Pages a cada push na `main`. |

## Persistência dos dados

O estado fica em `localStorage`, na chave `trilha-tech-pm-v1`, com este formato:

```json
{ "startDate": "...", "goal": 6, "tasks": {}, "deliverables": {},
  "resources": {}, "checklist": {}, "notes": {}, "savedAt": 0 }
```

Consequências práticas:

- os dados são **por navegador e por dispositivo** — abrir em outro aparelho começa do zero;
- limpar dados do site / navegar em aba anônima apaga o progresso;
- a tela de **Ajustes** tem exportar/importar backup (JSON) e "apagar progresso".

## Rodando localmente

`file://` não serve — o runtime carrega `assets/` por HTTP. Use um servidor:

```bash
python3 -m http.server 8000
# abra http://localhost:8000
```

## Publicando

Todo push na `main` dispara o workflow, que habilita o Pages (se preciso) e
publica a raiz do repositório. Se o Pages ainda não estiver ativo, também dá
para ligar em **Settings → Pages → Source: Deploy from a branch → `main` / `/`**.
