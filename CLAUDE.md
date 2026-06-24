# Expenses-Acc — guia para o assistente

App pessoal de registo de despesas.
**Sem build, sem npm.** Site estático (GitHub Pages), PWA. Sincroniza via **GitHub** (não tem Supabase).

## Estrutura
- `index.html` — **ficheiro único** (~837 linhas): markup + CSS + JS tudo dentro. (Ainda NÃO dividido como o SplitBill/FestasBV.)
- `sw.js` — service worker (cache PWA).
- Não mexer: `apple-touch-icon.png`, `manifest.json`.

## Como NÃO gastar tokens à toa
- **Não leias o `index.html` todo.** O `<script>` está em secções com comentários `// ─── X ───`. Faz `grep` pelo título e lê só essa. Secções:
  `DATA` · `GITHUB CONFIG` · `STATE` · `HELPERS` · `SYNC UI` · **`GITHUB IO`** · `INIT` · `RENDER` · **`ACTIONS`** · `GO`
- Faz **edições cirúrgicas** (diffs pequenos). **Nunca reescrevas o ficheiro inteiro.**
- Se crescer, vale a pena dividir em `index.html` + `app.js` + `style.css` (como já fiz no SplitBill e FestasBV).

## Regras técnicas (não partir a app)
- O JS está inline e há handlers `onclick="…"` → as funções têm de ser **globais** (não converter para module).
- **PWA/cache:** se alterares o HTML/CSS/JS, **sobe a versão do CACHE no `sw.js`**.
- **Sync GitHub:** o token é **introduzido pelo utilizador em runtime** (guardado em `localStorage`) — **não está no código, nunca o coloques hardcoded**. Os dados são gravados em `diogoandrefsilva-ghc/AppDataJSON` → `expensesacc-data.json`. ⚠️ Esse repo é **público** (os dados são legíveis por qualquer pessoa).

## Deploy
GitHub Pages a partir de `main`. Um push para `main` publica.
