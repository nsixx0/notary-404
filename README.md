# Cartório 404 — espelho estático (1998)

Site fictício de terror/creepypasta. Em 1998, Elias Harrow (20 anos) procura
documentos de familiares mortos e encontra o "Westborough County Clerk Office".

## Como rodar

- **Qualquer navegador:** abra `index.html` (duplo clique) ou rode `python -m http.server 8000`
  e acesse `http://localhost:8000/`.
- **Windows 98 / Internet Explorer 5+:** copie a pasta para o Win98 (disquete, CD, pasta
  compartilhada da VM) e abra `index.html`. Ou sirva a pasta no PC hospedeiro e acesse
  `http://<ip-do-host>:8000/` pelo IE da VM (use **http**, não https).
- **Rejogar a história:** abra qualquer página com `?reset=1` (ex.: `index.html?reset=1`).

## Estrutura

```
index.html, 404.html        páginas de entrada
pages/                      demais páginas (records, death, preemptive, protocol,
                            witnesses, fees, email, doc)
css/base.css                visual "site de governo 1998" (tabelas, bevel, Win98)
css/horror.css              estágios de terror (stage1..3) e glitch
js/boot.js                  único <script> de cada página; carrega os módulos
js/core/                    compat (helpers IE5), storage, data (A HISTORIA), layout
js/features/                countdown, stage, reveal, bind, glitch
js/pages/                   um script por página que tem lógica própria
img/                        GIFs/JPG gerados (selo, badges, foto do anexo)
```

- **Mudar a história** (nome, nascimento, parentes, datas): `js/core/data.js`.
- **Mudar menu / letreiro / rodapé:** `js/core/layout.js`.
- **Estágios de terror:** `js/features/stage.js` decide o estágio; `css/horror.css` define o visual.

| Estágio | Gatilho | Efeito |
|---|---|---|
| 0 | — | site de governo normal |
| 1 | visitou *Records Request* | letreiro e cores levemente erradas, link secreto aparece |
| 2 | clicou em *Proceed* | site escurece, selo abre o olho, glitches aleatórios |
| 3 | contagem de 5 min zerou | site morto, "Last updated: TOMORROW", Witness C |

## Compatibilidade com Win98

Todo o código é HTML 4.01 + CSS1/2 + JavaScript ES3: sem `const/let`, `forEach`,
`localStorage` obrigatório, flexbox, `rgba`, `position:fixed`. O estado da história usa
`localStorage` → cookies → `window.name` (para o IE via `file://`), e janelas abertas
por `window.open` recebem o estado pela URL.
Requer IE 5.0 ou superior (o Win98 original traz IE4: atualize para o IE5/5.5/6).
